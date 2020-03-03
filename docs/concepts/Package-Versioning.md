---
title: Reference k verzi balíčku NuGet
description: Přesné podrobnosti o zadání čísel a rozsahů verzí pro další balíčky, na kterých závisí balíček NuGet, a jak se nainstalují závislosti.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 912c0d015e2f499bc7386483bc6c35ecd765d3d4
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230860"
---
# <a name="package-versioning"></a><span data-ttu-id="2ff40-103">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="2ff40-103">Package versioning</span></span>

<span data-ttu-id="2ff40-104">U konkrétního balíčku se vždy používá identifikátor jeho balíčku a přesné číslo verze.</span><span class="sxs-lookup"><span data-stu-id="2ff40-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="2ff40-105">Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) v NuGet.org má k dispozici několik desítek specifických balíčků, od verze *4.1.10311* po verzi *6.1.3* (nejnovější stabilní verze) a řadu předběžných verzí, jako je *6.2.0-Beta1*.</span><span class="sxs-lookup"><span data-stu-id="2ff40-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="2ff40-106">Při vytváření balíčku přiřadíte konkrétní číslo verze s volitelnou příponou textu v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="2ff40-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="2ff40-107">Při využívání balíčků můžete na druhou stranu zadat buď přesné číslo verze, nebo rozsah přijatelných verzí.</span><span class="sxs-lookup"><span data-stu-id="2ff40-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="2ff40-108">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="2ff40-108">In this topic:</span></span>

- <span data-ttu-id="2ff40-109">[Základní informace o verzích](#version-basics) včetně přípon předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="2ff40-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="2ff40-110">Rozsahy verzí</span><span class="sxs-lookup"><span data-stu-id="2ff40-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="2ff40-111">Normalizovaná čísla verzí</span><span class="sxs-lookup"><span data-stu-id="2ff40-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="2ff40-112">Základy verzí</span><span class="sxs-lookup"><span data-stu-id="2ff40-112">Version basics</span></span>

<span data-ttu-id="2ff40-113">Konkrétní číslo verze je ve formátu *hlavní. podverze. Oprava [-přípona]*, kde tyto komponenty mají následující význam:</span><span class="sxs-lookup"><span data-stu-id="2ff40-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="2ff40-114">*Hlavní*: přerušující se změny</span><span class="sxs-lookup"><span data-stu-id="2ff40-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="2ff40-115">*Vedlejší*: nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="2ff40-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="2ff40-116">*Oprava*: zpětně kompatibilní opravy chyb</span><span class="sxs-lookup"><span data-stu-id="2ff40-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="2ff40-117">*-Přípona* (volitelné): spojovník následovaný řetězcem, který označuje předběžnou verzi (podle [konvence sémantické verze nebo SemVer 1,0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="2ff40-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="2ff40-118">**4.6**</span><span class="sxs-lookup"><span data-stu-id="2ff40-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="2ff40-119">nuget.org odmítne jakékoli nahrání balíčku, který nemá přesné číslo verze.</span><span class="sxs-lookup"><span data-stu-id="2ff40-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="2ff40-120">Verze musí být zadaná v `.nuspec` nebo souboru projektu, který se používá k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="2ff40-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="2ff40-121">Předběžné verze verzí</span><span class="sxs-lookup"><span data-stu-id="2ff40-121">Pre-release versions</span></span>

<span data-ttu-id="2ff40-122">Pro technicky řečeno, tvůrci balíčků můžou použít libovolný řetězec jako příponu k označení předprodejní verze, protože NuGet považuje takovou verzi za předběžnou verzi a neprovede žádnou další interpretaci.</span><span class="sxs-lookup"><span data-stu-id="2ff40-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="2ff40-123">To znamená, že NuGet zobrazí úplný řetězec verze v jakémkoli uživatelském rozhraní, a ponechává všechny výklady významu přípony pro příjemce.</span><span class="sxs-lookup"><span data-stu-id="2ff40-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="2ff40-124">V takovém případě vývojáři balíčku většinou následují jako rozpoznané konvence pojmenování:</span><span class="sxs-lookup"><span data-stu-id="2ff40-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="2ff40-125">`-alpha`: verze alfa, která se obvykle používá pro práci a experimentování.</span><span class="sxs-lookup"><span data-stu-id="2ff40-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="2ff40-126">`-beta`: beta verze, obvykle ta, která je dokončena pro příští plánované vydání, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="2ff40-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="2ff40-127">`-rc`: verze Release Candidate, obvykle verze, která je potenciálně finální (stabilní), pokud se objevují významné chyby.</span><span class="sxs-lookup"><span data-stu-id="2ff40-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="2ff40-128">NuGet 4.3.0 + podporuje [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), která podporuje předběžná vydání čísel s tečkami Notation, jako v *1.0.1-Build. 23*.</span><span class="sxs-lookup"><span data-stu-id="2ff40-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="2ff40-129">Zápis tečky není u verzí NuGet před 4.3.0 podporován.</span><span class="sxs-lookup"><span data-stu-id="2ff40-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="2ff40-130">Můžete použít formulář jako *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="2ff40-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="2ff40-131">Při překládání odkazů na balíčky a více verzí balíčku se liší pouze příponou, NuGet zvolí verzi bez přípony a pak použije přednost na předběžné verze v obráceném abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="2ff40-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="2ff40-132">Například následující verze se volí v uvedeném pořadí:</span><span class="sxs-lookup"><span data-stu-id="2ff40-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="2ff40-133">2.0.0 sémantických verzí</span><span class="sxs-lookup"><span data-stu-id="2ff40-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="2ff40-134">Pomocí NuGet 4.3.0 + a sady Visual Studio 2017 verze 15.3 + NuGet podporuje [sémantickou správu verzí 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="2ff40-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="2ff40-135">Některé sémantiky SemVer v 2.0.0 se ve starších klientech nepodporují.</span><span class="sxs-lookup"><span data-stu-id="2ff40-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="2ff40-136">NuGet považuje verzi balíčku za SemVer v 2.0.0, pokud je splněn některý z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="2ff40-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="2ff40-137">Jmenovka před vydáním je oddělená tečkami, například *1.0.0-Alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="2ff40-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="2ff40-138">Verze obsahuje sestavení – metadata, například *1.0.0 + githash* .</span><span class="sxs-lookup"><span data-stu-id="2ff40-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="2ff40-139">V případě nuget.org je balíček definován jako balíček SemVer v 2.0.0, pokud je splněn některý z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="2ff40-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="2ff40-140">Vlastní verze balíčku je kompatibilní s SemVer v 2.0.0, ale ne SemVer v 1.0.0, jak je definováno výše.</span><span class="sxs-lookup"><span data-stu-id="2ff40-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="2ff40-141">Všechny rozsahy verzí závislostí balíčku mají minimální nebo maximální verzi, která je kompatibilní s SemVer v 2.0.0, ale ne SemVer v 1.0.0 kompatibilní, definovaná výše; například *[1.0.0-Alpha. 1,)*.</span><span class="sxs-lookup"><span data-stu-id="2ff40-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="2ff40-142">Pokud nahrajete balíček SemVer v 2.0.0 pro nuget.org, balíček je neviditelná pro starší klienty a je k dispozici pouze pro následující klienty NuGet:</span><span class="sxs-lookup"><span data-stu-id="2ff40-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="2ff40-143">4.3.0 NuGet +</span><span class="sxs-lookup"><span data-stu-id="2ff40-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="2ff40-144">Visual Studio 2017 verze 15.3 +</span><span class="sxs-lookup"><span data-stu-id="2ff40-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="2ff40-145">Visual Studio 2015 s [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="2ff40-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="2ff40-146">DotNet</span><span class="sxs-lookup"><span data-stu-id="2ff40-146">dotnet</span></span>
  - <span data-ttu-id="2ff40-147">dotnetcore. exe (sada .NET SDK 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="2ff40-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="2ff40-148">Klienti třetích stran:</span><span class="sxs-lookup"><span data-stu-id="2ff40-148">Third-party clients:</span></span>

- <span data-ttu-id="2ff40-149">JetBrains řidiče</span><span class="sxs-lookup"><span data-stu-id="2ff40-149">JetBrains Rider</span></span>
- <span data-ttu-id="2ff40-150">Paket verze 5.0 +</span><span class="sxs-lookup"><span data-stu-id="2ff40-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="2ff40-151">Rozsahy verzí</span><span class="sxs-lookup"><span data-stu-id="2ff40-151">Version ranges</span></span>

<span data-ttu-id="2ff40-152">Při odkazování na závislosti balíčků podporuje NuGet použití zápisu intervalů pro určení rozsahů verzí shrnutý takto:</span><span class="sxs-lookup"><span data-stu-id="2ff40-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="2ff40-153">Zápis</span><span class="sxs-lookup"><span data-stu-id="2ff40-153">Notation</span></span> | <span data-ttu-id="2ff40-154">Použité pravidlo</span><span class="sxs-lookup"><span data-stu-id="2ff40-154">Applied rule</span></span> | <span data-ttu-id="2ff40-155">Popis</span><span class="sxs-lookup"><span data-stu-id="2ff40-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="2ff40-156">1.0</span><span class="sxs-lookup"><span data-stu-id="2ff40-156">1.0</span></span> | <span data-ttu-id="2ff40-157">× ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-157">x ≥ 1.0</span></span> | <span data-ttu-id="2ff40-158">Minimální verze, včetně</span><span class="sxs-lookup"><span data-stu-id="2ff40-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="2ff40-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="2ff40-159">(1.0,)</span></span> | <span data-ttu-id="2ff40-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-160">x > 1.0</span></span> | <span data-ttu-id="2ff40-161">Minimální verze, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="2ff40-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="2ff40-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="2ff40-162">[1.0]</span></span> | <span data-ttu-id="2ff40-163">x = = 1,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-163">x == 1.0</span></span> | <span data-ttu-id="2ff40-164">Přesná shoda verze</span><span class="sxs-lookup"><span data-stu-id="2ff40-164">Exact version match</span></span> |
| <span data-ttu-id="2ff40-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="2ff40-165">(,1.0]</span></span> | <span data-ttu-id="2ff40-166">× ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-166">x ≤ 1.0</span></span> | <span data-ttu-id="2ff40-167">Maximální verze, včetně</span><span class="sxs-lookup"><span data-stu-id="2ff40-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="2ff40-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="2ff40-168">(,1.0)</span></span> | <span data-ttu-id="2ff40-169">x < 1,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-169">x < 1.0</span></span> | <span data-ttu-id="2ff40-170">Maximální verze, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="2ff40-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="2ff40-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="2ff40-171">[1.0,2.0]</span></span> | <span data-ttu-id="2ff40-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="2ff40-173">Přesný rozsah (včetně)</span><span class="sxs-lookup"><span data-stu-id="2ff40-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="2ff40-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="2ff40-174">(1.0,2.0)</span></span> | <span data-ttu-id="2ff40-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="2ff40-176">Přesný rozsah, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="2ff40-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="2ff40-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="2ff40-177">[1.0,2.0)</span></span> | <span data-ttu-id="2ff40-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="2ff40-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="2ff40-179">Smíšené celkové minimální a exkluzivní verze</span><span class="sxs-lookup"><span data-stu-id="2ff40-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="2ff40-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="2ff40-180">(1.0)</span></span>    | <span data-ttu-id="2ff40-181">neplatné</span><span class="sxs-lookup"><span data-stu-id="2ff40-181">invalid</span></span> | <span data-ttu-id="2ff40-182">neplatné</span><span class="sxs-lookup"><span data-stu-id="2ff40-182">invalid</span></span> |

<span data-ttu-id="2ff40-183">Při použití formátu PackageReference NuGet podporuje také použití plovoucího zápisu, \*pro hlavní, dílčí, opravné a předběžné verze částí čísla.</span><span class="sxs-lookup"><span data-stu-id="2ff40-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="2ff40-184">Plovoucí verze nejsou podporovány ve formátu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="2ff40-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="2ff40-185">Mezi rozsahy verzí v PackageReference patří předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="2ff40-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="2ff40-186">V případě návrhu nebudou plovoucí verze překládat předběžné verze, pokud se na ně nerozhodnete.</span><span class="sxs-lookup"><span data-stu-id="2ff40-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="2ff40-187">Stav související žádosti o funkci najdete v tématu věnovaném [problému 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="2ff40-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="2ff40-188">Příklady</span><span class="sxs-lookup"><span data-stu-id="2ff40-188">Examples</span></span>

<span data-ttu-id="2ff40-189">Vždy zadejte verzi nebo rozsah verzí pro závislosti balíčku v souborech projektu, `packages.config` soubory a `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="2ff40-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="2ff40-190">Bez verze nebo rozsahu verze sada NuGet 2.8. x a starší zvolí nejnovější dostupnou verzi balíčku při řešení závislosti, zatímco NuGet 3. x a novější zvolí nejnižší verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="2ff40-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="2ff40-191">Zadání verze nebo rozsahu verze zabrání této nejistotě.</span><span class="sxs-lookup"><span data-stu-id="2ff40-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="2ff40-192">Odkazy v souborech projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="2ff40-192">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="2ff40-193">**Odkazy v `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="2ff40-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="2ff40-194">V `packages.config`je každá závislost uvedená s přesným `version` atributem, který se používá při obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="2ff40-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="2ff40-195">Atribut `allowedVersions` se používá jenom během operací aktualizace k omezení verzí, na které se balíček může aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="2ff40-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="2ff40-196">**Odkazy v souborech `.nuspec`**</span><span class="sxs-lookup"><span data-stu-id="2ff40-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="2ff40-197">Atribut `version` v elementu `<dependency>` popisuje verze rozsahu, které jsou pro závislost přijatelné.</span><span class="sxs-lookup"><span data-stu-id="2ff40-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="2ff40-198">Normalizovaná čísla verzí</span><span class="sxs-lookup"><span data-stu-id="2ff40-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="2ff40-199">Toto je zásadní změna pro NuGet 3,4 a novější.</span><span class="sxs-lookup"><span data-stu-id="2ff40-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="2ff40-200">Při získávání balíčků z úložiště během instalace, přeinstalace nebo obnovení operací, NuGet 3.4 + zpracovává čísla verzí následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2ff40-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="2ff40-201">Počáteční nuly jsou odebrány z čísel verzí:</span><span class="sxs-lookup"><span data-stu-id="2ff40-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="2ff40-202">Hodnota nula ve čtvrté části čísla verze bude vynechána.</span><span class="sxs-lookup"><span data-stu-id="2ff40-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="2ff40-203">operace `pack` a `restore` normalizují verze, kdykoli je to možné.</span><span class="sxs-lookup"><span data-stu-id="2ff40-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="2ff40-204">U balíčků už je tato normalizace neovlivněna čísly verzí v samotných balíčcích. má vliv jenom na to, jak NuGet odpovídá verzím při řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="2ff40-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="2ff40-205">Úložiště balíčků NuGet ale musí tyto hodnoty nakládat stejným způsobem jako NuGet, aby se zabránilo duplikaci verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="2ff40-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="2ff40-206">Proto úložiště, které obsahuje verzi *1,0* balíčku, by nemělo také hostovat verzi *1.0.0* jako samostatný a jiný balíček.</span><span class="sxs-lookup"><span data-stu-id="2ff40-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
