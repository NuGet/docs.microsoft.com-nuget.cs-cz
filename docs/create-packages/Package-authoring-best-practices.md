---
title: Osvědčené postupy pro vytváření balíčků
description: Všeobecný průvodce osvědčenými postupy pro vytváření vysoce kvalitních balíčků NuGet.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: ec1532900bed7d13ea2400afe9f855105a5c2fde
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209888"
---
# <a name="package-authoring-best-practices"></a>Osvědčené postupy pro vytváření balíčků

Cílem těchto pokynů je poskytnout NuGet balíčků jednoduchý odkaz na vytváření a publikování vysoce kvalitních balíčků. Zaměřuje se především na osvědčené postupy specifické pro balíček, jako jsou metadata a balení. Podrobnější návrhy pro vytváření vysoce kvalitních knihoven najdete v pokynech pro open [source knihovny](/dotnet/standard/library-guidance/)pro .NET.

## <a name="types-of-recommendations"></a>Typy doporučení

Každý článek obsahuje čtyři typy doporučení: **Do**, **Consider**, **Avoid** a **Do not**. Typ doporučení určuje, jak blízko by se mělo postupovat.

Téměř vždy byste měli postupovat podle **doporučení Do.** Například:

✔️ DO obsahují krátký popis balíčku, který popisuje, k čemu ho máte.

Na druhou stranu zvažte, **jestli** byste obecně měli dodržovat doporučení, ale existují legitimní výjimky pravidla:

✔️, že NuGet název balíčku s předponou, která splňuje NuGet předpony [rezervace](../nuget-org/id-prefix-reservation.md).

**Vyhněte** se doporučením zmiňte věci, které obecně nejsou dobrý nápad, ale porušení pravidla někdy dává smysl:

❌VYHNĚTE NuGet, které vyžadují přesnou verzi.

A nakonec, **nedávají doporučení** naznačovat něco, co byste téměř nikdy neměli dělat:

❌ NEPOUŽÍVEJTE vlastnost `LicenseUrl` metadat.

## <a name="create-a-nuget-package"></a>Vytvoření NuGet balíčku

Nejnovější doporučený způsob vytvoření balíčku NuGet je z projektu [ve stylu sady SDK.](../resources/check-project-format.md) Vlastnosti projektu ve stylu sady SDK, včetně [cílové architektury](/dotnet/standard/frameworks) a [metadat balíčku](#package-metadata), jsou definovány v [souboru projektu](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file).

Vytvořte balíček z projektu ve stylu sady SDK definováním požadovaných vlastností a balením [v Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) nebo rozhraní příkazového řádku [dotnet.](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)

✔️ vytvořte projekt ve stylu sady SDK a vytvořte (zabalte) balíček pomocí Visual Studio nebo rozhraní příkazového řádku dotnet.

Podrobnější pokyny týkající se vytváření balíčků, včetně potřebných klientských nástrojů, příkladu souboru projektu a příkazů, najdete v tématu Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku [dotnet.](./creating-a-package-dotnet-cli.md)

Pokud se chcete rozhodnout, na která rozhraní .NET se má cílit, podívejte se na naše nejnovější pokyny pro [cílení napříč platformami.](/dotnet/standard/library-guidance/cross-platform-targeting)

## <a name="package-metadata"></a>Metadata balíčků

Metadata jsou základní součástí libovolného NuGet balíčku. Kvalita metadat může výrazně ovlivnit zjistitelnost, použitelnost a důvěryhodnost balíčku.

V Visual Studio se doporučuje zadat metadata balíčku tak, že Project > vlastnosti [Project Name] > Package.

Elementy metadat balíčku lze [zadat také přímo v souboru projektu](./creating-a-package-msbuild.md#set-properties).

Níže je uvedeno mapování tabulky a popis dostupných elementů metadat balíčku:

| Visual Studio názvu vlastnosti                       | [Project souboru nebo MSBuild vlastnosti](/dotnet/core/tools/csproj#packagereleasenotes)                              | [Název vlastnosti Nuspec](/nuget/reference/nuspec#general-form-and-schema)   | Popis                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`id`](/nuget/reference/nuspec#id)                                        | Název nebo identifikátor balíčku.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](/nuget/reference/msbuild-targets#pack-target)                                                      | [`version`](/nuget/reference/nuspec#version)                              | NuGet verze balíčku.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](/nuget/reference/msbuild-targets#pack-target)                                                                 | [`authors`](/nuget/reference/nuspec#authors)                              | Čárkami oddělený seznam autorů balíčků, kteří často používají "pěkný název" jednotlivce nebo organizace.           |
| [`Description`](#description)                     | [`Description`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`description`](/nuget/reference/nuspec#description)                      | Popis balíčku.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`copyright`](/nuget/reference/nuspec#copyright)                          | Podrobnosti o autorských právech balíčku.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)     | [`license type="expression"`](/nuget/reference/nuspec#license)            | Výraz licence SPDX.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)           | [`license type="file"`](/nuget/reference/nuspec#license)                  | Cesta k souboru vlastní licence.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](/nuget/reference/nuspec#projecturl)                        | Adresa URL domovské stránky projektu.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                      | [`icon`](/nuget/reference/nuspec#icon)                                    | Cesta k souboru obrázku ikony balíčku                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](/nuget/reference/msbuild-targets#pack-target)                                                       | [`repository url`](/nuget/reference/nuspec#repository)                    | Adresa URL úložiště, ze kterého byl balíček sestaven.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository type`](/nuget/reference/nuspec#repository)                   | Typ úložiště, na které adresa URL úložiště odkazuje (tj. "git").                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`tags`](/nuget/reference/nuspec#tags)                                    | Seznam značek a klíčových slov oddělených mezerou, které popisují balíček. Značky se používají při hledání balíčků.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](/nuget/reference/msbuild-targets#pack-target)                                         | [`releaseNotes`](/nuget/reference/nuspec#releasenotes)                    | Popis změn provedených v této verzi balíčku                                                     |
### <a name="package-id"></a>ID balíčku

Pokud publikujete zcela nový balíček:

✔️ SI ID balíčku, které je jedinečné a jasně odlišené od existujících balíčků na NuGet.org.
> Pokud chcete zkontrolovat, jestli je ID balíčku jedinečné a odliší se, můžete ho vyhledat na webu NuGet.org nebo zkontrolovat, jestli existuje následující odkaz: https://www.nuget.org/packages/<package name \> .

✔️, že NuGet název balíčku s předponou, která splňuje NuGet [předpony rezervace](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria).
> Rezervace ID předpony pro váš balíček vám umožní získat ověřenou značku zaškrtnutí: ![ image](media/Verified-check-mark.png)
> 
> Další informace najdete v dokumentu [rezervace Předpona ID](../nuget-org/id-prefix-reservation.md) balíčku.

### <a name="package-version"></a>Verze balíčku

✔️ verzi svého balíčku [NuGet Použít SemVer.](https://semver.org/)
> V podstatě to znamená použití formátu Major.Minor.Patch[-prerelease].

✔️ balíček publikovat jako předběžnou verzi, pokud je nestabilní nebo ve verzi Preview. [](./prerelease-packages.md)

Pokročilejší pokyny najdete v průvodci [s sekcí](/dotnet/standard/library-guidance/versioning) verzí knihoven .NET.

### <a name="authors"></a>Autoři

✔️ pro "pěkný jméno" vaší organizace nebo vaší organizace použijte pole autora.
> Pokud je například uživatelské jméno NuGet.org "jdoe", může použití "Jane Doe" pro pole autora pomoct zákazníkům rozpoznat mě jako autora. Pokud uživatelské jméno organizace NuGet.org je ContosoToolkit, může být použití contoso corporation rozpoznatelné a inspirovat více důvěry spotřebitelů.
### <a name="description"></a>Popis

✔️ DO obsahují krátký popis (až 4 000 znaků) pro popis balíčku.
> Popisy balíčků jsou jedním z nejvýznamnějších polí, která se zobrazí při hledání v NuGet NuGet bude pravděpodobně první věcí, na kterou se potenciální spotřebiteli podívá, aby zjistili, jestli je pro ně balíček správný.

### <a name="copyright"></a>Copyright

✔️ zvažte použití autorských práv k balíčku s názvem nebo <autorskými právy (c) \> <\> roku.
>Oznámení o autorských právech v podstatě značí, že vaše práce se bez vašeho oprávnění nekopíruje. Zahrnutí oznámení o autorských právech do balíčku je snadné a neuškodí!

Příklad: Copyright (c) Contoso 2020

### <a name="licensing"></a>Licencování

✔️ do [balíčku zahrřte licenční výraz](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)nebo licenční soubor.
> [!IMPORTANT]
> Projekt bez licence má ve výchozím nastavení výhradní [autorská](https://choosealicense.com/no-permission/)práva, což znamená, že jste neudělují žádným oprávnění k používání vašeho projektu.

❌ NEPOUŽÍVEJTE zastaralou vlastnost `LicenseUrl` metadat.
> To představuje právní nejednoznačnost, protože změny licencí na adrese URL zpětně změní zobrazenou licenci pro předchozí verze balíčku.

#### <a name="if-your-package-is-open-source"></a>Pokud je váš balíček [open source](https://opensource.org/osd)

✔️, aby [open source váš](https://choosealicense.com/) balíček open source, zvolte vlastní open source.
> *"Open source licence jsou licence, které jsou v souladu s definicí open source – ve stručnosti umožňují volně používat, upravovat a sdílet software."* – Open Source Initiative. Další informace o open source a open source iniciativě najdete https://opensource.org/ v .

✔️ ZVAŽTE [zahrnutí výrazu licence do balíčku](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Výrazy licencí se předchytá nejsnadnějším způsobem a zviditelní je pro uživatele, pokud mohou váš balíček použít nebo pokud se licence změnila. 
> [!Note]
> NuGet.org přijímá výrazy licencí pouze pro licence schválené iniciativou Open Source initiative nebo Free Software Foundation.

#### <a name="if-your-package-is-not-open-source"></a>Pokud váš balíček není open source

✔️ zahrnout [licenční soubor do balíčku](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Do balíčku je možné přidat jakýkoli licenční soubor (.txt nebo .md), včetně nestandardních licencí. 

### <a name="project-url"></a>Project Adresu url

✔️ ZVÁŽIT zahrnutí odkazu na přidružený projekt, úložiště nebo web společnosti.
> Váš projektový web by měl mít vše, co uživatelé potřebují vědět o vašem balíčku, a pravděpodobně tam budou hledat dokumentaci.

### <a name="icon"></a>Ikona

✔️ ZVAŽTE [zahrnutí ikony s balíčkem,](../reference/msbuild-targets.md#packing-an-icon-image-file) která vám pomůže ho vizuálně odlišit. Je to poměrně malý doplněk, který může zlepšit vnímání kvality balíčku.
> Ikony mohou být specifické pro jednotlivé balíčky nebo logo značky.

✔️ použít obrázek, který je 128 × 128 a má transparentní pozadí (PNG) pro nejlepší výsledky zobrazení.
> NuGet automaticky škáluje image na klienta, na které se zobrazuje.

❌ NEPOUŽÍVEJTE zastaralou vlastnost `IconUrl` metadat.

### <a name="repository-type-and-url"></a>Typ a adresa URL úložiště

✔️ zvažte nastavení [zdrojového odkazu](/dotnet/standard/library-guidance/sourcelink) pro automatické přidání metadat správy zdrojového kódu do balíčku NuGet a usnadnění ladění vaší knihovny.
> Zdrojový odkaz automaticky přidá `Repository URL` a `Repository Type` do metadat balíčku. Přidá taky konkrétní potvrzení přidružené k vaší verzi balíčku.

### <a name="tags"></a>Značky

✔️ zahrnout několik značek s klíčovými podmínkami týkajícími se vašeho balíčku, aby se zvýšila zjistitelnost.
> značky se přeberou v úvahu v NuGet algoritmus pro hledání organizace a jsou zvláště užitečné pro výrazy, které nejsou v ID balíčku, ale jsou relevantní.

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

- [Vytvoření a publikování balíčku (rozhraní příkazového řádku dotnet)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Vytvoření a publikování balíčku (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
