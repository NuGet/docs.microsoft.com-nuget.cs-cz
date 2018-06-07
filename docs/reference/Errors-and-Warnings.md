---
title: Referenční upozornění a chyby NuGet
description: Úplný referenční varování a chyby vystavené NuGet během různé operace NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 368a9554c5caf92b709f9b29e16b8a7cdb264eec
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818513"
---
# <a name="errors-and-warnings"></a><span data-ttu-id="c5e39-103">Chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-103">Errors and warnings</span></span>

<span data-ttu-id="c5e39-104">V NuGet 4.3.0+ chyby a upozornění jsou číslované, jak je popsáno v tomto tématu a poskytují podrobné informace můžete vyřešit problémy související se situací.</span><span class="sxs-lookup"><span data-stu-id="c5e39-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="c5e39-105">S chybami a upozorněními tady jsou k dispozici jenom s [na základě PackageReference](../consume-packages/package-references-in-project-files.md) projekty a NuGet 4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="c5e39-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="c5e39-106">NuGet rovněž ctí vlastnosti nástroje MSBuild potlačení upozornění nebo zvýšit jejich chyby.</span><span class="sxs-lookup"><span data-stu-id="c5e39-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="c5e39-107">Další informace najdete v tématu [postupy: potlačení upozornění kompilátoru](/visualstudio/ide/how-to-suppress-compiler-warnings) v dokumentaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5e39-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="c5e39-108">**Chyby**</span><span class="sxs-lookup"><span data-stu-id="c5e39-108">**Errors**</span></span>

| <span data-ttu-id="c5e39-109">Skupina</span><span class="sxs-lookup"><span data-stu-id="c5e39-109">Group</span></span> | <span data-ttu-id="c5e39-110">Chyba čísla</span><span class="sxs-lookup"><span data-stu-id="c5e39-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c5e39-111">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="c5e39-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="c5e39-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c5e39-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="c5e39-113">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="c5e39-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="c5e39-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (dříve NU1607), [NU1108](#nu1108) (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="c5e39-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="c5e39-115">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="c5e39-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="c5e39-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c5e39-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="c5e39-117">**Upozornění**</span><span class="sxs-lookup"><span data-stu-id="c5e39-117">**Warnings**</span></span>

| <span data-ttu-id="c5e39-118">Skupina</span><span class="sxs-lookup"><span data-stu-id="c5e39-118">Group</span></span> | <span data-ttu-id="c5e39-119">Čísla upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c5e39-120">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="c5e39-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c5e39-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="c5e39-122">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="c5e39-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="c5e39-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c5e39-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="c5e39-124">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="c5e39-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="c5e39-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="c5e39-126">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="c5e39-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="c5e39-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="c5e39-128">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="c5e39-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="c5e39-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="c5e39-130">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="c5e39-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c5e39-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="c5e39-132">Podepsaný balíčků (vytvoření a ověření)</span><span class="sxs-lookup"><span data-stu-id="c5e39-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="c5e39-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="c5e39-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="c5e39-134">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="c5e39-134">Invalid input errors</span></span>

<span data-ttu-id="c5e39-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c5e39-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="c5e39-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="c5e39-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-137">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-137">**Issue**</span></span> | <span data-ttu-id="c5e39-138">Projekt neobsahuje jeden nebo více rozhraní.</span><span class="sxs-lookup"><span data-stu-id="c5e39-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="c5e39-139">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-139">**Example message**</span></span> | <span data-ttu-id="c5e39-140">*Projekt projA neurčuje žádné cílové rozhraní v c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="c5e39-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="c5e39-141">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-141">**Solution**</span></span> | <span data-ttu-id="c5e39-142">Přidat `TargetFramework` nebo `TargetFrameworks` vlastnost k souboru zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="c5e39-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="c5e39-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-144">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-144">**Issue**</span></span> | <span data-ttu-id="c5e39-145">Neplatná kombinace vstupy společně s ZRUŠTE – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="c5e39-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="c5e39-146">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-146">**Example message**</span></span> | <span data-ttu-id="c5e39-147">*'CLEAR' nelze použít ve spojení s další hodnoty*</span><span class="sxs-lookup"><span data-stu-id="c5e39-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="c5e39-148">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-148">**Solution**</span></span> | <span data-ttu-id="c5e39-149">Použít ZRUŠTE sám o sobě a vynechat možnost všechny ostatní vstupy.</span><span class="sxs-lookup"><span data-stu-id="c5e39-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="c5e39-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="c5e39-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-151">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-151">**Issue**</span></span> | <span data-ttu-id="c5e39-152">`PackageTargetFallback` a `AssetTargetFallback` poskytovat různé chování pro výběr prostředky a nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="c5e39-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="c5e39-153">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-153">**Example message**</span></span> | <span data-ttu-id="c5e39-154">*PackageTargetFallback a AssetTargetFallback nelze použít společně. Odeberte PackageTargetFallback(deprecated) odkazy z prostředí projektu.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="c5e39-155">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-155">**Solution**</span></span> | <span data-ttu-id="c5e39-156">Odeberte nepoužívané `PackageTargetFallback` element z projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="c5e39-157">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="c5e39-157">Missing package and project errors</span></span>

<span data-ttu-id="c5e39-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="c5e39-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="c5e39-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="c5e39-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-160">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-160">**Issue**</span></span> | <span data-ttu-id="c5e39-161">Skupina závislosti není možné přeložit.</span><span class="sxs-lookup"><span data-stu-id="c5e39-161">A dependency group not be resolved.</span></span> <span data-ttu-id="c5e39-162">Toto je obecná problém pro typy, které nejsou balíčky nebo projekty.</span><span class="sxs-lookup"><span data-stu-id="c5e39-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="c5e39-163">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-163">**Example message**</span></span> | <span data-ttu-id="c5e39-164">*Nelze přeložit System.Missing pro net45*</span><span class="sxs-lookup"><span data-stu-id="c5e39-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="c5e39-165">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-165">**Solution**</span></span> | <span data-ttu-id="c5e39-166">Otevřete soubor projektu a zkontrolujte seznam jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="c5e39-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="c5e39-167">Zkontrolujte, zda má každá závislost na zdroje balíčku, kterou používáte, a zda balíček podporuje cílový framework projektu na.</span><span class="sxs-lookup"><span data-stu-id="c5e39-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="c5e39-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="c5e39-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-169">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-169">**Issue**</span></span> | <span data-ttu-id="c5e39-170">Balíček nebyl nalezen na žádné zdroje.</span><span class="sxs-lookup"><span data-stu-id="c5e39-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="c5e39-171">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-171">**Example message**</span></span> | <span data-ttu-id="c5e39-172">*Nepodařilo se najít balíček System.Missing. Neexistují žádné balíčky s tímto id v zdrojích: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="c5e39-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="c5e39-173">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-173">**Solution**</span></span> | <span data-ttu-id="c5e39-174">Zkontrolujte závislosti projektu v sadě Visual Studio a zajistit tak, že používáte správný balíček identifikátor a verzi číslo.</span><span class="sxs-lookup"><span data-stu-id="c5e39-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="c5e39-175">Také zkontrolujte, zda [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md) identifikuje zdroje balíčku vaší očekávají, že používat.</span><span class="sxs-lookup"><span data-stu-id="c5e39-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="c5e39-176">Pokud používáte balíčky, které mají [sémantické verze 2.0.0](../reference/package-versioning.md#semantic-versioning-200), ujistěte se, že používáte V3 kanálu, `https://api.nuget.org/v3/index.json`v [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c5e39-176">If you use packages that have [Semantic Versioning 2.0.0](../reference/package-versioning.md#semantic-versioning-200), please make sure that you are using the V3 feed, `https://api.nuget.org/v3/index.json`, in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="c5e39-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="c5e39-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-178">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-178">**Issue**</span></span> | <span data-ttu-id="c5e39-179">Identifikátor balíčku se nenašel, ale nenašla se verze v rozsahu zadaná závislost na některý ze zdrojů.</span><span class="sxs-lookup"><span data-stu-id="c5e39-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="c5e39-180">Rozsah může být určena balíček a nikoli uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5e39-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="c5e39-181">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-181">**Example message**</span></span> | <span data-ttu-id="c5e39-182">*Nejde najít balíček NuGet.Versioning s verzí (> = 9.0.1)<br/> -30 nalezena verze v nuget.org [nejbližší verze: 4.0.0]<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -nalezen 9 verze v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032]<br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="c5e39-183">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-183">**Solution**</span></span> | <span data-ttu-id="c5e39-184">Upravte soubor projektu a opravte verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5e39-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="c5e39-185">Také zkontrolujte, zda [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md) identifikuje zdroje balíčku vaší očekávají, že používat.</span><span class="sxs-lookup"><span data-stu-id="c5e39-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="c5e39-186">Potřebujete verzi requeted změnit, pokud tento balíček je odkazován objektem projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="c5e39-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="c5e39-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="c5e39-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-188">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-188">**Issue**</span></span> | <span data-ttu-id="c5e39-189">Projektu zadána stabilní verze pro rozsah závislostí, ale v tomto rozsahu nebyly nalezeny žádné stabilní verze.</span><span class="sxs-lookup"><span data-stu-id="c5e39-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="c5e39-190">Nebyly nalezeny předběžných verzí, ale nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="c5e39-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="c5e39-191">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-191">**Example message**</span></span> | <span data-ttu-id="c5e39-192">*Nelze najít stabilní balíček NuGet.Versioning s verzí (> = 3.0.0)<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -verze 9 najít v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032] <br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="c5e39-193">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-193">**Solution**</span></span> |  <span data-ttu-id="c5e39-194">Upravte rozsah verze v souboru projektu zahrnout předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="c5e39-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="c5e39-195">V tématu [Správa verzí balíčku](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="c5e39-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="c5e39-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="c5e39-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-197">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-197">**Issue**</span></span> | <span data-ttu-id="c5e39-198">ProjectReference odkazuje na soubor, který neexistuje.</span><span class="sxs-lookup"><span data-stu-id="c5e39-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="c5e39-199">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-199">**Example message**</span></span> | <span data-ttu-id="c5e39-200">*Odkaz na projekt neexistuje 'c:\a.csproj'. Zkontrolujte, že je odkaz na projekt platný a zda existuje soubor projektu.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="c5e39-201">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-201">**Solution**</span></span> | <span data-ttu-id="c5e39-202">Upravte soubor projektu buď opravte cestu k odkazované projektu nebo odebrat odkaz na úplně, pokud je již nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="c5e39-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="c5e39-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="c5e39-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-204">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-204">**Issue**</span></span> | <span data-ttu-id="c5e39-205">Soubor projektu existuje, ale pro něj k dispozici žádné informace pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="c5e39-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="c5e39-206">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-206">**Example message**</span></span> | <span data-ttu-id="c5e39-207">*Nelze číst informace o projektu pro 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="c5e39-208">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-208">**Solution**</span></span> | <span data-ttu-id="c5e39-209">V sadě Visual Studio chyba může znamenat, že projekt odpojen, v takovém případě projekt znovu načíst.</span><span class="sxs-lookup"><span data-stu-id="c5e39-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="c5e39-210">Z příkazového řádku, to může znamenat, že soubor je poškozený nebo že neobsahuje vlastní "po importy" target potřebná pro obnovení k načtení projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="c5e39-211">Zkontrolujte, zda soubor projektu je platný a obsahuje cílový "po importy".</span><span class="sxs-lookup"><span data-stu-id="c5e39-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="c5e39-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="c5e39-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-213">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-213">**Issue**</span></span> | <span data-ttu-id="c5e39-214">Omezení závislostí nelze přeložit.</span><span class="sxs-lookup"><span data-stu-id="c5e39-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="c5e39-215">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-215">**Example message**</span></span> | <span data-ttu-id="c5e39-216">*Nelze vyhovět konfliktním žádostem pro {id}: {cesta konflikt} Framework: {cíl grafu}*</span><span class="sxs-lookup"><span data-stu-id="c5e39-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="c5e39-217">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-217">**Solution**</span></span> | <span data-ttu-id="c5e39-218">Upravte soubor projektu k určení širší rozsahy závislost, nikoli přesnou verzi.</span><span class="sxs-lookup"><span data-stu-id="c5e39-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="c5e39-219">NU1107 (dříve NU1607)</span><span class="sxs-lookup"><span data-stu-id="c5e39-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-220">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-220">**Issue**</span></span> | <span data-ttu-id="c5e39-221">Nelze vyřešit omezení závislost mezi balíčky.</span><span class="sxs-lookup"><span data-stu-id="c5e39-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="c5e39-222">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-222">**Example message**</span></span> | <span data-ttu-id="c5e39-223">*Pro NuGet.Versioning zjištěn konflikt verzí. Odkazují na balíček přímo z projektu k vyřešení tohoto problému.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="c5e39-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="c5e39-224">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-224">**Solution**</span></span> | <span data-ttu-id="c5e39-225">Balíčky s omezeními závislosti na přesné verze neumožňují dalších balíčků v případě potřeby zvýšit verze.</span><span class="sxs-lookup"><span data-stu-id="c5e39-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="c5e39-226">Přidáte odkaz na balíček přímo (v souboru projektu) s přesnou verzi vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="c5e39-226">Add a reference to the package directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="c5e39-227">NU1108 (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="c5e39-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-228">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-228">**Issue**</span></span> | <span data-ttu-id="c5e39-229">Byla rozpoznána cyklická závislost.</span><span class="sxs-lookup"><span data-stu-id="c5e39-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="c5e39-230">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-230">**Example message**</span></span> | <span data-ttu-id="c5e39-231">*Byl zjištěn cyklus: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="c5e39-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="c5e39-232">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-232">**Solution**</span></span> | <span data-ttu-id="c5e39-233">Balíček je vytvořené nesprávně; Obraťte se na vlastníka balíčku a opravte chyb.</span><span class="sxs-lookup"><span data-stu-id="c5e39-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="c5e39-234">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="c5e39-234">Compatibility errors</span></span>

<span data-ttu-id="c5e39-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c5e39-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="c5e39-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="c5e39-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-237">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-237">**Issue**</span></span> | <span data-ttu-id="c5e39-238">Závislosti projektu neobsahuje rozhraní kompatibilní s aktuálním projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="c5e39-239">Obvykle je cílový framework projektu na vyšší verzi než náročné projekt.</span><span class="sxs-lookup"><span data-stu-id="c5e39-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="c5e39-240">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-240">**Example message**</span></span> | <span data-ttu-id="c5e39-241">*ServerWeb projektu není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Projekt podporuje ServerWeb:<br/> -netstandard1.6 (. Monikerů NETStandard, verze = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, verze = verze 1.0)*</span><span class="sxs-lookup"><span data-stu-id="c5e39-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="c5e39-242">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-242">**Solution**</span></span> | <span data-ttu-id="c5e39-243">Změňte cílový framework projektu na stejné nebo nižší verzi než náročné projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="c5e39-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="c5e39-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-245">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-245">**Issue**</span></span> | <span data-ttu-id="c5e39-246">Závislost balíček neobsahuje žádné prostředky, které jsou kompatibilní s projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="c5e39-247">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-247">**Example message**</span></span> | <span data-ttu-id="c5e39-248">*Balíček System.ComponentModel.EventBasedAsync 4.0.11 není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Balíček podporuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, verze = verze 1.0)<br/> -monotouch10 (MonoTouch, verze = verze 1.0)<br/> -net45 (. NETFramework, verze = v4.5)<br/> -netcore50 (. NETCore, verze = v5.0)<br/> -netstandard1.0 (. Monikerů NETStandard, verze = verze 1.0)<br/> -přenositelností net45 + win8 + wp8 + wpa81 (. NETPortable, verze = v0.0, profil = Profile259)<br/> -win8 (Windows, verze = v8.0)<br/> -wp8 (WindowsPhone, verze = v8.0)<br/> -wpa81 (WindowsPhoneApp, verze = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="c5e39-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="c5e39-249">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-249">**Solution**</span></span> | <span data-ttu-id="c5e39-250">Změňte cílový framework projektu na na takový, který podporuje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5e39-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="c5e39-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="c5e39-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-252">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-252">**Issue**</span></span> | <span data-ttu-id="c5e39-253">Balíček nepodporuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="c5e39-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="c5e39-254">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-254">**Example message**</span></span> | <span data-ttu-id="c5e39-255">*System.Example 1.0.0 poskytuje kompilaci referenční sestavení pro a.dll na net461, ale neexistuje žádné kompatibilní sestavení za běhu.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="c5e39-256">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-256">**Solution**</span></span> | <span data-ttu-id="c5e39-257">Změna `RuntimeIdentifier` hodnoty používané v projektu podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="c5e39-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="c5e39-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="c5e39-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-259">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-259">**Issue**</span></span> | <span data-ttu-id="c5e39-260">Balíček vyžaduje funkce nebo rozhraní není aktuálně podporovaná nainstalovaná verze balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5e39-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="c5e39-261">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-261">**Example message**</span></span> | <span data-ttu-id="c5e39-262">*Balíček 'NuGet.Versioning' vyžaduje NuGet verze klienta, 5.0.0' nebo vyšší, ale aktuální verze NuGet je '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="c5e39-263">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-263">**Solution**</span></span> | <span data-ttu-id="c5e39-264">Nainstalujte novější verzi systému NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5e39-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="c5e39-265">V tématu [NuGet instalaci klienta nástroje](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="c5e39-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="c5e39-266">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-266">Invalid input warnings</span></span>

<span data-ttu-id="c5e39-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c5e39-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="c5e39-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="c5e39-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-269">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-269">**Issue**</span></span> | <span data-ttu-id="c5e39-270">Obnovení projektu se pokouší pracovat na nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="c5e39-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="c5e39-271">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-271">**Example message**</span></span> | <span data-ttu-id="c5e39-272">*Složka 'c:\projects\a' neobsahuje projekt k obnovení.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="c5e39-273">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-273">**Solution**</span></span> | <span data-ttu-id="c5e39-274">Spusťte obnovení nuget ve složce, která obsahuje projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="c5e39-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="c5e39-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-276">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-276">**Issue**</span></span> | <span data-ttu-id="c5e39-277">`RuntimeSupports` obsahuje neplatný profil.</span><span class="sxs-lookup"><span data-stu-id="c5e39-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="c5e39-278">Obvykle se podporuje profil nebyl nalezen v `runtime.json` souboru z aktuální závislostí balíčků.</span><span class="sxs-lookup"><span data-stu-id="c5e39-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="c5e39-279">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-279">**Example message**</span></span> | <span data-ttu-id="c5e39-280">*Neznámý kompatibility profilu: aaa*</span><span class="sxs-lookup"><span data-stu-id="c5e39-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="c5e39-281">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-281">**Solution**</span></span> | <span data-ttu-id="c5e39-282">Zkontrolujte `RuntimeSupports` hodnotu ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="c5e39-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="c5e39-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-284">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-284">**Issue**</span></span> | <span data-ttu-id="c5e39-285">Závislosti projektu neimportuje cíle obnovení NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5e39-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="c5e39-286">To se podobá NU1105 ale zde bude přeskočena projektu a ignorovat místo způsobuje všechny obnovení nezdaří.</span><span class="sxs-lookup"><span data-stu-id="c5e39-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="c5e39-287">Komplexní řešení často existují jiné typy projektů, které nemusí podporovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="c5e39-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="c5e39-288">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-288">**Example message**</span></span> | <span data-ttu-id="c5e39-289">*Přeskočení obnovení pro projekt 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="c5e39-290">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-290">**Solution**</span></span> | <span data-ttu-id="c5e39-291">Toto může nastat projekty, které neimportujte běžné props nebo cíle, které automaticky importovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="c5e39-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="c5e39-292">Pokud projekt není potřeba obnovit to můžete ignorovat.</span><span class="sxs-lookup"><span data-stu-id="c5e39-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="c5e39-293">Upravte, jinak hodnota ovlivněných projektu pro přidání cíle pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="c5e39-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="c5e39-294">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="c5e39-294">Unexpected package version warnings</span></span>

<span data-ttu-id="c5e39-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c5e39-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="c5e39-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="c5e39-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-297">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-297">**Issue**</span></span> | <span data-ttu-id="c5e39-298">Přímé projektu závislost byla bumped na vyšší verzi než zadaný projekt.</span><span class="sxs-lookup"><span data-stu-id="c5e39-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="c5e39-299">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-299">**Example message**</span></span> | <span data-ttu-id="c5e39-300">*Zadaná závislost byla NuGet.Versioning (> = 3.5.0), ale skončila s NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="c5e39-301">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-301">**Solution**</span></span> | <span data-ttu-id="c5e39-302">Aktualizujte závislostí v projektu na příslušnou verzi.</span><span class="sxs-lookup"><span data-stu-id="c5e39-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="c5e39-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="c5e39-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-304">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-304">**Issue**</span></span> | <span data-ttu-id="c5e39-305">Závislost balíčku chybí dolní mez.</span><span class="sxs-lookup"><span data-stu-id="c5e39-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="c5e39-306">To neumožňuje obnovení najít *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="c5e39-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="c5e39-307">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="c5e39-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c5e39-308">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5e39-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c5e39-309">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-309">**Example message**</span></span> | <span data-ttu-id="c5e39-310">*NuGet.Packaging 4.0.0 neposkytuje (včetně). dolní mez pro závislosti NuGet.Versioning (> 3.5.0). Přibližná nejlepší shody třídy 3.6.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="c5e39-311">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-311">**Solution**</span></span> | <span data-ttu-id="c5e39-312">Je to obvykle balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="c5e39-312">This is usually a package authoring error.</span></span> <span data-ttu-id="c5e39-313">Požádejte autora balíčku k vyřešení problému.</span><span class="sxs-lookup"><span data-stu-id="c5e39-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="c5e39-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="c5e39-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-315">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-315">**Issue**</span></span> | <span data-ttu-id="c5e39-316">Zadaná závislost balíčku na verzi, která nebyla nalezena.</span><span class="sxs-lookup"><span data-stu-id="c5e39-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="c5e39-317">Obvykle zdroje balíčku neobsahuje očekávaný dolní hranice verze.</span><span class="sxs-lookup"><span data-stu-id="c5e39-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="c5e39-318">Vyšší verzi byl použit místo toho, který se liší od co balíček vytvořený proti.</span><span class="sxs-lookup"><span data-stu-id="c5e39-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="c5e39-319">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="c5e39-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c5e39-320">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="c5e39-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c5e39-321">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5e39-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c5e39-322">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-322">**Example message**</span></span> | <span data-ttu-id="c5e39-323">NuGet.Packaging 4.0.0 závisí na NuGet.Versioning (> = 4.0.0), ale 4.0.0 nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="c5e39-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="c5e39-324">Přibližná nejlepší shody třídy 5.0.0 byl vyřešen.</span><span class="sxs-lookup"><span data-stu-id="c5e39-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="c5e39-325">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-325">**Solution**</span></span> | <span data-ttu-id="c5e39-326">Pokud balíček očekává ještě neuvolnil to může být balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="c5e39-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="c5e39-327">Požádejte autora balíčku k vyřešení problému.</span><span class="sxs-lookup"><span data-stu-id="c5e39-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="c5e39-328">Pokud byla vydána balíčku, potom zkontrolujte, zda je k dispozici na zdroje balíčku, kterou používáte.</span><span class="sxs-lookup"><span data-stu-id="c5e39-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="c5e39-329">Pokud používáte privátní zdroje, musíte aktualizovat balíček na který informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="c5e39-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="c5e39-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-331">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-331">**Issue**</span></span> | <span data-ttu-id="c5e39-332">Závislosti projektu nedefinuje dolní mez.</span><span class="sxs-lookup"><span data-stu-id="c5e39-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="c5e39-333">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="c5e39-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c5e39-334">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="c5e39-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c5e39-335">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5e39-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c5e39-336">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-336">**Example message**</span></span> | <span data-ttu-id="c5e39-337">*Projektu závislosti NuGet.Versioning (< = 9.0.0) doe neobsahuje (včetně). dolní mez. Zahrňte dolní hranice verze závislosti zajistit obnovení konzistentní výsledky.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="c5e39-338">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-338">**Solution**</span></span> | <span data-ttu-id="c5e39-339">Aktualizace projektu `PackageReference` `Version` atribut zahrnout dolní mez.</span><span class="sxs-lookup"><span data-stu-id="c5e39-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="c5e39-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="c5e39-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-341">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-341">**Issue**</span></span> | <span data-ttu-id="c5e39-342">Balíček závislostí zadat omezení verze na vyšší verzi balíčku, než obnovení nakonec přeložit.</span><span class="sxs-lookup"><span data-stu-id="c5e39-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="c5e39-343">To znamená z důvodu "nejbližší wins" pravidlo při rozpoznávání balíčky, blíž k uživateli balíčku v grafu může mít přepsat vzdáleným balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5e39-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="c5e39-344">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-344">**Example message**</span></span> | <span data-ttu-id="c5e39-345">*Zjištěna přechod na starší verzi balíčku: NuGet.Versioning z 4.0.0 k 3.5.0. Odkazují na balíček přímo z projektu a vyberte jinou verzi.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="c5e39-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="c5e39-346">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-346">**Solution**</span></span> | <span data-ttu-id="c5e39-347">Přidejte přímý odkaz na projekt pro vyšší verzi balíčku, který chcete použít.</span><span class="sxs-lookup"><span data-stu-id="c5e39-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="c5e39-348">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="c5e39-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="c5e39-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-350">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-350">**Issue**</span></span> | <span data-ttu-id="c5e39-351">Vyřešený balíček je vyšší, než povoluje omezení závislostí.</span><span class="sxs-lookup"><span data-stu-id="c5e39-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="c5e39-352">To znamená, že balíček odkazuje na projekt přepsání omezení závislost z jiných balíčků.</span><span class="sxs-lookup"><span data-stu-id="c5e39-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="c5e39-353">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-353">**Example message**</span></span> | <span data-ttu-id="c5e39-354">*Verze balíčku zjištěné mimo omezení závislost: x 1.0.0 vyžaduje y (= 1.0.0), ale verze y 2.0.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="c5e39-355">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-355">**Solution**</span></span> | <span data-ttu-id="c5e39-356">V některých případech to je úmyslné a lze potlačit upozornění.</span><span class="sxs-lookup"><span data-stu-id="c5e39-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="c5e39-357">Změňte, jinak hodnota projektu odkaz na balíček, který chcete rozšířit jeho omezení verze.</span><span class="sxs-lookup"><span data-stu-id="c5e39-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="c5e39-358">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="c5e39-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="c5e39-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-360">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-360">**Issue**</span></span> | <span data-ttu-id="c5e39-361">`PackageTargetFallback` / `AssetTargetFallback` byl použit k výběru prostředky z balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5e39-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="c5e39-362">Upozornění uživatelům vědět, že prostředky nemusí být 100 % kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="c5e39-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="c5e39-363">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-363">**Example message**</span></span> | <span data-ttu-id="c5e39-364">*Balíček NuGet.Versioning se obnovil pomocí 'přenositelností net45 + win8' místo toho cílový framework projektu 'netstandard1.5'. Tento balíček nemusí být plně kompatibilní s projektem.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="c5e39-365">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-365">**Solution**</span></span> | <span data-ttu-id="c5e39-366">Změňte cílový framework projektu na na takový, který podporuje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5e39-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="c5e39-367">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="c5e39-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="c5e39-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-369">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-369">**Issue**</span></span> | <span data-ttu-id="c5e39-370">Při načítání informačního kanálu došlo k chybě při `IgnoreFailedSources` je nastaven na hodnotu true, převádí ji nezávažné upozornění.</span><span class="sxs-lookup"><span data-stu-id="c5e39-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="c5e39-371">To může obsahovat jakékoli zprávy a je obecná.</span><span class="sxs-lookup"><span data-stu-id="c5e39-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="c5e39-372">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-372">**Example message**</span></span> | <span data-ttu-id="c5e39-373">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="c5e39-373">n/a</span></span> |
| <span data-ttu-id="c5e39-374">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-374">**Solution**</span></span> | <span data-ttu-id="c5e39-375">Upravte konfiguraci zadat platné zdroje.</span><span class="sxs-lookup"><span data-stu-id="c5e39-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="c5e39-376">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="c5e39-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="c5e39-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c5e39-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="c5e39-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="c5e39-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-379">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-379">**Issue**</span></span> | <span data-ttu-id="c5e39-380">Bez konkrétní vnitřní chyba z NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5e39-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="c5e39-381">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-381">**Solution**</span></span> | <span data-ttu-id="c5e39-382">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="c5e39-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="c5e39-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="c5e39-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-384">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-384">**Issue**</span></span> | <span data-ttu-id="c5e39-385">Bez konkrétní interní upozornění z NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5e39-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="c5e39-386">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-386">**Solution**</span></span> | <span data-ttu-id="c5e39-387">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="c5e39-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="c5e39-388">Podepsaný balíčků (vytvoření a ověření)</span><span class="sxs-lookup"><span data-stu-id="c5e39-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="c5e39-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="c5e39-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="c5e39-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="c5e39-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="c5e39-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="c5e39-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-392">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-392">**Issue**</span></span> | <span data-ttu-id="c5e39-393">Není dost konkrétní chyby související s podepisování balíčku a podepsaný balíček ověření.</span><span class="sxs-lookup"><span data-stu-id="c5e39-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="c5e39-394">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-394">**Solution**</span></span> | <span data-ttu-id="c5e39-395">Zkontrolujte protokoly pro další informace.</span><span class="sxs-lookup"><span data-stu-id="c5e39-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="c5e39-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="c5e39-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-397">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-397">**Issue**</span></span> | <span data-ttu-id="c5e39-398">Neplatné argumenty buď [přihlásit příkaz](../tools/cli-ref-sign.md) nebo [ověřte příkaz](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="c5e39-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="c5e39-399">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-399">**Solution**</span></span> | <span data-ttu-id="c5e39-400">Zkontrolujte a opravte zadaných argumentů.</span><span class="sxs-lookup"><span data-stu-id="c5e39-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="c5e39-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="c5e39-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-402">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-402">**Issue**</span></span> | <span data-ttu-id="c5e39-403">`-Timestamper` s nebyla zadána možnost [příkaz přihlašovací nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="c5e39-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="c5e39-404">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-404">**Example message**</span></span> | <span data-ttu-id="c5e39-405">*'-Timestamper' nebyla zadána možnost. Podepsaného balíčku nebudou označen časovým razítkem.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="c5e39-406">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-406">**Solution**</span></span> | <span data-ttu-id="c5e39-407">Zadejte `-Timestamper` možnost s `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="c5e39-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="c5e39-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="c5e39-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-409">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-409">**Issue**</span></span> | <span data-ttu-id="c5e39-410">Balíček nepodepsané zadaná k [nuget ověřte příkaz](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="c5e39-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="c5e39-411">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-411">**Solution**</span></span> | <span data-ttu-id="c5e39-412">Spustit `nuget verify` s podepsaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5e39-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="c5e39-413">V tématu [přihlásit balíček](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="c5e39-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="c5e39-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="c5e39-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-415">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-415">**Issue**</span></span> | <span data-ttu-id="c5e39-416">Zkontrolujte integritu balíčku se nezdařila, což znamená, že byla od Podepisovaný manipulováno podepsaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5e39-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="c5e39-417">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-417">**Solution**</span></span> | <span data-ttu-id="c5e39-418">Zkontrolujte počítač pomocí antivirového softwaru.</span><span class="sxs-lookup"><span data-stu-id="c5e39-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="c5e39-419">Daný balíček odebrat z počítače, znovu ji nainstalujte a operaci opakujte.</span><span class="sxs-lookup"><span data-stu-id="c5e39-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="c5e39-420">Pokud potíže potrvají, obraťte se na vlastníka zdrojových souborů balíčku a balíček vlastníka.</span><span class="sxs-lookup"><span data-stu-id="c5e39-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="c5e39-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="c5e39-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-422">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-422">**Issue**</span></span> | <span data-ttu-id="c5e39-423">Vytváření řetězu certifikátů se nezdařilo pro primární podpis.</span><span class="sxs-lookup"><span data-stu-id="c5e39-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="c5e39-424">Primární podpisový certifikát není důvěryhodný, odvolán, nebo není k dispozici informace o odvolání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="c5e39-425">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-425">**Example message**</span></span> | <span data-ttu-id="c5e39-426">*Upozornění: NU3018: Funkce zrušení se nepodařilo ověření odvolání certifikátu.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="c5e39-427">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-427">**Solution**</span></span> | <span data-ttu-id="c5e39-428">Používejte důvěryhodné a platný certifikát.</span><span class="sxs-lookup"><span data-stu-id="c5e39-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="c5e39-429">Zkontrolujte připojení k Internetu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="c5e39-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="c5e39-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c5e39-431">**Problém**</span><span class="sxs-lookup"><span data-stu-id="c5e39-431">**Issue**</span></span> | <span data-ttu-id="c5e39-432">Vytváření řetězu certifikátů se nezdařilo pro podpis časové razítko.</span><span class="sxs-lookup"><span data-stu-id="c5e39-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="c5e39-433">Časové razítko podpisový certifikát není důvěryhodný, odvolán, nebo není k dispozici informace o odvolání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="c5e39-434">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="c5e39-434">**Example message**</span></span> | <span data-ttu-id="c5e39-435">*Upozornění: NU3028: Funkce zrušení se nepodařilo ověření odvolání certifikátu.*</span><span class="sxs-lookup"><span data-stu-id="c5e39-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="c5e39-436">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="c5e39-436">**Solution**</span></span> | <span data-ttu-id="c5e39-437">Používejte důvěryhodné a platný certifikát.</span><span class="sxs-lookup"><span data-stu-id="c5e39-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="c5e39-438">Zkontrolujte připojení k Internetu.</span><span class="sxs-lookup"><span data-stu-id="c5e39-438">Check internet connectivity.</span></span> |
