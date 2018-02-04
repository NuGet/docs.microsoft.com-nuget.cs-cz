---
title: Soubor project.json NuGet s projekty UWP | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Popis použití souboru project.json k sledování závislostí NuGet v projektech pro univerzální platformu Windows (UWP)."
keywords: "NuGet závislosti, NuGet a UPW, UWP a project.json, soubor project.json NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f1ec086d6404c441ca5ad53028af2265a2344905
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-and-uwp"></a>Project.JSON a UWP

> [!Important]
> Tento obsah je zastaralý. Projekty využít buď `packages.config` nebo PackageReference formáty.

Tento dokument popisuje strukturu balíčku, která využívá funkce v NuGet 3 + (Visual Studio 2015 a novější). `minClientVersion` Vlastnost vaší `.nuspec` slouží k stavu, že potřebujete popsané nastavením na 3.1 funkce.

## <a name="adding-uwp-support-to-an-existing-package"></a>Přidání podpory UPW do existujícího balíčku

Pokud máte existující balíček a chcete přidat podporu pro aplikace UWP, pak nemusíte přijmout balení formát, který je popsaný v tomto poli. Stačí přijmout tento formát, pokud potřebujete funkce popisuje a chcete-li pracovat pouze s klienty, které byly aktualizovány na verzi 3 + klienta NuGet.

## <a name="i-already-target-netcore45"></a>I již cíle netcore45

Pokud cílíte `netcore45` již a nemusíte zde využít výhod funkcí, není vyžadována žádná akce. `netcore45`balíčky mohou být spotřebovávána aplikace UWP.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Chcete využít výhod konkrétní rozhraní API systému Windows 10

V takovém případě je nutné přidat `uap10.0` cíle Přezdívka framework (TFM nebo TxM) do vašeho balíčku. Vytvořte novou složku na balíček a přidejte sestavení, která je kompilovaná pro práci s Windows 10 do této složky.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Není zapotřebí rozhraní API specifické pro Windows 10, ale mají nové funkce rozhraní .NET nebo již nemáte netcore45

V takovém případě byste přidali `dotnet` TxM do vašeho balíčku. Na rozdíl od jiných TxMs `dotnet` není určeno, útoku na nebo platformu. Je oznamující, že váš balíček funguje na jakékoli platformě, která závislostmi práci. Při vytváření balíčku s `dotnet` TxM, budete pravděpodobně mít mnoho další závislosti konkrétní TxM ve vaší `.nuspec`, jako je třeba definovat BCL balíčky, závisí na, například `System.Text`, `System.Xml`atd. Umístění, které fungují těchto závislostí na definovat, které pracuje vašeho balíčku.

### <a name="how-do-i-find-out-my-dependencies"></a>Jak zjistím Moje závislosti

Existují dva způsoby, jak zjistit, které závislosti do seznamu:

1. Použití [NuSpec závislostí generátor](https://github.com/onovotny/ReferenceGenerator) **3. stran** nástroj. Nástroj automatizuje proces a aktualizace vašeho `.nuspec` soubor s balíčky závislých na sestavení. Je k dispozici prostřednictvím balíčku NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Podle pevného) Použití `ILDasm` podívat se na vaše `.dll` chcete zobrazit, jaké sestavení jsou skutečně potřeba za běhu. Pak stanovit, který NuGet balíček každá pocházet z.

Najdete v článku [ `project.json` ](project-json.md) téma podrobné informace o funkcích, které pomáhají při vytváření balíčku, který podporuje `dotnet` TxM.

> [!Important]
> Pokud váš balíček je určen pro práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složky, aby se zabránilo upozornění a potenciální problémy s kompatibilitou.

## <a name="directory-structure"></a>Struktura adresářů

Balíčky NuGet formátu mají následující dobře známou složku a chování:

| Folder | Chování |
| --- | --- |
| Sestavení | Obsahuje nástroje MSBuild cíle a soubory props v této složce jsou jinak integrované do projektu, ale jinak není žádná změna. |
| Nástroje | `install.ps1`a `uninstall.ps1` se nespustí. `init.ps1`funguje jako má vždy. |
| Obsah | Obsah není automaticky zkopírují do projektu uživatele. Podpora pro zahrnutí obsahu v projektu je plánovaná pro novější verzi. |
| Lib | Pro mnoho balíčky `lib` funguje stejným způsobem jako v NuGet 2.x, ale s rozšířené možnosti pro jaké názvy dá se použít uvnitř ho a lepší logiku pro výběr správné podsložky při využívání balíčky. Ale při použití ve spojení s `ref`, `lib` složka obsahuje sestavení, které implementují plochy definované v sestavení `ref` složky. |
| REF | `ref`je volitelné složka, který obsahuje sestavení .NET definování veřejnosti prostor (veřejné typy a metody) pro aplikaci zkompilovat proti. Sestavení v této složce může mít žádné implementace, se používají výhradně k definování povrchu pro kompilátor. Pokud balíček neobsahuje žádné `ref` složku, pak se `lib` je referenční sestavení a implementace sestavení. |
| Moduly runtime | `runtimes`je volitelné složka, která obsahuje konkrétní kódu operačního systému, třeba architektura procesoru a binární soubory závislé na platformu operačního systému konkrétní nebo jinak. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>MSBuild cíle a soubory props do balíčků

Balíčky NuGet může obsahovat `.targets` a `.props` soubory, které jsou importovány do jakékoli projektu nástroje MSBuild, který je balíček nainstalován do. V NuGet 2.x, k tomu bylo potřeba vložením `<Import>` příkazů do `.csproj` souboru, v NuGet 3.0 není k dispozici žádná konkrétní "instalace do projektu" akce. Místo toho v procesu obnovení balíčku zapíše dva soubory `[projectname].nuget.props` a `[projectname].NuGet.targets`.

MSBuild zná hledání tyto dva soubory a automaticky je importuje téměř začátku a konci procesu sestavení projektu. To poskytuje velmi podobné chování NuGet 2.x, ale jeden hlavní rozdíl: *neexistuje žádné zaručenou pořadí cíle nebo props souborů v tomto případě*. Však poskytuje způsoby, jak pořadí cíle prostřednictvím nástroje MSBuild `BeforeTargets` a `AfterTargets` atributy `<Target>` definice (najdete v části [Target – Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>LIB a Ref

Chování `lib` složky významně nezměnilo ve NuGet v3. Musí být v rámci dílčí složky s názvem po TxM však ve všech sestaveních a už může být umístěno přímo ve `lib` složky. TxM je název platformu, která by měla fungovat pro daný prostředek v balíčku. Logicky Toto jsou rozšíření z Monikery cílový Framework (TFM), například `net45`, `net46`, `netcore50`, a `dnxcore50` jsou všechny příklady TxMs (najdete v části [cílové rozhraní](../reference/target-frameworks.md). TxM mohou odkazovat na rozhraní (TFM) a také další oblasti povrchu specifické pro platformu. Například TxM UWP (`uap10.0`) představuje možnosti útoku na rozhraní .NET, jakož i prostor oblasti systému Windows pro aplikace UWP.

Příklad lib struktury:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` Složka obsahuje sestavení, které se používají v době běhu. Pro většinu balíčky složku ve složce `lib` pro každý cíl TxMs je všechno, co je vyžadován.

## <a name="ref"></a>REF

Jsou někdy případech, kdy by měla být použita jiném sestavení při kompilaci (referenční sestavení .NET do této dnes). Pro případy, použijte složku nejvyšší úrovně s názvem `ref` (zkratka pro "referenční sestavení").

Většina autoři balíček nevyžadují `ref` složky. Je vhodné pro balíčky, které potřebují k zajištění konzistentní útoku pro kompilaci a technologii IntelliSense, ale pak mít jinou implementaci pro různé TxMs. Největších případ použití tyto `System.*` balíčky, které vznikají jako součást přenosů .NET Core na NuGet. Tyto balíčky mají různé implementace, které jsou právě unified konzistentní sada ref sestavení.

Mechanicky sestavení součástí `ref` složky jsou předávány kompilátoru referenční sestavení. Pro ty z vás, kteří použili csc.exe Toto jsou sestavení jsme jsou předány [možnost/reference jazyka C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) přepínače.

Struktura `ref` složky je stejný jako `lib`, například:

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

V tomto příkladu sestavení v `ref` adresáře by být identické.

## <a name="runtimes"></a>Moduly runtime

Moduly runtime složka obsahuje sestavení a nativní knihovny potřebné ke spuštění na konkrétní "moduly runtime", které jsou obvykle definovány Architektura operačního systému a procesoru. Tyto moduly runtime jsou identifikovány pomocí [Runtime identifikátorů (RID)](/dotnet/core/rid-catalog) například `win`, `win-x86`, `win7-x86`, `win8-64`atd.

## <a name="native-light-up"></a>Nativní lehký up

Následující příklad ukazuje balíček, který má čistě spravované implementace pro několik platforem, ale používá nativní Pomocné rutiny v systému Windows 8, kde můžete volání do nativního rozhraní API systému Windows 8 specifické.

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

Daný balíček výše provedou následující akce:

- Pokud není v systému Windows 8 `lib/net40/MyLibrary.dll` sestavení používá.

- Když v systému Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` se používá a `native/MyNativeHelper.dll` se zkopíruje na výstup buildu.

V příkladu nahoře `lib/net40` sestavení je čistě spravovaného kódu, zatímco sestavení ve složce moduly runtime bude p/invoke do sestavení nativní pomocná k volání rozhraní API specifická pro Windows 8.

Jediným `lib` složky je někdy být zachyceny, takže pokud je konkrétní složce runtime je zvolen přes konkrétní – modul runtime `lib`. Nativní složka je aditivní, pokud existuje ho zkopíruje do výstupu sestavení.

## <a name="managed-wrapper"></a>Spravovaná obálka

Pro odeslání balíčku, který je plně spravovaná obálka přes nativní sestavení je další způsob použití moduly runtime. V tomto scénáři vytvoříte balíček, podobně jako tento:

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

V takovém případě není žádná nejvyšší úrovně `lib` žádné implementace tohoto balíčku, který není závislý na odpovídající nativní sestavení je složka jako tuto složku jako zde. Pokud spravované sestavení `MyLibrary.dll`, se přesně stejná v obou případech pak jsme může pro něj nejvyšší úrovni `lib` složky, ale protože nedostatečná nativní sestavení nemá způsobit, že balíček k selhání instalace, pokud byla nainstalovaná na platformě, pak se použije lib nejvyšší úrovně, ale žádné nativní sestavení by zkopírují nebyl win-x86 nebo win-x64.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Vytváření balíčků NuGet 2 a NuGet 3

Pokud chcete vytvořit balíček, který mohou být spotřebovávána projektů pomocí `packages.config` také jako balíčky pomocí `project.json` pak následujících podmínek:

- REF a moduly runtime fungovat jenom na NuGet 3. Obě jsou ignorovány NuGet 2.

- Nelze spoléhat na `install.ps1` nebo `uninstall.ps1` funkce. Tyto soubory provést při použití `packages.config`, ale jsou ignorovány s `project.json`. Takže vašeho balíčku musí být možné bez je spuštěná. `init.ps1`stále běží na NuGet 3.

- Cíle a Props instalace je jiné, proto se ujistěte, že váš balíček funguje podle očekávání na obou klientských počítačích.

- Podadresáře lib musí být TxM v NuGet 3. Knihovny nelze umístit na nejnižší úrovni `lib` složky.

- Obsah není automaticky zkopíruje s NuGet 3. Příjemci vašeho balíčku může kopírovat soubory sami nebo pomocí některého nástroje, například Spouštěče úloh k automatizaci kopírování souborů.

- Zdroj a konfiguračním souboru transformace se nespustí 3 NuGet.

Pokud podporujete NuGet 2 a 3 a vaše `minClientVersion` by měla být nejnižší verzi klienta NuGet 2, který na funguje vašeho balíčku. V případě existující balíček není vhodné měnit.