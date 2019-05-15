---
title: Zpráva k vydání verze NuGet 5.0 RTM
description: Zpráva k vydání verze NuGet 5.0, včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610669"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="d03c6-103">Zpráva k vydání verze 5.0 verze NuGet</span><span class="sxs-lookup"><span data-stu-id="d03c6-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="d03c6-104">Distribuce vozidel NuGet:</span><span class="sxs-lookup"><span data-stu-id="d03c6-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d03c6-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="d03c6-105">NuGet version</span></span> | <span data-ttu-id="d03c6-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d03c6-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d03c6-107">K dispozici v rozhraní .NET SDK, pomocí kterých</span><span class="sxs-lookup"><span data-stu-id="d03c6-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d03c6-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="d03c6-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d03c6-109">Visual Studio 2019 version 16.0</span><span class="sxs-lookup"><span data-stu-id="d03c6-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d03c6-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d03c6-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="d03c6-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="d03c6-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d03c6-112">Visual Studio 2019 version 16.0.4</span><span class="sxs-lookup"><span data-stu-id="d03c6-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d03c6-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d03c6-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="d03c6-114"><sup>1</sup>nainstalované s Visual Studio 2019 se sadou .NET Core</span><span class="sxs-lookup"><span data-stu-id="d03c6-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="d03c6-115"><sup>2</sup>dostupné jako volitelná instalace s Visual Studio 2019 se sadou .NET Core</span><span class="sxs-lookup"><span data-stu-id="d03c6-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="d03c6-116">Shrnutí: Co je nového v 5.0</span><span class="sxs-lookup"><span data-stu-id="d03c6-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="d03c6-117">Podpora pro obnovení [filtrované řešení](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) v aplikaci Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="d03c6-117">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="d03c6-118">`BuildTransitive` složka umožňuje balíčky přechodně přispívat cíle/props do projektu hostitel - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="d03c6-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="d03c6-119">Lepší podpora pro scénáře PackageReference v rozhraní API vektory IV NuGet – [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="d03c6-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="d03c6-120">`nuget.exe pack project.json` se už nepoužívá - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="d03c6-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="d03c6-121">Modul plugin poskytovatele přihlašovacích údajů 1. generace bylo nahrazeno [2. generace](https://aka.ms/nuget-cross-platform-authentication-plugin) a bude brzy přestanou používat - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="d03c6-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d03c6-122">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="d03c6-122">Issues fixed in this release</span></span>

<span data-ttu-id="d03c6-123">**Chyby**</span><span class="sxs-lookup"><span data-stu-id="d03c6-123">**Bugs**</span></span>

* <span data-ttu-id="d03c6-124">Vyhněte se při obnovení NoOp, \*. dgspec.json zápis v adresáři obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="d03c6-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="d03c6-125">Oprávnění u souborů, které vytvářejí ~/.nuget jsou příliš open - [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="d03c6-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="d03c6-126">`dotnet list package --outdated` nebude fungovat u jiných zdrojů, které je třeba ověřování - [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="d03c6-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="d03c6-127">NuGet.VisualStudio.IVsPackageInstaller - volání na projektu se žádný balíček odkazuje vždy používá soubor packages.config, i v případě, že ve výchozím nastavení je na PackageReference – [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="d03c6-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="d03c6-128">PMC: Update-Package v delisted balíčky přeinstalujete selže ("Nepodařilo se najít balíček").</span><span class="sxs-lookup"><span data-stu-id="d03c6-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="d03c6-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="d03c6-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="d03c6-130">Přidat oznámení třetích stran v našem úložišti a VSIX – [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="d03c6-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="d03c6-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage měli nainstalovat nejnovější verzi, pokud žádné verzi uvedenou - [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="d03c6-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="d03c6-132">--interaktivní podporu pro dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="d03c6-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="d03c6-133">Při obnovování se soubor zámku, by neměla být vyvolána NU1603 upozornění.</span><span class="sxs-lookup"><span data-stu-id="d03c6-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="d03c6-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="d03c6-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="d03c6-135">NuGet by neměl tisk cesta k projektu během obnovení s minimálním protokolováním - [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="d03c6-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="d03c6-136">--interaktivní podporu pro dotnet odebrat balíček - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="d03c6-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="d03c6-137">Přidat zpět NuGet.Packaging.Core s TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="d03c6-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="d03c6-138">plugins_cache potřebuje kratší cestu fungovat dobře - [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="d03c6-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="d03c6-139">Dáváte přednost cestu k msbuild zjišťování, pokud uživatel nežádali verze konkrétní msbuild - [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="d03c6-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="d03c6-140">`nuget.exe /?` zveřejnit msbuild správná verze – [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="d03c6-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="d03c6-141">NuGet.targets(498,5): Chyba: Nelze najít část cesty "/ tmp/NuGetScratch – v mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="d03c6-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="d03c6-142">obnovení zbytečně zobrazí obsah odkazovaný balíček v mezipaměti machine - všechny verze [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="d03c6-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="d03c6-143">Automatické zjišťování MSBuild vždy vybere 16.0 po instalaci a 2019 ve verzi Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="d03c6-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="d03c6-144">DotNet seznamu balíčku v řešení výstupy duplicitní položky framework – [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="d03c6-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="d03c6-145">Výjimka "prázdnou cestu název není platný" při volání IVsPackageInstaller.InstallPackage na staré projekty a balíčky složka neexistuje.</span><span class="sxs-lookup"><span data-stu-id="d03c6-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="d03c6-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="d03c6-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="d03c6-147">minimální podrobnost nástroje MSBuild/t: Restore by měl být minimálnější - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="d03c6-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="d03c6-148">VS pro 16.0 NuGet uživatelského rozhraní obsahuje nečitelná karty z důvodu problémů s barva - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="d03c6-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="d03c6-149">NuGet.Core & NuGet.Clients License.txt vyjasnění - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="d03c6-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="d03c6-150">Složka globální balíčku obnovení zbytečně zobrazí při pokusu určit typ - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="d03c6-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="d03c6-151">Chyby z vynucení soubor zámku se měla zobrazit v okně Seznam chyb - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="d03c6-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="d03c6-152">Oprava problémů NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="d03c6-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="d03c6-153">Přizpůsobit jeho instalace aktualizace nástroje MSBuild místo – [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="d03c6-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="d03c6-154">NuGet.Build.Tasks.Pack by měl být vývojovou závislost - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="d03c6-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="d03c6-155">Přidat balíček rozšiřovacím bodem pro včetně symboly – ladění [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="d03c6-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="d03c6-156">`dotnet pack` mělo zachovat rozsah verzí závislosti v vytvořený soubor nupkg (i když je použita verze s plovoucí desetinnou čárkou) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="d03c6-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="d03c6-157">`dotnet restore` selže na ověřeného zdroje při individuální konfigurace má také zdroj - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="d03c6-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="d03c6-158">Balíček by nemělo omezit sadu BuildActions souborů obsahu – [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="d03c6-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="d03c6-159">Pomocí ProjectReference, který vyžaduje AssetTargetFallback úspěšné, by měla upozornění.</span><span class="sxs-lookup"><span data-stu-id="d03c6-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="d03c6-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="d03c6-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="d03c6-161">Zablokování kvůli problémy s tvorbou vláken při volání do prohlášení CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="d03c6-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="d03c6-162">`dotnet add package` nepoužívá přihlašovacích údajů z globální konfigurace pro zadaný v místních konfiguračních - zdroj [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="d03c6-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="d03c6-163">Problémy s tvorbou vláken MEF, že se volá asynchronní kód cesty - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="d03c6-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="d03c6-164">Podepisování: hlášená dvakrát a bez zásobník volání – chyba [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="d03c6-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="d03c6-165">Instalace pomocí nedůvěryhodného podpisový certifikát podepsaný balíček by se zobrazit chyba – [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="d03c6-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="d03c6-166">Obnovení NuGet nesprávně chová jako operace NoOp při 2 projekty jsou sdílení directory obj – [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="d03c6-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="d03c6-167">Nelze použít token PAT s `dotnet restore` v Linuxu pomocí balíčků z ověřené informační kanál – [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="d03c6-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="d03c6-168">DotNet restore nezdaří z důvodu široké zakázané počítač kanál – [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="d03c6-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="d03c6-169">**Chcete**</span><span class="sxs-lookup"><span data-stu-id="d03c6-169">**DCRs**</span></span>

* <span data-ttu-id="d03c6-170">Upozornit budoucí odebrání "project.json balíčku dotnet" - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="d03c6-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="d03c6-171">Přidat upozornění na vyřazení pro modul plug-in credential Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="d03c6-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="d03c6-172">Podpis: Povolené úložiště tak, aby vyžadovala ověření klienta z každého balíčku jako úložiště podepsán--přes RepositorySignatures/5.0.0 prostředek - [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="d03c6-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="d03c6-173">omezit požadavek http na zdroji pomocí souboru NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="d03c6-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="d03c6-174">NuGet zaměřit Net472 (usnadní vyčištění 16,0 sestavení VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="d03c6-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="d03c6-175">PMC: Odebrat příkaz OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="d03c6-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="d03c6-176">Zkontrolujte mapování NetCoreApp 3.0 NetStandard 2.1 – [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="d03c6-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="d03c6-177">Přidání podpory netstandard2.0 NuGet.\* balíčků - [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="d03c6-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="d03c6-178">Umožnil autorům balíčků k definování sestavení prostředky přenosné chování - [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="d03c6-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="d03c6-179">Podpora funkce filtru řešení VS 2019.</span><span class="sxs-lookup"><span data-stu-id="d03c6-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="d03c6-180">Podporuje také projekt není v řešení nebo uvolněné projekty.</span><span class="sxs-lookup"><span data-stu-id="d03c6-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="d03c6-181">Třeba obnovit tak získají kompletní řešení (prostřednictvím rozhraní příkazového řádku nebo VS) first – [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="d03c6-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="d03c6-182">NuGet 5.0 sestavení tak, aby vyžadovala .NET 4.7.2 (prostřednictvím změnit TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="d03c6-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="d03c6-183">NuGetLicenseData z NuGet.Packaging by měl být veřejným typem.</span><span class="sxs-lookup"><span data-stu-id="d03c6-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="d03c6-184">Aktualizujte metadata licence ingestována z spdx.</span><span class="sxs-lookup"><span data-stu-id="d03c6-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="d03c6-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="d03c6-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="d03c6-186">Odebrat zastaralé nastavení rozhraní API – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="d03c6-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="d03c6-187">Alternativní řešení obnovení vypršení časového limitu v systémech s 1 cpu – [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="d03c6-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="d03c6-188">NuGet upřednostňuje ověřování NTLM, i když nejsou přihlašovací údaje do souboru NuGet.config – přidání možností konfigurace k filtrování typů ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="d03c6-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="d03c6-189">Povolit EmbedInteropTypes pro PackageReference (odpovídající souboru Packages.Config schopnost) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="d03c6-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="d03c6-190">**[Seznam všech problémů, které jsou opravené v této verzi - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="d03c6-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="d03c6-191">Shrnutí: Co je nového v 5.0.2</span><span class="sxs-lookup"><span data-stu-id="d03c6-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="d03c6-192">Zabezpečení (při spuštění prostřednictvím dotnet.exe nebo mono.exe) – s správná oprávnění by měl vytvořit složku obj [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="d03c6-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="d03c6-193">obnovení nuget.exe v mono, MacOS se nezdaří s vlastní soubor nuget.config a `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="d03c6-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="d03c6-194">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="d03c6-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="d03c6-195">Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="d03c6-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="d03c6-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="d03c6-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="d03c6-197">Problém</span><span class="sxs-lookup"><span data-stu-id="d03c6-197">Issue</span></span>
<span data-ttu-id="d03c6-198">Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="d03c6-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="d03c6-199">To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="d03c6-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="d03c6-200">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="d03c6-200">Workaround</span></span>
<span data-ttu-id="d03c6-201">Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` Nothing:</span><span class="sxs-lookup"><span data-stu-id="d03c6-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="d03c6-202">Jak balíčky, které se obnoví ze záložní složky budou nyní stáhnout z webu NuGet.org, použijte tento fragment se upozornění.</span><span class="sxs-lookup"><span data-stu-id="d03c6-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
