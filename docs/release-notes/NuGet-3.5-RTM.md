---
title: Poznámky k verzi NuGet 3,5 RTM
description: Poznámky k verzi pro NuGet 3,5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776347"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="a3569-103">Zpráva k vydání verze NuGet 3,5</span><span class="sxs-lookup"><span data-stu-id="a3569-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="a3569-104">Poznámky k verzi [pro NuGet 3,5 – RC](../release-notes/nuget-3.5-RC.md)  |  [Poznámky k verzi NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="a3569-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a3569-105">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="a3569-105">Bug Fixes</span></span>

* <span data-ttu-id="a3569-106">Pack nepoužívá MSBuild 14,1 na mono- [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="a3569-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="a3569-107">Karta aktualizace nevybere nejnovější dostupnou verzi, kterou chcete aktualizovat místo toho vyberte možnost aktuální nainstalovaná verze – [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="a3569-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="a3569-108">Opravte chybu po ověření privátního informačního kanálu v2 MyGet a kliknutím na Zobrazit x další výsledky – [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="a3569-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="a3569-109">Zprávy protokolu se zdají být v opačném pořadí pro uživatelské rozhraní [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="a3569-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="a3569-110">v 3.4.4 – obnovení NuGet vyvolá "formát dané cesty se nepodporuje"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="a3569-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="a3569-111">NuGet cmdLine 3,6 beta nedodržuje-Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="a3569-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="a3569-112">IKVM zpomalit instalaci na velký projekt – [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="a3569-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="a3569-113">Aktualizace nuget.exe – sám sebe zachovává aktualizaci sebe sama [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="a3569-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="a3569-114">3,5 instalace/obnovení ze sdílené složky UNC má na výkon regresi z 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="a3569-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="a3569-115">Chyba při instalaci MOQ z uživatelského rozhraní pro správu balíčků pro projekt net451 – [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="a3569-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="a3569-116">Karta instalovat na úrovni řešení nezobrazuje verzi balíčku [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="a3569-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="a3569-117">xproj `project.json` aktualizace z nainstalované karty ztratí stav – [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="a3569-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="a3569-118">Sada NuGet Pack na `.csproj` ignorování prázdných souborů v `.nuspec` souboru [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="a3569-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="a3569-119">Projekty webů hostované ve službě IIS by neměly způsobit selhání obnovení- [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="a3569-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="a3569-120">Pověření nebyla načtena z Nuget.Config, když hodnota V3 Endpoint přesměrovává na v2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="a3569-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="a3569-121">Sada NuGet Pack nemůže přeložit sestavení při načítání metadat přenositelného sestavení- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="a3569-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="a3569-122">NuGet nejde najít `msbuild.exe` na mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="a3569-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="a3569-123">Sada nuget.exe Pack nepovoluje značku předběžného vydání, která začíná čísly- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="a3569-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="a3569-124">instalace balíčku NuGet se na VS2015E nezdařila – [#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="a3569-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="a3569-125">Hodnota allowedversions filtr nepracuje na úrovni řešení – [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="a3569-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="a3569-126">Operace obnovení se náhodně nezdařila, protože položka se stejným klíčem již byla přidána.</span><span class="sxs-lookup"><span data-stu-id="a3569-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="a3569-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="a3569-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="a3569-128">Nejde nainstalovat NuGet. Common v `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635) .</span><span class="sxs-lookup"><span data-stu-id="a3569-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="a3569-129">Když použijete uživatelské rozhraní k vyhledání zdroje v2, FindPackagesById se pro každé ID – pojmenuje dvakrát. – [#2517](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="a3569-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="a3569-130">Balíčky nemůžou záviset na projektech – [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="a3569-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="a3569-131">nuget.exe Pack – vyloučení je dokumentováno, ale není podporováno – [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="a3569-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="a3569-132">Problémy s chybovými zprávami, pokud je oddíl ' contentFiles ' `.nuspec` neplatný – [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="a3569-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="a3569-133">Push vždycky odesílá celý balíček dvakrát pomocí ověřených zdrojů balíčků – [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="a3569-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="a3569-134">Nebyly zadány žádné informace při volání nuget.exe Update \*. csproj, ale projekt nemá `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="a3569-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="a3569-135">`packages.config` obnovení se neopakuje u stavových kódů 5xx ze zdrojů v2 – [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="a3569-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="a3569-136">Dvojitá tečka v souboru src v `.nuspec` nefunguje – [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="a3569-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="a3569-137">CoreCLR Restore musí ignorovat informační kanály s [#2942](https://github.com/NuGet/Home/issues/2942) šifrování.</span><span class="sxs-lookup"><span data-stu-id="a3569-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="a3569-138">Zpracování 403 nuget.exe push – nesprávné zobrazení výzvy k zadání přihlašovacích údajů – [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="a3569-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="a3569-139">Aktualizace NuGet prostřednictvím Správce balíčků odebere z `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888) vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="a3569-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="a3569-140">NuGet. PackageManagement. VisualStudio se pokusí načíst "NuGet. TeamFoundationServer14", ale název této knihovny DLL se změnil na "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="a3569-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="a3569-141">Uživatelské rozhraní Správce balíčků nezobrazuje nově aktualizovanou verzi [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="a3569-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="a3569-142">Update-Package pokus o použití PackageID, verze místo balíčku. Version- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="a3569-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="a3569-143">v případě, že projekt nepoužívá NuGet ( `packages.config` nebo `project.json` ) – [#2766](https://github.com/NuGet/Home/issues/2766) , by se měla chyba NuGet Restore csproj.</span><span class="sxs-lookup"><span data-stu-id="a3569-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="a3569-144">Chyba TFS "[soubor] není ve vašem pracovním prostoru nalezena, nebo nemáte oprávnění k přístupu" během upgradu nebo odinstalace, když je řešení/projekt svázán se správou zdrojových kódů TFS- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="a3569-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="a3569-145">balíček aktualizace nezíská závislosti pro balíčky, které nejsou cílové, [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="a3569-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="a3569-146">Neexistuje žádný způsob, jak nastavit úroveň podrobností protokolů pro akce uživatelského rozhraní Správce balíčků NuGet – [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="a3569-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="a3569-147">Konfigurace NuGet je neplatná – VS 2015 VSIX (v 3.4.3) – [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="a3569-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="a3569-148">DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nefunguje [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="a3569-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="a3569-149">vydaná verze NuGet 3.4.3-získání hodnoty nemůže být null při sestavení balíčku- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="a3569-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="a3569-150">příkaz Restore nepoužívá uložená pověření z Nuget.Config pro informační kanály VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="a3569-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="a3569-151">[dotnet restore]--ConfigFile je relativní k projektu dir místo příkazového řádku cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="a3569-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="a3569-152">Nadměrný příděl v comparsion kódu verze – [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="a3569-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="a3569-153">Víc instancí nuget.exe, který se pokouší nainstalovat stejný balíček paralelně, způsobí [#2628](https://github.com/NuGet/Home/issues/2628) typu Double-Write.</span><span class="sxs-lookup"><span data-stu-id="a3569-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="a3569-154">Informace o závislostech nejsou ukládány do mezipaměti pro operace více projektů – [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="a3569-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="a3569-155">Nainstalovat a aktualizovat balíčky pro stahování bez kontroly složky balíčků jako první [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="a3569-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="a3569-156">Pokud je seznam zdrojů balíčků prázdný, nejde přidat zdroj balíčku prostřednictvím uživatelského rozhraní (NuGet 3.4. x) – [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="a3569-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="a3569-157">Zavádějící Chyba při pokusu o instalaci balíčku, který závisí na době návrhu Facade- [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="a3569-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="a3569-158">Instalace balíčku z konzoly PackageManager s nastavením "vše" se snaží pouze první zdroj – [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="a3569-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="a3569-159">Nejnovější beta verze rozzipovává ModernHttpClient – [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="a3569-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="a3569-160">VS2015 chyby při spuštění s využitím samočinně připraveného 3.4.1U NuGet- [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="a3569-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="a3569-161">Příkaz Update může být trochu podrobnější, pokud si ho vyžádáme...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="a3569-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="a3569-162">Místně sestavený VSIX by měl mít stejné knihovny DLL a soubory jako sestavení CI.</span><span class="sxs-lookup"><span data-stu-id="a3569-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="a3569-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="a3569-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="a3569-164">Oprava upozornění na downgrade NuGet v sestavení – [#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="a3569-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="a3569-165">Neúspěšné ověření zdroje balíčku (3 časy) je blokované [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="a3569-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="a3569-166">Obsah balíčku se neobnovil správně při instalaci balíčku z kanálu NuGet v 3.3 + s argumentem-bez mezipaměti, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="a3569-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="a3569-167">Instalace NuGet se všemi zdroji balíčků, ale chybějící balíček v 1 zdroji, [#2322](https://github.com/NuGet/Home/issues/2322) se nezdařil.</span><span class="sxs-lookup"><span data-stu-id="a3569-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="a3569-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + \* lt; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="a3569-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="a3569-169">Nainstalovat bloky v případě neúspěšného ověření u jednoho zdroje – [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="a3569-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="a3569-170">`.nuspec` Rozsah verze by měl přepsat-IncludeReferencedProjects verze- [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="a3569-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="a3569-171">Update-Package velmi pomalu – probíhá pokus o shromáždění informací o závislostech "- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="a3569-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="a3569-172">Balíček NuGet s degradací downgrade se zabalí, když dávka aktualizuje své závislosti – [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="a3569-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="a3569-173">nuget.exe Update zruší silný název sestavení a soukromý atribut.</span><span class="sxs-lookup"><span data-stu-id="a3569-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="a3569-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="a3569-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="a3569-175">Relativní cesta k souboru pro "DefaultPushSource" – [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="a3569-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="a3569-176">Vylepšit zprávy o chybách překladače – [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="a3569-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="a3569-177">příkaz Update-Package v v3 se nezdařil s balíčky, které nejsou v zadaném zdrojovém [#1013](https://github.com/NuGet/Home/issues/1013) .</span><span class="sxs-lookup"><span data-stu-id="a3569-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="a3569-178">Používání relativních cest pro zdroje balíčků je problematické při použití [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="a3569-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="a3569-179">Chybějící závislost v NUPKG-File vygenerované z projektu, pokud již existuje nepřímá závislost s požadavkem nižší verze – [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="a3569-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="a3569-180">Odstranění projektu zavře odpovídající okno uživatelského rozhraní, ale Přejmenování projektu nejmenuje okno uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a3569-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="a3569-181">Všimněte si, že PMC naslouchat Přejmenování projektu a události odebrání projektu – [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="a3569-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="a3569-182">[Webové zatížení Willow] Vytváření zablokování Razor V3 WSP – [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="a3569-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="a3569-183">Instalace nebo obnovení určitého balíčku se nezdařila s názvem "balíček obsahuje více souborů nuspec".</span><span class="sxs-lookup"><span data-stu-id="a3569-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="a3569-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="a3569-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="a3569-185">Malá ID & `packages.config` scénářích – [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="a3569-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="a3569-186">[3,5 – beta2] Při obnovení balíčku se nepovedlo obnovit starší balíčky – [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="a3569-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="a3569-187">sada NuGet Pack nuceně přidává soubory. TT do složky obsahu bez ohledu na to, co [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="a3569-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="a3569-188">aktualizace – balíček webové aplikace ASP.NET generuje upozornění související se souborem: Source- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="a3569-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="a3569-189">Chyba sady NuGet Pack csproj (with `project.json` ), pokud v souboru JSON nejsou žádné packOptions a Owner – [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="a3569-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="a3569-190">sada NuGet Pack pro `project.json` ignoruje značky packOptions, jako jsou souhrn, autoři, vlastníci atd. [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="a3569-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="a3569-191">NullReferenceException přes NuGet. balení. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="a3569-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="a3569-192">Sada NuGet Pack ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="a3569-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="a3569-193">Aktualizace více balíčků s vrácením změn ponechá projekt v nefunkčním stavu – [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="a3569-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="a3569-194">ContentFiles v případě, že nejsou přidány pro projekty netstandard – [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="a3569-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="a3569-195">Nelze zabalit správně cílení knihovny na .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="a3569-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="a3569-196">Soubor – > nový projekt – > knihovna tříd (přenosná) projekt se nezdařil v VS2015 a Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="a3569-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="a3569-197">Chyba nuGet – 1.0.0-\* není platný řetězec verze – [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="a3569-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="a3569-198">Find-Package se nepovede zobrazit, ale funguje Install-Package [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="a3569-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="a3569-199">Chyba při instalaci balíčku jQuery. ověření na dev15- [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="a3569-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="a3569-200">sada NuGet Pack pro xproj je nastavená na neplatnou cílovou cestu – [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="a3569-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="a3569-201">Při instalaci VS 2015 Update 3 na VS, kde se používá chyba NuGet verze 3.5.0 – [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="a3569-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="a3569-202">"Blokováno packages.config" v `project.json` (projekt UWP, a. k. a integrovaná sestavení) – [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="a3569-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="a3569-203">Aktualizujte rozhraní příkazového řádku dotnet nainstalovaného skriptem sestavení na preview2-003121, což je oficiální sestavení preview2.</span><span class="sxs-lookup"><span data-stu-id="a3569-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="a3569-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="a3569-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="a3569-205">Uživatelské rozhraní Správce balíčků: po aktualizaci balíčku nezobrazuje novou verzi [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="a3569-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="a3569-206">-ApiKey při odstraňování příkazového řádku není přečten/odeslán v 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="a3569-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="a3569-207">Nesprávný řetězec: stabilní verze balíčku by neměla mít v závislosti na předběžné verzi.</span><span class="sxs-lookup"><span data-stu-id="a3569-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="a3569-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="a3569-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="a3569-209">OptimizedZipPackage cache opouští prázdné složky – [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="a3569-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="a3569-210">Vytváření projektu PCL (net46 a Windows 10) pro získání výjimky NullRef.</span><span class="sxs-lookup"><span data-stu-id="a3569-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="a3569-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="a3569-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="a3569-212">Aktualizace NuGet by měla poskytnout informativní zprávu, pokud je vyšší verze omezená omezením hodnota allowedversions- [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="a3569-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="a3569-213">Problémy s obnovením NuGet V3 – [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="a3569-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="a3569-214">Modul plug-in přihlašovacích údajů se ukončil s chybou-1/při stahování balíčku při použití zprostředkovatelů přihlašovacích údajů s více zdroji – [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="a3569-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="a3569-215">`project.json` obnovení NuGet způsobí opětovnou kompilaci, když se nic nezměnilo – [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="a3569-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="a3569-216">Balíčky symbolů by se neměly nikdy používat při instalaci nebo aktualizaci – [#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="a3569-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="a3569-217">VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="a3569-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="a3569-218">Označení neoznačených prvků UIElement v uživatelském rozhraní Správce balíčků pro usnadnění přístupu [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="a3569-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="a3569-219">Přenosná rozhraní s rozdělenými profily se odmítnou.</span><span class="sxs-lookup"><span data-stu-id="a3569-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="a3569-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="a3569-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="a3569-221">Správce balíčků NuGet by měl zrušit zaškrtnutí tohoto seznamu možností v podrobnostech balíčků se nevztahuje na `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="a3569-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="a3569-222">nuget.exe push/Delete nepoužívá klíč rozhraní API – [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="a3569-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="a3569-223">Odeberte uzamčenou vlastnost ze souboru zámku – [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="a3569-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="a3569-224">Aktualizace NuGet 3.3.0 se nezdařila s dodatečným omezením... definované v packages.config zabrání této operaci. '</span><span class="sxs-lookup"><span data-stu-id="a3569-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="a3569-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="a3569-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="a3569-226">Instalace balíčku z místního zdroje, který neexistuje, vyvolá nefalešnou zprávu- [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="a3569-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="a3569-227">Filtr dostupný k upgradu zobrazuje upgrady, které porušují omezení verze – [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="a3569-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="a3569-228">Nativní balíčky nelze aktualizovat – [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="a3569-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="a3569-229">Funkce</span><span class="sxs-lookup"><span data-stu-id="a3569-229">Features</span></span>

* <span data-ttu-id="a3569-230">Podpora nastavení CopyLocal na hodnotu false u odkazů přidaných pomocí NuGet- [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="a3569-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="a3569-231">Podpora nuget.exe pro MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="a3569-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="a3569-232">Podpora balíčku pro.`csproj`</span><span class="sxs-lookup"><span data-stu-id="a3569-232">Pack support for .`csproj`</span></span><span data-ttu-id="a3569-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="a3569-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="a3569-234">Zakázat akci uživatele, když se spustí akce uživatele – [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="a3569-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="a3569-235">NuGet by měl přidat podporu pro `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="a3569-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="a3569-236">V NuGet 2. x chybí kompatibility rozhraní, které jsou už v 3. x, [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="a3569-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="a3569-237">Podpora pro složky záložních balíčků – [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="a3569-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="a3569-238">Navrhněte a implementujte fiktivní typ balíčku, který podporuje balíčky nástrojů – [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="a3569-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="a3569-239">Přidejte rozhraní API, abyste získali cestu ke složce globálních balíčků – [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="a3569-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="a3569-240">Povolit SemVer 2.0.0 v balíčku – [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="a3569-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="a3569-241">Chcete odeslat obecnou</span><span class="sxs-lookup"><span data-stu-id="a3569-241">DCRs</span></span>

* <span data-ttu-id="a3569-242">Parametr push-timeout nuget.exe nefunguje – [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="a3569-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="a3569-243">Text popisu balíčku by měl být vybrán – [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="a3569-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="a3569-244">Povolení nuget.exe vytváření `.props` a `.targets` souborů pro `.nuproj` projekty [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="a3569-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="a3569-245">Přidání rozhraní API rozšíření pro porovnání platforem s importy – [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="a3569-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="a3569-246">Skrýt možnosti závislosti při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="a3569-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="a3569-247">Vytisknout nuget.exe záhlaví verze v podrobném výstupu – [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="a3569-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="a3569-248">NuGet potřebuje, aby uživatelé věděli, že při upgradu nebo instalaci v dotnet TFM může dojít k problémům – [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="a3569-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="a3569-249">Upozorňovat na neplatnou instalaci/upgrade pro Project w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="a3569-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="a3569-250">Řešení potíží s výkonem pomocí nástroje reformer a NuGet pro Update- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="a3569-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="a3569-251">Přidání podpory netcoreapp11 a netstandard17 – [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="a3569-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="a3569-252">Využití atributu AssemblyMetadata – pro `.nuspec` nahrazení tokenů – [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="a3569-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
