---
title: Předběžné verze v balíčcích NuGet
description: Pokyny k vytváření balíčky v předběžné verzi
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 696f51905198defdbfd475ba7d010ac3e27ac557
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877946"
---
# <a name="building-pre-release-packages"></a>Vytváření balíčky v předběžné verzi

Pokaždé, když vydáte aktualizovaného balíčku pomocí nové číslo verze, NuGet bere v úvahu, že jedna jako "nejnovější stabilní verzi" jak je znázorněno, například uživatelské rozhraní Správce balíčků sady Visual Studio:

![Nejnovější stabilní verze zobrazující uživatelské rozhraní Správce balíčků](media/Prerelease_01-LatestStable.png)

Stabilní verze je ten, který se považuje za dostatečně spolehlivé na to, který se má použít v produkčním prostředí. Nejnovější stabilní verze je také ten, který se nainstaluje jako aktualizace balíčku nebo při obnovení balíčků (v souladu s omezeními, jak je popsáno v [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)).

Pro podporu životního cyklu verze softwaru, NuGet 1.6 nebo novější umožňuje distribuční balíčky v předběžné verzi, kde číslo verze zahrnuje příponu sémantické správy verzí, například `-alpha`, `-beta`, nebo `-rc`. Další informace najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).

Tyto verze můžete určit třemi způsoby:

- `.nuspec` soubor: zahrnout příponu sémantickou verzi v `version` element:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- `.csproj` soubor: zahrnout příponu sémantickou verzi v `PackageVersion` element:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- Atributy sestavení: Zadejte verzi pomocí `AssemblyInformationalVersionAttribute`:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet vybere tuto hodnotu místo verze zadaná v `AssemblyVersion` atribut, který nepodporuje sémantické správy verzí.

Jakmile budete připraveni k uvolnění stabilní verzi, odeberte příponu a balíček má přednost před všechny předběžné verze. Znovu, naleznete v tématu [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Instalace a aktualizace předběžné verze balíčků

Ve výchozím nastavení NuGet nezahrnuje předběžných verzí při práci s balíčky, ale toto chování můžete změnit následujícím způsobem:

- **Uživatelské rozhraní Správce balíčků v sadě Visual Studio**: V **spravovat balíčky NuGet** uživatelského rozhraní, zkontrolujte **zahrnout předběžné verze** pole:

    ![Políčko zahrnout předběžné verze v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Nastavení nebo zrušením zaškrtnutí tohoto políčka se aktualizuje uživatelské rozhraní Správce balíčků a seznam dostupných verzí, kterou můžete nainstalovat.

- **Konzola správce balíčků**: Použití `-IncludePrerelease` přepněte se `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, a `Update-Package` příkazy. Odkazovat [referenční informace prostředí PowerShell](../tools/powershell-reference.md).

- **Rozhraní příkazového řádku NuGet**: Použití `-prerelease` přepněte se `install`, `update`, `delete`, a `mirror` příkazy. Odkazovat [odkaz na rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Sémantické správy verzí

[Semantic Versioning nebo SemVer konvence](http://semver.org/spec/v1.0.0.html) popisuje, jak využívat řetězce v číslech verzí na významu základní kód.

V této konvenci, každá verze má tři části `Major.Minor.Patch`, s následující význam:

- `Major`: Změny způsobující chyby
- `Minor`: Nové funkce, ale zpětně kompatibilní
- `Patch`: Zpětně kompatibilní chyby opravuje pouze

Předběžné verze jsou rozlišeny pak připojením spojovníkem a řetězec za číslo opravy. Technicky vzato můžete použít *jakékoli* řetězec po spojovníkem a NuGet bude považovat za balíček předběžné verze. Celé číslo verze NuGet pak zobrazí v příslušné uživatelské rozhraní, byste museli opustit příjemci k interpretaci význam sami.

To na paměti je obecně vhodné sledovat rozpoznaný konvence pojmenování, jako je následující:

- `-alpha`: Alfa verze, obvykle se používá pro nedokončenou prací a experimentování
- `-beta`: Betaverze, obvykle ten, který je funkce pro další plánované vydání, ale může obsahovat známé chyby.
- `-rc`: Verze Release candidate, obvykle, která je potenciálně konečné vydání (stabilní), není-li významný chyby se objeví.

> [!Note]
> Podporuje NuGet 4.3.0+ [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), která podporuje předběžné verze čísla pomocí zápisu s tečkou, stejně jako v `1.0.1-build.23`. Verze NuGet starší než 4.3.0 nepodporuje zápisu s tečkou. V dřívějších verzích balíčku nuget, můžete použít formuláře jako `1.0.1-build23` , ale to vždy považovaná za Předběžná verze.

Libovolné přípony použijete, ale NuGet se jim přednost ve vzestupném abecedním pořadí:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

Jak je znázorněno, verze bez žádné přípony bude vždy přednost předběžné verze. Všimněte si také, že pokud použijte číselné přípony značkami předběžné verze, které můžou používat číslicemi čísla (nebo více), pomocí úvodní nuly. jako beta01 a beta05 Ujistěte se, že budou řadit správně při čísla narůstají.
