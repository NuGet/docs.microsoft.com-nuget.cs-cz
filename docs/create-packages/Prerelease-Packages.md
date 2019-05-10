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
# <a name="building-pre-release-packages"></a><span data-ttu-id="4ef19-103">Vytváření balíčky v předběžné verzi</span><span class="sxs-lookup"><span data-stu-id="4ef19-103">Building pre-release packages</span></span>

<span data-ttu-id="4ef19-104">Pokaždé, když vydáte aktualizovaného balíčku pomocí nové číslo verze, NuGet bere v úvahu, že jedna jako "nejnovější stabilní verzi" jak je znázorněno, například uživatelské rozhraní Správce balíčků sady Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="4ef19-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Nejnovější stabilní verze zobrazující uživatelské rozhraní Správce balíčků](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="4ef19-106">Stabilní verze je ten, který se považuje za dostatečně spolehlivé na to, který se má použít v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="4ef19-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="4ef19-107">Nejnovější stabilní verze je také ten, který se nainstaluje jako aktualizace balíčku nebo při obnovení balíčků (v souladu s omezeními, jak je popsáno v [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="4ef19-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="4ef19-108">Pro podporu životního cyklu verze softwaru, NuGet 1.6 nebo novější umožňuje distribuční balíčky v předběžné verzi, kde číslo verze zahrnuje příponu sémantické správy verzí, například `-alpha`, `-beta`, nebo `-rc`.</span><span class="sxs-lookup"><span data-stu-id="4ef19-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="4ef19-109">Další informace najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="4ef19-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="4ef19-110">Tyto verze můžete určit třemi způsoby:</span><span class="sxs-lookup"><span data-stu-id="4ef19-110">You can specify such versions in three ways:</span></span>

- <span data-ttu-id="4ef19-111">`.nuspec` soubor: zahrnout příponu sémantickou verzi v `version` element:</span><span class="sxs-lookup"><span data-stu-id="4ef19-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="4ef19-112">`.csproj` soubor: zahrnout příponu sémantickou verzi v `PackageVersion` element:</span><span class="sxs-lookup"><span data-stu-id="4ef19-112">`.csproj` file: include the semantic version suffix in the `PackageVersion` element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="4ef19-113">Atributy sestavení: Zadejte verzi pomocí `AssemblyInformationalVersionAttribute`:</span><span class="sxs-lookup"><span data-stu-id="4ef19-113">Assembly attributes: specify the version using `AssemblyInformationalVersionAttribute`:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="4ef19-114">NuGet vybere tuto hodnotu místo verze zadaná v `AssemblyVersion` atribut, který nepodporuje sémantické správy verzí.</span><span class="sxs-lookup"><span data-stu-id="4ef19-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="4ef19-115">Jakmile budete připraveni k uvolnění stabilní verzi, odeberte příponu a balíček má přednost před všechny předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="4ef19-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="4ef19-116">Znovu, naleznete v tématu [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="4ef19-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="4ef19-117">Instalace a aktualizace předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="4ef19-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="4ef19-118">Ve výchozím nastavení NuGet nezahrnuje předběžných verzí při práci s balíčky, ale toto chování můžete změnit následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="4ef19-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="4ef19-119">**Uživatelské rozhraní Správce balíčků v sadě Visual Studio**: V **spravovat balíčky NuGet** uživatelského rozhraní, zkontrolujte **zahrnout předběžné verze** pole:</span><span class="sxs-lookup"><span data-stu-id="4ef19-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Políčko zahrnout předběžné verze v sadě Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="4ef19-121">Nastavení nebo zrušením zaškrtnutí tohoto políčka se aktualizuje uživatelské rozhraní Správce balíčků a seznam dostupných verzí, kterou můžete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="4ef19-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="4ef19-122">**Konzola správce balíčků**: Použití `-IncludePrerelease` přepněte se `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, a `Update-Package` příkazy.</span><span class="sxs-lookup"><span data-stu-id="4ef19-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="4ef19-123">Odkazovat [referenční informace prostředí PowerShell](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="4ef19-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="4ef19-124">**Rozhraní příkazového řádku NuGet**: Použití `-prerelease` přepněte se `install`, `update`, `delete`, a `mirror` příkazy.</span><span class="sxs-lookup"><span data-stu-id="4ef19-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="4ef19-125">Odkazovat [odkaz na rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="4ef19-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="4ef19-126">Sémantické správy verzí</span><span class="sxs-lookup"><span data-stu-id="4ef19-126">Semantic versioning</span></span>

<span data-ttu-id="4ef19-127">[Semantic Versioning nebo SemVer konvence](http://semver.org/spec/v1.0.0.html) popisuje, jak využívat řetězce v číslech verzí na významu základní kód.</span><span class="sxs-lookup"><span data-stu-id="4ef19-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="4ef19-128">V této konvenci, každá verze má tři části `Major.Minor.Patch`, s následující význam:</span><span class="sxs-lookup"><span data-stu-id="4ef19-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="4ef19-129">`Major`: Změny způsobující chyby</span><span class="sxs-lookup"><span data-stu-id="4ef19-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="4ef19-130">`Minor`: Nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="4ef19-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="4ef19-131">`Patch`: Zpětně kompatibilní chyby opravuje pouze</span><span class="sxs-lookup"><span data-stu-id="4ef19-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="4ef19-132">Předběžné verze jsou rozlišeny pak připojením spojovníkem a řetězec za číslo opravy.</span><span class="sxs-lookup"><span data-stu-id="4ef19-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="4ef19-133">Technicky vzato můžete použít *jakékoli* řetězec po spojovníkem a NuGet bude považovat za balíček předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="4ef19-133">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="4ef19-134">Celé číslo verze NuGet pak zobrazí v příslušné uživatelské rozhraní, byste museli opustit příjemci k interpretaci význam sami.</span><span class="sxs-lookup"><span data-stu-id="4ef19-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="4ef19-135">To na paměti je obecně vhodné sledovat rozpoznaný konvence pojmenování, jako je následující:</span><span class="sxs-lookup"><span data-stu-id="4ef19-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="4ef19-136">`-alpha`: Alfa verze, obvykle se používá pro nedokončenou prací a experimentování</span><span class="sxs-lookup"><span data-stu-id="4ef19-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="4ef19-137">`-beta`: Betaverze, obvykle ten, který je funkce pro další plánované vydání, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="4ef19-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="4ef19-138">`-rc`: Verze Release candidate, obvykle, která je potenciálně konečné vydání (stabilní), není-li významný chyby se objeví.</span><span class="sxs-lookup"><span data-stu-id="4ef19-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="4ef19-139">Podporuje NuGet 4.3.0+ [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), která podporuje předběžné verze čísla pomocí zápisu s tečkou, stejně jako v `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="4ef19-139">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="4ef19-140">Verze NuGet starší než 4.3.0 nepodporuje zápisu s tečkou.</span><span class="sxs-lookup"><span data-stu-id="4ef19-140">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="4ef19-141">V dřívějších verzích balíčku nuget, můžete použít formuláře jako `1.0.1-build23` , ale to vždy považovaná za Předběžná verze.</span><span class="sxs-lookup"><span data-stu-id="4ef19-141">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="4ef19-142">Libovolné přípony použijete, ale NuGet se jim přednost ve vzestupném abecedním pořadí:</span><span class="sxs-lookup"><span data-stu-id="4ef19-142">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="4ef19-143">Jak je znázorněno, verze bez žádné přípony bude vždy přednost předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="4ef19-143">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="4ef19-144">Všimněte si také, že pokud použijte číselné přípony značkami předběžné verze, které můžou používat číslicemi čísla (nebo více), pomocí úvodní nuly. jako beta01 a beta05 Ujistěte se, že budou řadit správně při čísla narůstají.</span><span class="sxs-lookup"><span data-stu-id="4ef19-144">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
