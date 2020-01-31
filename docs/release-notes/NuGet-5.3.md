---
title: Zpráva k vydání verze NuGet 5,3
description: Poznámky k verzi pro NuGet 5,3, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: ca71c5b9ef546f3ea92e55763d5059466ac3a930
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813751"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="c0e43-103">Zpráva k vydání verze NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="c0e43-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="c0e43-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="c0e43-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="c0e43-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="c0e43-105">NuGet version</span></span> | <span data-ttu-id="c0e43-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0e43-106">Available in Visual Studio version</span></span>| <span data-ttu-id="c0e43-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c0e43-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="c0e43-108">**5.3.0**</span><span class="sxs-lookup"><span data-stu-id="c0e43-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c0e43-109">Visual Studio 2019 verze 16,3</span><span class="sxs-lookup"><span data-stu-id="c0e43-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="c0e43-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="c0e43-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="c0e43-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="c0e43-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c0e43-112">Visual Studio 2019 verze 16.3.6</span><span class="sxs-lookup"><span data-stu-id="c0e43-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="c0e43-113">Budoucí verze: 3.0.101</span><span class="sxs-lookup"><span data-stu-id="c0e43-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="c0e43-114"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="c0e43-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="c0e43-115">Shrnutí: Novinky v 5,3</span><span class="sxs-lookup"><span data-stu-id="c0e43-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="c0e43-116">[Ikona balíčku se dá vložit do balíčku](../reference/msbuild-targets.md#packing-an-icon-image-file), takže nemusíte potřebovat externí adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c0e43-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="c0e43-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="c0e43-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="c0e43-118">Vylepšené zabezpečení pomocí SHA sledování a vynucení pro balíčky. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="c0e43-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="c0e43-119">Povolit vyřazení zastaralých a starších balíčků NuGet [#2867](https://github.com/NuGet/Home/issues/2867) | [blogový příspěvek](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](../nuget-org/deprecate-packages.md)</span><span class="sxs-lookup"><span data-stu-id="c0e43-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](../nuget-org/deprecate-packages.md)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c0e43-120">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="c0e43-120">Issues fixed in this release</span></span>

<span data-ttu-id="c0e43-121">**Štěnic**</span><span class="sxs-lookup"><span data-stu-id="c0e43-121">**Bugs**</span></span>

* <span data-ttu-id="c0e43-122">Balíčky NuGet vytvořené pomocí sady 3.0.100-preview9 SDK nemůžou používat uživatelé sady SDK 2,2... v závislosti na časovém pásmu [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="c0e43-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="c0e43-123">Uvozovky "znaky v cestě způsobují" nepovolené znaky v cestě "`nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="c0e43-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="c0e43-124">VS: sestavení jsou plně Ngen-Ed, ne částečně Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="c0e43-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="c0e43-125">Snižte využití paměti (odhlášení odběru událostí) – [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="c0e43-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="c0e43-126">Zpráva "Error_UnableToFindProjectInfo" není gramaticky správná – [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="c0e43-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="c0e43-127">Vylepšení NU1403 – ověřte všechny balíčky, včetně očekávaných nebo skutečných hodnot SHA- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="c0e43-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="c0e43-128">Více výčtu ve `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="c0e43-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="c0e43-129">Vrácení "> interní" změny v PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="c0e43-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="c0e43-130">IVsPackageSourceProvider. getsources (...) má nesprávně definované chování výjimky – [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="c0e43-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="c0e43-131">Vytvořte znovu PluginManager konstruktor – [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="c0e43-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="c0e43-132">Metriky pro sledování obnovovací frekvence uživatelského rozhraní PM – [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="c0e43-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="c0e43-133">Při instalaci prostřednictvím uživatelského rozhraní Správce balíčků snížit počet aktualizací uživatelského rozhraní [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="c0e43-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="c0e43-134">Telemetrie: hodnoty DateTime používají formáty specifické pro jazykovou verzi – [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="c0e43-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="c0e43-135">Omezení aktualizací uživatelského rozhraní na kartě Procházet uživatelského rozhraní Správce balíčků #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="c0e43-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="c0e43-136">[Selhání testu] "Nelze analyzovat konfigurační soubor", zobrazí se výzva dvakrát [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="c0e43-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="c0e43-137">Vyvolejte NU5037 chybu se správnou stránkou dokumentu, která vysvětluje opravy zákazníků (v balíčku chybí požadovaný soubor nuspec) – [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="c0e43-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="c0e43-138">V případě změny RuntimeIdentifier projektu se obnovení uzamčeného režimu nepovede – [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="c0e43-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="c0e43-139">Nastavit čtení nastavení v VS-opožděné [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="c0e43-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="c0e43-140">Regrese v `Nuget sources add` způsobí, že znak ":", šestnáctková hodnota 0x3A, nemůže být zahrnutá v názvu "Errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="c0e43-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="c0e43-141">Zprostředkovatelé přihlašovacích údajů plug-in NuGet – skrýt okno procesu – [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="c0e43-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="c0e43-142">Vynutilí PackagePathResolver je absolutní cesta – [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="c0e43-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="c0e43-143">Omezení aktualizací uživatelského rozhraní na kartách instalace a aktualizace uživatelského rozhraní Správce balíčků – [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="c0e43-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="c0e43-144">**DCR**</span><span class="sxs-lookup"><span data-stu-id="c0e43-144">**DCR:**</span></span>

* <span data-ttu-id="c0e43-145">Aktualizace rozhraní Xamarin pro mapování na NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="c0e43-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="c0e43-146">Povolit kopírování obsahu okna Preview správce balíčků pro Install/Update- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="c0e43-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="c0e43-147">Povolit obnovení souborů. proj – [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="c0e43-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="c0e43-148">Zavedení `NUGET_NETFX_PLUGIN_PATHS` a `NUGET_NETCORE_PLUGIN_PATHS` pro podporu konfigurace současně [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="c0e43-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="c0e43-149">Povolit více verzí pro PackageDownload pomocí atributu Version- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="c0e43-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="c0e43-150">Možnosti Add-SolutionDirectory a-PackageDirectory do NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="c0e43-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="c0e43-151">**[Seznam všech problémů opravených v této verzi – 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="c0e43-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="c0e43-152">Shrnutí: co je nového v 5.3.1.</span><span class="sxs-lookup"><span data-stu-id="c0e43-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="c0e43-153">Modul plug-in: úloha byla zrušena. zrušení vlivu na vytvoření instance modulu plug-in [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="c0e43-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="c0e43-154">Úloha obnovení nemůže být bezpečně spuštěna dvakrát v jednom procesu (při použití zprostředkovatelů pověření) – [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="c0e43-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
