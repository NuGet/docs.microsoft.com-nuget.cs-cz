---
title: Reference k verzi balíčku NuGet
description: Přesné podrobnosti o zadání čísel a rozsahů verzí pro další balíčky, na kterých závisí balíček NuGet, a jak se nainstalují závislosti.
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 77b96e83f8fc7afd391537d16120d037585dd379
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859197"
---
# <a name="package-versioning"></a><span data-ttu-id="4c93b-103">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="4c93b-103">Package versioning</span></span>

<span data-ttu-id="4c93b-104">U konkrétního balíčku se vždy používá identifikátor jeho balíčku a přesné číslo verze.</span><span class="sxs-lookup"><span data-stu-id="4c93b-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="4c93b-105">Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) v NuGet.org má k dispozici několik desítek specifických balíčků, od verze *4.1.10311* po verzi *6.1.3* (nejnovější stabilní verze) a řadu předběžných verzí, jako je *6.2.0-Beta1*.</span><span class="sxs-lookup"><span data-stu-id="4c93b-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="4c93b-106">Při vytváření balíčku přiřadíte konkrétní číslo verze s volitelnou příponou textu v předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="4c93b-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="4c93b-107">Při využívání balíčků můžete na druhou stranu zadat buď přesné číslo verze, nebo rozsah přijatelných verzí.</span><span class="sxs-lookup"><span data-stu-id="4c93b-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="4c93b-108">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="4c93b-108">In this topic:</span></span>

- <span data-ttu-id="4c93b-109">[Základní informace o verzích](#version-basics) včetně přípon předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="4c93b-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="4c93b-110">Rozsahy verzí</span><span class="sxs-lookup"><span data-stu-id="4c93b-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="4c93b-111">Normalizovaná čísla verzí</span><span class="sxs-lookup"><span data-stu-id="4c93b-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="4c93b-112">Základy verzí</span><span class="sxs-lookup"><span data-stu-id="4c93b-112">Version basics</span></span>

<span data-ttu-id="4c93b-113">Konkrétní číslo verze je ve formátu *hlavní. podverze. Oprava [-přípona]*, kde tyto komponenty mají následující význam:</span><span class="sxs-lookup"><span data-stu-id="4c93b-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="4c93b-114">*Hlavní*: přerušující se změny</span><span class="sxs-lookup"><span data-stu-id="4c93b-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="4c93b-115">*Vedlejší*: nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="4c93b-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="4c93b-116">*Oprava*: zpětně kompatibilní opravy chyb</span><span class="sxs-lookup"><span data-stu-id="4c93b-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="4c93b-117">*-Přípona* (volitelné): spojovník následovaný řetězcem, který označuje předběžnou verzi (podle [konvence sémantické verze nebo SemVer 1,0](https://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="4c93b-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="4c93b-118">**Příklady:**</span><span class="sxs-lookup"><span data-stu-id="4c93b-118">**Examples:**</span></span>

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="4c93b-119">nuget.org odmítne jakékoli nahrání balíčku, který nemá přesné číslo verze.</span><span class="sxs-lookup"><span data-stu-id="4c93b-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="4c93b-120">Verze musí být zadaná v `.nuspec` souboru projektu nebo, který se používá k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="4c93b-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="4c93b-121">Předběžné verze verzí</span><span class="sxs-lookup"><span data-stu-id="4c93b-121">Pre-release versions</span></span>

<span data-ttu-id="4c93b-122">Pro technicky řečeno, tvůrci balíčků můžou použít libovolný řetězec jako příponu k označení předprodejní verze, protože NuGet považuje takovou verzi za předběžnou verzi a neprovede žádnou další interpretaci.</span><span class="sxs-lookup"><span data-stu-id="4c93b-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="4c93b-123">To znamená, že NuGet zobrazí úplný řetězec verze v jakémkoli uživatelském rozhraní, a ponechává všechny výklady významu přípony pro příjemce.</span><span class="sxs-lookup"><span data-stu-id="4c93b-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="4c93b-124">V takovém případě vývojáři balíčku většinou následují jako rozpoznané konvence pojmenování:</span><span class="sxs-lookup"><span data-stu-id="4c93b-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="4c93b-125">`-alpha`: Verze alfa, která se obvykle používá pro práci a experimentování.</span><span class="sxs-lookup"><span data-stu-id="4c93b-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="4c93b-126">`-beta`: Beta verze, obvykle ta, která je dokončena pro další plánované vydání, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="4c93b-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="4c93b-127">`-rc`: Verze Release Candidate, obvykle verze, která je potenciálně finální (stabilní), pokud se neobjeví významné chyby.</span><span class="sxs-lookup"><span data-stu-id="4c93b-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="4c93b-128">NuGet 4.3.0 + podporuje [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), která podporuje předběžná vydání čísel s tečkami Notation, jako v *1.0.1-Build. 23*.</span><span class="sxs-lookup"><span data-stu-id="4c93b-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="4c93b-129">Zápis tečky není u verzí NuGet před 4.3.0 podporován.</span><span class="sxs-lookup"><span data-stu-id="4c93b-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="4c93b-130">Můžete použít formulář jako *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="4c93b-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="4c93b-131">Při překládání odkazů na balíčky a více verzí balíčku se liší pouze příponou, NuGet zvolí verzi bez přípony a pak použije přednost na předběžné verze v obráceném abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="4c93b-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="4c93b-132">Například následující verze se volí v uvedeném pořadí:</span><span class="sxs-lookup"><span data-stu-id="4c93b-132">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="4c93b-133">Sémantika správy verzí 2.0.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="4c93b-134">Pomocí NuGet 4.3.0 + a sady Visual Studio 2017 verze 15.3 + NuGet podporuje [sémantickou správu verzí 2.0.0](https://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="4c93b-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="4c93b-135">Některé sémantiky SemVer v 2.0.0 se ve starších klientech nepodporují.</span><span class="sxs-lookup"><span data-stu-id="4c93b-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="4c93b-136">NuGet považuje verzi balíčku za SemVer v 2.0.0, pokud je splněn některý z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="4c93b-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="4c93b-137">Jmenovka před vydáním je oddělená tečkami, například *1.0.0-Alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="4c93b-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="4c93b-138">Verze obsahuje sestavení – metadata, například *1.0.0 + githash* .</span><span class="sxs-lookup"><span data-stu-id="4c93b-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="4c93b-139">V případě nuget.org je balíček definován jako balíček SemVer v 2.0.0, pokud je splněn některý z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="4c93b-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="4c93b-140">Vlastní verze balíčku je kompatibilní s SemVer v 2.0.0, ale ne SemVer v 1.0.0, jak je definováno výše.</span><span class="sxs-lookup"><span data-stu-id="4c93b-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="4c93b-141">Všechny rozsahy verzí závislostí balíčku mají minimální nebo maximální verzi, která je kompatibilní s SemVer v 2.0.0, ale ne SemVer v 1.0.0 kompatibilní, definovaná výše; například *[1.0.0-Alpha. 1,)*.</span><span class="sxs-lookup"><span data-stu-id="4c93b-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="4c93b-142">Pokud nahrajete balíček SemVer v 2.0.0 pro nuget.org, balíček je neviditelná pro starší klienty a je k dispozici pouze pro následující klienty NuGet:</span><span class="sxs-lookup"><span data-stu-id="4c93b-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="4c93b-143">4.3.0 NuGet +</span><span class="sxs-lookup"><span data-stu-id="4c93b-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="4c93b-144">Visual Studio 2017 verze 15.3 +</span><span class="sxs-lookup"><span data-stu-id="4c93b-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="4c93b-145">Visual Studio 2015 s [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="4c93b-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="4c93b-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="4c93b-146">dotnet</span></span>
  - <span data-ttu-id="4c93b-147">dotnetcore.exe (.NET SDK 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="4c93b-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="4c93b-148">Klienti třetích stran:</span><span class="sxs-lookup"><span data-stu-id="4c93b-148">Third-party clients:</span></span>

- <span data-ttu-id="4c93b-149">JetBrains řidiče</span><span class="sxs-lookup"><span data-stu-id="4c93b-149">JetBrains Rider</span></span>
- <span data-ttu-id="4c93b-150">Paket verze 5.0 +</span><span class="sxs-lookup"><span data-stu-id="4c93b-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="4c93b-151">Rozsahy verzí</span><span class="sxs-lookup"><span data-stu-id="4c93b-151">Version ranges</span></span>

<span data-ttu-id="4c93b-152">Při odkazování na závislosti balíčků podporuje NuGet použití zápisu intervalů pro určení rozsahů verzí shrnutý takto:</span><span class="sxs-lookup"><span data-stu-id="4c93b-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="4c93b-153">Notace</span><span class="sxs-lookup"><span data-stu-id="4c93b-153">Notation</span></span> | <span data-ttu-id="4c93b-154">Použité pravidlo</span><span class="sxs-lookup"><span data-stu-id="4c93b-154">Applied rule</span></span> | <span data-ttu-id="4c93b-155">Popis</span><span class="sxs-lookup"><span data-stu-id="4c93b-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="4c93b-156">1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-156">1.0</span></span> | <span data-ttu-id="4c93b-157">× ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="4c93b-157">x ≥ 1.0</span></span> | <span data-ttu-id="4c93b-158">Minimální verze (včetně)</span><span class="sxs-lookup"><span data-stu-id="4c93b-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="4c93b-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="4c93b-159">(1.0,)</span></span> | <span data-ttu-id="4c93b-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-160">x > 1.0</span></span> | <span data-ttu-id="4c93b-161">Minimální verze (vyjma)</span><span class="sxs-lookup"><span data-stu-id="4c93b-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="4c93b-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="4c93b-162">[1.0]</span></span> | <span data-ttu-id="4c93b-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-163">x == 1.0</span></span> | <span data-ttu-id="4c93b-164">Přesná shoda verze</span><span class="sxs-lookup"><span data-stu-id="4c93b-164">Exact version match</span></span> |
| <span data-ttu-id="4c93b-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="4c93b-165">(,1.0]</span></span> | <span data-ttu-id="4c93b-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-166">x ≤ 1.0</span></span> | <span data-ttu-id="4c93b-167">Maximální verze (včetně)</span><span class="sxs-lookup"><span data-stu-id="4c93b-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="4c93b-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="4c93b-168">(,1.0)</span></span> | <span data-ttu-id="4c93b-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-169">x < 1.0</span></span> | <span data-ttu-id="4c93b-170">Maximální verze (vyjma)</span><span class="sxs-lookup"><span data-stu-id="4c93b-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="4c93b-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="4c93b-171">[1.0,2.0]</span></span> | <span data-ttu-id="4c93b-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="4c93b-173">Přesný rozsah (včetně)</span><span class="sxs-lookup"><span data-stu-id="4c93b-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="4c93b-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="4c93b-174">(1.0,2.0)</span></span> | <span data-ttu-id="4c93b-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="4c93b-176">Přesný rozsah (vyjma)</span><span class="sxs-lookup"><span data-stu-id="4c93b-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="4c93b-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="4c93b-177">[1.0,2.0)</span></span> | <span data-ttu-id="4c93b-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="4c93b-179">Kombinace minimální (včetně) a maximální (vyjma) verze</span><span class="sxs-lookup"><span data-stu-id="4c93b-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="4c93b-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="4c93b-180">(1.0)</span></span>    | <span data-ttu-id="4c93b-181">neplatné</span><span class="sxs-lookup"><span data-stu-id="4c93b-181">invalid</span></span> | <span data-ttu-id="4c93b-182">neplatné</span><span class="sxs-lookup"><span data-stu-id="4c93b-182">invalid</span></span> |

<span data-ttu-id="4c93b-183">Při použití formátu PackageReference NuGet podporuje také použití plovoucího zápisu, \* pro části hlavních, dílčích, oprav a předběžných verzí přípony.</span><span class="sxs-lookup"><span data-stu-id="4c93b-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="4c93b-184">Plovoucí verze se ve formátu nepodporují `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="4c93b-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="4c93b-185">Je-li zadána plovoucí verze, pravidlo je vyhodnoceno na nejvyšší existující verzi, která odpovídá popisu verze.</span><span class="sxs-lookup"><span data-stu-id="4c93b-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="4c93b-186">Příklady plovoucí verze a jejich řešení jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="4c93b-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="4c93b-187">Mezi rozsahy verzí v PackageReference patří předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="4c93b-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="4c93b-188">V případě návrhu nebudou plovoucí verze překládat předběžné verze, pokud se na ně nerozhodnete.</span><span class="sxs-lookup"><span data-stu-id="4c93b-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="4c93b-189">Stav související žádosti o funkci najdete v tématu věnovaném [problému 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="4c93b-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="4c93b-190">Příklady</span><span class="sxs-lookup"><span data-stu-id="4c93b-190">Examples</span></span>

<span data-ttu-id="4c93b-191">V souborech projektu, souborech a souborech vždy zadejte verzi nebo rozsah verzí pro závislosti balíčku `packages.config` `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="4c93b-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="4c93b-192">Bez verze nebo rozsahu verze sada NuGet 2.8. x a starší zvolí nejnovější dostupnou verzi balíčku při řešení závislosti, zatímco NuGet 3. x a novější zvolí nejnižší verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="4c93b-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="4c93b-193">Zadání verze nebo rozsahu verze zabrání této nejistotě.</span><span class="sxs-lookup"><span data-stu-id="4c93b-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="4c93b-194">Odkazy v souborech projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="4c93b-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="4c93b-195">Řešení plovoucí verze</span><span class="sxs-lookup"><span data-stu-id="4c93b-195">Floating version resolutions</span></span> 

| <span data-ttu-id="4c93b-196">Verze</span><span class="sxs-lookup"><span data-stu-id="4c93b-196">Version</span></span> | <span data-ttu-id="4c93b-197">Verze jsou k dispozici na serveru</span><span class="sxs-lookup"><span data-stu-id="4c93b-197">Versions present on server</span></span> | <span data-ttu-id="4c93b-198">Řešení</span><span class="sxs-lookup"><span data-stu-id="4c93b-198">Resolution</span></span> | <span data-ttu-id="4c93b-199">Důvod</span><span class="sxs-lookup"><span data-stu-id="4c93b-199">Reason</span></span> | <span data-ttu-id="4c93b-200">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4c93b-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="4c93b-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-201">1.1.0</span></span> <br> <span data-ttu-id="4c93b-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="4c93b-202">1.1.1</span></span> <br> <span data-ttu-id="4c93b-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-203">1.2.0</span></span> <br> <span data-ttu-id="4c93b-204">1.3.0-alfa</span><span class="sxs-lookup"><span data-stu-id="4c93b-204">1.3.0-alpha</span></span>  | <span data-ttu-id="4c93b-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-205">1.2.0</span></span> | <span data-ttu-id="4c93b-206">Nejvyšší stabilní verze.</span><span class="sxs-lookup"><span data-stu-id="4c93b-206">The highest stable version.</span></span> |
| <span data-ttu-id="4c93b-207">1,1. \*</span><span class="sxs-lookup"><span data-stu-id="4c93b-207">1.1.\*</span></span> | <span data-ttu-id="4c93b-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-208">1.1.0</span></span> <br> <span data-ttu-id="4c93b-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="4c93b-209">1.1.1</span></span> <br> <span data-ttu-id="4c93b-210">1.1.2 – alfa</span><span class="sxs-lookup"><span data-stu-id="4c93b-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="4c93b-211">1.2.0-alfa</span><span class="sxs-lookup"><span data-stu-id="4c93b-211">1.2.0-alpha</span></span> | <span data-ttu-id="4c93b-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="4c93b-212">1.1.1</span></span> | <span data-ttu-id="4c93b-213">Nejvyšší stabilní verze, která respektuje zadaný vzor.</span><span class="sxs-lookup"><span data-stu-id="4c93b-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="4c93b-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="4c93b-214">\* - \*</span></span> | <span data-ttu-id="4c93b-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-215">1.1.0</span></span> <br> <span data-ttu-id="4c93b-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="4c93b-216">1.1.1</span></span> <br> <span data-ttu-id="4c93b-217">1.1.2 – alfa</span><span class="sxs-lookup"><span data-stu-id="4c93b-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="4c93b-218">1.3.0 – beta verze</span><span class="sxs-lookup"><span data-stu-id="4c93b-218">1.3.0-beta</span></span>  | <span data-ttu-id="4c93b-219">1.3.0 – beta verze</span><span class="sxs-lookup"><span data-stu-id="4c93b-219">1.3.0-beta</span></span> | <span data-ttu-id="4c93b-220">Nejvyšší verze, včetně nestabilních verzí.</span><span class="sxs-lookup"><span data-stu-id="4c93b-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="4c93b-221">K dispozici v aplikaci Visual Studio verze 16,6, NuGet verze 5,6, .NET Core SDK verze 3.1.300</span><span class="sxs-lookup"><span data-stu-id="4c93b-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="4c93b-222">1,1. *-*</span><span class="sxs-lookup"><span data-stu-id="4c93b-222">1.1.\* - \*</span></span> | <span data-ttu-id="4c93b-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="4c93b-223">1.1.0</span></span> <br> <span data-ttu-id="4c93b-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="4c93b-224">1.1.1</span></span> <br> <span data-ttu-id="4c93b-225">1.1.2 – alfa</span><span class="sxs-lookup"><span data-stu-id="4c93b-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="4c93b-226">1.1.2 – beta</span><span class="sxs-lookup"><span data-stu-id="4c93b-226">1.1.2-beta</span></span> <br> <span data-ttu-id="4c93b-227">1.3.0 – beta verze</span><span class="sxs-lookup"><span data-stu-id="4c93b-227">1.3.0-beta</span></span>  | <span data-ttu-id="4c93b-228">1.1.2 – beta</span><span class="sxs-lookup"><span data-stu-id="4c93b-228">1.1.2-beta</span></span> | <span data-ttu-id="4c93b-229">Nejvyšší verze, která je v souladu se vzorem a včetně nestabilních verzí.</span><span class="sxs-lookup"><span data-stu-id="4c93b-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="4c93b-230">K dispozici v aplikaci Visual Studio verze 16,6, NuGet verze 5,6, .NET Core SDK verze 3.1.300</span><span class="sxs-lookup"><span data-stu-id="4c93b-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="4c93b-231">**Odkazy v `packages.config` :**</span><span class="sxs-lookup"><span data-stu-id="4c93b-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="4c93b-232">V je `packages.config` každá závislost uvedená s přesným `version` atributem, který se používá při obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="4c93b-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="4c93b-233">`allowedVersions`Atribut se používá jenom během operací aktualizace k omezení verzí, na které se balíček může aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="4c93b-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="4c93b-234">**Odkazy v `.nuspec` souborech**</span><span class="sxs-lookup"><span data-stu-id="4c93b-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="4c93b-235">`version`Atribut v `<dependency>` elementu popisuje verze rozsahu, které jsou přijatelné pro závislost.</span><span class="sxs-lookup"><span data-stu-id="4c93b-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="4c93b-236">Normalizovaná čísla verzí</span><span class="sxs-lookup"><span data-stu-id="4c93b-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="4c93b-237">Toto je zásadní změna pro NuGet 3,4 a novější.</span><span class="sxs-lookup"><span data-stu-id="4c93b-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="4c93b-238">Při získávání balíčků z úložiště během instalace, přeinstalace nebo obnovení operací, NuGet 3.4 + zpracovává čísla verzí následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="4c93b-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="4c93b-239">Počáteční nuly jsou odebrány z čísel verzí:</span><span class="sxs-lookup"><span data-stu-id="4c93b-239">Leading zeroes are removed from version numbers:</span></span>

  <span data-ttu-id="4c93b-240">1,00 se považuje za 1,0 1.01.1 se zpracovává jako 1.1.1 1.00.0.1 se považuje za 1.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="4c93b-240">1.00 is treated as 1.0 1.01.1 is treated as 1.1.1 1.00.0.1 is treated as 1.0.0.1</span></span>

- <span data-ttu-id="4c93b-241">Hodnota nula ve čtvrté části čísla verze bude vynechána.</span><span class="sxs-lookup"><span data-stu-id="4c93b-241">A zero in the fourth part of the version number will be omitted</span></span>

  <span data-ttu-id="4c93b-242">1.0.0.0 se považuje za 1.0.0 1.0.01.0 se považuje za 1.0.1.</span><span class="sxs-lookup"><span data-stu-id="4c93b-242">1.0.0.0 is treated as 1.0.0 1.0.01.0 is treated as 1.0.1</span></span>

- <span data-ttu-id="4c93b-243">Metadata buildu SemVer 2.0.0 se odebrala.</span><span class="sxs-lookup"><span data-stu-id="4c93b-243">SemVer 2.0.0 build metadata is removed</span></span>

  <span data-ttu-id="4c93b-244">1.0.7 + r3456 se považují za 1.0.7</span><span class="sxs-lookup"><span data-stu-id="4c93b-244">1.0.7+r3456 is treated as 1.0.7</span></span>

<span data-ttu-id="4c93b-245">`pack` a `restore` operace normalizují verze, kdykoli je to možné.</span><span class="sxs-lookup"><span data-stu-id="4c93b-245">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="4c93b-246">U balíčků už je tato normalizace neovlivněna čísly verzí v samotných balíčcích. má vliv jenom na to, jak NuGet odpovídá verzím při řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="4c93b-246">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="4c93b-247">Úložiště balíčků NuGet ale musí tyto hodnoty nakládat stejným způsobem jako NuGet, aby se zabránilo duplikaci verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="4c93b-247">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="4c93b-248">Proto úložiště, které obsahuje verzi *1,0* balíčku, by nemělo také hostovat verzi *1.0.0* jako samostatný a jiný balíček.</span><span class="sxs-lookup"><span data-stu-id="4c93b-248">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>

## <a name="where-nugetversion-diverges-from-semantic-versioning"></a><span data-ttu-id="4c93b-249">Kde se NuGetVersion odchylují od sémantické správy verzí</span><span class="sxs-lookup"><span data-stu-id="4c93b-249">Where NuGetVersion diverges from Semantic Versioning</span></span>

<span data-ttu-id="4c93b-250">Pokud chcete programově používat verze balíčků NuGet, důrazně doporučujeme použít [balíček NuGet. Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span><span class="sxs-lookup"><span data-stu-id="4c93b-250">If you want to programatically use NuGet package versions, it is strongly recommended to use [the package NuGet.Versioning](https://www.nuget.org/packages/NuGet.Versioning).</span></span> <span data-ttu-id="4c93b-251">Statickou metodu `NuGetVersion.Parse(string)` lze použít k analýze řetězců verze a `VersionComparer` lze ji použít k řazení `NuGetVersion` instancí.</span><span class="sxs-lookup"><span data-stu-id="4c93b-251">The static method `NuGetVersion.Parse(string)` can be used to parse the version strings, and `VersionComparer` can be used to sort `NuGetVersion` instances.</span></span>

<span data-ttu-id="4c93b-252">Pokud implementujete funkce NuGet v jazyce, který neběží na platformě .NET, najdete tady známý seznam rozdílů mezi `NuGetVersion` a sémantickou správou verzí a důvody, proč nemusí existující knihovna sémantických verzí fungovat pro balíčky, které už jsou publikované v NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4c93b-252">If you are implementing NuGet functionality in a language that does not run on .NET, here are the known list of differences between `NuGetVersion` and Semantic Versioning, and the reasons why an existing Semantic Versioning library might not work for packages already published on nuget.org.</span></span>

1. <span data-ttu-id="4c93b-253">`NuGetVersion` podporuje segment čtvrté verze, `Revision` , aby byl kompatibilní s nebo nadmnožinou, [`System.Version`](/dotnet/api/system.version) .</span><span class="sxs-lookup"><span data-stu-id="4c93b-253">`NuGetVersion` supports a 4th version segment, `Revision`, to be compatible with, or a superset of, [`System.Version`](/dotnet/api/system.version).</span></span> <span data-ttu-id="4c93b-254">Proto s výjimkou předprodejní a popisků metadat je řetězec verze `Major.Minor.Patch.Revision` .</span><span class="sxs-lookup"><span data-stu-id="4c93b-254">Therefore, excluding prerelease and metadata labels, a version string is `Major.Minor.Patch.Revision`.</span></span> <span data-ttu-id="4c93b-255">Jak je to normalizace podle výše popsané výše, pokud `Revision` je nula, je z normalizovaného řetězce verze vynechán.</span><span class="sxs-lookup"><span data-stu-id="4c93b-255">As per version normalization described above, if `Revision` is zero, it is omit from the normalized version string.</span></span>
2. <span data-ttu-id="4c93b-256">`NuGetVersion` vyžaduje, aby byl definován hlavní segment.</span><span class="sxs-lookup"><span data-stu-id="4c93b-256">`NuGetVersion` only requires the major segment to be defined.</span></span> <span data-ttu-id="4c93b-257">Všechny ostatní jsou volitelné a odpovídají nule.</span><span class="sxs-lookup"><span data-stu-id="4c93b-257">All others are optional, and are equivalent to zero.</span></span> <span data-ttu-id="4c93b-258">To znamená, že `1` ,, `1.0` `1.0.0` a `1.0.0.0` jsou všechny přijaty a rovné.</span><span class="sxs-lookup"><span data-stu-id="4c93b-258">This means that `1`, `1.0`, `1.0.0`, and `1.0.0.0` are all accepted and equal.</span></span>
3. <span data-ttu-id="4c93b-259">`NuGetVersion` používá porovnání řetězců insenstive Case pro předběžné verze komponent.</span><span class="sxs-lookup"><span data-stu-id="4c93b-259">`NuGetVersion` uses case insenstive string comparisons for pre-release components.</span></span> <span data-ttu-id="4c93b-260">To znamená, že `1.0.0-alpha` a `1.0.0-Alpha` jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="4c93b-260">This means that `1.0.0-alpha` and `1.0.0-Alpha` are equal.</span></span>
