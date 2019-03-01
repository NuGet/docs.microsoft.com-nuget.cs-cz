---
title: Poznámky k verzi 5.0 preview NuGet
description: Zpráva k vydání verze NuGet 5.0 verzí Preview, včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196197"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="65ac3-103">Zpráva k vydání verze NuGet 5.0 ve verzi Preview</span><span class="sxs-lookup"><span data-stu-id="65ac3-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="65ac3-104">NuGet 5.0 předběžné verze</span><span class="sxs-lookup"><span data-stu-id="65ac3-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="65ac3-105">27. únoru 2010 - [NuGet 5.0 ve verzi Preview 4](#summary-whats-new-in-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="65ac3-105">February 27, 2010 - [NuGet 5.0 Preview 4](#summary-whats-new-in-50-preview-4)</span></span>
* <span data-ttu-id="65ac3-106">13. února 2019 - [NuGet 5.0 ve verzi Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="65ac3-106">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="65ac3-107">Od 23. května 2019 - [NuGet 5.0 ve verzi Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="65ac3-107">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="65ac3-108">Shrnutí: Co je nového ve verzi Preview 4 NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="65ac3-108">Summary: What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="65ac3-109">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="65ac3-109">Issues fixed in this release</span></span>

<span data-ttu-id="65ac3-110">**Chyby:**</span><span class="sxs-lookup"><span data-stu-id="65ac3-110">**Bugs:**</span></span>

* <span data-ttu-id="65ac3-111">NuGet.VisualStudio.IVsPackageInstaller - volání na projektu se žádný balíček odkazuje vždy používá soubor packages.config, i v případě, že ve výchozím nastavení je na PackageReference – [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="65ac3-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="65ac3-112">PMC: Update-Package v delisted balíčky přeinstalujete selže ("Nepodařilo se najít balíček").</span><span class="sxs-lookup"><span data-stu-id="65ac3-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="65ac3-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="65ac3-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="65ac3-114">Přidat oznámení třetích stran v našem úložišti a VSIX – [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="65ac3-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="65ac3-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage měli nainstalovat nejnovější verzi, pokud žádné verzi uvedenou - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="65ac3-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="65ac3-116">--interaktivní podporu pro dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="65ac3-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="65ac3-117">Při obnovování se soubor zámku, by neměla být vyvolána NU1603 upozornění.</span><span class="sxs-lookup"><span data-stu-id="65ac3-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="65ac3-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="65ac3-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="65ac3-119">NuGet by neměl tisk cesta k projektu během obnovení s minimálním protokolováním - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="65ac3-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="65ac3-120">--interaktivní podporu pro dotnet odebrat balíček - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="65ac3-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="65ac3-121">Přidat zpět NuGet.Packaging.Core s TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="65ac3-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="65ac3-122">plugins_cache potřebuje kratší cestu fungovat dobře - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="65ac3-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="65ac3-123">Dáváte přednost cestu k msbuild zjišťování, pokud uživatel nežádali verze konkrétní msbuild - [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="65ac3-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="65ac3-124">**Chcete:**</span><span class="sxs-lookup"><span data-stu-id="65ac3-124">**DCRs:**</span></span>

* <span data-ttu-id="65ac3-125">omezit požadavek http na zdroji pomocí souboru NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="65ac3-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="65ac3-126">NuGet zaměřit Net472 (usnadní vyčištění 16,0 sestavení VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="65ac3-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="65ac3-127">PMC: Odebrat příkaz OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="65ac3-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="65ac3-128">Zkontrolujte mapování NetCoreApp 3.0 NetStandard 2.1 – [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="65ac3-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="65ac3-129">Přidání podpory netstandard2.0 NuGet.\* balíčků - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="65ac3-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="65ac3-130">Shrnutí: Co je nového ve verzi Preview 3 NuGet 5.0</span><span class="sxs-lookup"><span data-stu-id="65ac3-130">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="65ac3-131">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="65ac3-131">Issues fixed in this release</span></span> 

<span data-ttu-id="65ac3-132">**Chyby:**</span><span class="sxs-lookup"><span data-stu-id="65ac3-132">**Bugs:**</span></span>

* <span data-ttu-id="65ac3-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="65ac3-133">nuget.exe /?</span></span> <span data-ttu-id="65ac3-134">zveřejnit msbuild správná verze – [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="65ac3-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="65ac3-135">NuGet.targets(498,5): Chyba: Nelze najít část cesty "/ tmp/NuGetScratch – v mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="65ac3-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="65ac3-136">obnovení zbytečně zobrazí obsah odkazovaný balíček v mezipaměti machine - všechny verze [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="65ac3-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="65ac3-137">Automatické zjišťování MSBuild vždy vybere 16.0 po instalaci a 2019 ve verzi Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="65ac3-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="65ac3-138">DotNet seznamu balíčku v řešení výstupy duplicitní položky framework – [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="65ac3-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="65ac3-139">Výjimka "prázdnou cestu název není platný" při volání IVsPackageInstaller.InstallPackage na staré projekty a balíčky složka neexistuje.</span><span class="sxs-lookup"><span data-stu-id="65ac3-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="65ac3-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="65ac3-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="65ac3-141">minimální podrobnost nástroje MSBuild/t: Restore by měl být minimálnější - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="65ac3-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="65ac3-142">**Chcete:**</span><span class="sxs-lookup"><span data-stu-id="65ac3-142">**DCRs:**</span></span>

* <span data-ttu-id="65ac3-143">Umožnil autorům balíčků k definování sestavení prostředky přenosné chování - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="65ac3-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="65ac3-144">Povolit obnovení v sadě Visual Studio úspěšná, když projekt není součástí řešení nebo není načten, ale se dříve obnovila - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="65ac3-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="65ac3-145">Shrnutí: Co je nového ve verzi 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="65ac3-145">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="65ac3-146">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="65ac3-146">Issues fixed in this release</span></span>

<span data-ttu-id="65ac3-147">**Chyby:**</span><span class="sxs-lookup"><span data-stu-id="65ac3-147">**Bugs:**</span></span>

* <span data-ttu-id="65ac3-148">VS pro 16.0 NuGet uživatelského rozhraní obsahuje nečitelná karty z důvodu problémů s barva - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="65ac3-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="65ac3-149">NuGet.Core & NuGet.Clients License.txt vyjasnění - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="65ac3-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="65ac3-150">Složka globální balíčku obnovení zbytečně zobrazí při pokusu určit typ - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="65ac3-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="65ac3-151">Chyby z vynucení soubor zámku se měla zobrazit v okně Seznam chyb - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="65ac3-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="65ac3-152">Oprava problémů NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="65ac3-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="65ac3-153">Přizpůsobení nástroje MSBuild aktualizace v umístění instalace.</span><span class="sxs-lookup"><span data-stu-id="65ac3-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="65ac3-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="65ac3-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="65ac3-155">NuGet.Build.Tasks.Pack by měl být vývojovou závislost - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="65ac3-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="65ac3-156">Přidat balíček rozšiřovacím bodem pro včetně symboly – ladění [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="65ac3-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="65ac3-157">balíčku DotNet mělo zachovat rozsah verzí závislosti v vytvořený soubor nupkg.</span><span class="sxs-lookup"><span data-stu-id="65ac3-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="65ac3-158">(i když je použita verze s plovoucí desetinnou čárkou) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="65ac3-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="65ac3-159">DotNet restore selže ověřeného zdroje, pokud uživatelské úrovni konfigurace má také zdroj - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="65ac3-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="65ac3-160">Balíček by nemělo omezit sadu BuildActions souborů obsahu – [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="65ac3-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="65ac3-161">Pomocí projectreference, který vyžaduje AssetTargetFallback úspěšné, by měla upozornění.</span><span class="sxs-lookup"><span data-stu-id="65ac3-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="65ac3-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="65ac3-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="65ac3-163">Zablokování kvůli problémy s tvorbou vláken při volání do prohlášení CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="65ac3-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="65ac3-164">příkaz DotNet add balíček nebude používat přihlašovací údaje z globální konfigurace zdroje zadaného v místním souboru config - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="65ac3-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="65ac3-165">Práce s vlákny problémy s MEF se volalo asynchronní cest v kódu – [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="65ac3-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="65ac3-166">Podepisování: hlášená dvakrát a bez zásobník volání – chyba [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="65ac3-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="65ac3-167">Instalace pomocí nedůvěryhodného podpisový certifikát podepsaný balíček by se zobrazit chyba – [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="65ac3-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="65ac3-168">Obnovení NuGet nesprávně chová jako operace NoOp při 2 projekty jsou sdílení directory obj – [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="65ac3-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="65ac3-169">Nelze použít token PAT s dotnet restore v Linuxu pomocí balíčků z ověřené informační kanál – [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="65ac3-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="65ac3-170">DotNet restore nezdaří z důvodu široké zakázané počítač kanál – [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="65ac3-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="65ac3-171">**Chcete:**</span><span class="sxs-lookup"><span data-stu-id="65ac3-171">**DCRs:**</span></span>

* <span data-ttu-id="65ac3-172">NuGet 5.0 sestavení tak, aby vyžadovala .NET 4.7.2 (prostřednictvím změnit TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="65ac3-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="65ac3-173">NuGetLicenseData z NuGet.Packaging by měl být veřejným typem.</span><span class="sxs-lookup"><span data-stu-id="65ac3-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="65ac3-174">Aktualizujte metadata licence ingestována z spdx.</span><span class="sxs-lookup"><span data-stu-id="65ac3-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="65ac3-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="65ac3-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="65ac3-176">Odebrat zastaralé nastavení rozhraní API – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="65ac3-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="65ac3-177">Alternativní řešení obnovení vypršení časového limitu v systémech s 1 cpu – [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="65ac3-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="65ac3-178">NuGet upřednostňuje ověřování NTLM, i když nejsou přihlašovací údaje do souboru NuGet.config – přidání možností konfigurace k filtrování typů ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="65ac3-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="65ac3-179">Povolit EmbedInteropTypes pro PackageReference (odpovídající souboru Packages.Config schopnost) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="65ac3-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="65ac3-180">Seznam všech chyby opravené v této verzi 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="65ac3-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="65ac3-181">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="65ac3-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="65ac3-182">Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="65ac3-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="65ac3-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="65ac3-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="65ac3-184">**Problém** při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="65ac3-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="65ac3-185">To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="65ac3-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="65ac3-186">**Alternativní řešení** využití záložní složky zakázat nastavením `RestoreAdditionalProjectSources` na hodnotu nothing.</span><span class="sxs-lookup"><span data-stu-id="65ac3-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="65ac3-187">`<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.</span><span class="sxs-lookup"><span data-stu-id="65ac3-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
