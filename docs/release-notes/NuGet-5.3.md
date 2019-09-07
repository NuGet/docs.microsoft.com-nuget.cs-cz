---
title: Zpráva k vydání verze NuGet 5,3
description: Poznámky k verzi pro NuGet 5,3, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774099"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="07345-103">Zpráva k vydání verze NuGet 5,3</span><span class="sxs-lookup"><span data-stu-id="07345-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="07345-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="07345-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="07345-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="07345-105">NuGet version</span></span> | <span data-ttu-id="07345-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07345-106">Available in Visual Studio version</span></span>| <span data-ttu-id="07345-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="07345-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="07345-108">**5.3.0 – preview3**</span><span class="sxs-lookup"><span data-stu-id="07345-108">**5.3.0-preview3**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="07345-109">Visual Studio 2019 verze 16,3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="07345-109">Visual Studio 2019 version 16.3 Preview 3</span></span>](https://visualstudio.microsoft.com/vs/preview/) | <span data-ttu-id="07345-110">[3.0.100 – preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="07345-110">[3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |

<span data-ttu-id="07345-111"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="07345-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53-preview-3"></a><span data-ttu-id="07345-112">Shrnut Co je nového ve verzi 5,3 Preview 3</span><span class="sxs-lookup"><span data-stu-id="07345-112">Summary: What's New in 5.3 preview 3</span></span>

* <span data-ttu-id="07345-113">[Ikona balíčku se dá vložit do balíčku](../reference/msbuild-targets.md#packing-an-icon-image-file), takže nemusíte potřebovat externí adresu URL.</span><span class="sxs-lookup"><span data-stu-id="07345-113">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="07345-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="07345-114"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="07345-115">Vylepšené zabezpečení pomocí SHA sledování a vynucení pro balíčky. config- [#7281](https://github.com/NuGet/Home/issues/7281)</span><span class="sxs-lookup"><span data-stu-id="07345-115">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="07345-116">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="07345-116">Issues fixed in this release</span></span>

<span data-ttu-id="07345-117">**Štěnic**</span><span class="sxs-lookup"><span data-stu-id="07345-117">**Bugs**</span></span>

* <span data-ttu-id="07345-118">VS: sestavení jsou plně Ngen-Ed, ne částečně Ngen-Ed- [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="07345-118">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="07345-119">Snižte využití paměti (odhlášení odběru událostí) – [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="07345-119">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="07345-120">Zpráva "Error_UnableToFindProjectInfo" není gramaticky správná – [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="07345-120">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="07345-121">Vylepšení NU1403 – ověřte všechny balíčky, včetně očekávaných nebo skutečných hodnot SHA- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="07345-121">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="07345-122">Vícenásobné výčty v NuGetPackageManager. PreviewUpdatePackagesAsync- [#8401](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="07345-122">Multiple enumeration in NuGetPackageManager.PreviewUpdatePackagesAsync - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="07345-123">Vrácení "> interní" změny v PluginProcess- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="07345-123">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="07345-124">IVsPackageSourceProvider. getsources (...) má nesprávně definované chování výjimky – [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="07345-124">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="07345-125">Vytvořte znovu PluginManager konstruktor – [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="07345-125">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="07345-126">Metriky pro sledování obnovovací frekvence uživatelského rozhraní PM – [#8369](https://github.com/NuGet/Home/issues/8369)</span><span class="sxs-lookup"><span data-stu-id="07345-126">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="07345-127">Při instalaci prostřednictvím uživatelského rozhraní Správce balíčků snížit počet aktualizací uživatelského rozhraní [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="07345-127">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="07345-128">Telemetrie: hodnoty DateTime používají formáty specifické pro jazykovou verzi – [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="07345-128">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="07345-129">Omezení aktualizací uživatelského rozhraní na kartě Procházet uživatelského rozhraní Správce balíčků #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="07345-129">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="07345-130">[Selhání testu] "Nelze analyzovat konfigurační soubor", zobrazí se výzva dvakrát [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="07345-130">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="07345-131">Vyvolejte NU5037 chybu se správnou stránkou dokumentu, která vysvětluje opravy zákazníků (v balíčku chybí požadovaný soubor nuspec) – [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="07345-131">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="07345-132">V případě změny RuntimeIdentifier projektu se obnovení uzamčeného režimu nepovede – [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="07345-132">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="07345-133">Nastavit čtení nastavení v VS-opožděné [#8156](https://github.com/NuGet/Home/issues/8156)</span><span class="sxs-lookup"><span data-stu-id="07345-133">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="07345-134">Regrese v "zdrojů NuGet Add" způsobuje "znak", ":", šestnáctkovou hodnotu 0x3A, nelze zahrnout do názvu "Errors- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="07345-134">Regression in 'Nuget sources add' causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="07345-135">Zprostředkovatelé přihlašovacích údajů plug-in NuGet – skrýt okno procesu – [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="07345-135">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="07345-136">Vynutilí PackagePathResolver je absolutní cesta – [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="07345-136">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="07345-137">Omezení aktualizací uživatelského rozhraní na kartách instalace a aktualizace uživatelského rozhraní Správce balíčků – [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="07345-137">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="07345-138">**DCR**</span><span class="sxs-lookup"><span data-stu-id="07345-138">**DCR:**</span></span>

* <span data-ttu-id="07345-139">Aktualizace rozhraní Xamarin pro mapování na NetStandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)</span><span class="sxs-lookup"><span data-stu-id="07345-139">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="07345-140">Povolit kopírování obsahu okna Preview správce balíčků pro Install/Update- [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="07345-140">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="07345-141">Povolit obnovení souborů. proj – [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="07345-141">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="07345-142">Zavedení `NUGET_NETFX_PLUGIN_PATHS` a`NUGET_NETCORE_PLUGIN_PATHS` podpora konfigurace současně [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="07345-142">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="07345-143">Povolit více verzí pro PackageDownload pomocí atributu Version- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="07345-143">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="07345-144">Možnosti Add-SolutionDirectory a-PackageDirectory do NuGet. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)</span><span class="sxs-lookup"><span data-stu-id="07345-144">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

* <span data-ttu-id="07345-145">Povolit, aby balíček NuGet byl deterministický [#6229](https://github.com/NuGet/Home/issues/6229)</span><span class="sxs-lookup"><span data-stu-id="07345-145">Enable NuGet Pack to be deterministic - [#6229](https://github.com/NuGet/Home/issues/6229)</span></span>

<span data-ttu-id="07345-146">**[Seznam všech problémů opravených v této verzi – 5,3 Preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="07345-146">**[List of all issues fixed in this release - 5.3 preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>
