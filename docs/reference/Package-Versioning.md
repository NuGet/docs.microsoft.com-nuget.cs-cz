---
title: Odkaz na balíček NuGet verze
description: Přesné údaje o zadání čísel verzí a rozsahy adres pro další balíčky, na které závisí balíčku NuGet, a jak jsou závislosti nainstalované.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549770"
---
# <a name="package-versioning"></a><span data-ttu-id="54f5e-103">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="54f5e-103">Package versioning</span></span>

<span data-ttu-id="54f5e-104">Konkrétní balíček je vždy rozumělo použití jeho identifikátor balíčku a číslem přesnou verzi.</span><span class="sxs-lookup"><span data-stu-id="54f5e-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="54f5e-105">Například [Entity Framework](https://www.nuget.org/packages/EntityFramework/) na nuget.org má několik desítek konkrétní balíčky k dispozici od verze *4.1.10311* verzi *6.1.3* (nejnovější stabilní verze vydání) a širokou škálu předběžných verzí, jako jsou *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="54f5e-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="54f5e-106">Při vytváření balíčku, přiřaďte číslo konkrétní verze s příponou volitelný text, který předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="54f5e-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="54f5e-107">Při využívání balíčků, na druhé straně může zadáte číslo přesnou verzi nebo rozsah verzí přijatelné.</span><span class="sxs-lookup"><span data-stu-id="54f5e-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="54f5e-108">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="54f5e-108">In this topic:</span></span>

- <span data-ttu-id="54f5e-109">[Základní informace o verzi](#version-basics) včetně přípony předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="54f5e-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="54f5e-110">Rozsahů verzí a zástupných znacích</span><span class="sxs-lookup"><span data-stu-id="54f5e-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="54f5e-111">Čísla verzí normalizované</span><span class="sxs-lookup"><span data-stu-id="54f5e-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="54f5e-112">Základní informace o verzi</span><span class="sxs-lookup"><span data-stu-id="54f5e-112">Version basics</span></span>

<span data-ttu-id="54f5e-113">Číslo konkrétní verze má formát *Hlavníverze.podverze.oprava [-přípona]*, kde komponenty mají následující význam:</span><span class="sxs-lookup"><span data-stu-id="54f5e-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="54f5e-114">*Hlavní*: Rozbíjející změny v</span><span class="sxs-lookup"><span data-stu-id="54f5e-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="54f5e-115">*Vedlejší*: nové funkce, ale zpětně kompatibilní</span><span class="sxs-lookup"><span data-stu-id="54f5e-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="54f5e-116">*Oprava*: pouze zpětně kompatibilní opravy chyb</span><span class="sxs-lookup"><span data-stu-id="54f5e-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="54f5e-117">*-Přípony* (volitelné): spojovník následovaný řetězec označující Předběžná verze (následující [Semantic Versioning nebo SemVer 1.0 konvence](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="54f5e-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="54f5e-118">**Příklady:**</span><span class="sxs-lookup"><span data-stu-id="54f5e-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="54f5e-119">nuget.org odmítne všechny nahrávání balíčku, který nemá číslem přesnou verzi.</span><span class="sxs-lookup"><span data-stu-id="54f5e-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="54f5e-120">Verze musí být zadán v `.nuspec` nebo soubor projektu používá k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="54f5e-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="54f5e-121">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="54f5e-121">Pre-release versions</span></span>

<span data-ttu-id="54f5e-122">Technicky vzato Tvůrce balíčku můžete použít libovolný řetězec jako příponu k označení předprodejní verze NuGet považuje předběžné verze těchto verzí a díky žádná interpretace.</span><span class="sxs-lookup"><span data-stu-id="54f5e-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="54f5e-123">To znamená je zahrnuta NuGet zobrazí řetězec na plnou verzi v jakékoli uživatelské rozhraní, byste museli opustit jakékoli výklad tuto příponu význam příjemci.</span><span class="sxs-lookup"><span data-stu-id="54f5e-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="54f5e-124">Ale nutné dodat, balíček vývojáři obvykle postupují podle rozpoznaný zásady vytváření názvů:</span><span class="sxs-lookup"><span data-stu-id="54f5e-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="54f5e-125">`-alpha`: Alfa verze, obvykle se používá pro nedokončenou prací a experimentování.</span><span class="sxs-lookup"><span data-stu-id="54f5e-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="54f5e-126">`-beta`: Betaverze, obvykle ten, který je funkce pro další plánované vydání, ale může obsahovat známé chyby.</span><span class="sxs-lookup"><span data-stu-id="54f5e-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="54f5e-127">`-rc`: Verze Release candidate, obvykle, která je potenciálně konečné vydání (stabilní), není-li významný chyby se objeví.</span><span class="sxs-lookup"><span data-stu-id="54f5e-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="54f5e-128">Podporuje NuGet 4.3.0+ [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), která podporuje předběžné verze čísla pomocí zápisu s tečkou, stejně jako v *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="54f5e-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="54f5e-129">Verze NuGet starší než 4.3.0 nepodporuje zápisu s tečkou.</span><span class="sxs-lookup"><span data-stu-id="54f5e-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="54f5e-130">Můžete použít formuláře jako *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="54f5e-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="54f5e-131">Při řešení a odkazy na balíček více verzí balíčku se liší pouze podle přípony, NuGet nejprve zvolí verze bez přípony a potom použije prioritu předběžných verzí ve vzestupném abecedním pořadí.</span><span class="sxs-lookup"><span data-stu-id="54f5e-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="54f5e-132">Například následující verze vybere v uvedeném pořadí:</span><span class="sxs-lookup"><span data-stu-id="54f5e-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="54f5e-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="54f5e-134">Díky NuGet 4.3.0+ a sady Visual Studio 2017 verze 15.3 + podporuje NuGet [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="54f5e-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="54f5e-135">Některé sémantiku SemVer v2.0.0 nepodporují starší klienti.</span><span class="sxs-lookup"><span data-stu-id="54f5e-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="54f5e-136">NuGet bere v úvahu verze balíčku bude SemVer v2.0.0 konkrétní, pokud je splněna jedna z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="54f5e-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="54f5e-137">Předběžné verze je popisek oddělené tečkou, třeba *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="54f5e-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="54f5e-138">Verze má metadat sestavení, například *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="54f5e-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="54f5e-139">Pro nuget.org balíček definován jako balíček v2.0.0 SemVer, pokud je splněna jedna z následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="54f5e-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="54f5e-140">Verze balíčku vlastní je SemVer v2.0.0 předpisům, ale není SemVer v1.0.0 předpisy, podle výše.</span><span class="sxs-lookup"><span data-stu-id="54f5e-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="54f5e-141">Některé z rozsahů verzí závislost balíčku má minimální nebo maximální verzi, která je SemVer v2.0.0 předpisům, ale není SemVer v1.0.0 předpisy, výše; například *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="54f5e-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="54f5e-142">Pokud odešlete balíček v2.0.0 konkrétní SemVer na nuget.org, balíček je viditelný pro starší klienty a k dispozici pro následující klienty NuGet:</span><span class="sxs-lookup"><span data-stu-id="54f5e-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="54f5e-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="54f5e-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="54f5e-144">Visual Studio 2017 verze 15.3 +</span><span class="sxs-lookup"><span data-stu-id="54f5e-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="54f5e-145">Visual Studio 2015 se sadou [v3.6.0 NuGet VSIX](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="54f5e-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="54f5e-146">DotNet</span><span class="sxs-lookup"><span data-stu-id="54f5e-146">dotnet</span></span>
  - <span data-ttu-id="54f5e-147">dotnetcore.exe (2.0.0+ sady .NET SDK)</span><span class="sxs-lookup"><span data-stu-id="54f5e-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="54f5e-148">Klienti třetích stran:</span><span class="sxs-lookup"><span data-stu-id="54f5e-148">Third-party clients:</span></span>

- <span data-ttu-id="54f5e-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="54f5e-149">JetBrains Rider</span></span>
- <span data-ttu-id="54f5e-150">Stáhnout verzi 5.0 +</span><span class="sxs-lookup"><span data-stu-id="54f5e-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="54f5e-151">Rozsahů verzí a zástupných znacích</span><span class="sxs-lookup"><span data-stu-id="54f5e-151">Version ranges and wildcards</span></span>

<span data-ttu-id="54f5e-152">Při odkazování na závislosti balíčků, podporuje NuGet, pomocí notace interval pro zadání rozsahu verzí shrnout takto:</span><span class="sxs-lookup"><span data-stu-id="54f5e-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="54f5e-153">Zápis</span><span class="sxs-lookup"><span data-stu-id="54f5e-153">Notation</span></span> | <span data-ttu-id="54f5e-154">Použité pravidlo</span><span class="sxs-lookup"><span data-stu-id="54f5e-154">Applied rule</span></span> | <span data-ttu-id="54f5e-155">Popis</span><span class="sxs-lookup"><span data-stu-id="54f5e-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="54f5e-156">1.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-156">1.0</span></span> | <span data-ttu-id="54f5e-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-157">x ≥ 1.0</span></span> | <span data-ttu-id="54f5e-158">Minimální verze (včetně)</span><span class="sxs-lookup"><span data-stu-id="54f5e-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="54f5e-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="54f5e-159">(1.0,)</span></span> | <span data-ttu-id="54f5e-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-160">x > 1.0</span></span> | <span data-ttu-id="54f5e-161">Minimální verze exkluzivní</span><span class="sxs-lookup"><span data-stu-id="54f5e-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="54f5e-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="54f5e-162">[1.0]</span></span> | <span data-ttu-id="54f5e-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-163">x == 1.0</span></span> | <span data-ttu-id="54f5e-164">Shoda přesnou verzi</span><span class="sxs-lookup"><span data-stu-id="54f5e-164">Exact version match</span></span> |
| <span data-ttu-id="54f5e-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="54f5e-165">(,1.0]</span></span> | <span data-ttu-id="54f5e-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-166">x ≤ 1.0</span></span> | <span data-ttu-id="54f5e-167">Maximální verze, včetně</span><span class="sxs-lookup"><span data-stu-id="54f5e-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="54f5e-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="54f5e-168">(,1.0)</span></span> | <span data-ttu-id="54f5e-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-169">x < 1.0</span></span> | <span data-ttu-id="54f5e-170">Maximální verze exkluzivní</span><span class="sxs-lookup"><span data-stu-id="54f5e-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="54f5e-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="54f5e-171">[1.0,2.0]</span></span> | <span data-ttu-id="54f5e-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="54f5e-173">Přesné rozsahu, včetně</span><span class="sxs-lookup"><span data-stu-id="54f5e-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="54f5e-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="54f5e-174">(1.0,2.0)</span></span> | <span data-ttu-id="54f5e-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="54f5e-176">Přesný rozsah exkluzivní</span><span class="sxs-lookup"><span data-stu-id="54f5e-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="54f5e-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="54f5e-177">[1.0,2.0)</span></span> | <span data-ttu-id="54f5e-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="54f5e-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="54f5e-179">Smíšené včetně minimální a výhradní maximální verze</span><span class="sxs-lookup"><span data-stu-id="54f5e-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="54f5e-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="54f5e-180">(1.0)</span></span>    | <span data-ttu-id="54f5e-181">neplatné</span><span class="sxs-lookup"><span data-stu-id="54f5e-181">invalid</span></span> | <span data-ttu-id="54f5e-182">neplatné</span><span class="sxs-lookup"><span data-stu-id="54f5e-182">invalid</span></span> |

<span data-ttu-id="54f5e-183">Při použití formátu PackageReference NuGet podporuje také pomocí zástupných znaků zápisu, \*pro hlavní, vedlejší, opravy a příponu předběžné verze část čísla.</span><span class="sxs-lookup"><span data-stu-id="54f5e-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="54f5e-184">Zástupné znaky se nepodporují `packages.config` formátu.</span><span class="sxs-lookup"><span data-stu-id="54f5e-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="54f5e-185">Předběžné verze nejsou zahrnuty při rozpoznávání rozsahů verzí.</span><span class="sxs-lookup"><span data-stu-id="54f5e-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="54f5e-186">Předběžné verze *jsou* zahrnuty při použití zástupného znaku (\*).</span><span class="sxs-lookup"><span data-stu-id="54f5e-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="54f5e-187">Rozsah verzí *[1.0,2.0]*, například nezahrnuje 2.0 beta, ale zástupné zápis _2.0-\*_ nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="54f5e-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="54f5e-188">Zobrazit [vydat 912](https://github.com/NuGet/Home/issues/912) pro další informace o zástupných znacích předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="54f5e-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="54f5e-189">Příklady</span><span class="sxs-lookup"><span data-stu-id="54f5e-189">Examples</span></span>

<span data-ttu-id="54f5e-190">Vždy v souborech projektu, zadejte verzi nebo rozsah verzí pro závislosti balíčků `packages.config` soubory, a `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="54f5e-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="54f5e-191">Bez verzi nebo rozsah verzí, NuGet 2.8.x a dříve zvolí nejnovější verze balíčku k dispozici při překladu závislost, zatímco NuGet 3.x a později zvolí nejnižší verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="54f5e-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="54f5e-192">Určení verze nebo verze rozsah předchází tento nejistoty.</span><span class="sxs-lookup"><span data-stu-id="54f5e-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="54f5e-193">Odkazy v souborech projektu (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="54f5e-193">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="54f5e-194">**Odkazy v `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="54f5e-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="54f5e-195">V `packages.config`, všech závislostí je uvedený s přesná `version` atribut, který se používá při obnovování balíčků.</span><span class="sxs-lookup"><span data-stu-id="54f5e-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="54f5e-196">`allowedVersions` Atribut se používá pouze během operace aktualizace, chcete-li omezit verze, ke kterým může aktualizovat balíček.</span><span class="sxs-lookup"><span data-stu-id="54f5e-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="54f5e-197">**Odkazy v `.nuspec` soubory**</span><span class="sxs-lookup"><span data-stu-id="54f5e-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="54f5e-198">`version` Atribut `<dependency>` element popisuje rozsah verzí, které jsou přijatelné pro závislost.</span><span class="sxs-lookup"><span data-stu-id="54f5e-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="54f5e-199">Čísla verzí normalizované</span><span class="sxs-lookup"><span data-stu-id="54f5e-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="54f5e-200">Toto je zásadní změny pro NuGet 3.4 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="54f5e-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="54f5e-201">Získání balíčků z úložiště během instalace, přeinstalujte nebo obnovení operací, zpracovává NuGet 3.4 + čísla verzí následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="54f5e-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="54f5e-202">Počáteční nuly jsou odebrány z čísel verzí:</span><span class="sxs-lookup"><span data-stu-id="54f5e-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="54f5e-203">Nula v čtvrtá součást čísla verze budou vypuštěny.</span><span class="sxs-lookup"><span data-stu-id="54f5e-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="54f5e-204">Tato normalizace nemá vliv na čísla verzí v balíčcích. ovlivňuje pouze jak odpovídá NuGet verze, pokud řešení závislostí.</span><span class="sxs-lookup"><span data-stu-id="54f5e-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="54f5e-205">Úložiště balíčků NuGet však musí zpracovat tyto hodnoty stejným způsobem jako NuGet, aby se zabránilo duplikování verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="54f5e-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="54f5e-206">Proto úložiště, který obsahuje verzi *1.0* balíčku nemělo by hostovat také verze *1.0.0* jako samostatné a odlišné balíček.</span><span class="sxs-lookup"><span data-stu-id="54f5e-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
