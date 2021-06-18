---
title: Zpráva k vydání verze NuGet 5.10
description: Poznámky k verzi pro NuGet 5.10, včetně nových funkcí, oprav chyb a souborů DCR
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356535"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="e55ca-103">Zpráva k vydání verze NuGet 5.10</span><span class="sxs-lookup"><span data-stu-id="e55ca-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="e55ca-104">Distribuční vozidla NuGet:</span><span class="sxs-lookup"><span data-stu-id="e55ca-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e55ca-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="e55ca-105">NuGet version</span></span> | <span data-ttu-id="e55ca-106">K dispozici ve Visual Studio verzi</span><span class="sxs-lookup"><span data-stu-id="e55ca-106">Available in Visual Studio version</span></span> | <span data-ttu-id="e55ca-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e55ca-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="e55ca-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="e55ca-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e55ca-109">Visual Studio 2019 verze 16.10</span><span class="sxs-lookup"><span data-stu-id="e55ca-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e55ca-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e55ca-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="e55ca-111"><sup>1</sup> Nainstalované s Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="e55ca-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="e55ca-112">Visual Studio verze 16.10, MSBuild 16.10 a .NET 5.0.300+ vyžaduje NuGet.exe 5.10 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="e55ca-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="e55ca-113">Shrnutí: Co je nového ve windows 5.10</span><span class="sxs-lookup"><span data-stu-id="e55ca-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="e55ca-114">Podepisování: Implementujte příkaz dotnet trusted-signers [– #8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="e55ca-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="e55ca-115">Zakázat výchozí ověřování v Linuxu, ale ve výchozím nastavení je povolené ve Windows – [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="e55ca-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="e55ca-116">Přidání proměnné ENV pro ověření podepisování balíčků v .NET 5+ Linux/MAC – [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="e55ca-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="e55ca-117">Vylepšení výkonu instalace nových balíčků pro velká řešení – [#10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="e55ca-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="e55ca-118">Přidejte typ projektu `nfproj` do seznamu supportedProjectExtensions pro rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="e55ca-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="e55ca-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="e55ca-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e55ca-120">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="e55ca-120">Issues fixed in this release</span></span>

* <span data-ttu-id="e55ca-121">Potlačení <requireLicenseAcceptance> elementu při balení projektu – [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="e55ca-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="e55ca-122">Upozornění [CPVM] verze Preview by se měla zobrazit v rozhraní příkazového řádku dotnet – [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="e55ca-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="e55ca-123">Aktualizujte barevné tokeny pozadí a popředí pmui na CommonDocumentColors – [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="e55ca-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="e55ca-124">[Bug Bash] Při rychlém přepínání mezi kartami v uživatelském rozhraní PM se Seznam chyb chyba Operace byla zrušena uživatelem – [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="e55ca-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="e55ca-125">Uživatelské rozhraní PM: Zvýšení výkonu instalace balíčku na úrovni řešení – [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="e55ca-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="e55ca-126">GetService nahraďte GetServiceAsync všude v NuGet.Clients – [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="e55ca-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="e55ca-127">NuGet.exe s výkonem balíčku s `..` relativní cestou – [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="e55ca-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="e55ca-128">Výkon "balíčku NuGet" se snižuje s rostoucími úrovněmi ve zdrojových cestách – [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="e55ca-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="e55ca-129">Při balení nuspec s duplicitními soubory se NuGet ne chybně nelišuje.</span><span class="sxs-lookup"><span data-stu-id="e55ca-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="e55ca-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="e55ca-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="e55ca-131">Balíček NuGet "Zadaný DateTimeOffset nelze převést na časové razítko souboru Zip" – [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="e55ca-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="e55ca-132">Časová razítka souboru zabalených balíčků se posunou o časové pásmo – [#7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="e55ca-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="e55ca-133">Nu1004 by měl obsahovat další informace s možností akce – [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="e55ca-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="e55ca-134">[Bug Bash] [Test Failure] Prázdný nebo poškozený soubor zámku by se neměl aktualizovat při spuštění dotnet restore --use-lock-file --locked-mode – [#8640](https://github.com/NuGet/Home/issues/8640)</span><span class="sxs-lookup"><span data-stu-id="e55ca-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="e55ca-135">NuGetVersionRange umožňuje parsovat logicky nesprávné rozsahy – [#9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="e55ca-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="e55ca-136">Uživatelské rozhraní PM nemůže zobrazit rozlišitelnou barvu pozadí mezi vybranými a najetými zdroji balíčků – [#9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="e55ca-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="e55ca-137">Zaškrtávací políčko pro výběr projektů, na které se má nainstalovat, nečte čtečka obrazovky – [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="e55ca-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="e55ca-138">Výchozí výběr verze podokna podrobností Rozevírací seznam by měl být Nainstalováno/NejnovějšíStable na kartách Nainstalované/Aktualizace [– #9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="e55ca-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="e55ca-139">Odebrání účtu alternativního řešení pro některé verze .NET 5 SDK hlásí TargetPlatformMoniker ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="e55ca-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="e55ca-140">dotnet nuget verify is too quiet – [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="e55ca-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="e55ca-141">Rozsah verzí nemůže parsovat jednociferné rozsahy – [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="e55ca-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="e55ca-142">Správce řešení VS vyvolá během ladění výjimku null – [#10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="e55ca-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="e55ca-143">Přesunutí zpráv o výjimce rozhraní příkazového řádku do souborů prostředků řetězců [– #10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="e55ca-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="e55ca-144">Odebrání neschopového kódu (TabItemButtonAutomationPeer) [– #10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="e55ca-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="e55ca-145">Místní nabídka Aktualizovat by se měla posunout k první vybrané [položce](https://github.com/NuGet/Home/issues/10498) – #10498</span><span class="sxs-lookup"><span data-stu-id="e55ca-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="e55ca-146">Podrobnosti PMUI řešení se překrývají vodorovným pruhem – [#10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="e55ca-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="e55ca-147">Podepisování: Podrobnosti primárního podpisu se nezobrazují, když vypršela platnost certifikátu a časové razítko je nedůvěryhodné – [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="e55ca-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="e55ca-148">Pokud žádné povolené zdroje neumožňují zobrazení uživatelského rozhraní PM, [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="e55ca-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="e55ca-149">Metadata balíčků (podrobnosti, vyněcování) se někdy nečtou z nuget.org v CodeSpaces – [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="e55ca-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="e55ca-150">Inicializace PMUI selže s výjimkou během ladicí relace – [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="e55ca-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="e55ca-151">Obnovení nuget vede k selhání kontroly integrity balíčků v systému Big Endian [– #10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="e55ca-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="e55ca-152">Místo PackagingException je vyvolána výjimka FormatException [– #10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="e55ca-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="e55ca-153">CPVM – Problémy se souběžnosti v algoritmu cházek v grafu – [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="e55ca-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="e55ca-154">Přidání telemetrie verze PowerShellu PMC – [#10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="e55ca-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="e55ca-155">Zvýšení výkonu řazení NuGetVersion – [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="e55ca-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="e55ca-156">Přidání důvěryhodných podpisů má nekonzistentní argumenty – [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="e55ca-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="e55ca-157">Vs2019 v16.9.0: Přepnutím karet ve Správce balíčků NuGetu z "Aktualizace" na "Nainstalováno" se rámec ne aktualizován.</span><span class="sxs-lookup"><span data-stu-id="e55ca-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="e55ca-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="e55ca-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="e55ca-159">Odeberte "v" z čísla verze v PMUI – [#10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="e55ca-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="e55ca-160">INuGetProjectService.GetInstalledPackagesAsync vyvolá výjimku před přijetím nominace systému projektu CPS – [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="e55ca-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="e55ca-161">Vložené ikony způsobují odepření přístupu ze zdroje Microsoft Visual Studio offline balíčky na kartě Procházet [– #10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="e55ca-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="e55ca-162">INuGetProjectService.GetInstalledPackagesAsync vyvolá výjimku, když není nastavená vlastnost MSBuildProjectExtensionsPath – [#10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="e55ca-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="e55ca-163">"dotnet nuget remove source nuget.org" nefunguje poprvé – [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="e55ca-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="e55ca-164">Nuget blokuje vlákno fondu vláken v asynchronní metodě, která synchronně volá vlákno uživatelského rozhraní – [#10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="e55ca-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="e55ca-165">Nástroje – > možnosti –> řetězec Správce balíčků NuGet je zkrácený – [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="e55ca-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="e55ca-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` je neschůdný kód a snížení výkonu [– #10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="e55ca-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="e55ca-167">Použití vložené ikony v balíčcích sady NuGet SDK [– #10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="e55ca-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="e55ca-168">Aktualizace seznamu licencí SPDX – [#10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="e55ca-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="e55ca-169">**[Seznam všech problémů opravených v této verzi – 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="e55ca-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="e55ca-170">**[Seznam potvrzení v této verzi – 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="e55ca-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="e55ca-171">Komunitní příspěvky</span><span class="sxs-lookup"><span data-stu-id="e55ca-171">Community contributions</span></span>

<span data-ttu-id="e55ca-172">Děkujeme všem přispěvatelům, kteří této verzi NuGet pomohli udělat vynikající!</span><span class="sxs-lookup"><span data-stu-id="e55ca-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="e55ca-173">Kdo</span><span class="sxs-lookup"><span data-stu-id="e55ca-173">Who</span></span>|<span data-ttu-id="e55ca-174">PRS</span><span class="sxs-lookup"><span data-stu-id="e55ca-174">PRs</span></span>|<span data-ttu-id="e55ca-175">Problémy</span><span class="sxs-lookup"><span data-stu-id="e55ca-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="e55ca-176">přidchytá–z</span><span class="sxs-lookup"><span data-stu-id="e55ca-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="e55ca-177">3991</span><span class="sxs-lookup"><span data-stu-id="e55ca-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="e55ca-178">Rozsah verzí nemůže parsovat jednociferné rozsahy – [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="e55ca-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="e55ca-179">omajid (id souboru)</span><span class="sxs-lookup"><span data-stu-id="e55ca-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="e55ca-180">3860</span><span class="sxs-lookup"><span data-stu-id="e55ca-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="e55ca-181">Nefunkční build.sh NuGet.Client [– #10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="e55ca-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="e55ca-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="e55ca-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="e55ca-183">3623</span><span class="sxs-lookup"><span data-stu-id="e55ca-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="e55ca-184">Nefunkční build.sh NuGet.Client [– #10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="e55ca-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="e55ca-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="e55ca-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="e55ca-186">3953</span><span class="sxs-lookup"><span data-stu-id="e55ca-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="e55ca-187">Výkon "balíčku NuGet" se snižuje s rostoucími úrovněmi ve zdrojových cestách – [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="e55ca-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="e55ca-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="e55ca-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="e55ca-189">3953</span><span class="sxs-lookup"><span data-stu-id="e55ca-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="e55ca-190">NuGet.exe s výkonem balíčku .</span><span class="sxs-lookup"><span data-stu-id="e55ca-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="e55ca-191">relative path – [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="e55ca-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="e55ca-192">přichytávka-smyšlová</span><span class="sxs-lookup"><span data-stu-id="e55ca-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="e55ca-193">3940</span><span class="sxs-lookup"><span data-stu-id="e55ca-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="e55ca-194">CPVM – Problémy se souběžnosti v algoritmu cházek v grafu – [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="e55ca-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="e55ca-195">přisudky</span><span class="sxs-lookup"><span data-stu-id="e55ca-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="e55ca-196">3943</span><span class="sxs-lookup"><span data-stu-id="e55ca-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="e55ca-197">Přidejte typ projektu nfproj do seznamu supportedProjectExtensions pro rozhraní příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="e55ca-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="e55ca-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="e55ca-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="e55ca-199">Váš názor – vítejte</span><span class="sxs-lookup"><span data-stu-id="e55ca-199">Feedback welcome</span></span>

<span data-ttu-id="e55ca-200">Vaše názory jsou pro nás důležité.</span><span class="sxs-lookup"><span data-stu-id="e55ca-200">Your feedback is important to us.</span></span>  <span data-ttu-id="e55ca-201">Pokud se v této verzi vyskytnou nějaké problémy, podívejte se na naše [problémy GitHubu](https://github.com/NuGet/Home/issues) a [komunitu vývojářů pro Visual Studio](https://developercommunity.visualstudio.com/) , kde najdete stávající problémy.</span><span class="sxs-lookup"><span data-stu-id="e55ca-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="e55ca-202">Pro nové problémy v rámci NuGet ohlaste [problém GitHubu](https://github.com/NuGet/Home/issues/new).</span><span class="sxs-lookup"><span data-stu-id="e55ca-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="e55ca-203">Pro obecné problémy s prostředím NuGet nám dejte informace v části **Help > nahlásit problém** pomocí možnosti [nahlásit problém](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) , která se nachází ve vašem oblíbeném prostředí IDE.</span><span class="sxs-lookup"><span data-stu-id="e55ca-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
