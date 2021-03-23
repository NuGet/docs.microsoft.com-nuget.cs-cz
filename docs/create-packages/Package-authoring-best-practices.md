---
title: Osvědčené postupy pro vytváření balíčků
description: Obecná příručka k osvědčeným postupům pro vytváření vysoce kvalitních balíčků NuGet.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: 7475cf655876f2c127e79a16ccf67c0c723d164f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859067"
---
# <a name="package-authoring-best-practices"></a>Osvědčené postupy pro vytváření balíčků

Tento návod je určený k tomu, aby autoři balíčku NuGet vytvořili nezjednodušený odkaz na vytváření a publikování vysoce kvalitních balíčků. Primárně se zaměřuje na osvědčené postupy specifické pro konkrétní balíčky, jako jsou metadata a balení. Další podrobné návrhy pro vytváření knihoven s vysokou kvalitou najdete v tématu doprovodné materiály [ke knihovně .NET Open Source](https://docs.microsoft.com/dotnet/standard/library-guidance/).

## <a name="types-of-recommendations"></a>Typy doporučení

Každý článek nabízí čtyři typy doporučení: **udělejte**, **zvažte**, **Vyhněte** se a **nepoužívejte.** Typ doporučení indikuje, jak by mělo následovat.

Měli byste téměř **vždy postupovat podle doporučení do** . Například:

✔️ Zahrňte krátký popis balíčku, který popisuje, pro který z nich je.

Na druhé **straně doporučujeme, abyste měli doporučení obecně** , ale existují legitimní výjimky pro toto pravidlo:

✔️ Zvažte možnost zvolit název balíčku NuGet s předponou, která splňuje [kritéria](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)rezervace předpon NuGet.

**Vyhněte** se doporučením označení věcí, které obecně nejsou dobrý nápad, ale porušení pravidla je někdy vhodné:

❌ Vyhněte se odkazům na balíček NuGet, které vyžadují přesnou verzi.

A nakonec nenaznačují doporučení, co byste měli skoro **nikdy dělat:**

❌ Nepoužívejte `LicenseUrl` vlastnost metadata.

## <a name="create-a-nuget-package"></a>Vytvoření balíčku NuGet

Nejnovější doporučený způsob, jak vytvořit balíček NuGet, je z [projektu ve stylu sady SDK](https://docs.microsoft.com/nuget/resources/check-project-format). Vlastnosti projektu ve stylu sady SDK, včetně [cílové architektury](https://docs.microsoft.com/dotnet/standard/frameworks) a [metadat balíčku](#package-metadata), jsou definovány v [souboru projektu](https://docs.microsoft.com/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Vytvořte balíček z projektu ve stylu sady SDK definováním požadovaných vlastností a balení v sadě [Visual Studio](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli) nebo rozhraní příkazového [řádku dotnet](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli).

✔️ vytvořit projekt ve stylu sady SDK a vytvořit (balíček) balíček pomocí sady Visual Studio nebo rozhraní příkazového řádku dotnet.

Podrobnější pokyny týkající se vytváření balíčků včetně nezbytných nástrojů klienta, příkladu souboru projektu a příkazů najdete v tématu [Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet](https://docs.microsoft.com/nuget/create-packages/creating-a-package-dotnet-cli).

Informace o tom, které rozhraní .NET Framework se mají zaměřit, najdete v našich [nejnovějších pokynech pro cílení na různé platformy](https://docs.microsoft.com/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Metadata balíčků

Metadata jsou základní komponentou balíčku NuGet. Kvalita vašich metadat může značně ovlivnit zjistitelnost, použitelnost a důvěryhodnost vašeho balíčku.

V aplikaci Visual Studio doporučujeme zadat metadata balíčku do projektu > vlastnosti [název projektu] > balíčku.

Prvky metadat balíčku lze také [zadat přímo v souboru projektu](https://docs.microsoft.com/nuget/create-packages/creating-a-package-msbuild#set-properties).

Níže je mapování tabulky a popis dostupných prvků metadat balíčku:

| Název vlastnosti sady Visual Studio                   | [Název souboru projektu nebo vlastnosti MSBuild](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                          | [Název vlastnosti nuspec](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema) | Popis                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| [`Package id`](#package-id)                   | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                            | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                      | Název nebo identifikátor balíčku.                    |
| [`Package version`](#package-version)         | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                  | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                            | Verze balíčku NuGet                                           |
| [`Authors`](#authors)                         | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                            | Čárkami oddělený seznam autorů balíčků, často se používá "Přezdívka" jednotlivce nebo organizace.                             |
| [`Description`](#description)                 | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                        | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                    | Popis balíčku                                                                |
| [`Copyright`](#copyright)                     | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                            | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                        | Podrobnosti o autorských právech pro balíček.                                                                      |
| [`Licensing - Expression`](#licensing)        | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file) | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)          | Výraz SPDX licence.       |
| [`Licensing - File`](#licensing)              | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)       | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                | Cesta k souboru vlastní licence                                               |
| [`Project URL`](#project-url)                 | `PackageProjectUrl`                                                                                                                     | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                      | Adresa URL domovské stránky projektu.                                                                                   |
| [`Icon File`](#icon)                          | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                  | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                  | Cesta k souboru obrázku ikony balíčku                                                                      |
| [`Repository URL`](#repository-type-and-url)  | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                    | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)               | Adresa URL úložiště, ze kterého byl balíček sestaven.                                                           |
| [`Repository type`](#repository-type-and-url) | [`RepositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                 | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)              | Typ úložiště, na které adresa URL úložiště odkazuje (např. Git)                                                   |
| [`Tags`](#tags)                               | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                        | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                  | Mezerou oddělený seznam značek a klíčových slov, které popisují balíček. Značky se používají při hledání balíčků. |
| [`Release notes`](#release-notes)             | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                  | Popis změn provedených v této verzi balíčku.                                                 |

### <a name="package-id"></a>ID balíčku

Pokud publikujete úplně nový balíček:

✔️ Vyberte ID balíčku, které je jedinečné a jasně se odlišuje od stávajících balíčků v NuGet.org.
> Můžete zkontrolovat, jestli je ID balíčku jedinečné a differentiable, a to tak, že vyhledáte ID v NuGet.org nebo zkontrolujete, jestli následující odkaz existuje: https://www.nuget.org/packages/<package název \> .

✔️ Zvažte možnost zvolit název balíčku NuGet s předponou, která splňuje [kritéria rezervace předpon](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation#id-prefix-reservation-criteria)NuGet.
> Po zachovávání ID předpony balíčku se vám zobrazí ověřená značka zaškrtnutí: ![ Obrázek](media/Verified-check-mark.png)
> 
> Další informace najdete v [dokumentaci k rezervované předponě ID balíčku](https://docs.microsoft.com/nuget/nuget-org/id-prefix-reservation) .

### <a name="package-version"></a>Verze balíčku

✔️ Zvažte použití [SemVer](https://semver.org/) pro verzi balíčku NuGet.
> V podstatě to znamená použití formátu hlavní. podverze. patch [-inverze].

✔️ publikovat balíček jako [předběžnou verzi balíčku](https://docs.microsoft.com/nuget/create-packages/prerelease-packages) , pokud není stabilní nebo ve verzi Preview.

Pokročilejší doprovodné [materiály najdete v Průvodci správou verzí knihovny .NET](https://docs.microsoft.com/dotnet/standard/library-guidance/versioning) .

### <a name="authors"></a>Autoři

✔️ Použijte pole Author pro "Přezdívka" nebo "Přezdívka" vaší organizace.
> Pokud je například moje uživatelské jméno NuGet.org "pnovak", pak se pro pole Author používá Jana Karásek, může to pomoci uživatelům pochopit jako autora. Pokud je uživatelské jméno NuGet.org vaší organizace "ContosoToolkit", pak se používá contoso Corporation, může být lépe rozpoznatelný a inspirovatější důvěryhodnost zákazníků.
### <a name="description"></a>Popis

pro popis balíčku ✔️ zahrnout krátký popis (až 4000 znaků).
> Popisy balíčků jsou jedním z nejvýraznějších polí umístěných v nástroji NuGet Search a pravděpodobně budou prvními uživateli, kteří budou mít možnost zjistit, zda je balíček pro ně pro ně nejvhodnější.

### <a name="copyright"></a>Copyright

✔️ Zvažte použití autorského práva k balíčku pomocí autorského práva (c) <název/společnost \> <Year \> .
>Oznámení o autorských právech v podstatě indikuje, že vaši práci nejde zkopírovat bez vašeho svolení. Zahrnutí oznámení o autorských právech do balíčku je jednoduché a nebude dělat žádné škody.

Příklad: Copyright (c) contoso 2020

### <a name="licensing"></a>Licencování

✔️ do [balíčku zahrnout licenční výraz nebo soubor s licencí](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Projekt bez licence se nastaví na [výhradní Copyright](https://choosealicense.com/no-permission/), což znamená, že jste nikomu neudělili oprávnění k používání vašeho projektu.

❌ Nepoužívejte nepoužitou vlastnost zastaralá `LicenseUrl` metadata.
> To představuje právní nejednoznačnost, protože změny licencí na adrese URL budou zpětně změněny zobrazené licence pro předchozí verze balíčků.

#### <a name="if-your-package-is-open-source"></a>Pokud je váš balíček [Open Source](https://opensource.org/osd)

✔️ [zvolit open source licenci](https://choosealicense.com/) , aby byl váš otevřený zdroj balíčku.
> *"Open Source licence jsou licence, které jsou v rozporu s definicí open source – v krátkém případě umožňují volně používat, upravovat a sdílet software."* -Open Source Initiative. Další informace o open source softwaru a z open source iniciativy najdete v části https://opensource.org/ .

✔️ Zvažte [zahrnutí licenčního výrazu do balíčku](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Výrazy s licenčními výrazy jsou zřetelnější a umožňují uživatelům, kteří můžou použít váš balíček, nebo pokud se licence změnila. 
> [!Note]
> NuGet.org akceptuje pouze licenční výrazy pro licence, které jsou schváleny v rámci iniciativy Open Source nebo Free Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Pokud váš balíček není open source

✔️ do [balíčku zahrnout licenční soubor](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file).
> Do balíčku můžete přidat jakýkoli soubor s licencí (. txt nebo. MD), včetně nestandardních licencí. 

### <a name="project-url"></a>Adresa URL projektu

✔️ Zvažte zahrnutí odkazu do přidruženého projektu, úložiště nebo webu společnosti.
> Váš projektový web by měl mít všechny uživatele, kteří o vašem balíčku potřebují, a pravděpodobně bude, kde uživatelé hledají dokumentaci.

### <a name="icon"></a>Ikona

✔️ Zvažte [zahrnutí ikony s balíčkem](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file) , které vám pomůžou vizuálně odlišit. Je to relativně malé přidání, které může zlepšit vnímání kvality balíčku.
> Ikony můžou být specifické pro jednotlivé balíčky nebo jako logo značky.

✔️ použít obrázek, který je 128 × 128 a má transparentní pozadí (PNG) pro nejlepší výsledky zobrazení.
> NuGet automaticky škálovat bitovou kopii na klienta, na kterém se zobrazuje.

❌ Nepoužívejte nepoužitou vlastnost zastaralá `IconUrl` metadata.

### <a name="repository-type-and-url"></a>Typ a adresa URL úložiště

✔️ Zvažte nastavení [zdrojového odkazu](https://docs.microsoft.com/dotnet/standard/library-guidance/sourcelink) na automatické přidání metadat správy zdrojového kódu do balíčku NuGet a usnadnění ladění vaší knihovny.
> Zdrojový odkaz automaticky přidá `Repository URL` a `Repository Type` do metadat balíčku. Přidá taky konkrétní potvrzení přidružené k vaší verzi balíčku.

### <a name="tags"></a>Značky

✔️ zahrnout několik značek s klíčovými podmínkami týkajícími se vašeho balíčku, aby se zvýšila zjistitelnost.
> Značky se přijímají v rámci NuGet. vyhledávacího algoritmu organizace a jsou zvláště užitečné pro výrazy, které nejsou v ID balíčku, ale jsou relevantní.

Pokud jste například publikovali balíček pro řetězce protokolu do konzoly, budu zahrnovat: "protokolování, protokol, konzola, řetězec, výstup"

### <a name="release-notes"></a>Poznámky k verzi

✔️ VZÍT v úvahu poznámky k verzi s každou aktualizací, která obsahuje informace o tom, jaké změny byly provedeny.
> I když není pro poznámky k verzi nutný žádný konkrétní formát, doporučujeme, abyste měli následující:
>
> 1. Změny způsobující chyby
> 2. Nové funkce
> 3. Opravy chyb
> 
> Pokud už ve svém úložišti Vysledujete poznámky k verzi nebo protokol změn, můžete taky přidat odkaz na příslušný soubor.

## <a name="related-topics"></a>Související témata

- [Vytvoření a publikování balíčku (rozhraní příkazového řádku dotnet)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)
- [Vytvoření a publikování balíčku (Visual Studio)](https://docs.microsoft.com/nuget/quickstart/create-and-publish-a-package-using-visual-studio?tabs=netcore-cli)
