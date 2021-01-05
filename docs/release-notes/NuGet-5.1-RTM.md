---
title: Poznámky k verzi NuGet 5,1 RTM
description: Poznámky k verzi pro NuGet 5,1, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699857"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="a47b6-103">Zpráva k vydání verze NuGet 5,1</span><span class="sxs-lookup"><span data-stu-id="a47b6-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="a47b6-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="a47b6-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a47b6-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="a47b6-105">NuGet version</span></span> | <span data-ttu-id="a47b6-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a47b6-106">Available in Visual Studio version</span></span>| <span data-ttu-id="a47b6-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a47b6-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="a47b6-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="a47b6-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a47b6-109">Visual Studio 2019 verze 16,1</span><span class="sxs-lookup"><span data-stu-id="a47b6-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a47b6-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a47b6-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="a47b6-111"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="a47b6-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="a47b6-112"><sup>2</sup> . K dispozici jako volitelná instalace se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="a47b6-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="a47b6-113">Shrnutí: Novinky v 5,1</span><span class="sxs-lookup"><span data-stu-id="a47b6-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="a47b6-114">Podpora pro přeskočení nabízených oznámení balíčku, pokud už existuje, aby bylo možné lepší integraci s pracovními postupy CI/CD – [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="a47b6-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="a47b6-115">Visual Studio teď nabízí pohodlný odkaz na stránku Galerie nuget.org balíčku – [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="a47b6-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="a47b6-116">Podpora nových prostředků .NET Core 3,0, jako jsou například [cílené balíčky](https://github.com/dotnet/cli/issues/10006) a [sady runtime](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="a47b6-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="a47b6-117">Sada NuGet Pack a podpora obnovení pro FrameworkReferences, aby bylo možné povolit cílení a běhové odkazy na balíčky – [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="a47b6-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="a47b6-118">Podpora "stažení pouze" balíčku s PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="a47b6-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="a47b6-119">Vylučte za běhu a cílení balíčků z výsledků hledání & obnovení grafu pomocí PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="a47b6-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a47b6-120">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="a47b6-120">Issues fixed in this release</span></span>

<span data-ttu-id="a47b6-121">**Štěnic**</span><span class="sxs-lookup"><span data-stu-id="a47b6-121">**Bugs**</span></span>

* <span data-ttu-id="a47b6-122">Moduly plug-in: ztráty podrobností výjimky během vytváření modulu plug-in – [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="a47b6-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="a47b6-123">Rozsah PackageReference s výhradním dolním limitem nefunguje, pokud dolní hranice je k dispozici na jednom ze zdrojů.</span><span class="sxs-lookup"><span data-stu-id="a47b6-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="a47b6-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="a47b6-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="a47b6-125">Vylepšit zprávu IsPackableFalseError [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="a47b6-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="a47b6-126">Soubor zámku balíčků – při změně grafu projektu znovu vygeneruje soubor zámku – [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="a47b6-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="a47b6-127">ProjectSystem Chyba: balíčky NuGet získávají Automatické odebrání – [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="a47b6-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="a47b6-128">Přidejte cíl pro vrácení FrameworkReference, který se podobá CollectPackageDownloads a CollectPackageReferences- [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="a47b6-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="a47b6-129">Mezipaměť HTTP: prostředek RepositoryResources není uložený v mezipaměti způsobem, který je ve verzi [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="a47b6-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="a47b6-130">Protokolování: výjimka zásobníky volání není hlášena s detailní podrobností – [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="a47b6-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="a47b6-131">Změňte všechny adresy URL dokumentů NuGet na použití HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="a47b6-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="a47b6-132">Vylepšit zprávu upozornění NU3024 – [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="a47b6-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="a47b6-133">Při odebrání packagereference zamknout soubor bez aktualizace – [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="a47b6-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="a47b6-134">Zlepšení zpracování případných chyb při ověřování licenseurl a licenčního prvku v nuspec- [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="a47b6-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="a47b6-135">PM uživatelské rozhraní: klikněte pravým tlačítkem na záhlaví karty a kliknutím na Otevřít umístění souboru dojde k chybě – [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="a47b6-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="a47b6-136">Moduly plug-in: protokol, když se proces modulu plug-in ukončí – [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="a47b6-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="a47b6-137">Moduly plug-in: vysoká míra kolizí při protokolování hodnot DateTime – [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="a47b6-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="a47b6-138">Manifest. ReadFrom se nezdařil při každém nuspec s LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="a47b6-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="a47b6-139">RestoreLockedMode: Neočekávaná NU1004 při ProjectReference odkazuje na projekt s vlastním AssemblyName- [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="a47b6-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="a47b6-140">Lepší chybová zpráva, když spuštění modulu plug-in selhává s výjimkou [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="a47b6-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="a47b6-141">Při obnovení NoOp Vyhněte se tomu \* .dgspec.jspři zápisu do adresáře obj – [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="a47b6-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="a47b6-142">GeneratePathProperty = true nemůže generovat vlastnost při neshodě případu – [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="a47b6-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="a47b6-143">Nastavení: neplatný znak v cestě zdroje balíčku může selhat a [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="a47b6-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="a47b6-144">Pokud se soubor zámku odstraní, obnovení negeneruje soubor zámku na NoOp- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="a47b6-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="a47b6-145">Adresa URL licence a licence způsobily chybu čtení s metadaty [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="a47b6-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="a47b6-146">Neošetřené výjimky v V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="a47b6-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="a47b6-147">nuget.exe vrátí ukončovací kód nula pro neplatné argumenty – [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="a47b6-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="a47b6-148">Aktualizace chyb a varovných dokumentů pro vyjádření souvisejících scénářů podepisování – [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="a47b6-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="a47b6-149">Soubor prostředků by měl použít relativní cesty, aby bylo možné přesouvat projekty snadněji [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="a47b6-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="a47b6-150">**Chcete odeslat obecnou**</span><span class="sxs-lookup"><span data-stu-id="a47b6-150">**DCRs**</span></span>

* <span data-ttu-id="a47b6-151">Moduly plug-in: povolení protokolování diagnostiky – [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="a47b6-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="a47b6-152">Nastavte Tizen 6 na NetStandard 2,1 – [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="a47b6-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="a47b6-153">**[Seznam všech problémů opravených v této verzi – 5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="a47b6-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
