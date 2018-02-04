---
title: "Odkaz na balíček NuGet verze | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Přesné informace o zadání čísla verzí a rozsahy adres pro jiné balíčky, na který závislý balíček NuGet, a způsob instalace závislosti."
keywords: "Správa verzí, závislosti balíčků NuGet, verze závislostí NuGet, čísla verzí NuGet, verze balíčku NuGet, verze rozsahy, specifikace verze, normalizované verze čísla"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="package-versioning"></a><span data-ttu-id="da4b7-104">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="da4b7-104">Package versioning</span></span>

<span data-ttu-id="da4b7-105">Konkrétní balíček se vždy označuje pomocí jeho identifikátoru balíčku a představuje počet přesnou verzi.</span><span class="sxs-lookup"><span data-stu-id="da4b7-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="da4b7-106">Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) v nuget.org má několik desítek konkrétní balíčky k dispozici od verze *4.1.10311* verzi *6.1.3* (nejnovější stabilní verzi) a celou řadu předprodejní verze, jako jsou *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="da4b7-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="da4b7-107">Při vytváření balíčku, můžete přiřadit konkrétní verzi číslo s příponou volitelné text předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="da4b7-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="da4b7-108">Při využívání balíčky, na druhé straně, můžete číslo přesné verze nebo rozsah přijatelné verzí.</span><span class="sxs-lookup"><span data-stu-id="da4b7-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="da4b7-109">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="da4b7-109">In this topic:</span></span>

- <span data-ttu-id="da4b7-110">[Základní informace o verzi](#version-basics) včetně přípony předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="da4b7-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="da4b7-111">Verze rozsahy a zástupné znaky</span><span class="sxs-lookup"><span data-stu-id="da4b7-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="da4b7-112">Čísla verzí normalizovaný</span><span class="sxs-lookup"><span data-stu-id="da4b7-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="da4b7-113">Základní informace o verzi</span><span class="sxs-lookup"><span data-stu-id="da4b7-113">Version basics</span></span>

<span data-ttu-id="da4b7-114">Číslo konkrétní verze je ve formátu *Major.Minor.Patch [-přípona]*, kde součásti mají následující významy:</span><span class="sxs-lookup"><span data-stu-id="da4b7-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="da4b7-115">*Hlavní*: nejnovější změny</span><span class="sxs-lookup"><span data-stu-id="da4b7-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="da4b7-116">*Méně závažné*: nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="da4b7-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="da4b7-117">*Oprava*: pouze zpětně kompatibilní opravy chyb</span><span class="sxs-lookup"><span data-stu-id="da4b7-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="da4b7-118">*-Přípona* (volitelné): pomlčka následuje řetězec představující předběžné verze (následující [sémantické verze nebo SemVer 1.0 konvence](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="da4b7-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="da4b7-119">**Příklady:**</span><span class="sxs-lookup"><span data-stu-id="da4b7-119">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="da4b7-120">nuget.org odmítne všechny nahrávání balíčku, který představuje počet přesnou verzi chybí.</span><span class="sxs-lookup"><span data-stu-id="da4b7-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="da4b7-121">Verze musí být zadán v `.nuspec` nebo projektu soubor použitý k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="da4b7-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="da4b7-122">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="da4b7-122">Pre-release versions</span></span>

<span data-ttu-id="da4b7-123">Technicky platí, že tvůrci balíček můžete použít libovolný řetězec jako příponu k označení předběžné verze, jako NuGet zpracovává všechny tyto verze jako předběžné verze a umožňuje žádné jiné interpretace.</span><span class="sxs-lookup"><span data-stu-id="da4b7-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="da4b7-124">To znamená je zahrnuta NuGet zobrazí na plnou verzi řetězce v jakémkoli uživatelského rozhraní, a jakýkoli výklad význam tuto příponu k příjemce.</span><span class="sxs-lookup"><span data-stu-id="da4b7-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="da4b7-125">Ale nutné dodat, balíček vývojáři obvykle podle rozpoznaný zásady vytváření názvů:</span><span class="sxs-lookup"><span data-stu-id="da4b7-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="da4b7-126">`-alpha`: Alfa verze, obvykle se používá pro práce v průběhu a experimenty.</span><span class="sxs-lookup"><span data-stu-id="da4b7-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="da4b7-127">`-beta`: Beta verze, obvykle ten, který je funkce dokončení další plánované verze, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="da4b7-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="da4b7-128">`-rc`: Release candidate, obvykle verzi, která je potenciálně konečné (stable), pokud vznikat významné chyby.</span><span class="sxs-lookup"><span data-stu-id="da4b7-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="da4b7-129">Podporuje NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), který podporuje předběžné verze čísla s zápisu s tečkou, jako v *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="da4b7-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="da4b7-130">Verze NuGet před 4.3.0 nepodporuje zápisu s tečkou.</span><span class="sxs-lookup"><span data-stu-id="da4b7-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="da4b7-131">Můžete použít formuláře jako *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="da4b7-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="da4b7-132">Při rozpoznávání, že balíček odkazuje a více verzí balíčku liší pouze příponu, NuGet vybere první verze bez přípony a pak použije prioritu pro předběžné verze verze ve vzestupném abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="da4b7-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="da4b7-133">Například by být zvolena následující verze v uvedeném pořadí:</span><span class="sxs-lookup"><span data-stu-id="da4b7-133">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="da4b7-134">Sémantické verze 2.0.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="da4b7-135">NuGet 4.3.0+ a Visual Studio 2017 verze 15.3 +, podporuje NuGet [sémantické verze 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="da4b7-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="da4b7-136">Některé sémantiku SemVer v2.0.0 nepodporuje starší klienty.</span><span class="sxs-lookup"><span data-stu-id="da4b7-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="da4b7-137">NuGet zvažuje verze balíčku byl SemVer v2.0.0 konkrétní, pokud je splněna jedna z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="da4b7-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="da4b7-138">Předběžné verze popisek je oddělené tečkou, například *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="da4b7-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="da4b7-139">Verze má sestavení metadata, například *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="da4b7-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="da4b7-140">Pro nuget.org balíček definován jako balíček v2.0.0 SemVer, pokud platí některá z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="da4b7-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="da4b7-141">Verze balíčku pro vlastní je SemVer v2.0.0 kompatibilní, ale ne SemVer v1.0.0 předpisy, podle definice výše.</span><span class="sxs-lookup"><span data-stu-id="da4b7-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="da4b7-142">Žádné z rozsahů verze závislosti balíčku má minimální nebo maximální verzi, která je kompatibilní s SemVer v2.0.0, ale není SemVer v1.0.0 předpisy, definovaný nad; například *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="da4b7-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="da4b7-143">Pokud balíček v2.0.0 specifické SemVer nahrajete do nuget.org, je balíček neviditelná pro starší klienty a k dispozici pouze na následující klienty NuGet:</span><span class="sxs-lookup"><span data-stu-id="da4b7-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="da4b7-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="da4b7-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="da4b7-145">Visual Studio 2017 verze 15.3 +</span><span class="sxs-lookup"><span data-stu-id="da4b7-145">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="da4b7-146">Visual Studio 2015 se [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="da4b7-146">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="da4b7-147">dotnet.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="da4b7-147">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="da4b7-148">Klienti třetí strany:</span><span class="sxs-lookup"><span data-stu-id="da4b7-148">Third-party clients:</span></span>

- <span data-ttu-id="da4b7-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="da4b7-149">JetBrains Rider</span></span>
- <span data-ttu-id="da4b7-150">Stáhnout verze 5.0 +</span><span class="sxs-lookup"><span data-stu-id="da4b7-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="da4b7-151">Verze rozsahy a zástupné znaky</span><span class="sxs-lookup"><span data-stu-id="da4b7-151">Version ranges and wildcards</span></span>

<span data-ttu-id="da4b7-152">Při odkazování na závislosti balíčků, NuGet podporuje notaci interval pro určení rozsahu verzí shrnout takto:</span><span class="sxs-lookup"><span data-stu-id="da4b7-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="da4b7-153">Zápis</span><span class="sxs-lookup"><span data-stu-id="da4b7-153">Notation</span></span> | <span data-ttu-id="da4b7-154">Použité pravidlo</span><span class="sxs-lookup"><span data-stu-id="da4b7-154">Applied rule</span></span> | <span data-ttu-id="da4b7-155">Popis</span><span class="sxs-lookup"><span data-stu-id="da4b7-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="da4b7-156">1.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-156">1.0</span></span> | <span data-ttu-id="da4b7-157">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="da4b7-157">1.0 ≤ x</span></span> | <span data-ttu-id="da4b7-158">Minimální verze, včetně.</span><span class="sxs-lookup"><span data-stu-id="da4b7-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="da4b7-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="da4b7-159">(1.0,)</span></span> | <span data-ttu-id="da4b7-160">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="da4b7-160">1.0 < x</span></span> | <span data-ttu-id="da4b7-161">Minimální verze, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="da4b7-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="da4b7-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="da4b7-162">[1.0]</span></span> | <span data-ttu-id="da4b7-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-163">x == 1.0</span></span> | <span data-ttu-id="da4b7-164">Shoda přesnou verzi</span><span class="sxs-lookup"><span data-stu-id="da4b7-164">Exact version match</span></span> |
| <span data-ttu-id="da4b7-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="da4b7-165">(,1.0]</span></span> | <span data-ttu-id="da4b7-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-166">x ≤ 1.0</span></span> | <span data-ttu-id="da4b7-167">Maximální verze, včetně.</span><span class="sxs-lookup"><span data-stu-id="da4b7-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="da4b7-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="da4b7-168">(,1.0)</span></span> | <span data-ttu-id="da4b7-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-169">x < 1.0</span></span> | <span data-ttu-id="da4b7-170">Maximální verze, exkluzivní</span><span class="sxs-lookup"><span data-stu-id="da4b7-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="da4b7-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="da4b7-171">[1.0,2.0]</span></span> | <span data-ttu-id="da4b7-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="da4b7-173">Přesný rozsahu (včetně).</span><span class="sxs-lookup"><span data-stu-id="da4b7-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="da4b7-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="da4b7-174">(1.0,2.0)</span></span> | <span data-ttu-id="da4b7-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="da4b7-176">Přesný rozsah výhradní</span><span class="sxs-lookup"><span data-stu-id="da4b7-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="da4b7-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="da4b7-177">[1.0,2.0)</span></span> | <span data-ttu-id="da4b7-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="da4b7-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="da4b7-179">Smíšená (včetně) minimální a výhradní maximální verze</span><span class="sxs-lookup"><span data-stu-id="da4b7-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="da4b7-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="da4b7-180">(1.0)</span></span>    | <span data-ttu-id="da4b7-181">neplatné</span><span class="sxs-lookup"><span data-stu-id="da4b7-181">invalid</span></span> | <span data-ttu-id="da4b7-182">neplatné</span><span class="sxs-lookup"><span data-stu-id="da4b7-182">invalid</span></span> |

<span data-ttu-id="da4b7-183">Při použití formátu PackageReference, NuGet podporuje také notaci zástupný znak, \*, pro hlavní, vedlejší, opravy a příponu předběžné verze součástí číslo.</span><span class="sxs-lookup"><span data-stu-id="da4b7-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="da4b7-184">Zástupné znaky nejsou podporovány `packages.config` formátu.</span><span class="sxs-lookup"><span data-stu-id="da4b7-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="da4b7-185">Předběžné verze nejsou zahrnuty při rozpoznávání rozsahy verze.</span><span class="sxs-lookup"><span data-stu-id="da4b7-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="da4b7-186">Předběžné verze verze *jsou* zahrnuty při pomocí zástupného znaku (\*).</span><span class="sxs-lookup"><span data-stu-id="da4b7-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="da4b7-187">Rozsah verze *[1.0,2.0]*, například nezahrnuje 2.0 beta, ale zápis zástupný znak _2.0-\*_ nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="da4b7-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="da4b7-188">V tématu [vydání 912](https://github.com/NuGet/Home/issues/912) Další informace o předběžné verze zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="da4b7-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="da4b7-189">Příklady</span><span class="sxs-lookup"><span data-stu-id="da4b7-189">Examples</span></span>

<span data-ttu-id="da4b7-190">Vždy zadejte verzi nebo rozsahu verze závislosti balíčku v souborech projektu `packages.config` soubory, a `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="da4b7-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="da4b7-191">Bez verze nebo verze rozsah, NuGet 2.8.x a dříve vybere nejnovější verze balíčku k dispozici při rozpoznávání závislost, zatímco NuGet 3.x a později rozhodne nejnižší verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="da4b7-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="da4b7-192">Určení verze nebo verze, rozsah zabraňuje tato nejistoty.</span><span class="sxs-lookup"><span data-stu-id="da4b7-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="da4b7-193">Odkazy v souborech projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="da4b7-193">References in project files (PackageReference)</span></span>

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="da4b7-194">**Odkazy na v `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="da4b7-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="da4b7-195">V `packages.config`, každý závislostí je označené přesného `version` atribut, který se používá při obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="da4b7-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="da4b7-196">`allowedVersions` Atribut se používá pouze během operace aktualizace omezit verze, do kterých může aktualizovat balíček.</span><span class="sxs-lookup"><span data-stu-id="da4b7-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="da4b7-197">**Odkazy na v `.nuspec` soubory**</span><span class="sxs-lookup"><span data-stu-id="da4b7-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="da4b7-198">`version` Atribut `<dependency>` element popisuje rozsah verze, které jsou přijatelné pro závislost.</span><span class="sxs-lookup"><span data-stu-id="da4b7-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="da4b7-199">Čísla verzí normalizovaný</span><span class="sxs-lookup"><span data-stu-id="da4b7-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="da4b7-200">Toto je narušující změně pro NuGet 3.4 a novější.</span><span class="sxs-lookup"><span data-stu-id="da4b7-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="da4b7-201">Při získávání balíčky z úložiště během instalace, znovu nainstalovat, nebo obnovit operace, považuje NuGet 3.4 + čísla verzí následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="da4b7-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="da4b7-202">Úvodní nuly jsou odebrány z čísla verzí:</span><span class="sxs-lookup"><span data-stu-id="da4b7-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="da4b7-203">Nula v čtvrtá součást číslo verze bude vynechán.</span><span class="sxs-lookup"><span data-stu-id="da4b7-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="da4b7-204">Tato hodnota normalization nemá vliv na čísla verze v balíčcích sami; ovlivňuje způsob NuGet odpovídá jen verze při řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="da4b7-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="da4b7-205">Úložiště balíčku NuGet však musí považovat tyto hodnoty stejným způsobem jako NuGet aby duplikace verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="da4b7-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="da4b7-206">Proto úložiště, který obsahuje verzi *1.0* balíčku neměly hostovat taky verze *1.0.0* jako samostatné a jiný balíček.</span><span class="sxs-lookup"><span data-stu-id="da4b7-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
