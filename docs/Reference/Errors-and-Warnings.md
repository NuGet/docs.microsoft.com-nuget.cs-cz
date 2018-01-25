---
title: "NuGet Restore chyby a upozornění odkaz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Úplný referenční varování a chyby, které jsou vydány při obnovování balíčků NuGet"
keywords: "NuGet chyby, upozornění NuGet diagnostiky"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
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
ms.openlocfilehash: 9e22b63636980ce64017c950148d9005bf9c2fb1
ms.sourcegitcommit: ed01eaeef9bf488c36556b97247ca440384c0242
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="fe5cb-104">Chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-104">Errors and warnings</span></span>

<span data-ttu-id="fe5cb-105">V NuGet 4.3.0 chyby a upozornění jsou číslované, jak je popsáno v tomto tématu a poskytují podrobné informace můžete vyřešit problémy související se situací.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="fe5cb-106">S chybami a upozorněními tady jsou k dispozici jenom s [na základě PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) projekty a NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="fe5cb-107">NuGet rovněž ctí vlastnosti nástroje MSBuild potlačení upozornění nebo zvýšit jejich chyby.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="fe5cb-108">Další informace najdete v tématu [postupy: potlačení upozornění kompilátoru](/visualstudio/ide/how-to-suppress-compiler-warnings) v dokumentaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="fe5cb-109">**Chyby**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-109">**Errors**</span></span>

| <span data-ttu-id="fe5cb-110">Skupina</span><span class="sxs-lookup"><span data-stu-id="fe5cb-110">Group</span></span> | <span data-ttu-id="fe5cb-111">Chyba čísla</span><span class="sxs-lookup"><span data-stu-id="fe5cb-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="fe5cb-112">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="fe5cb-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="fe5cb-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="fe5cb-114">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="fe5cb-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="fe5cb-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (dříve NU1607), [NU1108](#nu1108) (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="fe5cb-116">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="fe5cb-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="fe5cb-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="fe5cb-118">**Upozornění**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-118">**Warnings**</span></span>

| <span data-ttu-id="fe5cb-119">Skupina</span><span class="sxs-lookup"><span data-stu-id="fe5cb-119">Group</span></span> | <span data-ttu-id="fe5cb-120">Čísla upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="fe5cb-121">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="fe5cb-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="fe5cb-123">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="fe5cb-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="fe5cb-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="fe5cb-125">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="fe5cb-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="fe5cb-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="fe5cb-127">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="fe5cb-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="fe5cb-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="fe5cb-129">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="fe5cb-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="fe5cb-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="fe5cb-131">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="fe5cb-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="fe5cb-133">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="fe5cb-133">Invalid input errors</span></span>

<span data-ttu-id="fe5cb-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="fe5cb-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="fe5cb-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-136">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-136">**Issue**</span></span> | <span data-ttu-id="fe5cb-137">Projekt neobsahuje jeden nebo více rozhraní.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="fe5cb-138">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-138">**Common causes**</span></span> | <span data-ttu-id="fe5cb-139">Neobsahuje projekt `TargetFramework` nebo `TargetFrameworks` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="fe5cb-140">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-140">**Example message**</span></span> | <span data-ttu-id="fe5cb-141">*Projekt projA neurčuje žádné cílové rozhraní v c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="fe5cb-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="fe5cb-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-143">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-143">**Issue**</span></span> | <span data-ttu-id="fe5cb-144">Neplatná kombinace vstupy společně s ZRUŠTE – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="fe5cb-145">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-145">**Common causes**</span></span> | <span data-ttu-id="fe5cb-146">CLEAR nelze kombinovat s ostatní vstupy.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="fe5cb-147">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-147">**Example message**</span></span> | <span data-ttu-id="fe5cb-148">*'CLEAR' nelze použít ve spojení s další hodnoty*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="fe5cb-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="fe5cb-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-150">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-150">**Issue**</span></span> | <span data-ttu-id="fe5cb-151">`PackageTargetFallback`a `AssetTargetFallback` poskytovat různé chování pro výběr prostředky a nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="fe5cb-152">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-152">**Common causes**</span></span> | <span data-ttu-id="fe5cb-153">Obě `PackageTargetFallback` a `AssetTargetFallback` existovat v projektu.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="fe5cb-154">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-154">**Example message**</span></span> | <span data-ttu-id="fe5cb-155">*PackageTargetFallback a AssetTargetFallback nelze použít společně. Odeberte PackageTargetFallback(deprecated) odkazy z prostředí projektu.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="fe5cb-156">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="fe5cb-156">Missing package and project errors</span></span>

<span data-ttu-id="fe5cb-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="fe5cb-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="fe5cb-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-159">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-159">**Issue**</span></span> | <span data-ttu-id="fe5cb-160">Skupina závislosti není možné přeložit.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-160">A dependency group not be resolved.</span></span> <span data-ttu-id="fe5cb-161">Toto je obecná problém pro typy, které nejsou balíčky nebo projekty.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="fe5cb-162">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-162">**Common causes**</span></span> | <span data-ttu-id="fe5cb-163">Projekt obsahuje závislost na položku, která neexistuje.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="fe5cb-164">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-164">**Example message**</span></span> | <span data-ttu-id="fe5cb-165">*Nelze přeložit System.Missing pro net45*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="fe5cb-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="fe5cb-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-167">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-167">**Issue**</span></span> | <span data-ttu-id="fe5cb-168">Balíček nebyl nalezen na žádné zdroje.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="fe5cb-169">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-169">**Common causes**</span></span> | <span data-ttu-id="fe5cb-170">Chybí zdroj správný balíček nebo identifikátor balíčku je nesprávný.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="fe5cb-171">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-171">**Example message**</span></span> | <span data-ttu-id="fe5cb-172">*Nepodařilo se najít balíček System.Missing. Neexistují žádné balíčky s tímto id v zdrojích: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="fe5cb-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="fe5cb-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-174">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-174">**Issue**</span></span> | <span data-ttu-id="fe5cb-175">Identifikátor balíčku se nenašel, ale nenašla se verze v rozsahu zadaná závislost na některý ze zdrojů.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="fe5cb-176">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-176">**Common causes**</span></span> | <span data-ttu-id="fe5cb-177">Chybí zdroj správný balíček nebo rozsah závislostí je nesprávný.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="fe5cb-178">Rozsah může být určena balíček a nikoli uživatele.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="fe5cb-179">Uživatel možná muset přejít k dispozici verze, pokud tento balíček je odkazován objektem projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="fe5cb-180">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-180">**Example message**</span></span> | <span data-ttu-id="fe5cb-181">*Nejde najít balíček NuGet.Versioning s verzí (> = 9.0.1)<br/> -30 nalezena verze v nuget.org [nejbližší verze: 4.0.0]<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -nalezen 9 verze v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032]<br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="fe5cb-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="fe5cb-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-183">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-183">**Issue**</span></span> | <span data-ttu-id="fe5cb-184">V rozsahu závislostí nebyly nalezeny žádné stabilní verze.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="fe5cb-185">Nebyly nalezeny předběžných verzí, ale nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="fe5cb-186">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-186">**Common causes**</span></span> | <span data-ttu-id="fe5cb-187">Projekt zadat stabilní verze pro rozsah závislostí.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="fe5cb-188">Uživatelé musí změnit rozsah verze zahrnout předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="fe5cb-189">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-189">**Example message**</span></span> | <span data-ttu-id="fe5cb-190">*Nelze najít stabilní balíček NuGet.Versioning s verzí (> = 3.0.0)<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -verze 9 najít v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032] <br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="fe5cb-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="fe5cb-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-192">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-192">**Issue**</span></span> | <span data-ttu-id="fe5cb-193">ProjectReference odkazuje na soubor, který neexistuje.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="fe5cb-194">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-194">**Common causes**</span></span> | <span data-ttu-id="fe5cb-195">Soubor projektu chybí disk nebo odkaz je nesprávný.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="fe5cb-196">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-196">**Example message**</span></span> | <span data-ttu-id="fe5cb-197">*Odkaz na projekt neexistuje 'c:\a.csproj'. Zkontrolujte, že je odkaz na projekt platný a zda existuje soubor projektu.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="fe5cb-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="fe5cb-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-199">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-199">**Issue**</span></span> | <span data-ttu-id="fe5cb-200">Soubor projektu existuje, ale pro něj k dispozici žádné informace pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="fe5cb-201">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-201">**Common causes**</span></span> | <span data-ttu-id="fe5cb-202">V sadě Visual Studio to může znamenat, že projekt je odpojen.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="fe5cb-203">Z příkazového řádku to může znamenat, že soubor je poškozený nebo že neobsahuje vlastní po importy cíl potřebná pro obnovení k načtení projektu.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="fe5cb-204">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-204">**Example message**</span></span> | <span data-ttu-id="fe5cb-205">*Nelze číst informace o projektu pro 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="fe5cb-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="fe5cb-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-207">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-207">**Issue**</span></span> | <span data-ttu-id="fe5cb-208">Omezení závislostí nelze přeložit.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="fe5cb-209">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-209">**Common causes**</span></span> | <span data-ttu-id="fe5cb-210">Balíčky obsahovat závislosti na přesné verze balíčku místo zprostředkovává rozsahy.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="fe5cb-211">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-211">**Example message**</span></span> | <span data-ttu-id="fe5cb-212">*Nelze vyhovět konfliktním žádostem pro {id}: {cesta konflikt} Framework: {cíl grafu}*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="fe5cb-213">NU1107 (dříve NU1607)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-214">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-214">**Issue**</span></span> | <span data-ttu-id="fe5cb-215">Nelze vyřešit omezení závislost mezi balíčky.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="fe5cb-216">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-216">**Common causes**</span></span> | <span data-ttu-id="fe5cb-217">Balíčky s omezeními závislosti na přesné verze neumožňují dalších balíčků v případě potřeby zvýšit verze.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="fe5cb-218">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-218">**Example message**</span></span> | <span data-ttu-id="fe5cb-219">*Pro NuGet.Versioning zjištěn konflikt verzí. Odkazují na balíček přímo z projektu k vyřešení tohoto problému.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="fe5cb-220">NU1108 (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-221">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-221">**Issue**</span></span> | <span data-ttu-id="fe5cb-222">Byla rozpoznána cyklická závislost.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="fe5cb-223">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-223">**Common causes**</span></span> | <span data-ttu-id="fe5cb-224">Balíček není správně vytvořeny.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="fe5cb-225">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-225">**Example message**</span></span> | <span data-ttu-id="fe5cb-226">*Byl zjištěn cyklus: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="fe5cb-227">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="fe5cb-227">Compatibility errors</span></span>

<span data-ttu-id="fe5cb-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="fe5cb-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="fe5cb-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-230">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-230">**Issue**</span></span> | <span data-ttu-id="fe5cb-231">Závislosti projektu neobsahuje rozhraní kompatibilní s aktuálním projektu.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="fe5cb-232">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-232">**Common causes**</span></span> | <span data-ttu-id="fe5cb-233">Cílový framework projektu na je vyšší verze než náročné projekt.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="fe5cb-234">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-234">**Example message**</span></span> | <span data-ttu-id="fe5cb-235">*ServerWeb projektu není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Projekt podporuje ServerWeb:<br/> -netstandard1.6 (. Monikerů NETStandard, verze = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, verze = verze 1.0)*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="fe5cb-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="fe5cb-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-237">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-237">**Issue**</span></span> | <span data-ttu-id="fe5cb-238">Závislost balíček neobsahuje žádné prostředky, které jsou kompatibilní s projektu.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="fe5cb-239">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-239">**Common causes**</span></span> | <span data-ttu-id="fe5cb-240">Balíček nepodporuje cílový framework projektu na.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="fe5cb-241">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-241">**Example message**</span></span> | <span data-ttu-id="fe5cb-242">*Balíček System.ComponentModel.EventBasedAsync 4.0.11 není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Balíček podporuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, verze = verze 1.0)<br/> -monotouch10 (MonoTouch, verze = verze 1.0)<br/> -net45 (. NETFramework, verze = v4.5)<br/> -netcore50 (. NETCore, verze = v5.0)<br/> -netstandard1.0 (. Monikerů NETStandard, verze = verze 1.0)<br/> -přenositelností net45 + win8 + wp8 + wpa81 (. NETPortable, verze = v0.0, profil = Profile259)<br/> -win8 (Windows, verze = v8.0)<br/> -wp8 (WindowsPhone, verze = v8.0)<br/> -wpa81 (WindowsPhoneApp, verze = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="fe5cb-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="fe5cb-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-244">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-244">**Issue**</span></span> | <span data-ttu-id="fe5cb-245">Balíček nepodporuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="fe5cb-246">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-246">**Common causes**</span></span> | <span data-ttu-id="fe5cb-247">Balíček nepodporuje aktuální `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="fe5cb-248">Změna `RuntimeIdentifier` hodnoty používané v projektu, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="fe5cb-249">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-249">**Example message**</span></span> | <span data-ttu-id="fe5cb-250">*System.Example 1.0.0 poskytuje kompilaci referenční sestavení pro a.dll na net461, ale neexistuje žádné kompatibilní sestavení za běhu.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="fe5cb-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="fe5cb-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-252">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-252">**Issue**</span></span> | <span data-ttu-id="fe5cb-253">Balíček vyžaduje funkce nebo rozhraní není aktuálně podporovaná nainstalovaná verze balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="fe5cb-254">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-254">**Common causes**</span></span> | <span data-ttu-id="fe5cb-255">Upgradujte rozšíření NuGet vyřešit problém.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="fe5cb-256">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-256">**Example message**</span></span> | <span data-ttu-id="fe5cb-257">*Balíček 'NuGet.Versioning' vyžaduje NuGet verze klienta, 5.0.0' nebo vyšší, ale aktuální verze NuGet je '4.3.0'. Pokud chcete upgradovat NuGet, přejděte na http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="fe5cb-258">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-258">Invalid input warnings</span></span>

<span data-ttu-id="fe5cb-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="fe5cb-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="fe5cb-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-261">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-261">**Issue**</span></span> | <span data-ttu-id="fe5cb-262">Obnovení projektu se pokouší pracovat na nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="fe5cb-263">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-263">**Common causes**</span></span> | <span data-ttu-id="fe5cb-264">Projekt chybí.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-264">The project is missing.</span></span> |
| <span data-ttu-id="fe5cb-265">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-265">**Example message**</span></span> | <span data-ttu-id="fe5cb-266">*Složka 'c:\projects\a' neobsahuje projekt k obnovení.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="fe5cb-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="fe5cb-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-268">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-268">**Issue**</span></span> | <span data-ttu-id="fe5cb-269">`RuntimeSupports`obsahuje neplatný profil.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="fe5cb-270">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-270">**Common causes**</span></span> | <span data-ttu-id="fe5cb-271">Podporuje profil nebyl nalezen v `runtime.json` souboru z aktuální závislostí balíčků.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="fe5cb-272">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-272">**Example message**</span></span> | <span data-ttu-id="fe5cb-273">*Neznámý kompatibility profilu: aaa*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="fe5cb-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="fe5cb-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-275">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-275">**Issue**</span></span> | <span data-ttu-id="fe5cb-276">Závislosti projektu neimportuje cíle obnovení NuGet.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="fe5cb-277">To se podobá NU1105 ale zde bude přeskočena projektu a ignorovat místo způsobuje všechny obnovení nezdaří.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="fe5cb-278">Komplexní řešení často existují jiné typy projektů, které nemusí podporovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="fe5cb-279">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-279">**Common causes**</span></span> | <span data-ttu-id="fe5cb-280">Toto může nastat projekty, které neimportujte běžné props nebo cíle, které automaticky importovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="fe5cb-281">Pokud projekt není potřeba obnovit to můžete ignorovat.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="fe5cb-282">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-282">**Example message**</span></span> | <span data-ttu-id="fe5cb-283">*Přeskočení obnovení pro projekt 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="fe5cb-284">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="fe5cb-284">Unexpected package version warnings</span></span>

<span data-ttu-id="fe5cb-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="fe5cb-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="fe5cb-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-287">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-287">**Issue**</span></span> | <span data-ttu-id="fe5cb-288">Přímé projektu závislost byla bumped na vyšší verzi než zadaný projekt.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="fe5cb-289">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-289">**Common causes**</span></span> | <span data-ttu-id="fe5cb-290">Jiný balíček závislostí vyžaduje vyšší verzi a bumped balíček.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="fe5cb-291">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-291">**Example message**</span></span> | <span data-ttu-id="fe5cb-292">*Zadaná závislost byla NuGet.Versioning (> = 3.5.0), ale skončila s NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="fe5cb-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="fe5cb-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-294">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-294">**Issue**</span></span> | <span data-ttu-id="fe5cb-295">Závislost balíčku chybí dolní mez.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="fe5cb-296">To neumožňuje obnovení najít *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="fe5cb-297">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="fe5cb-298">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="fe5cb-299">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-299">**Common causes**</span></span> | <span data-ttu-id="fe5cb-300">Je to obvykle balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="fe5cb-301">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-301">**Example message**</span></span> | <span data-ttu-id="fe5cb-302">*NuGet.Packaging 4.0.0 neposkytuje (včetně). dolní mez pro závislosti NuGet.Versioning (> 3.5.0). Přibližná nejlepší shody třídy 3.6.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="fe5cb-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="fe5cb-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-304">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-304">**Issue**</span></span> | <span data-ttu-id="fe5cb-305">Zadaná závislost balíčku na verzi, která nebyla nalezena.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="fe5cb-306">Vyšší verzi byl použit místo toho, který se liší od co balíček vytvořený proti.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="fe5cb-307">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="fe5cb-308">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="fe5cb-309">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="fe5cb-310">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-310">**Common causes**</span></span> | <span data-ttu-id="fe5cb-311">Zdroje balíčku neobsahuje očekávaný dolní hranice verze.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="fe5cb-312">Pokud balíček očekává ještě neuvolnil to může být balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="fe5cb-313">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-313">**Example message**</span></span> | <span data-ttu-id="fe5cb-314">NuGet.Packaging 4.0.0 závisí na NuGet.Versioning (> = 4.0.0), ale 4.0.0 nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="fe5cb-315">Přibližná nejlepší shody třídy 5.0.0 byl vyřešen.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="fe5cb-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="fe5cb-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-317">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-317">**Issue**</span></span> | <span data-ttu-id="fe5cb-318">Závislosti projektu nedefinuje dolní mez.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="fe5cb-319">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="fe5cb-320">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="fe5cb-321">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="fe5cb-322">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-322">**Common causes**</span></span> | <span data-ttu-id="fe5cb-323">Projektu *PackageReference* *verze* atributu se musí aktualizovat na zahrnují dolní mez.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="fe5cb-324">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-324">**Example message**</span></span> | <span data-ttu-id="fe5cb-325">*Projektu závislosti NuGet.Versioning (< = 9.0.0) doe neobsahuje (včetně). dolní mez. Zahrňte dolní hranice verze závislosti zajistit obnovení konzistentní výsledky.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="fe5cb-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="fe5cb-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-327">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-327">**Issue**</span></span> | <span data-ttu-id="fe5cb-328">Balíček závislostí zadat omezení verze na vyšší verzi balíčku, než obnovení nakonec přeložit.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="fe5cb-329">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-329">**Common causes**</span></span> | <span data-ttu-id="fe5cb-330">Nejbližší wins při rozpoznávání balíčky.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="fe5cb-331">Balíček blíž k uživateli v grafu může přepsat vzdáleným balíčku.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="fe5cb-332">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-332">**Example message**</span></span> | <span data-ttu-id="fe5cb-333">*Zjištěna přechod na starší verzi balíčku: NuGet.Versioning z 4.0.0 k 3.5.0. Odkazují na balíček přímo z projektu a vyberte jinou verzi.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="fe5cb-334">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="fe5cb-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="fe5cb-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-336">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-336">**Issue**</span></span> | <span data-ttu-id="fe5cb-337">Vyřešte balíčku je vyšší, než umožňuje omezení závislostí.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="fe5cb-338">V některých případech to je úmyslné a lze potlačit upozornění.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="fe5cb-339">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-339">**Common causes**</span></span> | <span data-ttu-id="fe5cb-340">Balíček odkazuje na projekt se přepíše omezení závislost z jiných balíčků.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="fe5cb-341">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-341">**Example message**</span></span> | <span data-ttu-id="fe5cb-342">*Verze balíčku zjištěné mimo omezení závislost: x 1.0.0 vyžaduje y (= 1.0.0), ale verze y 2.0.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="fe5cb-343">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="fe5cb-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="fe5cb-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-345">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-345">**Issue**</span></span> | <span data-ttu-id="fe5cb-346">*PackageTargetFallback/AssetTargetFallback* byl použit k výběru prostředky z balíčku.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="fe5cb-347">Toto je upozornění, aby mohl uživatel vědět, že prostředky nemusí být 100 % kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="fe5cb-348">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-348">**Common causes**</span></span> | <span data-ttu-id="fe5cb-349">Balíček nepodporuje rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="fe5cb-350">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-350">**Example message**</span></span> | <span data-ttu-id="fe5cb-351">*Balíček NuGet.Versioning se obnovil pomocí 'přenositelností net45 + win8' místo toho cílový framework projektu 'netstandard1.5'. Tento balíček nemusí být plně kompatibilní s projektem.*</span><span class="sxs-lookup"><span data-stu-id="fe5cb-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="fe5cb-352">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="fe5cb-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="fe5cb-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-354">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-354">**Issue**</span></span> | <span data-ttu-id="fe5cb-355">Při načítání informačního kanálu došlo k chybě při `IgnoreFailedSources` je nastaven na hodnotu true, převádí ji nezávažné upozornění.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="fe5cb-356">To může obsahovat jakékoli zprávy a je obecná.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="fe5cb-357">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-357">**Common causes**</span></span> | <span data-ttu-id="fe5cb-358">Zdroj je neplatný.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-358">The source is invalid.</span></span> |
| <span data-ttu-id="fe5cb-359">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-359">**Example message**</span></span> | <span data-ttu-id="fe5cb-360">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="fe5cb-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="fe5cb-361">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="fe5cb-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="fe5cb-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="fe5cb-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="fe5cb-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="fe5cb-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-364">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-364">**Issue**</span></span> | <span data-ttu-id="fe5cb-365">Bez konkrétní vnitřní chyba z NuGet.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="fe5cb-366">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-366">**Common causes**</span></span> | <span data-ttu-id="fe5cb-367">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="fe5cb-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="fe5cb-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="fe5cb-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="fe5cb-369">**Problém**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-369">**Issue**</span></span> | <span data-ttu-id="fe5cb-370">Bez konkrétní interní upozornění z NuGet.</span><span class="sxs-lookup"><span data-stu-id="fe5cb-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="fe5cb-371">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="fe5cb-371">**Common causes**</span></span> | <span data-ttu-id="fe5cb-372">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="fe5cb-372">Check the logs for more information</span></span> |
