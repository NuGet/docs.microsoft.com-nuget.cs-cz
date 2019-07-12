---
title: Zpráva k vydání verze NuGet 5.1 RTM
description: Zpráva k vydání verze pro NuGet 5.1, včetně nové funkce, opravy chyb a chcete.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842581"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="34c95-103">Poznámky k verzi 5.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="34c95-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="34c95-104">Distribuce vozidel NuGet:</span><span class="sxs-lookup"><span data-stu-id="34c95-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="34c95-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="34c95-105">NuGet version</span></span> | <span data-ttu-id="34c95-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34c95-106">Available in Visual Studio version</span></span>| <span data-ttu-id="34c95-107">K dispozici v rozhraní .NET SDK, pomocí kterých</span><span class="sxs-lookup"><span data-stu-id="34c95-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="34c95-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="34c95-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="34c95-109">Visual Studio 2019 version 16.1</span><span class="sxs-lookup"><span data-stu-id="34c95-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="34c95-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="34c95-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="34c95-111"><sup>1</sup>nainstalované s Visual Studio 2019 se sadou .NET Core</span><span class="sxs-lookup"><span data-stu-id="34c95-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="34c95-112"><sup>2</sup>dostupné jako volitelná instalace s Visual Studio 2019 se sadou .NET Core</span><span class="sxs-lookup"><span data-stu-id="34c95-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="34c95-113">Shrnutí: Co je nového v 5.1</span><span class="sxs-lookup"><span data-stu-id="34c95-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="34c95-114">Podpora přeskočit balíček push, pokud již existuje umožňující lepší integrace s pracovními postupy CI/CD - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="34c95-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="34c95-115">Visual Studio teď umožňuje pohodlný odkaz stránku Galerie nuget.org balíčku - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="34c95-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="34c95-116">Podpora pro nové materiály .NET Core 3.0 jako [Targeting Pack](https://github.com/dotnet/cli/issues/10006) a [balíčky Runtime](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="34c95-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="34c95-117">Balíček NuGet a obnovení podporu FrameworkReferences povolit cílení na modul runtime a odkazy na balíčky - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="34c95-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="34c95-118">Podpora "stáhnout pouze" balíček scénářem PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="34c95-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="34c95-119">Modul runtime Exlcude a targeting Pack z výsledky hledání & obnovení grafu pomocí PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="34c95-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="34c95-120">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="34c95-120">Issues fixed in this release</span></span>

<span data-ttu-id="34c95-121">**Chyby**</span><span class="sxs-lookup"><span data-stu-id="34c95-121">**Bugs**</span></span>

* <span data-ttu-id="34c95-122">Moduly plug-in: Podrobnosti o výjimce přijdete při vytváření modulu plug-in – [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="34c95-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="34c95-123">PackageReference rozsahu, s výhradním dolní mez nefunguje, pokud je dolní mez je k dispozici na jeden ze zdrojů.</span><span class="sxs-lookup"><span data-stu-id="34c95-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="34c95-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="34c95-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="34c95-125">Zlepšení IsPackableFalseError zpráva – [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="34c95-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="34c95-126">Zabalí zamknout soubor – soubor znovu vygenerovat zámku při změně projektu grafu – [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="34c95-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="34c95-127">ProjectSystem chyb: Balíčky Nuget získávání automaticky odebrány - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="34c95-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="34c95-128">Přidání cíle pro návrat FrameworkReference podobné CollectPackageDownloads a CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="34c95-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="34c95-129">HTTP mezipaměti:  Prostředek RepositoryResources neukládá do mezipaměti označené verzí způsobem – [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="34c95-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="34c95-130">Protokolování: zásobníky volání výjimky nejsou nahlásí se podrobné podrobností - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="34c95-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="34c95-131">Změnit všechny adresy URL NuGet dokumentace pro použití protokolu HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="34c95-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="34c95-132">Zlepšení NU3024 upozornění - [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="34c95-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="34c95-133">soubor zámku není při aktualizaci packagereference odebrat - [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="34c95-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="34c95-134">Zlepšení zpracování případu chyb při ověřování elementu licenseurl a licence v souboru nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="34c95-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="34c95-135">Klikněte pravým tlačítkem na záhlaví karty a kliknutím na "Otevřít umístění souboru" výsledkem je chyba – uživatelské rozhraní odp. - [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="34c95-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="34c95-136">Moduly plug-in: přihlášení při ukončení procesu modulu plug-in – [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="34c95-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="34c95-137">Moduly plug-in: míra vysoké kolizí v hodnotách data a času protokolování - [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="34c95-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="34c95-138">Manifest.ReadFrom selže na libovolný soubor nuspec s LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="34c95-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="34c95-139">RestoreLockedMode: Neočekávané NU1004 když ProjectReference odkazuje na projekt s vlastní AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="34c95-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="34c95-140">Lepší chybové zprávy při spuštění modulu plug-in selže s výjimkou - [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="34c95-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="34c95-141">Vyhněte se při obnovení NoOp, \*. dgspec.json zápis v adresáři obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="34c95-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="34c95-142">GeneratePathProperty = true nebude moci generovat vlastnost na velikosti písmen neshoda - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="34c95-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="34c95-143">Nastavení: neplatný znak v cestě zdroje balíčku může dojít k selhání VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="34c95-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="34c95-144">Pokud soubor zámku se odstraní, obnovení nelze vytvořit soubor zámku na NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="34c95-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="34c95-145">Adresa URL licence a licence způsobí, že čtení došlo k chybě s metadaty - [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="34c95-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="34c95-146">Neošetřené výjimky v V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="34c95-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="34c95-147">nuget.exe vrátí ukončovací kód nula při neplatných argumentech - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="34c95-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="34c95-148">Aktualizovat chyby a upozornění dokumentace tak, aby odrážely podpisový související scénáře - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="34c95-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="34c95-149">Soubor prostředků by měl používat relativní cesty k přesunutí projekty povolit snadněji - [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="34c95-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="34c95-150">**Chcete**</span><span class="sxs-lookup"><span data-stu-id="34c95-150">**DCRs**</span></span>

* <span data-ttu-id="34c95-151">Moduly plug-in: povolení protokolování diagnostiky - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="34c95-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="34c95-152">Zkontrolujte mapování Tizen 6 NetStandard 2.1 – [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="34c95-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="34c95-153">**[Seznam všech problémů, které jsou opravené v této verzi - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="34c95-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
