---
title: project.json dopad na autory balíčků NuGet
description: Podrobnosti o tom, jak implementace project.json v NuGet 3.x ovlivňuje autory balíčků, jako jsou nepodporované funkce, obsah a formát balíčku.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488200"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="8297c-103">Dopad souboru project.json při vytváření balíčků</span><span class="sxs-lookup"><span data-stu-id="8297c-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="8297c-104">Tento obsah je zastaralé.</span><span class="sxs-lookup"><span data-stu-id="8297c-104">This content is deprecated.</span></span> <span data-ttu-id="8297c-105">Projekty by `packages.config` měly používat formáty nebo PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8297c-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="8297c-106">Systém `project.json` používaný v NuGet 3+ ovlivňuje autory balíčků několika způsoby, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="8297c-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="8297c-107">Změny ovlivňující použití existujících balíčků</span><span class="sxs-lookup"><span data-stu-id="8297c-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="8297c-108">Tradiční balíčky NuGet podporují sadu funkcí, které nejsou přeneseny do přenosného světa.</span><span class="sxs-lookup"><span data-stu-id="8297c-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="8297c-109">Instalace a odinstalace skriptů jsou ignorovány</span><span class="sxs-lookup"><span data-stu-id="8297c-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="8297c-110">Model přenosnéobnovení, popsané v [rozlišení závislostí](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "čas instalace balíčku".</span><span class="sxs-lookup"><span data-stu-id="8297c-110">The transitive restore model, described in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="8297c-111">Balíček je k dispozici nebo není k dispozici, ale neexistuje žádný konzistentní proces, ke kterému dochází při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="8297c-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="8297c-112">Instalační skripty byly také podporovány pouze v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8297c-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="8297c-113">Ostatní IDC musel zesměšňovat rozhraní API rozšiřitelnosti sady Visual Studio k pokusu o podporu těchto skriptů a žádná podpora byla k dispozici v běžných editorů a nástrojů příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="8297c-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="8297c-114">Transformace obsahu nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="8297c-114">Content transforms are not supported</span></span>

<span data-ttu-id="8297c-115">Podobně jako instalační skripty, transformace spustit při instalaci balíčku a obvykle nejsou idempotentní.</span><span class="sxs-lookup"><span data-stu-id="8297c-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="8297c-116">Vzhledem k tomu, že již neexistuje žádný čas instalace, XDT Transformace a podobné funkce nejsou podporovány a jsou ignorovány, pokud takový balíček se používá v přenositelném scénáři.</span><span class="sxs-lookup"><span data-stu-id="8297c-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="8297c-117">Obsah</span><span class="sxs-lookup"><span data-stu-id="8297c-117">Content</span></span>

<span data-ttu-id="8297c-118">Tradiční balíčky NuGet jsou odesílání souborů obsahu, jako je zdrojový kód a konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="8297c-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="8297c-119">Obvykle se používají ve dvou scénářích:</span><span class="sxs-lookup"><span data-stu-id="8297c-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="8297c-120">Počáteční soubory klesly do projektu, takže uživatel může upravit později.</span><span class="sxs-lookup"><span data-stu-id="8297c-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="8297c-121">Běžným příkladem jsou výchozí konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="8297c-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="8297c-122">Soubory obsahu používané jako doprovodné sestavení nainstalovaných v projektu.</span><span class="sxs-lookup"><span data-stu-id="8297c-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="8297c-123">Příkladem zde by byl obrázek loga používaný sestavením.</span><span class="sxs-lookup"><span data-stu-id="8297c-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="8297c-124">Podpora obsahu je v současné době zakázána z podobných důvodů pro skripty a transformace, ale jsme v procesu navrhování podpory obsahu.</span><span class="sxs-lookup"><span data-stu-id="8297c-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="8297c-125">Soubory obsahu mohou být stále přenášeny uvnitř balíčků a jsou v současné době ignorovány, ale koncový uživatel je stále může zkopírovat na správné místo.</span><span class="sxs-lookup"><span data-stu-id="8297c-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="8297c-126">Můžete vidět jeden z návrhů na vrácení souborů obsahu a sledovat [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)jeho průběh, zde: .</span><span class="sxs-lookup"><span data-stu-id="8297c-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="8297c-127">Dopad pro autory balíčků</span><span class="sxs-lookup"><span data-stu-id="8297c-127">Impact for package authors</span></span>

<span data-ttu-id="8297c-128">Balíčky používající výše uvedené funkce by musely používat jiný mechanismus.</span><span class="sxs-lookup"><span data-stu-id="8297c-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="8297c-129">Nejčastěji užitečný mechanismus pro to by msbuild cíle nebo rekvizity, které i nadále získat plně podporovány.</span><span class="sxs-lookup"><span data-stu-id="8297c-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="8297c-130">Systém sestavení můžete zvolit vyzvednout další konvence v balíčku.</span><span class="sxs-lookup"><span data-stu-id="8297c-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="8297c-131">Tímto způsobem jsou podporovány cíle MSBuild a analyzátory Roslyn.</span><span class="sxs-lookup"><span data-stu-id="8297c-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="8297c-132">Je možné vytvářet balíčky, které `packages.config` podporuje `project.json` cíle a analyzátory pro a scénáře.</span><span class="sxs-lookup"><span data-stu-id="8297c-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="8297c-133">Balíčky, které se pokoušejí upravit projekt pro usnadnění spuštění obvykle pracovat ve velmi omezené sadě scénářů a místo toho by měly poskytnout soubor readme nebo pokyny, jak použít balíček.</span><span class="sxs-lookup"><span data-stu-id="8297c-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="8297c-134">Většina existujících balíčků by neměla používat formát balíčku popsaný níže.</span><span class="sxs-lookup"><span data-stu-id="8297c-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="8297c-135">Formát umožňuje nativní obsah jako scénář první třídy.</span><span class="sxs-lookup"><span data-stu-id="8297c-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="8297c-136">To znamená, že spravovaná sestavení závisí na implementacich v blízkosti hardwaru pro dodávku binárních implementací spolu se spravovanými sestaveními založenými na cílové platformě.</span><span class="sxs-lookup"><span data-stu-id="8297c-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="8297c-137">Například System.IO.Compression balíček využívá tuto technologii.</span><span class="sxs-lookup"><span data-stu-id="8297c-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="8297c-138">Stručně řečeno, pokud výše uvedené funkce není nezbytně nutné, doporučujeme držet se stávající formát balíčku, jako formát popsaný zde je podporován pouze NuGet 3.x +.</span><span class="sxs-lookup"><span data-stu-id="8297c-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="8297c-139">Bylo by možné vytvářet balíčky `packages.config` `project.json` pro práci pro oba a scénáře prostřednictvím shimming, ale je to často jednodušší jen strukturovat balíčky tradičním způsobem, bez zastaralé funkce uvedené výše.</span><span class="sxs-lookup"><span data-stu-id="8297c-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="8297c-140">Formát balíčku 3.x</span><span class="sxs-lookup"><span data-stu-id="8297c-140">3.x package format</span></span>

<span data-ttu-id="8297c-141">Formát balíčku 3.x umožňuje několik dalších funkcí mimo NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="8297c-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="8297c-142">Definování referenčnísestavení používané pro kompilaci a sadu sestavení implementace používané pro runtime na různých platformách nebo zařízeních.</span><span class="sxs-lookup"><span data-stu-id="8297c-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="8297c-143">Což vám umožní využít výhod specifických pro platformu API a zároveň poskytuje společnou plochu pro vaše spotřebitele.</span><span class="sxs-lookup"><span data-stu-id="8297c-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="8297c-144">Konkrétně to usnadňuje psaní zprostředkujících přenosných knihoven.</span><span class="sxs-lookup"><span data-stu-id="8297c-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="8297c-145">Umožňuje, aby se balíčky otáčely na platformách, například na operačních systémech nebo architektuře procesoru.</span><span class="sxs-lookup"><span data-stu-id="8297c-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="8297c-146">Umožňuje oddělení implementace specifické pro platformu doprovodné balíčky.</span><span class="sxs-lookup"><span data-stu-id="8297c-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="8297c-147">Podpora nativní závislosti jako prvotřídní občan.</span><span class="sxs-lookup"><span data-stu-id="8297c-147">Support Native dependencies as a first class citizen.</span></span>
