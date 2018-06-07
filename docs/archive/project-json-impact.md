---
title: Project.JSON dopad na autoři balíček NuGet
description: Podrobnosti o tom, jak implementace project.json v NuGet 3.x ovlivňuje balíček autoři, jako je například nepodporované funkce, obsahu a formátu balíčku.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3236846864483b2e4f8bdaca2fe285ecc571b415
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818526"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="ed8a7-103">Dopad project.json při vytváření balíčků</span><span class="sxs-lookup"><span data-stu-id="ed8a7-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="ed8a7-104">Tento obsah je zastaralý.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-104">This content is deprecated.</span></span> <span data-ttu-id="ed8a7-105">Projekty využít buď `packages.config` nebo PackageReference formáty.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="ed8a7-106">`project.json` Systém používaný v NuGet 3 + ovlivňuje balíček autoři několika způsoby, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="ed8a7-107">Změny, které mají vliv na použití existujícího balíčky</span><span class="sxs-lookup"><span data-stu-id="ed8a7-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="ed8a7-108">Tradiční balíčky NuGet podporovat sadu funkcí, které nejsou přenášejí do přenositelné world.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="ed8a7-109">Instalace a odinstalace skripty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="ed8a7-110">Model obnovení přenositelné popsané v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "čas instalace balíčku".</span><span class="sxs-lookup"><span data-stu-id="ed8a7-110">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="ed8a7-111">Balíček není přítomen nebo není přítomné, ale neexistuje žádný konzistentní proces, který nastane, když je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="ed8a7-112">Navíc instalace skripty byly podporovány pouze v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="ed8a7-113">Další integrovaného vývojového prostředí měla model rozšiřitelnosti Visual Studio rozhraní API se pokusit o podporu takové skripty a bez podpory nebylo k dispozici v běžné editory a nástroje příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="ed8a7-114">Transformace obsahu nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-114">Content transforms are not supported</span></span>

<span data-ttu-id="ed8a7-115">Podobně jako nainstaluje skripty, transformací spustit na balíček nainstalovat a nejsou obvykle idempotent.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="ed8a7-116">Vzhledem k tomu, že už žádný čas instalace se transformace XDT a podobné funkce nejsou podporovány a jsou ignorovány, pokud takové balíčku se používá ve scénáři přenositelné.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="ed8a7-117">Obsah</span><span class="sxs-lookup"><span data-stu-id="ed8a7-117">Content</span></span>

<span data-ttu-id="ed8a7-118">Tradiční balíčky NuGet jsou distribuovat soubory obsahu, jako je například zdrojového kódu a konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="ed8a7-119">Zde jsou obvykle se používá ve dvou scénářích:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="ed8a7-120">Počáteční soubory vyřadit do projektu, takže uživatel může upravit později.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="ed8a7-121">Častým příkladem je výchozí konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="ed8a7-122">Soubory obsahu použít jako companions na sestavení nainstalované v projektu.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="ed8a7-123">V příkladu v tomto poli může být obrázek loga používané sestavení.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="ed8a7-124">Podpora pro obsah je nyní zakázána pro podobné důvody pro skripty a transformace, ale Snažíme se vyřešit navrhování podporu pro obsah.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="ed8a7-125">Obsah souborů se dá pořád provést uvnitř balíčky a ignorují aktuálně, ale koncový uživatel kopírovat je na správné místo.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="ed8a7-126">Najdete v jednom návrhů přináší zpět soubory obsahu a postupujte podle jeho průběh zde: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="ed8a7-127">Dopad pro autory balíčku</span><span class="sxs-lookup"><span data-stu-id="ed8a7-127">Impact for package authors</span></span>

<span data-ttu-id="ed8a7-128">Balíčky pomocí výše uvedené funkce muset použít jiný mechanismus.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="ed8a7-129">Nejčastěji užitečné mechanismus by MSBuild cíle nebo props, které nadále získat plně podporované.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="ed8a7-130">Můžete zvolit systém sestavení vyzvedávat další konvence v balíčku.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="ed8a7-131">Toto je, jak jsou podporovány cíle MSBuild a také Roslyn analyzátorů.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="ed8a7-132">Je možné vytvořit balíčky, které podporuje cíle a analyzátory pro `packages.config` a `project.json` scénáře.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="ed8a7-133">Balíčky, které se pokusí změnit projekt, který má obvykle usnadňují spuštění ve velmi omezená sada scénářů fungovat a musí místo toho zadejte readme nebo pokyny o tom, jak pomocí balíčku.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="ed8a7-134">Většina stávajících balíčků by neměl muset použít formát balíčku, který je popsaný níže.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="ed8a7-135">Formát umožňuje nativní obsah jako první třídy scénáře.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="ed8a7-136">To znamená, že spravovaná sestavení závisí na blízko implementace hardwaru pro odeslání binární implementace spolu s spravované sestavení založená na cílové platformy.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="ed8a7-137">System.IO.Compression balíčku je třeba využitím této technologie.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="ed8a7-138">V souhrnu Pokud funkci výše není nezbytně nutné, doporučujeme provedením vykrvovacího vpichu s formátem existující balíček jako formát popsaný v tomto poli je podporován pouze NuGet 3.x+.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="ed8a7-139">Je možné vytvořit balíčky pro obě `packages.config` a `project.json` scénáře prostřednictvím shimming, ale je často jednodušší právě struktury balíčky tradičním způsobem, bez zastaralých funkcí uvedených výše.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="ed8a7-140">Formát balíčku 3.x</span><span class="sxs-lookup"><span data-stu-id="ed8a7-140">3.x package format</span></span>

<span data-ttu-id="ed8a7-141">Formát balíčku 3.x umožňuje několika další funkce nad rámec NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="ed8a7-142">Definování referenční sestavení používá pro kompilaci a sadu sestavení implementace používá pro modul runtime na různých platformách nebo zařízení.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="ed8a7-143">Která umožňuje využít výhod platformy konkrétní rozhraní API při současném poskytování běžné útoku pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="ed8a7-144">Konkrétně to usnadňuje vytváření zprostředkující přenosné knihovny jednodušší.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="ed8a7-145">Umožňuje balíčky do otáčení na platformách, například operační systémy nebo architekturu procesoru.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="ed8a7-146">Umožňuje oddělení platformy konkrétní implementace doprovodné balíčky.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="ed8a7-147">Jako první třídy občanem podporují nativní závislosti.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-147">Support Native dependencies as a first class citizen.</span></span>
