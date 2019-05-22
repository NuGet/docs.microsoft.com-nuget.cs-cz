---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975850"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="a48d2-101">Poznámky k verzi 5.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="a48d2-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="a48d2-102">Distribuce vozidel NuGet:</span><span class="sxs-lookup"><span data-stu-id="a48d2-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a48d2-103">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="a48d2-103">NuGet version</span></span> | <span data-ttu-id="a48d2-104">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a48d2-104">Available in Visual Studio version</span></span>| <span data-ttu-id="a48d2-105">K dispozici v rozhraní .NET SDK, pomocí kterých</span><span class="sxs-lookup"><span data-stu-id="a48d2-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="a48d2-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="a48d2-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a48d2-107">Visual Studio 2019 version 16.1</span><span class="sxs-lookup"><span data-stu-id="a48d2-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a48d2-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a48d2-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="a48d2-109"><sup>1</sup>nainstalované s Visual Studio 2019 se sadou .NET Core</span><span class="sxs-lookup"><span data-stu-id="a48d2-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="a48d2-110"><sup>2</sup>dostupné jako volitelná instalace s Visual Studio 2019 se sadou .NET Core</span><span class="sxs-lookup"><span data-stu-id="a48d2-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="a48d2-111">Shrnutí: Co je nového v 5.1</span><span class="sxs-lookup"><span data-stu-id="a48d2-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="a48d2-112">Podpora přeskočit balíček push, pokud již existuje umožňující lepší integrace s pracovními postupy CI/CD - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="a48d2-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="a48d2-113">Visual Studio teď umožňuje pohodlný odkaz stránku Galerie nuget.org balíčku - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="a48d2-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="a48d2-114">Podpora pro nové materiály .NET Core 3.0 jako [Targeting Pack](https://github.com/dotnet/cli/issues/10006) a [balíčky Runtime](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="a48d2-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="a48d2-115">Balíček NuGet a obnovení podporu FrameworkReferences povolit cílení na modul runtime a odkazy na balíčky - [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="a48d2-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="a48d2-116">Podpora "stáhnout pouze" balíček scénářem PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="a48d2-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="a48d2-117">Modul runtime Exlcude a targeting Pack z výsledky hledání & obnovení grafu pomocí PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="a48d2-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a48d2-118">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="a48d2-118">Issues fixed in this release</span></span>

<span data-ttu-id="a48d2-119">**Chyby**</span><span class="sxs-lookup"><span data-stu-id="a48d2-119">**Bugs**</span></span>

* <span data-ttu-id="a48d2-120">Moduly plug-in: Podrobnosti o výjimce přijdete při vytváření modulu plug-in – [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="a48d2-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="a48d2-121">PackageReference rozsahu, s výhradním dolní mez nefunguje, pokud je dolní mez je k dispozici na jeden ze zdrojů.</span><span class="sxs-lookup"><span data-stu-id="a48d2-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="a48d2-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="a48d2-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="a48d2-123">Zlepšení IsPackableFalseError zpráva – [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="a48d2-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="a48d2-124">Zabalí zamknout soubor – soubor znovu vygenerovat zámku při změně projektu grafu – [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="a48d2-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="a48d2-125">ProjectSystem chyb: Balíčky Nuget získávání automaticky odebrány - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="a48d2-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="a48d2-126">Přidání cíle pro návrat FrameworkReference podobné CollectPackageDownloads a CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="a48d2-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="a48d2-127">HTTP mezipaměti:  Prostředek RepositoryResources neukládá do mezipaměti označené verzí způsobem – [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="a48d2-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="a48d2-128">Protokolování: zásobníky volání výjimky nejsou nahlásí se podrobné podrobností - [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="a48d2-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="a48d2-129">Změnit všechny adresy URL NuGet dokumentace pro použití protokolu HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="a48d2-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="a48d2-130">Zlepšení NU3024 upozornění - [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="a48d2-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="a48d2-131">soubor zámku není při aktualizaci packagereference odebrat - [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="a48d2-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="a48d2-132">Zlepšení zpracování případu chyb při ověřování elementu licenseurl a licence v souboru nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="a48d2-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="a48d2-133">Klikněte pravým tlačítkem na záhlaví karty a kliknutím na "Otevřít umístění souboru" výsledkem je chyba – uživatelské rozhraní odp. - [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="a48d2-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="a48d2-134">Moduly plug-in: přihlášení při ukončení procesu modulu plug-in – [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="a48d2-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="a48d2-135">Moduly plug-in: míra vysoké kolizí v hodnotách data a času protokolování - [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="a48d2-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="a48d2-136">Manifest.ReadFrom selže na libovolný soubor nuspec s LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="a48d2-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="a48d2-137">RestoreLockedMode: Neočekávané NU1004 když ProjectReference odkazuje na projekt s vlastní AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="a48d2-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="a48d2-138">Lepší chybové zprávy při spuštění modulu plug-in selže s výjimkou - [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="a48d2-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="a48d2-139">Vyhněte se při obnovení NoOp, \*. dgspec.json zápis v adresáři obj - [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="a48d2-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="a48d2-140">GeneratePathProperty = true nebude moci generovat vlastnost na velikosti písmen neshoda - [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="a48d2-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="a48d2-141">Nastavení: neplatný znak v cestě zdroje balíčku může dojít k selhání VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="a48d2-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="a48d2-142">Pokud soubor zámku se odstraní, obnovení nelze vytvořit soubor zámku na NoOp - [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="a48d2-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="a48d2-143">Adresa URL licence a licence způsobí, že čtení došlo k chybě s metadaty - [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="a48d2-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="a48d2-144">Neošetřené výjimky v V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="a48d2-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="a48d2-145">nuget.exe vrátí ukončovací kód nula při neplatných argumentech - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="a48d2-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="a48d2-146">Aktualizovat chyby a upozornění dokumentace tak, aby odrážely podpisový související scénáře - [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="a48d2-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="a48d2-147">Soubor prostředků by měl používat relativní cesty k přesunutí projekty povolit snadněji - [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="a48d2-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="a48d2-148">**Chcete**</span><span class="sxs-lookup"><span data-stu-id="a48d2-148">**DCRs**</span></span>

* <span data-ttu-id="a48d2-149">Moduly plug-in: povolení protokolování diagnostiky - [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="a48d2-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="a48d2-150">Zkontrolujte mapování Tizen 6 NetStandard 2.1 – [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="a48d2-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="a48d2-151">**[Seznam všech problémů, které jsou opravené v této verzi - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="a48d2-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
