---
title: dopad Project.JSON autory balíčku NuGet
description: Podrobnosti o jak provádění project.json v NuGet 3.x ovlivňuje balíček autoři, jako jsou nepodporované funkce, obsah a formát balíčků.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 8c85c1a89469c491c6be1f81961197450744349c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545570"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="d4e1b-103">Dopad project.json při vytváření balíčků</span><span class="sxs-lookup"><span data-stu-id="d4e1b-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="d4e1b-104">Tento obsah je zastaralý.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-104">This content is deprecated.</span></span> <span data-ttu-id="d4e1b-105">Projekty by měl použít buď `packages.config` nebo PackageReference formátů.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="d4e1b-106">`project.json` Systému NuGet 3 + ovlivňuje autory balíčku několika způsoby, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="d4e1b-107">Změny ovlivňující existující balíčky využití</span><span class="sxs-lookup"><span data-stu-id="d4e1b-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="d4e1b-108">Tradiční balíčky NuGet podporují sadu funkcí, které nejsou přeneseny do světa tranzitivní.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="d4e1b-109">Instalace a odinstalace skripty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="d4e1b-110">Model tranzitivní obnovení, je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "čas instalace balíčku".</span><span class="sxs-lookup"><span data-stu-id="d4e1b-110">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="d4e1b-111">Balíček je k dispozici nebo není k dispozici, ale neexistuje žádný konzistentní proces, ke které dojde při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="d4e1b-112">Také nainstalujte skripty byly podporovány pouze v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="d4e1b-113">Jiná Integrovaná vývojová prostředí museli napodobení rozšiřitelnost sady Visual Studio rozhraní API, pokusí se podporují tyto skripty a bez podpory nebyl k dispozici v běžných editorů a nástroje příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="d4e1b-114">Transformace obsahu nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-114">Content transforms are not supported</span></span>

<span data-ttu-id="d4e1b-115">Podobně jako u skriptů instalace, transformace spustit na balíček nainstalovat a obvykle nejsou idempotentní.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="d4e1b-116">Protože neexistuje žádný čas instalace už, XDT transformaci a podobné funkce nejsou podporované a jsou ignorovány, pokud takové balíčku se používá v případě přechodné.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="d4e1b-117">Obsah</span><span class="sxs-lookup"><span data-stu-id="d4e1b-117">Content</span></span>

<span data-ttu-id="d4e1b-118">Tradiční balíčky NuGet dodávají soubory obsahu, jako je zdrojový kód a konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="d4e1b-119">Zde jsou obvykle nepoužívá ve dvou scénářích:</span><span class="sxs-lookup"><span data-stu-id="d4e1b-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="d4e1b-120">Počáteční soubory přetáhnout do projektu, aby uživatel mohl upravit později.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="d4e1b-121">Běžným příkladem je výchozí konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="d4e1b-122">Soubory obsahu použít jako companions pro sestavení nainstalovaná v projektu.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="d4e1b-123">Tento příklad by obrázek loga používané sestavení.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="d4e1b-124">Podpora pro obsah je aktuálně zakázáno podobné z důvodů pro skripty a transformace, ale Připravujeme k navrhování podpory pro obsah.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="d4e1b-125">Obsah souborů stále se dá provést uvnitř balíčky a ignorují aktuálně, ale koncový uživatel může stále zkopírují se do správné místo.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="d4e1b-126">Můžete sledovat některé návrhy přináší zpět soubory obsahu a postupujte podle jeho průběh, tady: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="d4e1b-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="d4e1b-127">Dopad pro autory balíčku</span><span class="sxs-lookup"><span data-stu-id="d4e1b-127">Impact for package authors</span></span>

<span data-ttu-id="d4e1b-128">Balíčky pomocí výše uvedené funkce byste měli používat jiný mechanismus.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="d4e1b-129">Nejčastěji užitečné mechanismus by nástroj MSBuild cíle/vlastnosti, které nadále Získejte plnou podporu.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="d4e1b-130">Systém sestavení můžete ke sbírání jiné konvence v balíčku.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="d4e1b-131">To je, jak jsou cíle nástroje MSBuild podporované a také analyzátory Roslyn.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="d4e1b-132">Je možné sestavovat balíčky, které podporuje cíle a analyzátory pro `packages.config` a `project.json` scénáře.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="d4e1b-133">Balíčky, které se pokusí změnit projekt k usnadnění spuštění obvykle fungují v velmi omezená sada scénářů a by měl místo toho zadejte soubor readme nebo pokyny o tom, jak pomocí balíčku.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="d4e1b-134">Většina stávajících balíčků by neměl muset použít balíček formátu popsaném níže.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="d4e1b-135">Formát umožňuje nativní obsah jako první třídy scénář.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="d4e1b-136">To znamená, že spravovaná sestavení závisí na blízko hardwaru implementace dodávat binární implementace spolu s spravovaná sestavení založené na cílové platformě.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="d4e1b-137">Třeba balíček System.IO.Compression využívá tuto technologii.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="d4e1b-138">V souhrnu Pokud výše uvedené funkce není nezbytně nutné, doporučujeme nastolit existující balíček formátu, formátu popsaném tady podporuje pouze NuGet 3.x+.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="d4e1b-139">Je možné vytvořit balíčky pro obě `packages.config` a `project.json` scénáře prostřednictvím překrývá se, ale často je jednodušší právě strukturovat balíčky tradičním způsobem, bez zastaralých funkcí uvedených výše.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="d4e1b-140">Formát balíčku 3.x</span><span class="sxs-lookup"><span data-stu-id="d4e1b-140">3.x package format</span></span>

<span data-ttu-id="d4e1b-141">Formát balíčku 3.x umožňuje některé další funkce nad rámec NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="d4e1b-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="d4e1b-142">Definování referenční sestavení při kompilaci a sadu sestavení implementace používá pro modul runtime na různých platformách a zařízeních.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="d4e1b-143">Tomu můžete využít výhod platformy konkrétní rozhraní API poskytuje běžné plochy pro vaše zákazníky.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="d4e1b-144">Konkrétně to usnadňuje vytváření zprostředkující přenosné knihovny jednodušší.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="d4e1b-145">Umožňuje balíčky zaměření na platformách, například operační systémy nebo architekturu procesoru.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="d4e1b-146">Umožňuje oddělit implementace pro konkrétní platformy doprovodná balíčků.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="d4e1b-147">Nativní závislosti služeb podpory jako doma.</span><span class="sxs-lookup"><span data-stu-id="d4e1b-147">Support Native dependencies as a first class citizen.</span></span>
