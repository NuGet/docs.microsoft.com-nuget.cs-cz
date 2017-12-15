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
ms.openlocfilehash: 3423e30eae07ff0c70a010576b8e701be027b847
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="errors-and-warnings"></a><span data-ttu-id="94d56-104">Chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-104">Errors and warnings</span></span>

<span data-ttu-id="94d56-105">V NuGet 4.3.0 chyby a upozornění jsou číslované, jak je popsáno v tomto tématu a poskytují podrobné informace můžete vyřešit problémy související se situací.</span><span class="sxs-lookup"><span data-stu-id="94d56-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="94d56-106">S chybami a upozorněními tady jsou k dispozici jenom s [na základě PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) projekty a NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="94d56-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="94d56-107">NuGet rovněž ctí vlastnosti nástroje MSBuild potlačení upozornění nebo zvýšit jejich chyby.</span><span class="sxs-lookup"><span data-stu-id="94d56-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="94d56-108">Další informace najdete v tématu [postupy: potlačení upozornění kompilátoru](https://docs.microsoft.com/visualstudio/ide/how-to-suppress-compiler-warnings) v dokumentaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94d56-108">For more information, see [How to: Suppress Compiler Warnings](https://docs.microsoft.com/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="94d56-109">**Chyby**</span><span class="sxs-lookup"><span data-stu-id="94d56-109">**Errors**</span></span>

| <span data-ttu-id="94d56-110">Skupina</span><span class="sxs-lookup"><span data-stu-id="94d56-110">Group</span></span> | <span data-ttu-id="94d56-111">Chyba čísla</span><span class="sxs-lookup"><span data-stu-id="94d56-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="94d56-112">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="94d56-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="94d56-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="94d56-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="94d56-114">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="94d56-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="94d56-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (dříve NU1607), [NU1108](#nu1107) (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="94d56-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="94d56-116">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="94d56-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="94d56-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="94d56-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="94d56-118">**Upozornění**</span><span class="sxs-lookup"><span data-stu-id="94d56-118">**Warnings**</span></span>

| <span data-ttu-id="94d56-119">Skupina</span><span class="sxs-lookup"><span data-stu-id="94d56-119">Group</span></span> | <span data-ttu-id="94d56-120">Čísla upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="94d56-121">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="94d56-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="94d56-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="94d56-123">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="94d56-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="94d56-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="94d56-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="94d56-125">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="94d56-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="94d56-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="94d56-127">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="94d56-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="94d56-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="94d56-129">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="94d56-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="94d56-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="94d56-131">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="94d56-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="94d56-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="94d56-133">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="94d56-133">Invalid input errors</span></span>

<span data-ttu-id="94d56-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="94d56-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="94d56-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="94d56-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-136">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-136">**Issue**</span></span> | <span data-ttu-id="94d56-137">Projekt neobsahuje jeden nebo více rozhraní.</span><span class="sxs-lookup"><span data-stu-id="94d56-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="94d56-138">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-138">**Common causes**</span></span> | <span data-ttu-id="94d56-139">Neobsahuje projekt `TargetFramework` nebo `TargetFrameworks` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="94d56-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="94d56-140">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-140">**Example message**</span></span> | <span data-ttu-id="94d56-141">*Projekt projA neurčuje žádné cílové rozhraní v c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="94d56-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="94d56-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="94d56-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-143">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-143">**Issue**</span></span> | <span data-ttu-id="94d56-144">Neplatná kombinace vstupy společně s ZRUŠTE – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="94d56-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="94d56-145">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-145">**Common causes**</span></span> | <span data-ttu-id="94d56-146">CLEAR nelze kombinovat s ostatní vstupy.</span><span class="sxs-lookup"><span data-stu-id="94d56-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="94d56-147">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-147">**Example message**</span></span> | <span data-ttu-id="94d56-148">*'CLEAR' nelze použít ve spojení s další hodnoty*</span><span class="sxs-lookup"><span data-stu-id="94d56-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="94d56-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="94d56-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-150">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-150">**Issue**</span></span> | <span data-ttu-id="94d56-151">`PackageTargetFallback`a `AssetTargetFallback` poskytovat různé chování pro výběr prostředky a nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="94d56-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="94d56-152">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-152">**Common causes**</span></span> | <span data-ttu-id="94d56-153">Obě `PackageTargetFallback` a `AssetTargetFallback` existovat v projektu.</span><span class="sxs-lookup"><span data-stu-id="94d56-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="94d56-154">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-154">**Example message**</span></span> | <span data-ttu-id="94d56-155">*PackageTargetFallback a AssetTargetFallback nelze použít společně. Odeberte PackageTargetFallback(deprecated) odkazy z prostředí projektu.*</span><span class="sxs-lookup"><span data-stu-id="94d56-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="94d56-156">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="94d56-156">Missing package and project errors</span></span>

<span data-ttu-id="94d56-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="94d56-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="94d56-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="94d56-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-159">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-159">**Issue**</span></span> | <span data-ttu-id="94d56-160">Skupina závislosti není možné přeložit.</span><span class="sxs-lookup"><span data-stu-id="94d56-160">A dependency group not be resolved.</span></span> <span data-ttu-id="94d56-161">Toto je obecná problém pro typy, které nejsou balíčky nebo projekty.</span><span class="sxs-lookup"><span data-stu-id="94d56-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="94d56-162">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-162">**Common causes**</span></span> | <span data-ttu-id="94d56-163">Projekt obsahuje závislost na položku, která neexistuje.</span><span class="sxs-lookup"><span data-stu-id="94d56-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="94d56-164">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-164">**Example message**</span></span> | <span data-ttu-id="94d56-165">*Nelze přeložit System.Missing pro net45*</span><span class="sxs-lookup"><span data-stu-id="94d56-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="94d56-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="94d56-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-167">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-167">**Issue**</span></span> | <span data-ttu-id="94d56-168">Balíček nebyl nalezen na žádné zdroje.</span><span class="sxs-lookup"><span data-stu-id="94d56-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="94d56-169">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-169">**Common causes**</span></span> | <span data-ttu-id="94d56-170">Chybí zdroj správný balíček nebo identifikátor balíčku je nesprávný.</span><span class="sxs-lookup"><span data-stu-id="94d56-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="94d56-171">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-171">**Example message**</span></span> | <span data-ttu-id="94d56-172">*Nepodařilo se najít balíček System.Missing. Neexistují žádné balíčky s tímto id v zdrojích: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="94d56-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="94d56-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="94d56-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-174">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-174">**Issue**</span></span> | <span data-ttu-id="94d56-175">Identifikátor balíčku se nenašel, ale nenašla se verze v rozsahu zadaná závislost na některý ze zdrojů.</span><span class="sxs-lookup"><span data-stu-id="94d56-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="94d56-176">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-176">**Common causes**</span></span> | <span data-ttu-id="94d56-177">Chybí zdroj správný balíček nebo rozsah závislostí je nesprávný.</span><span class="sxs-lookup"><span data-stu-id="94d56-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="94d56-178">Rozsah může být určena balíček a nikoli uživatele.</span><span class="sxs-lookup"><span data-stu-id="94d56-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="94d56-179">Uživatel možná muset přejít k dispozici verze, pokud tento balíček je odkazován objektem projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="94d56-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="94d56-180">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-180">**Example message**</span></span> | <span data-ttu-id="94d56-181">*Nejde najít balíček NuGet.Versioning s verzí (> = 9.0.1)<br/> -30 nalezena verze v nuget.org [nejbližší verze: 4.0.0]<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -nalezen 9 verze v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032]<br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="94d56-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="94d56-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="94d56-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-183">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-183">**Issue**</span></span> | <span data-ttu-id="94d56-184">V rozsahu závislostí nebyly nalezeny žádné stabilní verze.</span><span class="sxs-lookup"><span data-stu-id="94d56-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="94d56-185">Nebyly nalezeny předběžných verzí, ale nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="94d56-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="94d56-186">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-186">**Common causes**</span></span> | <span data-ttu-id="94d56-187">Projekt zadat stabilní verze pro rozsah závislostí.</span><span class="sxs-lookup"><span data-stu-id="94d56-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="94d56-188">Uživatelé musí změnit rozsah verze zahrnout předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="94d56-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="94d56-189">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-189">**Example message**</span></span> | <span data-ttu-id="94d56-190">*Nelze najít stabilní balíček NuGet.Versioning s verzí (> = 3.0.0)<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -verze 9 najít v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032] <br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="94d56-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="94d56-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="94d56-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-192">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-192">**Issue**</span></span> | <span data-ttu-id="94d56-193">ProjectReference odkazuje na soubor, který neexistuje.</span><span class="sxs-lookup"><span data-stu-id="94d56-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="94d56-194">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-194">**Common causes**</span></span> | <span data-ttu-id="94d56-195">Soubor projektu chybí disk nebo odkaz je nesprávný.</span><span class="sxs-lookup"><span data-stu-id="94d56-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="94d56-196">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-196">**Example message**</span></span> | <span data-ttu-id="94d56-197">*Odkaz na projekt neexistuje 'c:\a.csproj'. Zkontrolujte, že je odkaz na projekt platný a zda existuje soubor projektu.*</span><span class="sxs-lookup"><span data-stu-id="94d56-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="94d56-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="94d56-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-199">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-199">**Issue**</span></span> | <span data-ttu-id="94d56-200">Soubor projektu existuje, ale pro něj k dispozici žádné informace pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="94d56-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="94d56-201">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-201">**Common causes**</span></span> | <span data-ttu-id="94d56-202">V sadě Visual Studio to může znamenat, že projekt je odpojen.</span><span class="sxs-lookup"><span data-stu-id="94d56-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="94d56-203">Z příkazového řádku to může znamenat, že soubor je poškozený nebo že neobsahuje vlastní po importy cíl potřebná pro obnovení k načtení projektu.</span><span class="sxs-lookup"><span data-stu-id="94d56-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="94d56-204">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-204">**Example message**</span></span> | <span data-ttu-id="94d56-205">*Nelze číst informace o projektu pro 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="94d56-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="94d56-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="94d56-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-207">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-207">**Issue**</span></span> | <span data-ttu-id="94d56-208">Omezení závislostí nelze přeložit.</span><span class="sxs-lookup"><span data-stu-id="94d56-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="94d56-209">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-209">**Common causes**</span></span> | <span data-ttu-id="94d56-210">Balíčky obsahovat závislosti na přesné verze balíčku místo zprostředkovává rozsahy.</span><span class="sxs-lookup"><span data-stu-id="94d56-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="94d56-211">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-211">**Example message**</span></span> | <span data-ttu-id="94d56-212">*Nelze vyhovět konfliktním žádostem pro {id}: {cesta konflikt} Framework: {cíl grafu}*</span><span class="sxs-lookup"><span data-stu-id="94d56-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="94d56-213">< a name = "NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="94d56-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="94d56-214">NU1107 (dříve NU1607)</span><span class="sxs-lookup"><span data-stu-id="94d56-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-215">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-215">**Issue**</span></span> | <span data-ttu-id="94d56-216">Nelze vyřešit omezení závislost mezi balíčky.</span><span class="sxs-lookup"><span data-stu-id="94d56-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="94d56-217">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-217">**Common causes**</span></span> | <span data-ttu-id="94d56-218">Balíčky s omezeními závislosti na přesné verze neumožňují dalších balíčků v případě potřeby zvýšit verze.</span><span class="sxs-lookup"><span data-stu-id="94d56-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="94d56-219">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-219">**Example message**</span></span> | <span data-ttu-id="94d56-220">*Pro NuGet.Versioning zjištěn konflikt verzí. Odkazují na balíček přímo z projektu k vyřešení tohoto problému.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="94d56-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="94d56-221">< a name = "NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="94d56-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="94d56-222">NU1108 (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="94d56-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-223">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-223">**Issue**</span></span> | <span data-ttu-id="94d56-224">Byla rozpoznána cyklická závislost.</span><span class="sxs-lookup"><span data-stu-id="94d56-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="94d56-225">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-225">**Common causes**</span></span> | <span data-ttu-id="94d56-226">Balíček není správně vytvořeny.</span><span class="sxs-lookup"><span data-stu-id="94d56-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="94d56-227">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-227">**Example message**</span></span> | <span data-ttu-id="94d56-228">*Byl zjištěn cyklus: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="94d56-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="94d56-229">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="94d56-229">Compatibility errors</span></span>

<span data-ttu-id="94d56-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="94d56-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="94d56-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="94d56-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-232">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-232">**Issue**</span></span> | <span data-ttu-id="94d56-233">Závislosti projektu neobsahuje rozhraní kompatibilní s aktuálním projektu.</span><span class="sxs-lookup"><span data-stu-id="94d56-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="94d56-234">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-234">**Common causes**</span></span> | <span data-ttu-id="94d56-235">Cílový framework projektu na je vyšší verze než náročné projekt.</span><span class="sxs-lookup"><span data-stu-id="94d56-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="94d56-236">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-236">**Example message**</span></span> | <span data-ttu-id="94d56-237">*ServerWeb projektu není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Projekt podporuje ServerWeb:<br/> -netstandard1.6 (. Monikerů NETStandard, verze = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, verze = verze 1.0)*</span><span class="sxs-lookup"><span data-stu-id="94d56-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="94d56-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="94d56-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-239">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-239">**Issue**</span></span> | <span data-ttu-id="94d56-240">Závislost balíček neobsahuje žádné prostředky, které jsou kompatibilní s projektu.</span><span class="sxs-lookup"><span data-stu-id="94d56-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="94d56-241">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-241">**Common causes**</span></span> | <span data-ttu-id="94d56-242">Balíček nepodporuje cílový framework projektu na.</span><span class="sxs-lookup"><span data-stu-id="94d56-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="94d56-243">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-243">**Example message**</span></span> | <span data-ttu-id="94d56-244">*Balíček System.ComponentModel.EventBasedAsync 4.0.11 není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Balíček podporuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, verze = verze 1.0)<br/> -monotouch10 (MonoTouch, verze = verze 1.0)<br/> -net45 (. NETFramework, verze = v4.5)<br/> -netcore50 (. NETCore, verze = v5.0)<br/> -netstandard1.0 (. Monikerů NETStandard, verze = verze 1.0)<br/> -přenositelností net45 + win8 + wp8 + wpa81 (. NETPortable, verze = v0.0, profil = Profile259)<br/> -win8 (Windows, verze = v8.0)<br/> -wp8 (WindowsPhone, verze = v8.0)<br/> -wpa81 (WindowsPhoneApp, verze = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="94d56-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="94d56-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="94d56-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-246">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-246">**Issue**</span></span> | <span data-ttu-id="94d56-247">Balíček nepodporuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="94d56-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="94d56-248">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-248">**Common causes**</span></span> | <span data-ttu-id="94d56-249">Balíček nepodporuje aktuální `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="94d56-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="94d56-250">Změna `RuntimeIdentifier` hodnoty používané v projektu, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="94d56-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="94d56-251">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-251">**Example message**</span></span> | <span data-ttu-id="94d56-252">*System.Example 1.0.0 poskytuje kompilaci referenční sestavení pro a.dll na net461, ale neexistuje žádné kompatibilní sestavení za běhu.*</span><span class="sxs-lookup"><span data-stu-id="94d56-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="94d56-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="94d56-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-254">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-254">**Issue**</span></span> | <span data-ttu-id="94d56-255">Balíček vyžaduje funkce nebo rozhraní není aktuálně podporovaná nainstalovaná verze balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="94d56-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="94d56-256">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-256">**Common causes**</span></span> | <span data-ttu-id="94d56-257">Upgradujte rozšíření NuGet vyřešit problém.</span><span class="sxs-lookup"><span data-stu-id="94d56-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="94d56-258">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-258">**Example message**</span></span> | <span data-ttu-id="94d56-259">*Balíček 'NuGet.Versioning' vyžaduje NuGet verze klienta, 5.0.0' nebo vyšší, ale aktuální verze NuGet je '4.3.0'. Pokud chcete upgradovat NuGet, přejděte na http://docs.nuget.org/consume/installing-nuget.*</span><span class="sxs-lookup"><span data-stu-id="94d56-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="94d56-260">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-260">Invalid input warnings</span></span>

<span data-ttu-id="94d56-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="94d56-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="94d56-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="94d56-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-263">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-263">**Issue**</span></span> | <span data-ttu-id="94d56-264">Obnovení projektu se pokouší pracovat na nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="94d56-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="94d56-265">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-265">**Common causes**</span></span> | <span data-ttu-id="94d56-266">Projekt chybí.</span><span class="sxs-lookup"><span data-stu-id="94d56-266">The project is missing.</span></span> |
| <span data-ttu-id="94d56-267">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-267">**Example message**</span></span> | <span data-ttu-id="94d56-268">*Složka 'c:\projects\a' neobsahuje projekt k obnovení.*</span><span class="sxs-lookup"><span data-stu-id="94d56-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="94d56-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="94d56-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-270">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-270">**Issue**</span></span> | <span data-ttu-id="94d56-271">`RuntimeSupports`obsahuje neplatný profil.</span><span class="sxs-lookup"><span data-stu-id="94d56-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="94d56-272">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-272">**Common causes**</span></span> | <span data-ttu-id="94d56-273">Podporuje profil nebyl nalezen v `runtime.json` souboru z aktuální závislostí balíčků.</span><span class="sxs-lookup"><span data-stu-id="94d56-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="94d56-274">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-274">**Example message**</span></span> | <span data-ttu-id="94d56-275">*Neznámý kompatibility profilu: aaa*</span><span class="sxs-lookup"><span data-stu-id="94d56-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="94d56-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="94d56-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-277">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-277">**Issue**</span></span> | <span data-ttu-id="94d56-278">Závislosti projektu neimportuje cíle obnovení NuGet.</span><span class="sxs-lookup"><span data-stu-id="94d56-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="94d56-279">To se podobá NU1105 ale zde bude přeskočena projektu a ignorovat místo způsobuje všechny obnovení nezdaří.</span><span class="sxs-lookup"><span data-stu-id="94d56-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="94d56-280">Komplexní řešení často existují jiné typy projektů, které nemusí podporovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="94d56-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="94d56-281">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-281">**Common causes**</span></span> | <span data-ttu-id="94d56-282">Toto může nastat projekty, které neimportujte běžné props nebo cíle, které automaticky importovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="94d56-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="94d56-283">Pokud projekt není potřeba obnovit to můžete ignorovat.</span><span class="sxs-lookup"><span data-stu-id="94d56-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="94d56-284">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-284">**Example message**</span></span> | <span data-ttu-id="94d56-285">*Přeskočení obnovení pro projekt 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="94d56-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="94d56-286">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="94d56-286">Unexpected package version warnings</span></span>

<span data-ttu-id="94d56-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="94d56-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="94d56-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="94d56-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-289">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-289">**Issue**</span></span> | <span data-ttu-id="94d56-290">Přímé projektu závislost byla bumped na vyšší verzi než zadaný projekt.</span><span class="sxs-lookup"><span data-stu-id="94d56-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="94d56-291">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-291">**Common causes**</span></span> | <span data-ttu-id="94d56-292">Jiný balíček závislostí vyžaduje vyšší verzi a bumped balíček.</span><span class="sxs-lookup"><span data-stu-id="94d56-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="94d56-293">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-293">**Example message**</span></span> | <span data-ttu-id="94d56-294">*Zadaná závislost byla NuGet.Versioning (> = 3.5.0), ale skončila s NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="94d56-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="94d56-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="94d56-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-296">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-296">**Issue**</span></span> | <span data-ttu-id="94d56-297">Závislost balíčku chybí dolní mez.</span><span class="sxs-lookup"><span data-stu-id="94d56-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="94d56-298">To neumožňuje obnovení najít *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="94d56-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="94d56-299">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="94d56-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="94d56-300">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="94d56-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="94d56-301">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-301">**Common causes**</span></span> | <span data-ttu-id="94d56-302">Je to obvykle balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="94d56-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="94d56-303">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-303">**Example message**</span></span> | <span data-ttu-id="94d56-304">*NuGet.Packaging 4.0.0 neposkytuje (včetně). dolní mez pro závislosti NuGet.Versioning (> 3.5.0). Přibližná nejlepší shody třídy 3.6.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="94d56-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="94d56-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="94d56-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-306">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-306">**Issue**</span></span> | <span data-ttu-id="94d56-307">Zadaná závislost balíčku na verzi, která nebyla nalezena.</span><span class="sxs-lookup"><span data-stu-id="94d56-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="94d56-308">Vyšší verzi byl použit místo toho, který se liší od co balíček vytvořený proti.</span><span class="sxs-lookup"><span data-stu-id="94d56-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="94d56-309">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="94d56-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="94d56-310">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="94d56-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="94d56-311">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="94d56-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="94d56-312">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-312">**Common causes**</span></span> | <span data-ttu-id="94d56-313">Zdroje balíčku neobsahuje očekávaný dolní hranice verze.</span><span class="sxs-lookup"><span data-stu-id="94d56-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="94d56-314">Pokud balíček očekává ještě neuvolnil to může být balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="94d56-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="94d56-315">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-315">**Example message**</span></span> | <span data-ttu-id="94d56-316">NuGet.Packaging 4.0.0 závisí na NuGet.Versioning (> = 4.0.0), ale 4.0.0 nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="94d56-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="94d56-317">Přibližná nejlepší shody třídy 5.0.0 byl vyřešen.</span><span class="sxs-lookup"><span data-stu-id="94d56-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="94d56-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="94d56-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-319">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-319">**Issue**</span></span> | <span data-ttu-id="94d56-320">Závislosti projektu nedefinuje dolní mez.</span><span class="sxs-lookup"><span data-stu-id="94d56-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="94d56-321">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="94d56-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="94d56-322">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="94d56-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="94d56-323">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="94d56-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="94d56-324">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-324">**Common causes**</span></span> | <span data-ttu-id="94d56-325">Projektu *PackageReference* *verze* atributu se musí aktualizovat na zahrnují dolní mez.</span><span class="sxs-lookup"><span data-stu-id="94d56-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="94d56-326">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-326">**Example message**</span></span> | <span data-ttu-id="94d56-327">*Projektu závislosti NuGet.Versioning (< = 9.0.0) doe neobsahuje (včetně). dolní mez. Zahrňte dolní hranice verze závislosti zajistit obnovení konzistentní výsledky.*</span><span class="sxs-lookup"><span data-stu-id="94d56-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="94d56-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="94d56-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-329">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-329">**Issue**</span></span> | <span data-ttu-id="94d56-330">Balíček závislostí zadat omezení verze na vyšší verzi balíčku, než obnovení nakonec přeložit.</span><span class="sxs-lookup"><span data-stu-id="94d56-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="94d56-331">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-331">**Common causes**</span></span> | <span data-ttu-id="94d56-332">Nejbližší wins při rozpoznávání balíčky.</span><span class="sxs-lookup"><span data-stu-id="94d56-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="94d56-333">Balíček blíž k uživateli v grafu může přepsat vzdáleným balíčku.</span><span class="sxs-lookup"><span data-stu-id="94d56-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="94d56-334">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-334">**Example message**</span></span> | <span data-ttu-id="94d56-335">*Zjištěna přechod na starší verzi balíčku: NuGet.Versioning z 4.0.0 k 3.5.0. Odkazují na balíček přímo z projektu a vyberte jinou verzi.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="94d56-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="94d56-336">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="94d56-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="94d56-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="94d56-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="94d56-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-339">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-339">**Issue**</span></span> | <span data-ttu-id="94d56-340">Vyřešte balíčku je vyšší, než umožňuje omezení závislostí.</span><span class="sxs-lookup"><span data-stu-id="94d56-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="94d56-341">V některých případech to je úmyslné a lze potlačit upozornění.</span><span class="sxs-lookup"><span data-stu-id="94d56-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="94d56-342">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-342">**Common causes**</span></span> | <span data-ttu-id="94d56-343">Balíček odkazuje na projekt se přepíše omezení závislost z jiných balíčků.</span><span class="sxs-lookup"><span data-stu-id="94d56-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="94d56-344">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-344">**Example message**</span></span> | <span data-ttu-id="94d56-345">*Verze balíčku zjištěné mimo omezení závislost: x 1.0.0 vyžaduje y (= 1.0.0), ale verze y 2.0.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="94d56-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="94d56-346">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-346">Package fallback warnings</span></span>

[<span data-ttu-id="94d56-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="94d56-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="94d56-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="94d56-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-349">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-349">**Issue**</span></span> | <span data-ttu-id="94d56-350">*PackageTargetFallback/AssetTargetFallback* byl použit k výběru prostředky z balíčku.</span><span class="sxs-lookup"><span data-stu-id="94d56-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="94d56-351">Toto je upozornění, aby mohl uživatel vědět, že prostředky nemusí být 100 % kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="94d56-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="94d56-352">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-352">**Common causes**</span></span> | <span data-ttu-id="94d56-353">Balíček nepodporuje rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="94d56-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="94d56-354">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-354">**Example message**</span></span> | <span data-ttu-id="94d56-355">*Balíček NuGet.Versioning se obnovil pomocí 'přenositelností net45 + win8' místo toho cílový framework projektu 'netstandard1.5'. Tento balíček nemusí být plně kompatibilní s projektem.*</span><span class="sxs-lookup"><span data-stu-id="94d56-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="94d56-356">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-356">Feed warnings</span></span>

[<span data-ttu-id="94d56-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="94d56-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="94d56-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="94d56-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-359">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-359">**Issue**</span></span> | <span data-ttu-id="94d56-360">Při načítání informačního kanálu došlo k chybě při `IgnoreFailedSources` je nastaven na hodnotu true, převádí ji nezávažné upozornění.</span><span class="sxs-lookup"><span data-stu-id="94d56-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="94d56-361">To může obsahovat jakékoli zprávy a je obecná.</span><span class="sxs-lookup"><span data-stu-id="94d56-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="94d56-362">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-362">**Common causes**</span></span> | <span data-ttu-id="94d56-363">Zdroj je neplatný.</span><span class="sxs-lookup"><span data-stu-id="94d56-363">The source is invalid.</span></span> |
| <span data-ttu-id="94d56-364">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="94d56-364">**Example message**</span></span> | <span data-ttu-id="94d56-365">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="94d56-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="94d56-366">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="94d56-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="94d56-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="94d56-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="94d56-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="94d56-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-369">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-369">**Issue**</span></span> | <span data-ttu-id="94d56-370">Bez konkrétní vnitřní chyba z NuGet.</span><span class="sxs-lookup"><span data-stu-id="94d56-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="94d56-371">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-371">**Common causes**</span></span> | <span data-ttu-id="94d56-372">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="94d56-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="94d56-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="94d56-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="94d56-374">**Problém**</span><span class="sxs-lookup"><span data-stu-id="94d56-374">**Issue**</span></span> | <span data-ttu-id="94d56-375">Bez konkrétní interní upozornění z NuGet.</span><span class="sxs-lookup"><span data-stu-id="94d56-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="94d56-376">**Běžné příčiny**</span><span class="sxs-lookup"><span data-stu-id="94d56-376">**Common causes**</span></span> | <span data-ttu-id="94d56-377">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="94d56-377">Check the logs for more information</span></span> |
