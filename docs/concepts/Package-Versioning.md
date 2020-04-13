---
title: Odkaz na verzi balíčku NuGet
description: Přesné podrobnosti o určení čísla verzí a rozsahy pro jiné balíčky, na kterých závisí balíček NuGet a jak jsou nainstalovány závislosti.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147445"
---
# <a name="package-versioning"></a><span data-ttu-id="54586-103">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="54586-103">Package versioning</span></span>

<span data-ttu-id="54586-104">Konkrétní balíček je vždy odkazoval se na pomocí jeho identifikátor balíčku a přesné číslo verze.</span><span class="sxs-lookup"><span data-stu-id="54586-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="54586-105">Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) na nuget.org má několik desítek konkrétní chytací balíčky k dispozici, od verze *4.1.10311* na verzi *6.1.3* (nejnovější stabilní verze) a různé předběžné verze jako *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="54586-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="54586-106">Při vytváření balíčku přiřadíte konkrétní číslo verze s volitelnou příponou předběžné verze textu.</span><span class="sxs-lookup"><span data-stu-id="54586-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="54586-107">Při spotřebovávání balíčků můžete naopak zadat přesné číslo verze nebo rozsah přijatelných verzí.</span><span class="sxs-lookup"><span data-stu-id="54586-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="54586-108">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="54586-108">In this topic:</span></span>

- <span data-ttu-id="54586-109">[Základy verze](#version-basics) včetně předprodejních přípon.</span><span class="sxs-lookup"><span data-stu-id="54586-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="54586-110">Rozsahy verzí</span><span class="sxs-lookup"><span data-stu-id="54586-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="54586-111">Normalizovaná čísla verzí</span><span class="sxs-lookup"><span data-stu-id="54586-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="54586-112">Základy verzí</span><span class="sxs-lookup"><span data-stu-id="54586-112">Version basics</span></span>

<span data-ttu-id="54586-113">Konkrétní číslo verze je ve tvaru *Major.Minor.Patch[-Přípona]*, kde komponenty mají následující významy:</span><span class="sxs-lookup"><span data-stu-id="54586-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="54586-114">*Hlavní*: Prolomení změn</span><span class="sxs-lookup"><span data-stu-id="54586-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="54586-115">*Minor*: Nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="54586-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="54586-116">*Oprava*: Pouze opravy zpětně kompatibilních chyb</span><span class="sxs-lookup"><span data-stu-id="54586-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="54586-117">*-Přípona* (volitelně): pomlčka následovaná řetězcem označujícím předběžnou verzi (podle [sémantického správu verzí nebo konvence SemVer 1.0).](https://semver.org/spec/v1.0.0.html)</span><span class="sxs-lookup"><span data-stu-id="54586-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="54586-118">**Příklady:**</span><span class="sxs-lookup"><span data-stu-id="54586-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="54586-119">nuget.org odmítne jakýkoli balíček nahrát, který postrádá přesné číslo verze.</span><span class="sxs-lookup"><span data-stu-id="54586-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="54586-120">Verze musí být zadána v souboru `.nuspec` nebo projektu použitého k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="54586-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="54586-121">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="54586-121">Pre-release versions</span></span>

<span data-ttu-id="54586-122">Technicky vzato mohou tvůrci balíčků použít libovolný řetězec jako příponu k označení předběžné verze, protože NuGet zachází s jakoukoli takovou verzí jako s předběžnou verzí a neprovádí žádnou jinou interpretaci.</span><span class="sxs-lookup"><span data-stu-id="54586-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="54586-123">To znamená NuGet zobrazí řetězec plné verze v bez ohledu na ui se týká, takže jakýkoli výklad významu přípony pro spotřebitele.</span><span class="sxs-lookup"><span data-stu-id="54586-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="54586-124">To znamená, že vývojáři balíčků obecně dodržují uznávané konvence pojmenování:</span><span class="sxs-lookup"><span data-stu-id="54586-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="54586-125">`-alpha`: Alfa verze, obvykle používaná pro nedokončenou práci a experimentování.</span><span class="sxs-lookup"><span data-stu-id="54586-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="54586-126">`-beta`: Beta verze, obvykle taková, která je dokončena pro další plánovanou verzi, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="54586-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="54586-127">`-rc`: Release candidate, obvykle vydání, které je potenciálně konečné (stabilní), pokud se neobjeví významné chyby.</span><span class="sxs-lookup"><span data-stu-id="54586-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="54586-128">NuGet 4.3.0+ podporuje [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), který podporuje předverze čísla s tečkou notace, jako v *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="54586-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="54586-129">Dot notace není podporována s Verzemi NuGet před 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="54586-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="54586-130">Můžete použít formulář jako *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="54586-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="54586-131">Při řešení odkazů na balíček a více verzí balíčků se liší pouze příponou, NuGet nejprve vybere verzi bez přípony a pak použije přednost pro předběžné verze v obráceném abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="54586-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="54586-132">Například následující verze by byly vybrány v přesném pořadí:</span><span class="sxs-lookup"><span data-stu-id="54586-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="54586-133">Sémantická správa verzí 2.0.0</span><span class="sxs-lookup"><span data-stu-id="54586-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="54586-134">S NuGet 4.3.0+ a Visual Studio 2017 verze 15.3+, NuGet podporuje [sémantické versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="54586-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="54586-135">Některé sémantiky SemVer v2.0.0 nejsou podporovány ve starších klientů.</span><span class="sxs-lookup"><span data-stu-id="54586-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="54586-136">NuGet považuje verzi balíčku za SemVer v2.0.0 specifické, pokud je splněna některá z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="54586-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="54586-137">Předprodejní štítek je oddělen tečkami, například *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="54586-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="54586-138">Verze má metadata sestavení, například *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="54586-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="54586-139">Pro nuget.org je balíček definován jako balíček SemVer v2.0.0, pokud je splněn některý z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="54586-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="54586-140">Vlastní verze balíčku je kompatibilní s ssver v2.0.0, ale není kompatibilní s SemVer v1.0.0, jak je definováno výše.</span><span class="sxs-lookup"><span data-stu-id="54586-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="54586-141">Všechny rozsahy verze závislostí balíčku má minimální nebo maximální verzi, která je kompatibilní s semVer v2.0.0, ale není kompatibilní s semVer v1.0.0, definované výše; například *[1.0.0-alpha.1, ).*</span><span class="sxs-lookup"><span data-stu-id="54586-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="54586-142">Pokud nahrajete balíček specifický pro SemVer v2.0.0 do nuget.org, balíček je pro starší klienty neviditelný a je k dispozici pouze následujícím klientům NuGet:</span><span class="sxs-lookup"><span data-stu-id="54586-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="54586-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="54586-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="54586-144">Visual Studio 2017 verze 15.3+</span><span class="sxs-lookup"><span data-stu-id="54586-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="54586-145">Visual Studio 2015 s [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="54586-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="54586-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="54586-146">dotnet</span></span>
  - <span data-ttu-id="54586-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="54586-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="54586-148">Klienti třetích stran:</span><span class="sxs-lookup"><span data-stu-id="54586-148">Third-party clients:</span></span>

- <span data-ttu-id="54586-149">JetBrains Jezdec</span><span class="sxs-lookup"><span data-stu-id="54586-149">JetBrains Rider</span></span>
- <span data-ttu-id="54586-150">Paket verze 5.0+</span><span class="sxs-lookup"><span data-stu-id="54586-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="54586-151">Rozsahy verzí</span><span class="sxs-lookup"><span data-stu-id="54586-151">Version ranges</span></span>

<span data-ttu-id="54586-152">Při odkazování na závislosti balíčků, NuGet podporuje použití zápisu intervalu pro určení rozsahy verzí, shrnuty takto:</span><span class="sxs-lookup"><span data-stu-id="54586-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="54586-153">Notace</span><span class="sxs-lookup"><span data-stu-id="54586-153">Notation</span></span> | <span data-ttu-id="54586-154">Použité pravidlo</span><span class="sxs-lookup"><span data-stu-id="54586-154">Applied rule</span></span> | <span data-ttu-id="54586-155">Popis</span><span class="sxs-lookup"><span data-stu-id="54586-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="54586-156">1.0</span><span class="sxs-lookup"><span data-stu-id="54586-156">1.0</span></span> | <span data-ttu-id="54586-157">x ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="54586-157">x ≥ 1.0</span></span> | <span data-ttu-id="54586-158">Minimální verze včetně</span><span class="sxs-lookup"><span data-stu-id="54586-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="54586-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="54586-159">(1.0,)</span></span> | <span data-ttu-id="54586-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="54586-160">x > 1.0</span></span> | <span data-ttu-id="54586-161">Minimální verze, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="54586-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="54586-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="54586-162">[1.0]</span></span> | <span data-ttu-id="54586-163">x == 1,0</span><span class="sxs-lookup"><span data-stu-id="54586-163">x == 1.0</span></span> | <span data-ttu-id="54586-164">Přesná verze odpovídá</span><span class="sxs-lookup"><span data-stu-id="54586-164">Exact version match</span></span> |
| <span data-ttu-id="54586-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="54586-165">(,1.0]</span></span> | <span data-ttu-id="54586-166">x ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="54586-166">x ≤ 1.0</span></span> | <span data-ttu-id="54586-167">Maximální verze včetně</span><span class="sxs-lookup"><span data-stu-id="54586-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="54586-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="54586-168">(,1.0)</span></span> | <span data-ttu-id="54586-169">x < 1,0</span><span class="sxs-lookup"><span data-stu-id="54586-169">x < 1.0</span></span> | <span data-ttu-id="54586-170">Maximální verze, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="54586-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="54586-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="54586-171">[1.0,2.0]</span></span> | <span data-ttu-id="54586-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="54586-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="54586-173">Přesný rozsah včetně</span><span class="sxs-lookup"><span data-stu-id="54586-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="54586-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="54586-174">(1.0,2.0)</span></span> | <span data-ttu-id="54586-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="54586-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="54586-176">Přesný rozsah, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="54586-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="54586-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="54586-177">[1.0,2.0)</span></span> | <span data-ttu-id="54586-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="54586-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="54586-179">Smíšená minimální a exkluzivní maximální verze</span><span class="sxs-lookup"><span data-stu-id="54586-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="54586-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="54586-180">(1.0)</span></span>    | <span data-ttu-id="54586-181">neplatné</span><span class="sxs-lookup"><span data-stu-id="54586-181">invalid</span></span> | <span data-ttu-id="54586-182">neplatné</span><span class="sxs-lookup"><span data-stu-id="54586-182">invalid</span></span> |

<span data-ttu-id="54586-183">Při použití formátu PackageReference NuGet také podporuje použití \*plovoucí zápis, , pro hlavní, menší, patch a předprodejní přípona části čísla.</span><span class="sxs-lookup"><span data-stu-id="54586-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="54586-184">Plovoucí verze nejsou podporovány `packages.config` s formátem.</span><span class="sxs-lookup"><span data-stu-id="54586-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="54586-185">Rozsahy verzí v PackageReference zahrnují předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="54586-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="54586-186">Plovoucí verze podle návrhu neřeší předběžné verze, pokud nejsou odvráceny.</span><span class="sxs-lookup"><span data-stu-id="54586-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="54586-187">Stav žádosti o související funkce naleznete v [tématu problém 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="54586-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="54586-188">Příklady</span><span class="sxs-lookup"><span data-stu-id="54586-188">Examples</span></span>

<span data-ttu-id="54586-189">Vždy zadejte rozsah verze nebo verze pro `packages.config` závislosti balíčků `.nuspec` v souborech projektu, souborech a souborech.</span><span class="sxs-lookup"><span data-stu-id="54586-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="54586-190">Bez verze nebo rozsah verze NuGet 2.8.x a dříve vybere nejnovější dostupné verze balíčku při řešení závislosti, vzhledem k tomu, NuGet 3.x a později zvolí nejnižší verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="54586-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="54586-191">Určení verze nebo rozsah verze se této nejistotě vyhne.</span><span class="sxs-lookup"><span data-stu-id="54586-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="54586-192">Odkazy v souborech projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="54586-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="54586-193">**Odkazy v `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="54586-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="54586-194">V `packages.config`aplikaci je každá závislost `version` uvedena s přesným atributem, který se používá při obnově balíčků.</span><span class="sxs-lookup"><span data-stu-id="54586-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="54586-195">Atribut `allowedVersions` se používá pouze během operací aktualizace omezit verze, na které balíček může být aktualizován.</span><span class="sxs-lookup"><span data-stu-id="54586-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="54586-196">**Odkazy v `.nuspec` souborech**</span><span class="sxs-lookup"><span data-stu-id="54586-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="54586-197">Atribut `version` v `<dependency>` elementu popisuje verze rozsahu, které jsou přijatelné pro závislost.</span><span class="sxs-lookup"><span data-stu-id="54586-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="54586-198">Normalizovaná čísla verzí</span><span class="sxs-lookup"><span data-stu-id="54586-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="54586-199">Toto je narušující změna pro NuGet 3.4 a novější.</span><span class="sxs-lookup"><span data-stu-id="54586-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="54586-200">Při získávání balíčků z úložiště během instalace, přeinstalace nebo obnovení operací, NuGet 3.4+ zachází čísla verzí takto:</span><span class="sxs-lookup"><span data-stu-id="54586-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="54586-201">Počáteční nuly jsou odstraněny z čísel verzí:</span><span class="sxs-lookup"><span data-stu-id="54586-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="54586-202">Nula ve čtvrté části čísla verze bude vynechána.</span><span class="sxs-lookup"><span data-stu-id="54586-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- <span data-ttu-id="54586-203">Metadata sestavení SemVer 2.0.0 jsou odebrána.</span><span class="sxs-lookup"><span data-stu-id="54586-203">SemVer 2.0.0 build metadata is removed</span></span>

        1.0.7+r3456 is treated as 1.0.7

<span data-ttu-id="54586-204">`pack`a `restore` operace normalizují verze, kdykoli je to možné.</span><span class="sxs-lookup"><span data-stu-id="54586-204">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="54586-205">U již vytvořených balíčků nemá tato normalizace vliv na čísla verzí v samotných balíčcích; ovlivňuje pouze způsob, jakým NuGet odpovídá verzím při řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="54586-205">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="54586-206">Úložiště balíčků NuGet však musí zacházet s těmito hodnotami stejným způsobem jako NuGet, aby se zabránilo duplikaci verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="54586-206">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="54586-207">Úložiště, které obsahuje verzi *1.0* balíčku, by tedy nemělo být hostitelem verze *1.0.0* jako samostatného a odlišného balíčku.</span><span class="sxs-lookup"><span data-stu-id="54586-207">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
