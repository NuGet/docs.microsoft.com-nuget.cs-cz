---
title: "NuGet chyby a upozornění odkaz | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Úplný referenční varování a chyby vystavené NuGet během různé operace NuGet."
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
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 59bbe37d1a965e5167800148603869645fc5e0b2
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/12/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="770ce-104">Chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-104">Errors and warnings</span></span>

<span data-ttu-id="770ce-105">V NuGet 4.3.0+ chyby a upozornění jsou číslované, jak je popsáno v tomto tématu a poskytují podrobné informace můžete vyřešit problémy související se situací.</span><span class="sxs-lookup"><span data-stu-id="770ce-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="770ce-106">S chybami a upozorněními tady jsou k dispozici jenom s [na základě PackageReference](../consume-packages/package-references-in-project-files.md) projekty a NuGet 4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="770ce-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="770ce-107">NuGet rovněž ctí vlastnosti nástroje MSBuild potlačení upozornění nebo zvýšit jejich chyby.</span><span class="sxs-lookup"><span data-stu-id="770ce-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="770ce-108">Další informace najdete v tématu [postupy: potlačení upozornění kompilátoru](/visualstudio/ide/how-to-suppress-compiler-warnings) v dokumentaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="770ce-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="770ce-109">**Chyby**</span><span class="sxs-lookup"><span data-stu-id="770ce-109">**Errors**</span></span>

| <span data-ttu-id="770ce-110">Skupina</span><span class="sxs-lookup"><span data-stu-id="770ce-110">Group</span></span> | <span data-ttu-id="770ce-111">Chyba čísla</span><span class="sxs-lookup"><span data-stu-id="770ce-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="770ce-112">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="770ce-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="770ce-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="770ce-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="770ce-114">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="770ce-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="770ce-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (dříve NU1607), [NU1108](#nu1108) (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="770ce-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="770ce-116">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="770ce-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="770ce-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="770ce-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="770ce-118">**Upozornění**</span><span class="sxs-lookup"><span data-stu-id="770ce-118">**Warnings**</span></span>

| <span data-ttu-id="770ce-119">Skupina</span><span class="sxs-lookup"><span data-stu-id="770ce-119">Group</span></span> | <span data-ttu-id="770ce-120">Čísla upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="770ce-121">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="770ce-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="770ce-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="770ce-123">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="770ce-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="770ce-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="770ce-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="770ce-125">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="770ce-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="770ce-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="770ce-127">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="770ce-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="770ce-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="770ce-129">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="770ce-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="770ce-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="770ce-131">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="770ce-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="770ce-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="770ce-133">Podepsaný balíčků (vytvoření a ověření)</span><span class="sxs-lookup"><span data-stu-id="770ce-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="770ce-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="770ce-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="770ce-135">Neplatné vstupní chyby</span><span class="sxs-lookup"><span data-stu-id="770ce-135">Invalid input errors</span></span>

<span data-ttu-id="770ce-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="770ce-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="770ce-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="770ce-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-138">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-138">**Issue**</span></span> | <span data-ttu-id="770ce-139">Projekt neobsahuje jeden nebo více rozhraní.</span><span class="sxs-lookup"><span data-stu-id="770ce-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="770ce-140">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-140">**Example message**</span></span> | <span data-ttu-id="770ce-141">*Projekt projA neurčuje žádné cílové rozhraní v c:\tmp\projA.csproj*</span><span class="sxs-lookup"><span data-stu-id="770ce-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="770ce-142">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-142">**Solution**</span></span> | <span data-ttu-id="770ce-143">Přidat `TargetFramework` nebo `TargetFrameworks` vlastnost k souboru zadaného projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="770ce-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="770ce-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-145">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-145">**Issue**</span></span> | <span data-ttu-id="770ce-146">Neplatná kombinace vstupy společně s ZRUŠTE – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="770ce-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="770ce-147">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-147">**Example message**</span></span> | <span data-ttu-id="770ce-148">*'CLEAR' nelze použít ve spojení s další hodnoty*</span><span class="sxs-lookup"><span data-stu-id="770ce-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="770ce-149">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-149">**Solution**</span></span> | <span data-ttu-id="770ce-150">Použít ZRUŠTE sám o sobě a vynechat možnost všechny ostatní vstupy.</span><span class="sxs-lookup"><span data-stu-id="770ce-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="770ce-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="770ce-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-152">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-152">**Issue**</span></span> | <span data-ttu-id="770ce-153">`PackageTargetFallback` a `AssetTargetFallback` poskytovat různé chování pro výběr prostředky a nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="770ce-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="770ce-154">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-154">**Example message**</span></span> | <span data-ttu-id="770ce-155">*PackageTargetFallback a AssetTargetFallback nelze použít společně. Odeberte PackageTargetFallback(deprecated) odkazy z prostředí projektu.*</span><span class="sxs-lookup"><span data-stu-id="770ce-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="770ce-156">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-156">**Solution**</span></span> | <span data-ttu-id="770ce-157">Odeberte nepoužívané `PackageTargetFallback` element z projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="770ce-158">Chybějící chyby balíčku a projektu</span><span class="sxs-lookup"><span data-stu-id="770ce-158">Missing package and project errors</span></span>

<span data-ttu-id="770ce-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="770ce-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="770ce-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="770ce-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-161">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-161">**Issue**</span></span> | <span data-ttu-id="770ce-162">Skupina závislosti není možné přeložit.</span><span class="sxs-lookup"><span data-stu-id="770ce-162">A dependency group not be resolved.</span></span> <span data-ttu-id="770ce-163">Toto je obecná problém pro typy, které nejsou balíčky nebo projekty.</span><span class="sxs-lookup"><span data-stu-id="770ce-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="770ce-164">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-164">**Example message**</span></span> | <span data-ttu-id="770ce-165">*Nelze přeložit System.Missing pro net45*</span><span class="sxs-lookup"><span data-stu-id="770ce-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="770ce-166">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-166">**Solution**</span></span> | <span data-ttu-id="770ce-167">Otevřete soubor projektu a zkontrolujte seznam jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="770ce-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="770ce-168">Zkontrolujte, zda má každá závislost na zdroje balíčku, kterou používáte, a zda balíček podporuje cílový framework projektu na.</span><span class="sxs-lookup"><span data-stu-id="770ce-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="770ce-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="770ce-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-170">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-170">**Issue**</span></span> | <span data-ttu-id="770ce-171">Balíček nebyl nalezen na žádné zdroje.</span><span class="sxs-lookup"><span data-stu-id="770ce-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="770ce-172">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-172">**Example message**</span></span> | <span data-ttu-id="770ce-173">*Nepodařilo se najít balíček System.Missing. Neexistují žádné balíčky s tímto id v zdrojích: dotnet-core, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="770ce-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="770ce-174">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-174">**Solution**</span></span> | <span data-ttu-id="770ce-175">Zkontrolujte závislosti projektu v sadě Visual Studio a zajistit tak, že používáte správný balíček identifikátor a verzi číslo.</span><span class="sxs-lookup"><span data-stu-id="770ce-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="770ce-176">Také zkontrolujte, zda [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md) identifikuje zdroje balíčku vaší očekávají, že používat.</span><span class="sxs-lookup"><span data-stu-id="770ce-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="770ce-177">Pokud používáte balíčky, které mají [sémantické verze 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), ujistěte se, že používáte [V3 kanálu](https://api.nuget.org/v3/index.json) v [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="770ce-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="770ce-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="770ce-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-179">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-179">**Issue**</span></span> | <span data-ttu-id="770ce-180">Identifikátor balíčku se nenašel, ale nenašla se verze v rozsahu zadaná závislost na některý ze zdrojů.</span><span class="sxs-lookup"><span data-stu-id="770ce-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="770ce-181">Rozsah může být určena balíček a nikoli uživatele.</span><span class="sxs-lookup"><span data-stu-id="770ce-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="770ce-182">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-182">**Example message**</span></span> | <span data-ttu-id="770ce-183">*Nejde najít balíček NuGet.Versioning s verzí (> = 9.0.1)<br/> -30 nalezena verze v nuget.org [nejbližší verze: 4.0.0]<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -nalezen 9 verze v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032]<br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="770ce-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="770ce-184">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-184">**Solution**</span></span> | <span data-ttu-id="770ce-185">Upravte soubor projektu nebo `packages.config` opravit verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="770ce-185">Edit the project file or `packages.config` to correct the package version.</span></span> <span data-ttu-id="770ce-186">Také zkontrolujte, zda [NuGet konfigurace](../consume-packages/Configuring-NuGet-Behavior.md) identifikuje zdroje balíčku vaší očekávají, že používat.</span><span class="sxs-lookup"><span data-stu-id="770ce-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="770ce-187">Potřebujete verzi requeted změnit, pokud tento balíček je odkazován objektem projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="770ce-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="770ce-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="770ce-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-189">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-189">**Issue**</span></span> | <span data-ttu-id="770ce-190">Projektu zadána stabilní verze pro rozsah závislostí, ale v tomto rozsahu nebyly nalezeny žádné stabilní verze.</span><span class="sxs-lookup"><span data-stu-id="770ce-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="770ce-191">Nebyly nalezeny předběžných verzí, ale nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="770ce-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="770ce-192">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-192">**Example message**</span></span> | <span data-ttu-id="770ce-193">*Nelze najít stabilní balíček NuGet.Versioning s verzí (> = 3.0.0)<br/> -nalezen 10 verze v dotnet buildtools [nejbližší verze: 4.0.0-rc-2129]<br/> -verze 9 najít v NuGetVolatile [nejbližší verze: 3.0.0-beta-00032] <br/> -0 verze součástí dotnet základní<br/> -0 verze součástí roslyn dotnet.*</span><span class="sxs-lookup"><span data-stu-id="770ce-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="770ce-194">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-194">**Solution**</span></span> |  <span data-ttu-id="770ce-195">Upravit rozsah verze v souboru projektu nebo `packages.config` zahrnout předběžné verze.</span><span class="sxs-lookup"><span data-stu-id="770ce-195">Edit the version range in the project file or `packages.config` to include pre-release versions.</span></span> <span data-ttu-id="770ce-196">V tématu [Správa verzí balíčku](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="770ce-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="770ce-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="770ce-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-198">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-198">**Issue**</span></span> | <span data-ttu-id="770ce-199">ProjectReference odkazuje na soubor, který neexistuje.</span><span class="sxs-lookup"><span data-stu-id="770ce-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="770ce-200">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-200">**Example message**</span></span> | <span data-ttu-id="770ce-201">*Odkaz na projekt neexistuje 'c:\a.csproj'. Zkontrolujte, že je odkaz na projekt platný a zda existuje soubor projektu.*</span><span class="sxs-lookup"><span data-stu-id="770ce-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="770ce-202">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-202">**Solution**</span></span> | <span data-ttu-id="770ce-203">Upravte soubor projektu buď opravte cestu k odkazované projektu nebo odebrat odkaz na úplně, pokud je již nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="770ce-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="770ce-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="770ce-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-205">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-205">**Issue**</span></span> | <span data-ttu-id="770ce-206">Soubor projektu existuje, ale pro něj k dispozici žádné informace pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="770ce-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="770ce-207">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-207">**Example message**</span></span> | <span data-ttu-id="770ce-208">*Nelze číst informace o projektu pro 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="770ce-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="770ce-209">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-209">**Solution**</span></span> | <span data-ttu-id="770ce-210">V sadě Visual Studio chyba může znamenat, že projekt odpojen, v takovém případě projekt znovu načíst.</span><span class="sxs-lookup"><span data-stu-id="770ce-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="770ce-211">Z příkazového řádku, to může znamenat, že soubor je poškozený nebo že neobsahuje vlastní "po importy" target potřebná pro obnovení k načtení projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="770ce-212">Zkontrolujte, zda soubor projektu je platný a obsahuje cílový "po importy".</span><span class="sxs-lookup"><span data-stu-id="770ce-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="770ce-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="770ce-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-214">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-214">**Issue**</span></span> | <span data-ttu-id="770ce-215">Omezení závislostí nelze přeložit.</span><span class="sxs-lookup"><span data-stu-id="770ce-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="770ce-216">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-216">**Example message**</span></span> | <span data-ttu-id="770ce-217">*Nelze vyhovět konfliktním žádostem pro {id}: {cesta konflikt} Framework: {cíl grafu}*</span><span class="sxs-lookup"><span data-stu-id="770ce-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> 
| <span data-ttu-id="770ce-218">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-218">**Solution**</span></span> | <span data-ttu-id="770ce-219">Upravte soubor projektu nebo `packages.config` k určení širší rozsahy závislost, nikoli přesnou verzi.</span><span class="sxs-lookup"><span data-stu-id="770ce-219">Edit the project file or `packages.config` to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="770ce-220">NU1107 (dříve NU1607)</span><span class="sxs-lookup"><span data-stu-id="770ce-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-221">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-221">**Issue**</span></span> | <span data-ttu-id="770ce-222">Nelze vyřešit omezení závislost mezi balíčky.</span><span class="sxs-lookup"><span data-stu-id="770ce-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="770ce-223">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-223">**Example message**</span></span> | <span data-ttu-id="770ce-224">*Pro NuGet.Versioning zjištěn konflikt verzí. Odkazují na balíček přímo z projektu k vyřešení tohoto problému.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="770ce-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="770ce-225">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-225">**Solution**</span></span> | <span data-ttu-id="770ce-226">Balíčky s omezeními závislosti na přesné verze neumožňují dalších balíčků v případě potřeby zvýšit verze.</span><span class="sxs-lookup"><span data-stu-id="770ce-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="770ce-227">Přidat odkaz na projekt přímo (v souboru projektu nebo `packages.config`) s přesnou verzi vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="770ce-227">Add a reference to the project directly (in the project file or `packages.config`) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="770ce-228">NU1108 (dříve NU1606)</span><span class="sxs-lookup"><span data-stu-id="770ce-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-229">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-229">**Issue**</span></span> | <span data-ttu-id="770ce-230">Byla rozpoznána cyklická závislost.</span><span class="sxs-lookup"><span data-stu-id="770ce-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="770ce-231">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-231">**Example message**</span></span> | <span data-ttu-id="770ce-232">*Byl zjištěn cyklus: A -> B -> A*</span><span class="sxs-lookup"><span data-stu-id="770ce-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="770ce-233">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-233">**Solution**</span></span> | <span data-ttu-id="770ce-234">Balíček je vytvořené nesprávně; Obraťte se na vlastníka balíčku a opravte chyb.</span><span class="sxs-lookup"><span data-stu-id="770ce-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="770ce-235">Chyby kompatibility</span><span class="sxs-lookup"><span data-stu-id="770ce-235">Compatibility errors</span></span>

<span data-ttu-id="770ce-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="770ce-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="770ce-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="770ce-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-238">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-238">**Issue**</span></span> | <span data-ttu-id="770ce-239">Závislosti projektu neobsahuje rozhraní kompatibilní s aktuálním projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="770ce-240">Obvykle je cílový framework projektu na vyšší verzi než náročné projekt.</span><span class="sxs-lookup"><span data-stu-id="770ce-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="770ce-241">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-241">**Example message**</span></span> | <span data-ttu-id="770ce-242">*ServerWeb projektu není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Projekt podporuje ServerWeb:<br/> -netstandard1.6 (. Monikerů NETStandard, verze = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, verze = verze 1.0)*</span><span class="sxs-lookup"><span data-stu-id="770ce-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="770ce-243">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-243">**Solution**</span></span> | <span data-ttu-id="770ce-244">Změňte cílový framework projektu na stejné nebo nižší verzi než náročné projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="770ce-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="770ce-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-246">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-246">**Issue**</span></span> | <span data-ttu-id="770ce-247">Závislost balíček neobsahuje žádné prostředky, které jsou kompatibilní s projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="770ce-248">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-248">**Example message**</span></span> | <span data-ttu-id="770ce-249">*Balíček System.ComponentModel.EventBasedAsync 4.0.11 není kompatibilní s netstandard1.3 (. Monikerů NETStandard, verze = v1.3). Balíček podporuje System.ComponentModel.EventBasedAsync 4.0.11:<br/> -monoandroid10 (MonoAndroid, verze = verze 1.0)<br/> -monotouch10 (MonoTouch, verze = verze 1.0)<br/> -net45 (. NETFramework, verze = v4.5)<br/> -netcore50 (. NETCore, verze = v5.0)<br/> -netstandard1.0 (. Monikerů NETStandard, verze = verze 1.0)<br/> -přenositelností net45 + win8 + wp8 + wpa81 (. NETPortable, verze = v0.0, profil = Profile259)<br/> -win8 (Windows, verze = v8.0)<br/> -wp8 (WindowsPhone, verze = v8.0)<br/> -wpa81 (WindowsPhoneApp, verze = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="770ce-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="770ce-250">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-250">**Solution**</span></span> | <span data-ttu-id="770ce-251">Změňte cílový framework projektu na na takový, který podporuje balíčku.</span><span class="sxs-lookup"><span data-stu-id="770ce-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="770ce-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="770ce-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-253">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-253">**Issue**</span></span> | <span data-ttu-id="770ce-254">Balíček nepodporuje projektu `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="770ce-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="770ce-255">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-255">**Example message**</span></span> | <span data-ttu-id="770ce-256">*System.Example 1.0.0 poskytuje kompilaci referenční sestavení pro a.dll na net461, ale neexistuje žádné kompatibilní sestavení za běhu.*</span><span class="sxs-lookup"><span data-stu-id="770ce-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="770ce-257">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-257">**Solution**</span></span> | <span data-ttu-id="770ce-258">Změna `RuntimeIdentifier` hodnoty používané v projektu podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="770ce-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="770ce-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="770ce-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-260">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-260">**Issue**</span></span> | <span data-ttu-id="770ce-261">Balíček vyžaduje funkce nebo rozhraní není aktuálně podporovaná nainstalovaná verze balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="770ce-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="770ce-262">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-262">**Example message**</span></span> | <span data-ttu-id="770ce-263">*Balíček 'NuGet.Versioning' vyžaduje NuGet verze klienta, 5.0.0' nebo vyšší, ale aktuální verze NuGet je '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="770ce-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="770ce-264">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-264">**Solution**</span></span> | <span data-ttu-id="770ce-265">Nainstalujte novější verzi systému NuGet.</span><span class="sxs-lookup"><span data-stu-id="770ce-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="770ce-266">V tématu [NuGet instalaci klienta nástroje](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="770ce-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="770ce-267">Neplatné vstupní upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-267">Invalid input warnings</span></span>

<span data-ttu-id="770ce-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="770ce-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="770ce-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="770ce-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-270">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-270">**Issue**</span></span> | <span data-ttu-id="770ce-271">Obnovení projektu se pokouší pracovat na nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="770ce-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="770ce-272">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-272">**Example message**</span></span> | <span data-ttu-id="770ce-273">*Složka 'c:\projects\a' neobsahuje projekt k obnovení.*</span><span class="sxs-lookup"><span data-stu-id="770ce-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="770ce-274">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-274">**Solution**</span></span> | <span data-ttu-id="770ce-275">Spusťte obnovení nuget ve složce, která obsahuje projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="770ce-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="770ce-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-277">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-277">**Issue**</span></span> | <span data-ttu-id="770ce-278">`RuntimeSupports` obsahuje neplatný profil.</span><span class="sxs-lookup"><span data-stu-id="770ce-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="770ce-279">Obvykle se podporuje profil nebyl nalezen v `runtime.json` souboru z aktuální závislostí balíčků.</span><span class="sxs-lookup"><span data-stu-id="770ce-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="770ce-280">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-280">**Example message**</span></span> | <span data-ttu-id="770ce-281">*Neznámý kompatibility profilu: aaa*</span><span class="sxs-lookup"><span data-stu-id="770ce-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="770ce-282">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-282">**Solution**</span></span> | <span data-ttu-id="770ce-283">Zkontrolujte `RuntimeSupports` hodnotu ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="770ce-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="770ce-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="770ce-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-285">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-285">**Issue**</span></span> | <span data-ttu-id="770ce-286">Závislosti projektu neimportuje cíle obnovení NuGet.</span><span class="sxs-lookup"><span data-stu-id="770ce-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="770ce-287">To se podobá NU1105 ale zde bude přeskočena projektu a ignorovat místo způsobuje všechny obnovení nezdaří.</span><span class="sxs-lookup"><span data-stu-id="770ce-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="770ce-288">Komplexní řešení často existují jiné typy projektů, které nemusí podporovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="770ce-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="770ce-289">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-289">**Example message**</span></span> | <span data-ttu-id="770ce-290">*Přeskočení obnovení pro projekt 'c:\a.csproj'. Soubor projektu, může být neplatný nebo chybějící cíle, které jsou potřebné pro obnovení.*</span><span class="sxs-lookup"><span data-stu-id="770ce-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="770ce-291">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-291">**Solution**</span></span> | <span data-ttu-id="770ce-292">Toto může nastat projekty, které neimportujte běžné props nebo cíle, které automaticky importovat obnovení.</span><span class="sxs-lookup"><span data-stu-id="770ce-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="770ce-293">Pokud projekt není potřeba obnovit to můžete ignorovat.</span><span class="sxs-lookup"><span data-stu-id="770ce-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="770ce-294">Upravte, jinak hodnota ovlivněných projektu pro přidání cíle pro obnovení.</span><span class="sxs-lookup"><span data-stu-id="770ce-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="770ce-295">Upozornění verze neočekávané balíčku</span><span class="sxs-lookup"><span data-stu-id="770ce-295">Unexpected package version warnings</span></span>

<span data-ttu-id="770ce-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="770ce-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="770ce-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="770ce-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-298">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-298">**Issue**</span></span> | <span data-ttu-id="770ce-299">Přímé projektu závislost byla bumped na vyšší verzi než zadaný projekt.</span><span class="sxs-lookup"><span data-stu-id="770ce-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="770ce-300">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-300">**Example message**</span></span> | <span data-ttu-id="770ce-301">*Zadaná závislost byla NuGet.Versioning (> = 3.5.0), ale skončila s NuGet.Versioning 4.0.0.*</span><span class="sxs-lookup"><span data-stu-id="770ce-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="770ce-302">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-302">**Solution**</span></span> | <span data-ttu-id="770ce-303">Aktualizujte závislostí v projektu na příslušnou verzi.</span><span class="sxs-lookup"><span data-stu-id="770ce-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="770ce-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="770ce-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-305">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-305">**Issue**</span></span> | <span data-ttu-id="770ce-306">Závislost balíčku chybí dolní mez.</span><span class="sxs-lookup"><span data-stu-id="770ce-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="770ce-307">To neumožňuje obnovení najít *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="770ce-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="770ce-308">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="770ce-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="770ce-309">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="770ce-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="770ce-310">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-310">**Example message**</span></span> | <span data-ttu-id="770ce-311">*NuGet.Packaging 4.0.0 neposkytuje (včetně). dolní mez pro závislosti NuGet.Versioning (> 3.5.0). Přibližná nejlepší shody třídy 3.6.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="770ce-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="770ce-312">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-312">**Solution**</span></span> | <span data-ttu-id="770ce-313">Je to obvykle balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="770ce-313">This is usually a package authoring error.</span></span> <span data-ttu-id="770ce-314">Požádejte autora balíčku k vyřešení problému.</span><span class="sxs-lookup"><span data-stu-id="770ce-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="770ce-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="770ce-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-316">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-316">**Issue**</span></span> | <span data-ttu-id="770ce-317">Zadaná závislost balíčku na verzi, která nebyla nalezena.</span><span class="sxs-lookup"><span data-stu-id="770ce-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="770ce-318">Obvykle zdroje balíčku neobsahuje očekávaný dolní hranice verze.</span><span class="sxs-lookup"><span data-stu-id="770ce-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="770ce-319">Vyšší verzi byl použit místo toho, který se liší od co balíček vytvořený proti.</span><span class="sxs-lookup"><span data-stu-id="770ce-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="770ce-320">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="770ce-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="770ce-321">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="770ce-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="770ce-322">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="770ce-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="770ce-323">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-323">**Example message**</span></span> | <span data-ttu-id="770ce-324">NuGet.Packaging 4.0.0 závisí na NuGet.Versioning (> = 4.0.0), ale 4.0.0 nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="770ce-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="770ce-325">Přibližná nejlepší shody třídy 5.0.0 byl vyřešen.</span><span class="sxs-lookup"><span data-stu-id="770ce-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="770ce-326">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-326">**Solution**</span></span> | <span data-ttu-id="770ce-327">Pokud balíček očekává ještě neuvolnil to může být balíček pro tvorbu chyby.</span><span class="sxs-lookup"><span data-stu-id="770ce-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="770ce-328">Požádejte autora balíčku k vyřešení problému.</span><span class="sxs-lookup"><span data-stu-id="770ce-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="770ce-329">Pokud byla vydána balíčku, potom zkontrolujte, zda je k dispozici na zdroje balíčku, kterou používáte.</span><span class="sxs-lookup"><span data-stu-id="770ce-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="770ce-330">Pokud používáte privátní zdroje, musíte aktualizovat balíček na který informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="770ce-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="770ce-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="770ce-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-332">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-332">**Issue**</span></span> | <span data-ttu-id="770ce-333">Závislosti projektu nedefinuje dolní mez.</span><span class="sxs-lookup"><span data-stu-id="770ce-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="770ce-334">To znamená, že obnovení nebyl nalezen *nejlepší shodu*.</span><span class="sxs-lookup"><span data-stu-id="770ce-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="770ce-335">Každý obnovení bude float dolů pokusu o vyhledání na nižší verzi, která lze použít.</span><span class="sxs-lookup"><span data-stu-id="770ce-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="770ce-336">To znamená, přejde obnovení online a zkontrolujte všechny zdroje pokaždé, když místo použití balíčky, které již existují ve složce balíčku uživatele.</span><span class="sxs-lookup"><span data-stu-id="770ce-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="770ce-337">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-337">**Example message**</span></span> | <span data-ttu-id="770ce-338">*Projektu závislosti NuGet.Versioning (< = 9.0.0) doe neobsahuje (včetně). dolní mez. Zahrňte dolní hranice verze závislosti zajistit obnovení konzistentní výsledky.*</span><span class="sxs-lookup"><span data-stu-id="770ce-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="770ce-339">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-339">**Solution**</span></span> | <span data-ttu-id="770ce-340">Aktualizace projektu `PackageReference` `Version` atribut zahrnout dolní mez.</span><span class="sxs-lookup"><span data-stu-id="770ce-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="770ce-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="770ce-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-342">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-342">**Issue**</span></span> | <span data-ttu-id="770ce-343">Balíček závislostí zadat omezení verze na vyšší verzi balíčku, než obnovení nakonec přeložit.</span><span class="sxs-lookup"><span data-stu-id="770ce-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="770ce-344">To znamená z důvodu "nejbližší wins" pravidlo při rozpoznávání balíčky, blíž k uživateli balíčku v grafu může mít přepsat vzdáleným balíčku.</span><span class="sxs-lookup"><span data-stu-id="770ce-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="770ce-345">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-345">**Example message**</span></span> | <span data-ttu-id="770ce-346">*Zjištěna přechod na starší verzi balíčku: NuGet.Versioning z 4.0.0 k 3.5.0. Odkazují na balíček přímo z projektu a vyberte jinou verzi.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="770ce-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="770ce-347">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-347">**Solution**</span></span> | <span data-ttu-id="770ce-348">Přidejte přímý odkaz na projekt pro vyšší verzi balíčku, který chcete použít.</span><span class="sxs-lookup"><span data-stu-id="770ce-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="770ce-349">Řešitel konfliktů upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="770ce-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="770ce-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-351">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-351">**Issue**</span></span> | <span data-ttu-id="770ce-352">Vyřešený balíček je vyšší, než povoluje omezení závislostí.</span><span class="sxs-lookup"><span data-stu-id="770ce-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="770ce-353">To znamená, že balíček odkazuje na projekt přepsání omezení závislost z jiných balíčků.</span><span class="sxs-lookup"><span data-stu-id="770ce-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="770ce-354">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-354">**Example message**</span></span> | <span data-ttu-id="770ce-355">*Verze balíčku zjištěné mimo omezení závislost: x 1.0.0 vyžaduje y (= 1.0.0), ale verze y 2.0.0 byl vyřešen.*</span><span class="sxs-lookup"><span data-stu-id="770ce-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="770ce-356">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-356">**Solution**</span></span> | <span data-ttu-id="770ce-357">V některých případech to je úmyslné a lze potlačit upozornění.</span><span class="sxs-lookup"><span data-stu-id="770ce-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="770ce-358">Změňte, jinak hodnota projektu odkaz na balíček, který chcete rozšířit jeho omezení verze.</span><span class="sxs-lookup"><span data-stu-id="770ce-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="770ce-359">Balíček záložní upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="770ce-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="770ce-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-361">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-361">**Issue**</span></span> | <span data-ttu-id="770ce-362">`PackageTargetFallback` / `AssetTargetFallback` byl použit k výběru prostředky z balíčku.</span><span class="sxs-lookup"><span data-stu-id="770ce-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="770ce-363">Upozornění uživatelům vědět, že prostředky nemusí být 100 % kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="770ce-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="770ce-364">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-364">**Example message**</span></span> | <span data-ttu-id="770ce-365">*Balíček NuGet.Versioning se obnovil pomocí 'přenositelností net45 + win8' místo toho cílový framework projektu 'netstandard1.5'. Tento balíček nemusí být plně kompatibilní s projektem.*</span><span class="sxs-lookup"><span data-stu-id="770ce-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="770ce-366">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-366">**Solution**</span></span> | <span data-ttu-id="770ce-367">Změňte cílový framework projektu na na takový, který podporuje balíčku.</span><span class="sxs-lookup"><span data-stu-id="770ce-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="770ce-368">Informačního kanálu upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="770ce-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="770ce-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-370">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-370">**Issue**</span></span> | <span data-ttu-id="770ce-371">Při načítání informačního kanálu došlo k chybě při `IgnoreFailedSources` je nastaven na hodnotu true, převádí ji nezávažné upozornění.</span><span class="sxs-lookup"><span data-stu-id="770ce-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="770ce-372">To může obsahovat jakékoli zprávy a je obecná.</span><span class="sxs-lookup"><span data-stu-id="770ce-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="770ce-373">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-373">**Example message**</span></span> | <span data-ttu-id="770ce-374">není k dispozici</span><span class="sxs-lookup"><span data-stu-id="770ce-374">n/a</span></span> |
| <span data-ttu-id="770ce-375">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-375">**Solution**</span></span> | <span data-ttu-id="770ce-376">Upravte konfiguraci zadat platné zdroje.</span><span class="sxs-lookup"><span data-stu-id="770ce-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="770ce-377">NuGet vnitřní chyby a upozornění</span><span class="sxs-lookup"><span data-stu-id="770ce-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="770ce-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="770ce-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="770ce-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="770ce-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-380">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-380">**Issue**</span></span> | <span data-ttu-id="770ce-381">Bez konkrétní vnitřní chyba z NuGet.</span><span class="sxs-lookup"><span data-stu-id="770ce-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="770ce-382">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-382">**Solution**</span></span> | <span data-ttu-id="770ce-383">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="770ce-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="770ce-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="770ce-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-385">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-385">**Issue**</span></span> | <span data-ttu-id="770ce-386">Bez konkrétní interní upozornění z NuGet.</span><span class="sxs-lookup"><span data-stu-id="770ce-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="770ce-387">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-387">**Solution**</span></span> | <span data-ttu-id="770ce-388">Zkontrolujte protokoly pro další informace</span><span class="sxs-lookup"><span data-stu-id="770ce-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="770ce-389">Podepsaný balíčků (vytvoření a ověření)</span><span class="sxs-lookup"><span data-stu-id="770ce-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="770ce-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="770ce-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="770ce-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="770ce-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="770ce-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="770ce-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-393">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-393">**Issue**</span></span> | <span data-ttu-id="770ce-394">Není dost konkrétní chyby související s podepisování balíčku a podepsaný balíček ověření.</span><span class="sxs-lookup"><span data-stu-id="770ce-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="770ce-395">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-395">**Solution**</span></span> | <span data-ttu-id="770ce-396">Zkontrolujte protokoly pro další informace.</span><span class="sxs-lookup"><span data-stu-id="770ce-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="770ce-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="770ce-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-398">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-398">**Issue**</span></span> | <span data-ttu-id="770ce-399">Neplatné argumenty buď [přihlásit příkaz](../tools/cli-ref-sign.md) nebo [ověřte příkaz](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="770ce-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="770ce-400">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-400">**Solution**</span></span> | <span data-ttu-id="770ce-401">Zkontrolujte a opravte zadaných argumentů.</span><span class="sxs-lookup"><span data-stu-id="770ce-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="770ce-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="770ce-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-403">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-403">**Issue**</span></span> | <span data-ttu-id="770ce-404">`-Timestamper` s nebyla zadána možnost [příkaz přihlašovací nuget](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="770ce-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="770ce-405">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-405">**Example message**</span></span> | <span data-ttu-id="770ce-406">*'-Timestamper' nebyla zadána možnost. Podepsaného balíčku nebudou označen časovým razítkem.*</span><span class="sxs-lookup"><span data-stu-id="770ce-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="770ce-407">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-407">**Solution**</span></span> | <span data-ttu-id="770ce-408">Zadejte `-Timestamper` možnost s `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="770ce-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="770ce-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="770ce-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-410">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-410">**Issue**</span></span> | <span data-ttu-id="770ce-411">Balíček nepodepsané zadaná k [nuget ověřte příkaz](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="770ce-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="770ce-412">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-412">**Solution**</span></span> | <span data-ttu-id="770ce-413">Spustit `nuget verify` s podepsaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="770ce-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="770ce-414">V tématu [přihlásit balíček](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="770ce-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="770ce-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="770ce-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-416">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-416">**Issue**</span></span> | <span data-ttu-id="770ce-417">Zkontrolujte integritu balíčku se nezdařila, což znamená, že byla od Podepisovaný manipulováno podepsaného balíčku.</span><span class="sxs-lookup"><span data-stu-id="770ce-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="770ce-418">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-418">**Solution**</span></span> | <span data-ttu-id="770ce-419">Zkontrolujte počítač pomocí antivirového softwaru.</span><span class="sxs-lookup"><span data-stu-id="770ce-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="770ce-420">Daný balíček odebrat z počítače, znovu ji nainstalujte a operaci opakujte.</span><span class="sxs-lookup"><span data-stu-id="770ce-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="770ce-421">Pokud potíže potrvají, obraťte se na vlastníka zdrojových souborů balíčku a balíček vlastníka.</span><span class="sxs-lookup"><span data-stu-id="770ce-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="770ce-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="770ce-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-423">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-423">**Issue**</span></span> | <span data-ttu-id="770ce-424">Vytváření řetězu certifikátů se nezdařilo pro primární podpis.</span><span class="sxs-lookup"><span data-stu-id="770ce-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="770ce-425">Primární podpisový certifikát není důvěryhodný, odvolán, nebo není k dispozici informace o odvolání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="770ce-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="770ce-426">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-426">**Example message**</span></span> | <span data-ttu-id="770ce-427">*Upozornění: NU3018: Funkce zrušení se nepodařilo ověření odvolání certifikátu.*</span><span class="sxs-lookup"><span data-stu-id="770ce-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="770ce-428">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-428">**Solution**</span></span> | <span data-ttu-id="770ce-429">Používejte důvěryhodné a platný certifikát.</span><span class="sxs-lookup"><span data-stu-id="770ce-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="770ce-430">Zkontrolujte připojení k Internetu.</span><span class="sxs-lookup"><span data-stu-id="770ce-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="770ce-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="770ce-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="770ce-432">**Problém**</span><span class="sxs-lookup"><span data-stu-id="770ce-432">**Issue**</span></span> | <span data-ttu-id="770ce-433">Vytváření řetězu certifikátů se nezdařilo pro podpis časové razítko.</span><span class="sxs-lookup"><span data-stu-id="770ce-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="770ce-434">Časové razítko podpisový certifikát není důvěryhodný, odvolán, nebo není k dispozici informace o odvolání certifikátu.</span><span class="sxs-lookup"><span data-stu-id="770ce-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="770ce-435">**Příklad zprávy**</span><span class="sxs-lookup"><span data-stu-id="770ce-435">**Example message**</span></span> | <span data-ttu-id="770ce-436">*Upozornění: NU3028: Funkce zrušení se nepodařilo ověření odvolání certifikátu.*</span><span class="sxs-lookup"><span data-stu-id="770ce-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="770ce-437">**Řešení**</span><span class="sxs-lookup"><span data-stu-id="770ce-437">**Solution**</span></span> | <span data-ttu-id="770ce-438">Používejte důvěryhodné a platný certifikát.</span><span class="sxs-lookup"><span data-stu-id="770ce-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="770ce-439">Zkontrolujte připojení k Internetu.</span><span class="sxs-lookup"><span data-stu-id="770ce-439">Check internet connectivity.</span></span> |
