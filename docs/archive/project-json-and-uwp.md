---
title: project.jsNuGet na soubor s projekty UWP
description: Popis způsobu, jakým se project.jspro soubor používá ke sledování závislostí NuGet v projektech Univerzální platforma Windows (UWP).
author: JonDouglas
ms.author: jodou
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 30e2272aafb5d2ea8d932e3cb0209d97c30b3209
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773803"
---
# <a name="projectjson-and-uwp"></a>project.json a UPW

> [!Important]
> Tento obsah je zastaralý. Projekty by měly používat buď `packages.config` formáty PackageReference nebo.

Tento dokument popisuje strukturu balíčku, která využívá funkce v NuGet 3 + (Visual Studio 2015 a novější). `minClientVersion`Vlastnost `.nuspec` , kterou jste si popsali, můžete použít k určení, že budete potřebovat funkce popsané tady, a to tak, že ji nastavíte na 3,1.

## <a name="adding-uwp-support-to-an-existing-package"></a>Přidání podpory UWP do existujícího balíčku

Pokud máte existující balíček a chcete přidat podporu pro aplikace pro UWP, pak nemusíte v takovém případě popsaný formát balíčku přijmout. Tento formát je potřeba přijmout jenom v případě, že vyžadujete funkce, které popisuje, a jsou ochotní pracovat jenom s klienty, kteří se aktualizovaly na verzi 3 + klienta NuGet.

## <a name="i-already-target-netcore45"></a>Již jsem cílí na netcore45

Pokud už cílíte na cíl `netcore45` a nemusíte používat tyto funkce, není nutné provádět žádnou akci. `netcore45` balíčky můžou využívat aplikace UWP.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Chci využít výhod specifických rozhraní API pro Windows 10

V takovém případě musíte `uap10.0` do balíčku přidat moniker cílového rozhraní (TFM nebo TxM). Vytvořte ve svém balíčku novou složku a přidejte sestavení, které bylo zkompilováno pro práci s Windows 10, do této složky.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Nepotřebujem rozhraní API specifická pro Windows 10, ale chcete, aby už nové funkce .NET nebo netcore45 ještě neexistují.

V takovém případě byste přidali `dotnet` TxM do balíčku. Na rozdíl od jiných TxMs `dotnet` neznamená oblast povrchu nebo platformu. Uvádí, že váš balíček funguje na jakékoli platformě, na které fungují závislosti. Při sestavování balíčku s `dotnet` TxM pravděpodobně máte mnoho dalších závislostí specifických pro TxM `.nuspec` , protože potřebujete definovat balíčky BCL, na kterých jste závislí, například, `System.Text` `System.Xml` atd. Umístění, na kterých tyto závislosti pracují, definují, kde váš balíček funguje.

### <a name="how-do-i-find-out-my-dependencies"></a>Návody zjistit moje závislosti

Existují dva způsoby, jak zjistit, které závislosti se mají zobrazit:

1. Použijte nástroj [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) od **třetí strany** . Nástroj automatizuje proces a aktualizuje `.nuspec` soubor pomocí závislých balíčků při sestavování. Je k dispozici prostřednictvím balíčku NuGet [NuSpec. ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Pevným způsobem) Použijte `ILDasm` k `.dll` zobrazení informací o tom, jaká sestavení skutečně potřebují za běhu. Pak určete, ze kterého balíčku NuGet pocházejí.

[`project.json`](project-json.md)Podrobnosti o funkcích, které vám pomůžou při vytváření balíčku, který podporuje TxM, najdete v tématu `dotnet` .

> [!Important]
> Pokud má váš balíček sloužit k práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složku, aby se předešlo varování a potenciálním problémům s kompatibilitou.

## <a name="directory-structure"></a>Adresářová struktura

Balíčky NuGet v tomto formátu mají následující dobře známou složku a chování:

| Složka | Chování |
| --- | --- |
| Sestavení | Obsahuje cíle a soubory props nástroje MSBuild v této složce jsou v projektu integrovány jinak, ale v opačném případě nedojde ke změně. |
| Nástroje | `install.ps1` a `uninstall.ps1` nejsou spuštěny. `init.ps1` funguje stejně jako vždy. |
| Content | Obsah není automaticky zkopírován do projektu uživatele. Podpora pro zahrnutí obsahu v projektu je plánována pro pozdější verzi. |
| Knihovna | Pro mnoho balíčků `lib` funguje stejným způsobem jako v NuGet 2. x, ale s rozšířenými možnostmi, které je možné použít v ní, a lepší logikou pro vybírání správné podsložky při využívání balíčků. Nicméně při použití ve spojení s `ref` , `lib` Složka obsahuje sestavení, která implementují plochu určenou v sestaveních ve `ref` složce. |
| Odkazů | `ref` je volitelná složka, která obsahuje sestavení .NET, která definují veřejnou plochu (veřejné typy a metody) pro aplikaci, která má být zkompilována. Sestavení v této složce nemusí mít žádnou implementaci, jsou čistě použita k definování oblasti povrchu pro kompilátor. Pokud balíček nemá `ref` složku, pak `lib` je referenční sestavení i sestavení implementace. |
| Moduly runtime | `runtimes` je volitelná složka, která obsahuje kód specifický pro operační systém, jako je například architektura procesoru a specifické pro operační systém nebo jiné binární soubory závislé na platformě. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>Cíle a soubory props nástroje MSBuild v balíčcích

Balíčky NuGet mohou obsahovat `.targets` `.props` soubory a, které jsou importovány do jakéhokoli projektu MSBuild, do kterého je balíček nainstalován. V NuGet 2. x to bylo provedeno vložením `<Import>` příkazů do `.csproj` souboru, v NuGet 3,0 neexistuje žádná konkrétní akce "instalace do projektu". Proces obnovení balíčku místo toho zapisuje dva soubory `[projectname].nuget.props` a `[projectname].NuGet.targets` .

Nástroj MSBuild ví, že tyto dva soubory budou hledat, a automaticky je naimportuje poblíž začátku a blízko konce procesu sestavení projektu. To poskytuje velmi podobné chování jako NuGet 2. x, ale s jedním významným rozdílem: *v tomto případě není nijak zaručeno pořadí souborů targets/props*. Nástroj MSBuild však poskytuje možnosti pro seřazení cílů pomocí `BeforeTargets` atributů a `AfterTargets` `<Target>` definice (viz [element Target (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib a ref

Chování `lib` složky se v NuGet V3 významně nezměnilo. Nicméně všechna sestavení musí být v podsložkách s názvem po TxM a nelze je nadále umístit přímo do `lib` složky. TxM je název platformy, pro kterou má daný Asset v balíčku fungovat. Logicky jsou toto rozšíření monikerů cílového rozhraní (TFM), například,, `net45` `net46` `netcore50` a `dnxcore50` jsou všechny příklady TxMs (viz [cílové architektury](../reference/target-frameworks.md). TxM může odkazovat na rozhraní Framework (TFM) a také na jiné oblasti Surface specifické pro platformu. Například UWP TxM ( `uap10.0` ) představuje oblast povrchu rozhraní .NET a také plochu Windows pro aplikace UWP.

Ukázková struktura lib:

```
lib
├───net40
│       MyLibrary.dll
└───wp81
        MyLibrary.dll
```

`lib`Složka obsahuje sestavení, která se používají za běhu. Pro většinu balíčků `lib` je všechny požadované složky pro každý cílový TxMs.

## <a name="ref"></a>Odkazů

V některých případech se v průběhu kompilace mají použít jiné sestavení (referenční sestavení .NET to udělá dnes). V takových případech použijte složku na nejvyšší úrovni s názvem `ref` (krátká pro "referenční sestavení").

Většina tvůrců balíčků nevyžaduje `ref` složku. Je užitečné pro balíčky, které musí poskytovat konzistentní plochu pro kompilaci a IntelliSense, ale pak mají odlišnou implementaci pro různé TxMs. Největším případem použití tohoto jsou `System.*` balíčky, které se vytvářejí jako součást přenosu .NET Core na NuGet. Tyto balíčky mají různé implementace, které jsou sjednocené konzistentní sadou referenčních sestavení.

Mechanicky jsou sestavení obsažená ve `ref` složce referenční sestavení, která jsou předávána kompilátoru. Pro ty, které jste použili csc.exe jsou ta sestavení, která jsou předávána přepínači [možnosti jazyka C#/Reference](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) .

Struktura `ref` složky je stejná jako například `lib` :

```
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
```

V tomto příkladu jsou všechna sestavení v `ref` adresářích identická.

## <a name="runtimes"></a>Moduly runtime

Složka runtime obsahuje sestavení a nativní knihovny, které jsou nutné ke spuštění v konkrétních "modulech runtime", které jsou obecně definovány operačním systémem a architekturou procesoru. Tyto moduly runtime jsou identifikovány pomocí [identifikátorů modulu runtime (identifikátorů RID)](/dotnet/core/rid-catalog) , jako jsou,,, atd `win` `win-x86` `win7-x86` `win8-64` .

## <a name="native-helpers-to-use-platform-specific-apis"></a>Nativní pomocníky pro použití rozhraní API specifických pro konkrétní platformu

Následující příklad ukazuje balíček, který má čistě spravovanou implementaci pro několik platforem, ale používá nativní pomocníky v systému Windows 8, kde může volat nativní rozhraní API specifická pro systém Windows 8.

```
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
```

S ohledem na výše uvedený balíček dojde k následujícím akcím:

- Pokud není ve Windows 8, `lib/net40/MyLibrary.dll` používá se sestavení.

- Při použití v systému Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` je použit a `native/MyNativeHelper.dll` zkopírován do výstupu sestavení.

V příkladu výše `lib/net40` sestavení je čistě spravovaný kód, zatímco sestavení ve složce runtime budou p/Invoke do nativního sestavení pomocníka pro volání rozhraní API specifická pro systém Windows 8.

`lib`Je možné vybrat pouze jednu složku, takže pokud je složka specifická pro modul runtime, která je zvolena pouze pro konkrétní nemodul runtime `lib` . Nativní složka je aditivní, pokud existuje, je zkopírována do výstupu sestavení.

## <a name="managed-wrapper"></a>Spravovaná obálka

Dalším způsobem, jak použít modul runtime, je dodávat balíček, který je čistě spravovanou obálkou prostřednictvím nativního sestavení. V tomto scénáři vytvoříte balíček podobný následujícímu:

```
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
```

V takovém případě neexistuje složka nejvyšší úrovně `lib` jako tato složka, protože není k dispozici žádná implementace tohoto balíčku, která nespoléhá na příslušné nativní sestavení. Pokud bylo spravované sestavení `MyLibrary.dll` přesně stejné v obou těchto případech, můžeme ho umístit do složky na nejvyšší úrovni `lib` , ale vzhledem k tomu, že chybějící nativní sestavení nezpůsobí selhání balíčku, pokud byl nainstalován na platformu, která se nenainstalovala-x86 nebo Win-x64, bude použita knihovna lib nejvyšší úrovně, ale nezkopírovalo se žádné nativní sestavení.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Vytváření balíčků pro NuGet 2 a NuGet 3

Chcete-li vytvořit balíček, který mohou být spotřebovány projekty používajícími `packages.config` i balíčky, použijte `project.json` následující postup:

- Pouze referenční a běhové moduly fungují pouze na NuGet 3. Obě tyto parametry ignorují aplikace NuGet 2.

- Nemůžete spoléhat `install.ps1` na `uninstall.ps1` funkce nebo na funkci. Tyto soubory jsou spouštěny při použití `packages.config` , ale jsou ignorovány v `project.json` . Takže váš balíček musí být použitelný bez spuštění. `init.ps1` pořád běží na NuGet 3.

- Instalace cílů a vlastností se liší, takže se ujistěte, že váš balíček funguje na obou klientech podle očekávání.

- Podadresáře lib musí být TxM v NuGet 3. Knihovny nelze umístit do kořenového adresáře `lib` složky.

- Obsah se nekopíruje automaticky s NuGet 3. Příjemci vašeho balíčku by mohli sami zkopírovat soubory nebo použít nástroj jako Spouštěč úloh k automatizaci kopírování souborů.

- Transformace zdrojového a konfiguračního souboru nejsou spouštěny NuGet 3.

Pokud podporujete NuGet 2 a 3 `minClientVersion` , měla by se jednat o nejnižší verzi klienta NuGet 2, na které váš balíček funguje. V případě existujícího balíčku by neměl být nutné ho změnit.
