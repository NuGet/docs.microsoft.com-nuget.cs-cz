---
title: Poznámky k verzi 5.0 preview NuGet
description: Zpráva k vydání verze NuGet 5.0 verzí Preview, včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084952"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="57e8c-103">Zpráva k vydání verze NuGet 5.0 ve verzi Preview</span><span class="sxs-lookup"><span data-stu-id="57e8c-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="57e8c-104">Shrnutí: Co je nového ve verzi 5.0 Preview 2</span><span class="sxs-lookup"><span data-stu-id="57e8c-104">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="57e8c-105">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="57e8c-105">Issues fixed in this release</span></span>

#### <a name="bugs"></a><span data-ttu-id="57e8c-106">Chyby:</span><span class="sxs-lookup"><span data-stu-id="57e8c-106">Bugs:</span></span>

* <span data-ttu-id="57e8c-107">VS pro 16.0 NuGet uživatelského rozhraní obsahuje nečitelná karty z důvodu problémů s barva - [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="57e8c-107">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="57e8c-108">NuGet.Core & NuGet.Clients License.txt vyjasnění - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="57e8c-108">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="57e8c-109">Složka globální balíčku obnovení zbytečně zobrazí při pokusu určit typ - [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="57e8c-109">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="57e8c-110">Chyby z vynucení soubor zámku se měla zobrazit v okně Seznam chyb - [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="57e8c-110">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="57e8c-111">Oprava problémů NuGet.Configuration - [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="57e8c-111">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="57e8c-112">Přizpůsobení nástroje MSBuild aktualizace v umístění instalace.</span><span class="sxs-lookup"><span data-stu-id="57e8c-112">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="57e8c-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="57e8c-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="57e8c-114">NuGet.Build.Tasks.Pack by měl být vývojovou závislost - [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="57e8c-114">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="57e8c-115">Přidat balíček rozšiřovacím bodem pro včetně symboly – ladění [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="57e8c-115">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="57e8c-116">balíčku DotNet mělo zachovat rozsah verzí závislosti v vytvořený soubor nupkg.</span><span class="sxs-lookup"><span data-stu-id="57e8c-116">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="57e8c-117">(i když je použita verze s plovoucí desetinnou čárkou) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="57e8c-117">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="57e8c-118">DotNet restore selže ověřeného zdroje, pokud uživatelské úrovni konfigurace má také zdroj - [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="57e8c-118">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="57e8c-119">Balíček by nemělo omezit sadu BuildActions souborů obsahu – [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="57e8c-119">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="57e8c-120">Pomocí projectreference, který vyžaduje AssetTargetFallback úspěšné, by měla upozornění.</span><span class="sxs-lookup"><span data-stu-id="57e8c-120">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="57e8c-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="57e8c-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="57e8c-122">Zablokování kvůli problémy s tvorbou vláken při volání do prohlášení CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="57e8c-122">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="57e8c-123">příkaz DotNet add balíček nebude používat přihlašovací údaje z globální konfigurace zdroje zadaného v místním souboru config - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="57e8c-123">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="57e8c-124">Práce s vlákny problémy s MEF se volalo asynchronní cest v kódu – [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="57e8c-124">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="57e8c-125">Podepisování: hlášená dvakrát a bez zásobník volání – chyba [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="57e8c-125">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="57e8c-126">Instalace pomocí nedůvěryhodného podpisový certifikát podepsaný balíček by se zobrazit chyba – [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="57e8c-126">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="57e8c-127">Obnovení NuGet nesprávně chová jako operace NoOp při 2 projekty jsou sdílení directory obj – [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="57e8c-127">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="57e8c-128">Nelze použít token PAT s dotnet restore v Linuxu pomocí balíčků z ověřené informační kanál – [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="57e8c-128">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="57e8c-129">DotNet restore nezdaří z důvodu široké zakázané počítač kanál – [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="57e8c-129">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

#### <a name="dcrs"></a><span data-ttu-id="57e8c-130">Chcete</span><span class="sxs-lookup"><span data-stu-id="57e8c-130">DCRs</span></span>

* <span data-ttu-id="57e8c-131">NuGet 5.0 sestavení tak, aby vyžadovala .NET 4.7.2 (prostřednictvím změnit TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="57e8c-131">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="57e8c-132">NuGetLicenseData z NuGet.Packaging by měl být veřejným typem.</span><span class="sxs-lookup"><span data-stu-id="57e8c-132">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="57e8c-133">Aktualizujte metadata licence ingestována z spdx.</span><span class="sxs-lookup"><span data-stu-id="57e8c-133">Update license metadata ingested from spdx.</span></span><span data-ttu-id="57e8c-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="57e8c-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="57e8c-135">Odebrat zastaralé nastavení rozhraní API – [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="57e8c-135">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="57e8c-136">Alternativní řešení obnovení vypršení časového limitu v systémech s 1 cpu – [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="57e8c-136">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="57e8c-137">NuGet upřednostňuje ověřování NTLM, i když nejsou přihlašovací údaje do souboru NuGet.config – přidání možností konfigurace k filtrování typů ověřování pro přihlašovací údaje – [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="57e8c-137">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="57e8c-138">Povolit EmbedInteropTypes pro PackageReference (odpovídající souboru Packages.Config schopnost) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="57e8c-138">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="57e8c-139">Seznam všech chyby opravené v této verzi 5.0.0-preview2</span><span class="sxs-lookup"><span data-stu-id="57e8c-139">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a><span data-ttu-id="57e8c-140">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="57e8c-140">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="57e8c-141">DotNet nuget příkaz push--interaktivní vrátí chybu v systému Mac.</span><span class="sxs-lookup"><span data-stu-id="57e8c-141">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="57e8c-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="57e8c-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="57e8c-143">Problém</span><span class="sxs-lookup"><span data-stu-id="57e8c-143">Issue</span></span>
<span data-ttu-id="57e8c-144">`--interactive` Argument není předávaná pomocí rozhraní příkazového řádku dotnet což vede k chybě `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="57e8c-144">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="57e8c-145">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="57e8c-145">Workaround</span></span>
<span data-ttu-id="57e8c-146">Spuštění další příkaz dotnet pomocí interaktivní možnosti, jako `dotnet restore --interactive` a provést ověření.</span><span class="sxs-lookup"><span data-stu-id="57e8c-146">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="57e8c-147">Ověřování potom může do mezipaměti podle poskytovatele přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="57e8c-147">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="57e8c-148">Potom spusťte `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="57e8c-148">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="57e8c-149">Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu.</span><span class="sxs-lookup"><span data-stu-id="57e8c-149">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="57e8c-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="57e8c-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="57e8c-151">Problém</span><span class="sxs-lookup"><span data-stu-id="57e8c-151">Issue</span></span>
<span data-ttu-id="57e8c-152">Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="57e8c-152">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="57e8c-153">To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="57e8c-153">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="57e8c-154">Alternativní řešení</span><span class="sxs-lookup"><span data-stu-id="57e8c-154">Workaround</span></span>
<span data-ttu-id="57e8c-155">Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` na hodnotu nothing.</span><span class="sxs-lookup"><span data-stu-id="57e8c-155">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="57e8c-156">`<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.</span><span class="sxs-lookup"><span data-stu-id="57e8c-156">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
