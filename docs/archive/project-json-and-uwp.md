---
title: Soubor NuGet project.json s projekty UPW
description: Popis způsobu, jakým se soubor project.json používá ke sledování závislostí NuGet v projektech univerzální platformy Windows (UPW).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494378"
---
# <a name="projectjson-and-uwp"></a>project.json a UPW

> [!Important]
> Tento obsah je zastaralé. Projekty by `packages.config` měly používat formáty nebo PackageReference.

Tento dokument popisuje strukturu balíčku, která využívá funkce v NuGet 3 + (Visual Studio 2015 a novější). Vlastnost `minClientVersion` vašeho `.nuspec` můžete uvést, že budete potřebovat funkce popsané zde nastavením na 3.1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Přidání podpory UPW do existujícího balíčku

Pokud máte existující balíček a chcete přidat podporu pro aplikace UPW, pak nemusíte přijmout formát balení popsané zde. Tento formát je třeba přijmout pouze v případě, že potřebujete funkce, které popisuje a jsou ochotni pracovat pouze s klienty, které byly aktualizovány na verzi 3 + klienta NuGet.

## <a name="i-already-target-netcore45"></a>Už jsem cíl netcore45

Pokud již `netcore45` cílíte a nemusíte využívat funkce zde, není nutná žádná akce. `netcore45`balíčky mohou být spotřebovány aplikacemi UPW.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Chci využít výhod specifických api windows 10

V takovém případě je `uap10.0` třeba přidat zástupný název cílové ho rozhraní (TFM nebo TxM) do balíčku. Vytvořte novou složku v balíčku a přidejte sestavení, které bylo zkompilováno pro práci s Windows 10 do této složky.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Nepotřebuji windows 10 konkrétní rozhraní API, ale chcete nové .NET funkce nebo nemají netcore45 již

V takovém případě byste `dotnet` do balíčku přidali TxM. Na rozdíl od jiných `dotnet` TxMs, neznamená plochu nebo platformu. Uvádí, že váš balíček funguje na libovolné platformě, na které pracují vaše závislosti. Při vytváření balíčku `dotnet` s TxM, budete pravděpodobně mít mnohem více TxM `.nuspec`specifické závislosti ve vašem , jak je `System.Text`třeba `System.Xml`definovat Balíčky BCL, na kterých jste závislí, jako , , atd. Umístění, která tyto závislosti pracují na definovat, kde váš balíček funguje.

### <a name="how-do-i-find-out-my-dependencies"></a>Jak zjistím své závislosti

Existují dva způsoby, jak zjistit, které závislosti chcete uvést:

1. Použijte nástroj [NuSpec Dependency Generator třetí strany.](https://github.com/onovotny/ReferenceGenerator) **3rd party** Nástroj automatizuje proces a `.nuspec` aktualizuje soubor s závislé balíčky na sestavení. Je k dispozici prostřednictvím balíčku NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Tvrdá cesta) Pomocí `ILDasm` zobrazení na `.dll` vaše zobrazíte, jaké sestavení jsou skutečně potřeba za běhu. Pak určete, ze kterého balíčku NuGet pocházejí.

[`project.json`](project-json.md) Podrobnosti o funkcích, které pomáhají při vytváření balíčku, který podporuje TxM, najdete v tématu. `dotnet`

> [!Important]
> Pokud je váš balíček určen pro práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složku, aby se zabránilo upozornění a potenciální problémy s kompatibilitou.

## <a name="directory-structure"></a>Adresářová struktura

Balíčky NuGet používající tento formát mají následující dobře známou složku a chování:

| Složka | Chování |
| --- | --- |
| Sestavení | Obsahuje MSBuild cíle a rekvizity soubory v této složce jsou integrovány odlišně do projektu, ale jinak neexistuje žádná změna. |
| nástroje | `install.ps1`a `uninstall.ps1` nejsou spuštěny. `init.ps1`funguje jako vždy. |
| Obsah | Obsah není automaticky zkopírován do projektu uživatele. Podpora pro zahrnutí obsahu do projektu je plánována na pozdější vydání. |
| Lib | Pro mnoho `lib` balíčků funguje stejným způsobem jako v NuGet 2.x, ale s rozšířenými možnostmi pro jaké názvy lze použít uvnitř a lepší logiku pro výběr správné podsložky při náročné balíčky. Pokud je však `ref`složka `lib` použita ve spojení s , obsahuje sestavy, `ref` které implementují plochu vymezenou sestaveními ve složce. |
| Ref | `ref`je volitelná složka, která obsahuje sestavení rozhraní .NET definující veřejný povrch (veřejné typy a metody) pro kompilování aplikace. Sestavení v této složce může mít žádnou implementaci, jsou použity výhradně k definování plochy pro kompilátor. Pokud balíček `ref` nemá žádnou `lib` složku, pak je sestavení odkazu a sestavení implementace. |
| Runtime | `runtimes`je volitelná složka, která obsahuje kód specifický pro operační režim, například architekturu procesoru a binární soubory specifické pro operační službu nebo jinak závislé na platformě. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>MSBuild cíle a rekvizity soubory v balíčcích

Balíčky NuGet `.targets` `.props` mohou obsahovat a soubory, které jsou importovány do libovolného projektu MSBuild, do kterého je balíček nainstalován. V NuGet 2.x to bylo `<Import>` provedeno vložením příkazy do souboru, `.csproj` v NuGet 3.0 neexistuje žádná konkrétní akce "instalace k projektu". Místo toho proces obnovení `[projectname].nuget.props` balíčku `[projectname].NuGet.targets`zapíše dva soubory a .

MSBuild ví, že má hledat tyto dva soubory a automaticky je importuje v blízkosti začátku a na konci procesu sestavení projektu. To poskytuje velmi podobné chování NuGet 2.x, ale s jedním velkým rozdílem: *neexistuje žádné zaručené pořadí cílů / rekvizity soubory v tomto případě*. MSBuild však poskytuje způsoby, `BeforeTargets` jak `AfterTargets` objednat cíle `<Target>` prostřednictvím atributy a definice (viz [Cílový prvek (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib a odkaz

Chování `lib` složky se výrazně nezměnila v NuGet v3. Všechna sestavení však musí být v rámci podsložek pojmenovaný chrápl txm a již nemůže být umístěn přímo do `lib` složky. TxM je název platformy, pro kterou má daný prostředek v balíčku pracovat. Logicky se jedná o rozšíření názvů názvů target frameworku (TFM), `net45`například , `net46` `netcore50`, a `dnxcore50` jsou všechny příklady TxM (viz Cílové [rámce](../reference/target-frameworks.md). TxM může odkazovat na rámec (TFM) stejně jako jiné plochy specifické pro platformu. Například UWP TxM`uap10.0`( ) představuje plochu .NET, stejně jako plochu windows pro aplikace UPW.

Příklad lib struktura:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

Složka `lib` obsahuje sestavení, která se používají za běhu. Pro většinu balíčků `lib` je potřeba složka pod pro každý z cílových TxMs.

## <a name="ref"></a>Ref

Někdy existují případy, kdy by měl být použit jiný sestavení během kompilace (.NET reference sestavení to dnes). V těchto případech použijte složku nejvyšší `ref` úrovně s názvem (zkratka pro "Referenční sestavení").

Většina autorů balíčků nepožaduje `ref` složku. Je užitečné pro balíčky, které potřebují poskytnout konzistentní plochu pro kompilaci a IntelliSense, ale pak mají různé implementace pro různé TxMs. Největší případ použití tohoto `System.*` jsou balíčky, které jsou vyráběny jako součást odesílání .NET Core na NuGet. Tyto balíčky mají různé implementace, které jsou jednotné konzistentní sadu sestavení ref.

Mechanicky sestavení zahrnutá ve `ref` složce jsou referenční sestavení předávaná kompilátoru. Pro ty z vás, kteří používají csc.exe to jsou sestavení jsme předávání [C# /reference přepínač možnosti.](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option)

Struktura `ref` složky je stejná `lib`jako například:

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

V tomto příkladu sestavení `ref` v adresářích by všechny identické.

## <a name="runtimes"></a>Runtime

Složka runtimes obsahuje sestavení a nativní knihovny potřebné ke spuštění na konkrétní "runtimes", které jsou obecně definovány architekturou operačního systému a procesoru. Tyto runtime jsou identifikovány pomocí [identifikátorů runtime (ID),](/dotnet/core/rid-catalog) jako `win`jsou , `win-x86`, `win7-x86` `win8-64`, atd.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Nativní pomocníci pro použití api specifická pro platformu

Následující příklad ukazuje balíček, který má čistě spravovanou implementaci pro několik platforem, ale používá nativní pomocníky v systému Windows 8, kde může volat do nativních api pro Windows 8.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

Vzhledem k výše uvedenému balíčku se dějí následující věci:

- Pokud není v `lib/net40/MyLibrary.dll` systému Windows 8 sestavení se používá.

- Když na Windows `runtimes/win8-<architecture>/lib/MyLibrary.dll` 8 se `native/MyNativeHelper.dll` používá a zkopíruje se do výstupu sestavení.

Ve výše uvedeném příkladu `lib/net40` sestavení je čistě spravovaný kód, zatímco sestavení ve složce runtimes bude p/invoke do nativního pomocného sestavení volat api specifické pro Windows 8.

Je někdy `lib` vybrána pouze jedna složka, takže pokud existuje složka specifická pro běh `lib`za běhu, je vybrána přes nezaběhu . Nativní složka je aditivní, pokud existuje, je zkopírována do výstupu sestavení.

## <a name="managed-wrapper"></a>Spravovaný obálka

Dalším způsobem použití runtimes je doložit balíček, který je čistě spravované obálky přes nativní sestavení. V tomto scénáři vytvoříte balíček, jako je následující:

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

V tomto případě neexistuje žádná `lib` složka nejvyšší úrovně, protože neexistuje žádná implementace tohoto balíčku, který nespoléhá na odpovídající nativní sestavení. Pokud spravované sestavení, , byl přesně stejný v obou těchto případech pak `lib` bychom mohli dát do složky nejvyšší úrovně, ale protože nedostatek nativní sestavení nezpůsobí balíček nezdaří instalaci, `MyLibrary.dll`pokud byl nainstalován na platformě, která nebyla win-x86 nebo win-x64 pak nejvyšší úroveň lib by být použity, ale žádné nativní sestavení by být zkopírovány.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Vytváření balíčků pro NuGet 2 a NuGet 3

Pokud chcete vytvořit balíček, který může `packages.config` být spotřebován projekty pomocí, stejně jako balíčky pomocí `project.json` pak platí následující:

- Ref a runtimes pracovat pouze na NuGet 3. Oba jsou ignorovány NuGet 2.

- Nemůžete se `install.ps1` spoléhat ani `uninstall.ps1` fungovat. Tyto soubory se `packages.config`spouštějí při `project.json`použití , ale jsou ignorovány pomocí . Takže váš balíček musí být použitelný, aniž by běželi. `init.ps1`stále běží na NuGet 3.

- Cíle a rekvizity instalace se liší, takže se ujistěte, že váš balíček funguje podle očekávání na obou klientech.

- Podadresáře lib musí být TxM v NuGet 3. Knihovny nelze umístit do kořenového adresáře `lib` složky.

- Obsah není automaticky zkopírován pomocí NuGet 3. Spotřebitelé vašeho balíčku mohou zkopírovat soubory sami nebo použít nástroj jako posuč úkolu k automatizaci kopírování souborů.

- Transformace zdrojového a konfiguračního souboru nejsou spuštěny společností NuGet 3.

Pokud podporujete NuGet 2 a `minClientVersion` 3 pak vaše by měla být nejnižší verze klienta NuGet 2, který váš balíček funguje. V případě existujícího balíčku by se nemělo měnit.
