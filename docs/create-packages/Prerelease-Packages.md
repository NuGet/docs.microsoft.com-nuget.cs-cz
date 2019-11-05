---
title: Předběžné verze verzí v balíčcích NuGet
description: Doprovodné materiály k sestavování balíčků předběžných verzí
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610717"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="70bac-103">Sestavování balíčků předběžných verzí</span><span class="sxs-lookup"><span data-stu-id="70bac-103">Building pre-release packages</span></span>

<span data-ttu-id="70bac-104">Kdykoliv vydáte aktualizovaný balíček s novým číslem verze, NuGet ho považuje za "nejnovější stabilní verzi", jak je znázorněno v uživatelském rozhraní Správce balíčků v sadě Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="70bac-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Uživatelské rozhraní Správce balíčků zobrazující nejnovější stabilní verzi](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="70bac-106">Stabilní verze je ta, která je dostatečně spolehlivá, aby se mohla používat v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="70bac-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="70bac-107">Nejnovější stabilní verze je zároveň ta, která se nainstaluje jako aktualizace balíčku nebo během obnovování balíčku (v závislosti na tom, jak je popsáno v tématu [Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="70bac-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="70bac-108">Aby bylo možné podporovat životní cyklus vydání softwaru, NuGet 1,6 a novější umožňuje distribuci předběžných balíčků, kde číslo verze zahrnuje příponu sémantické verze, například `-alpha`, `-beta`nebo `-rc`.</span><span class="sxs-lookup"><span data-stu-id="70bac-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="70bac-109">Další informace najdete v tématu [Správa verzí balíčků](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="70bac-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="70bac-110">Tyto verze můžete zadat jedním z následujících způsobů:</span><span class="sxs-lookup"><span data-stu-id="70bac-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="70bac-111">**Pokud projekt používá [`PackageReference`](../consume-packages/package-references-in-project-files.md)** : zahrňte příponu sémantické verze do [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) elementu `.csproj` souboru:</span><span class="sxs-lookup"><span data-stu-id="70bac-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="70bac-112">**Pokud má váš projekt [`packages.config`](../reference/packages-config.md) soubor**: zahrňte příponu sémantické verze do [`version`](../reference/nuspec.md#version) elementu [`.nuspec`](../reference/nuspec.md) souboru:</span><span class="sxs-lookup"><span data-stu-id="70bac-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="70bac-113">Až budete připraveni uvolnit stabilní verzi, stačí odebrat příponu a balíček má přednost před všemi předběžnými verzemi.</span><span class="sxs-lookup"><span data-stu-id="70bac-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="70bac-114">Přečtěte si další informace v tématu [Správa verzí balíčků](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="70bac-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="70bac-115">Instalace a aktualizace balíčků předběžné verze</span><span class="sxs-lookup"><span data-stu-id="70bac-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="70bac-116">Ve výchozím nastavení NuGet nezahrnuje předběžné verze verzí při práci s balíčky, ale toto chování můžete změnit následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="70bac-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="70bac-117">**Uživatelské rozhraní Správce balíčků v aplikaci Visual Studio**: v uživatelském rozhraní **Spravovat balíčky NuGet** zaškrtněte políčko **zahrnout předběžné verze** :</span><span class="sxs-lookup"><span data-stu-id="70bac-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Zaškrtávací políčko zahrnout předběžné verze v aplikaci Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="70bac-119">Nastavením nebo zrušením zaškrtnutí tohoto políčka se obnoví uživatelské rozhraní Správce balíčků a seznam dostupných verzí, které můžete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="70bac-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="70bac-120">**Konzola správce balíčků**: použijte přepínač `-IncludePrerelease` s příkazy `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`a `Update-Package`.</span><span class="sxs-lookup"><span data-stu-id="70bac-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="70bac-121">Podívejte se na [referenční informace k prostředí PowerShell](../reference/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="70bac-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="70bac-122">Rozhraní příkazového **řádku NuGet**: použijte přepínač `-prerelease` s příkazy `install`, `update`, `delete`a `mirror`.</span><span class="sxs-lookup"><span data-stu-id="70bac-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="70bac-123">Přečtěte si [referenční informace k NUGET CLI](../reference/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="70bac-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="70bac-124">Sémantická verze</span><span class="sxs-lookup"><span data-stu-id="70bac-124">Semantic versioning</span></span>

<span data-ttu-id="70bac-125">[Sémantická verze nebo konvence SemVer](https://semver.org/spec/v1.0.0.html) popisuje, jak používat řetězce v číslech verzí k vyjádření významu základního kódu.</span><span class="sxs-lookup"><span data-stu-id="70bac-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="70bac-126">Každá verze v této konvenci má tři části `Major.Minor.Patch`s následujícím významem:</span><span class="sxs-lookup"><span data-stu-id="70bac-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="70bac-127">`Major`: přerušující se změny</span><span class="sxs-lookup"><span data-stu-id="70bac-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="70bac-128">`Minor`: nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="70bac-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="70bac-129">`Patch`: jenom zpětně kompatibilní opravy chyb</span><span class="sxs-lookup"><span data-stu-id="70bac-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="70bac-130">Předprodejní verze jsou potom označeny připojením pomlčky a řetězcem po čísle opravy.</span><span class="sxs-lookup"><span data-stu-id="70bac-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="70bac-131">Technicky řečeno, můžete použít *libovolný* řetězec po spojovníku a NuGet bude balíček zakládat jako předběžnou verzi.</span><span class="sxs-lookup"><span data-stu-id="70bac-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="70bac-132">NuGet pak zobrazí plné číslo verze v příslušném uživatelském rozhraní a ponechává spotřebitelům interpretovat význam pro sebe samé.</span><span class="sxs-lookup"><span data-stu-id="70bac-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="70bac-133">V takovém případě je obecně vhodné postupovat podle rozpoznaných konvencí pojmenování, jako jsou následující:</span><span class="sxs-lookup"><span data-stu-id="70bac-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="70bac-134">`-alpha`: verze alfa, obvykle se používá pro práci v průběhu a experimentování</span><span class="sxs-lookup"><span data-stu-id="70bac-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="70bac-135">`-beta`: beta verze, obvykle ta, která je dokončena pro příští plánované vydání, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="70bac-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="70bac-136">`-rc`: verze Release Candidate, obvykle verze, která je potenciálně finální (stabilní), pokud se objevují významné chyby.</span><span class="sxs-lookup"><span data-stu-id="70bac-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="70bac-137">NuGet 4.3.0 + podporuje [sémantickou správu verzí v 2.0.0](https://semver.org/spec/v2.0.0.html), která podporuje předběžné verze čísel s zápisem tečky, jako v `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="70bac-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="70bac-138">Zápis tečky není u verzí NuGet před 4.3.0 podporován.</span><span class="sxs-lookup"><span data-stu-id="70bac-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="70bac-139">V dřívějších verzích NuGet jste mohli použít tvar, jako je `1.0.1-build23` ale to se vždycky považuje za předběžnou verzi.</span><span class="sxs-lookup"><span data-stu-id="70bac-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="70bac-140">Bez ohledu na přípony, které použijete, ale NuGet jim dáte přednost v obráceném abecedním pořadí:</span><span class="sxs-lookup"><span data-stu-id="70bac-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="70bac-141">Jak je znázorněno, verze bez přípony vždy bude mít přednost před předběžnou verzí.</span><span class="sxs-lookup"><span data-stu-id="70bac-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="70bac-142">Úvodní 0s nejsou pro semver2 nutné, ale jsou ve starém schématu verze.</span><span class="sxs-lookup"><span data-stu-id="70bac-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="70bac-143">Použijete-li číselné přípony s předběžnými značkami, které mohou používat čísla s dvojitými číslicemi (nebo více), použijte úvodní nuly jako ve verzích beta. 01 a beta. 05, aby se zajistilo, že budou správně řazeny, když čísla získají větší hodnotu.</span><span class="sxs-lookup"><span data-stu-id="70bac-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="70bac-144">Toto doporučení platí pouze pro původní schéma verze.</span><span class="sxs-lookup"><span data-stu-id="70bac-144">This recommendation only applies to the old version schema.</span></span>
