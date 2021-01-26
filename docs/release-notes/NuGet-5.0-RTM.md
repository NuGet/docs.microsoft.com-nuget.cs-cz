---
title: Poznámky k verzi NuGet 5,0 RTM
description: Poznámky k verzi pro NuGet 5,0, včetně známých problémů, oprav chyb, nových funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 637db1ae128ce020c33e54e56148c848a5f905a5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776216"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="3bae6-103">Zpráva k vydání verze NuGet 5,0</span><span class="sxs-lookup"><span data-stu-id="3bae6-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="3bae6-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="3bae6-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3bae6-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="3bae6-105">NuGet version</span></span> | <span data-ttu-id="3bae6-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3bae6-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3bae6-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3bae6-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3bae6-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="3bae6-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3bae6-109">Visual Studio 2019 verze 16,0</span><span class="sxs-lookup"><span data-stu-id="3bae6-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3bae6-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3bae6-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="3bae6-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="3bae6-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3bae6-112">Visual Studio 2019 verze 16.0.4</span><span class="sxs-lookup"><span data-stu-id="3bae6-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3bae6-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3bae6-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="3bae6-114"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="3bae6-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="3bae6-115"><sup>2</sup> . K dispozici jako volitelná instalace se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="3bae6-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="3bae6-116">Shrnutí: Novinky v 5,0</span><span class="sxs-lookup"><span data-stu-id="3bae6-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="3bae6-117">Podpora pro obnovení [filtrovaných řešení](/visualstudio/ide/filtered-solutions?view=vs-2019) v aplikaci Visual Studio 2019 – [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="3bae6-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="3bae6-118">`BuildTransitive` Složka umožňuje balíčkům, aby byly do projektu hostitele zacíleny cílení na přispívat/props – [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="3bae6-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="3bae6-119">Lepší podpora scénářů PackageReference v rozhraní NuGet Ideographic API [](https://github.com/NuGet/Home/issues/7005)– #7005 [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="3bae6-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="3bae6-120">`nuget.exe pack project.json` se již nepoužívá- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="3bae6-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="3bae6-121">Modul plug-in zprostředkovatele přihlašovacích údajů pro Gen 1 byl nahrazen [2. Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) a bude brzy zastaralý – [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="3bae6-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3bae6-122">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="3bae6-122">Issues fixed in this release</span></span>

<span data-ttu-id="3bae6-123">**Štěnic**</span><span class="sxs-lookup"><span data-stu-id="3bae6-123">**Bugs**</span></span>

* <span data-ttu-id="3bae6-124">Při obnovení NoOp Vyhněte se tomu \* .dgspec.jspři zápisu do adresáře obj – [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="3bae6-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="3bae6-125">Oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená – [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="3bae6-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="3bae6-126">`dotnet list package --outdated` nefunguje se zdroji, které potřebují auth- [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="3bae6-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="3bae6-127">NuGet. VisualStudio. IVsPackageInstaller-volání na projekt bez odkazů na balíčky vždy používá packages.config, i když je výchozí nastavení nastaveno na PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="3bae6-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="3bae6-128">PMC: přeinstalace Update-Package se nezdařila ("nelze nalézt balíček") na delistované balíčky.</span><span class="sxs-lookup"><span data-stu-id="3bae6-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="3bae6-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="3bae6-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="3bae6-130">Přidání oznámení třetí strany do našeho úložiště a VSIX – [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="3bae6-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="3bae6-131">NuGet. VisualStudio. IVsPackageInstaller. InstallPackage by měl nainstalovat nejnovější verzi, pokud není zadána žádná verze- [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="3bae6-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="3bae6-132">--Interaktivní podpora pro příkaz dotnet NuGet push- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="3bae6-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="3bae6-133">Při obnovení pomocí souboru zámku by se nemělo vystavit upozornění NU1603.</span><span class="sxs-lookup"><span data-stu-id="3bae6-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="3bae6-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="3bae6-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="3bae6-135">NuGet by neměl tisknout cestu projektu během obnovení s minimálním protokolováním – [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="3bae6-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="3bae6-136">--Interaktivní podpora pro příkaz dotnet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="3bae6-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="3bae6-137">Přidejte zpět NuGet. balení. Core pomocí TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="3bae6-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="3bae6-138">plugins_cache potřebuje kratší cestu, aby správně fungovala [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="3bae6-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="3bae6-139">Preferovat cestu pro zjišťování nástroje MSBuild, pokud uživatel nepožádal o konkrétní verzi nástroje MSBuild – [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="3bae6-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="3bae6-140">`nuget.exe /?` měl by vypsat správné verze nástroje MSBuild – [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="3bae6-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="3bae6-141">NuGet. TARGETS (498; 5): Chyba: nepovedlo se najít část cesty/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793) .</span><span class="sxs-lookup"><span data-stu-id="3bae6-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="3bae6-142">Při obnovení se nenutně vytvoří výčet obsahu všech verzí odkazovaného balíčku v mezipaměti počítače – [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="3bae6-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="3bae6-143">Automatické zjišťování MSBuild vždy vybere 16,0 po instalaci VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="3bae6-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="3bae6-144">příkaz dotnet list na řešení má na výstupu duplicitní položky pro architekturu – [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="3bae6-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="3bae6-145">Výjimka "prázdný název cesty není platný" při volání IVsPackageInstaller. InstallPackage u starých projektů a složky balíčků neexistuje.</span><span class="sxs-lookup"><span data-stu-id="3bae6-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="3bae6-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="3bae6-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="3bae6-147">MSBuild/t: Obnova minimální podrobností by měla být větší minimální [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="3bae6-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="3bae6-148">Uživatelské rozhraní NuGet 16.0 sady VS má nečitelný tabulátory z důvodu problémů s barvou – [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="3bae6-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="3bae6-149">NuGet. Core & NuGet. klienti License.txt objasnění [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="3bae6-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="3bae6-150">Při pokusu o určení typu [#7596](https://github.com/NuGet/Home/issues/7596) se nenutně vytvoří výčet složky globálního balíčku.</span><span class="sxs-lookup"><span data-stu-id="3bae6-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="3bae6-151">Chyby z vynucení zámků souborů by se měly zobrazit v Seznam chyb okně – [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="3bae6-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="3bae6-152">Oprava problémů NuGet.Configuration – [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="3bae6-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="3bae6-153">Přizpůsobit k aktualizaci MSBuild umístění instalace – [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="3bae6-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="3bae6-154">NuGet. Build. Tasks. Pack by měla být vývojová závislost – [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="3bae6-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="3bae6-155">Přidat bod rozšíření balíčku pro zahrnutí symbolů ladění – [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="3bae6-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="3bae6-156">`dotnet pack` by měl zachovat rozsah verzí závislosti ve vytvořeném nupkg (i když se používá plovoucí verze) – [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="3bae6-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="3bae6-157">`dotnet restore`v ověřeném zdroji se nezdařila, pokud má konfigurace na úrovni uživatele také [#7209](https://github.com/NuGet/Home/issues/7209) zdroje.</span><span class="sxs-lookup"><span data-stu-id="3bae6-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="3bae6-158">Sada BuildActions by neměla omezovat sadu souborů obsahu – [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="3bae6-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="3bae6-159">Použití ProjectReference, které vyžaduje, aby AssetTargetFallback bylo úspěšné, by mělo upozorňovat.</span><span class="sxs-lookup"><span data-stu-id="3bae6-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="3bae6-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="3bae6-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="3bae6-161">Zablokování kvůli problémům s vlákny při volání do CPS (CommonProjectSystem) – [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="3bae6-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="3bae6-162">`dotnet add package` nepoužívá přihlašovací údaje z globální konfigurace pro zdroj zadaný v místní konfiguraci [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="3bae6-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="3bae6-163">Problémy s vlákny s rozhraním MEF volanou v případě asynchronních cest kódu – [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="3bae6-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="3bae6-164">Podepisování: Chyba nahlášená dvakrát a bez zásobníku volání- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="3bae6-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="3bae6-165">Při instalaci podepsaného balíčku s nedůvěryhodným podpisovým certifikátem by se měla zobrazit chyba [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="3bae6-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="3bae6-166">Obnovení NuGet je nesprávně NoOpsé, když 2 projekty sdílí adresář obj – [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="3bae6-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="3bae6-167">Nelze použít PAT se systémem `dotnet restore` v systému Linux s balíčky z ověřeného informačního kanálu – [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="3bae6-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="3bae6-168">dotnet restore se nepovedlo kvůli zakázanému kanálu pro nejrůznější počítače – [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="3bae6-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="3bae6-169">**Chcete odeslat obecnou**</span><span class="sxs-lookup"><span data-stu-id="3bae6-169">**DCRs**</span></span>

* <span data-ttu-id="3bae6-170">Upozornění na budoucí odebrání "dotnet Pack project.json"- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="3bae6-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="3bae6-171">Přidání upozornění na zastaralost pro modul plug-in Gen1 přihlašovacích údajů – [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="3bae6-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="3bae6-172">Podepisování: povolené úložiště, které vyžaduje ověření klienta každého balíčku jako úložiště pomocí RepositorySignatures/5.0.0 Resource- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="3bae6-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="3bae6-173">omezení počtu žádostí http na zdroj prostřednictvím NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="3bae6-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="3bae6-174">NuGet by měl cílit na Net472 (aby bylo možné vyčistit 16,0 sestavení VSIX) – [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="3bae6-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="3bae6-175">PMC: Odebrat příkaz OpenPackagePage- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="3bae6-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="3bae6-176">Vytvoření mapy NetCoreApp 3,0 na NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="3bae6-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="3bae6-177">Přidat podporu netstandard 2.0 do NuGet. \* Packages – [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="3bae6-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="3bae6-178">Umožňuje autorům balíčků definovat přenosné chování prostředků sestavení – [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="3bae6-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="3bae6-179">Podporuje funkci filtru řešení VS 2019.</span><span class="sxs-lookup"><span data-stu-id="3bae6-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="3bae6-180">Podporuje také projekt, který není v řešení, nebo uvolněné projekty.</span><span class="sxs-lookup"><span data-stu-id="3bae6-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="3bae6-181">Je nutné obnovit kompletní řešení (přes CLI nebo VS) první [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="3bae6-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="3bae6-182">Sestavení NuGet 5,0, která vyžadují .NET 4.7.2 (prostřednictvím TFM změny) – [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="3bae6-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="3bae6-183">NuGetLicenseData z NuGetu. balení musí být veřejný typ.</span><span class="sxs-lookup"><span data-stu-id="3bae6-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="3bae6-184">Aktualizuje metadata licencí z spdx.</span><span class="sxs-lookup"><span data-stu-id="3bae6-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="3bae6-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="3bae6-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="3bae6-186">Odebrat zastaralá rozhraní API pro nastavení – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="3bae6-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="3bae6-187">Časový limit obnovení v systémech s 1 procesorem [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="3bae6-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="3bae6-188">NuGet dává přednost ověřování NTLM i v případě, že existují přihlašovací údaje v NuGet.config-přidání možnosti konfigurace pro filtrování typů ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="3bae6-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="3bae6-189">Povolit EmbedInteropTypes pro PackageReference (odpovídá schopnosti Packages.Config) – [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="3bae6-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="3bae6-190">**[Seznam všech problémů opravených v této verzi – 5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="3bae6-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="3bae6-191">Shrnutí: co je nového v 5.0.2</span><span class="sxs-lookup"><span data-stu-id="3bae6-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="3bae6-192">Zabezpečení (při spuštění prostřednictvím dotnet.exe nebo mono.exe) – složka obj by měla být vytvořená se správnými oprávněními [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="3bae6-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="3bae6-193">nuget.exe obnovení mono/MacOS se nezdařila s vlastní nuget.config a `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="3bae6-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="3bae6-194">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="3bae6-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="3bae6-195">Balíčky v FallbackFolders nainstalované pomocí .NET Core SDK jsou vlastní instalace a ověření podpisu při selhání.</span><span class="sxs-lookup"><span data-stu-id="3bae6-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="3bae6-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="3bae6-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="3bae6-197">Problém</span><span class="sxs-lookup"><span data-stu-id="3bae6-197">Issue</span></span>
<span data-ttu-id="3bae6-198">Při použití dotnet.exe 2. x k obnovení projektu, který má více cílů netcoreapp 1. x a netcoreapp 2. x, se záložní složka považuje za informační kanál souboru.</span><span class="sxs-lookup"><span data-stu-id="3bae6-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="3bae6-199">To znamená, že při obnovení NuGet vybere balíček ze záložní složky a pokusí se ho nainstalovat do složky globálních balíčků a provede běžné ověřování podpisů, které selže.</span><span class="sxs-lookup"><span data-stu-id="3bae6-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="3bae6-200">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="3bae6-200">Workaround</span></span>
<span data-ttu-id="3bae6-201">Zakažte použití záložní složky nastavením na `RestoreAdditionalProjectSources` hodnotu Nothing:</span><span class="sxs-lookup"><span data-stu-id="3bae6-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="3bae6-202">Používejte je opatrně, protože balíčky, které by se obnovily ze záložní složky, se teď stáhnou z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3bae6-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>