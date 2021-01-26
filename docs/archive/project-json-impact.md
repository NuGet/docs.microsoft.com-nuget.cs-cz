---
title: project.jsdopad na autory balíčku NuGet
description: Podrobnosti o tom, jak implementace project.jsv nástroji NuGet 3. x ovlivňuje autory balíčků, jako jsou nepodporované funkce, obsah a formát balíčku.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 82b7ce7962ecccc9559ae25a8fe35a3820238049
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775394"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="42f2a-103">Dopad project.jsna při vytváření balíčků</span><span class="sxs-lookup"><span data-stu-id="42f2a-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="42f2a-104">Tento obsah je zastaralý.</span><span class="sxs-lookup"><span data-stu-id="42f2a-104">This content is deprecated.</span></span> <span data-ttu-id="42f2a-105">Projekty by měly používat buď `packages.config` formáty PackageReference nebo.</span><span class="sxs-lookup"><span data-stu-id="42f2a-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="42f2a-106">`project.json`Systém použitý v NuGet 3 + má vliv na autory balíčku několika způsoby, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="42f2a-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="42f2a-107">Změny ovlivňující existující využití balíčků</span><span class="sxs-lookup"><span data-stu-id="42f2a-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="42f2a-108">Tradiční balíčky NuGet podporují sadu funkcí, které se nepřenášejí do přenosného světa.</span><span class="sxs-lookup"><span data-stu-id="42f2a-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="42f2a-109">Skripty pro instalaci a odinstalaci se ignorují.</span><span class="sxs-lookup"><span data-stu-id="42f2a-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="42f2a-110">Model přenositelných obnovení, který je popsaný v tématu [řešení závislostí](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), nemá koncept "doba instalace balíčku".</span><span class="sxs-lookup"><span data-stu-id="42f2a-110">The transitive restore model, described in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="42f2a-111">Balíček je buď přítomen, nebo není přítomen, ale při instalaci balíčku se nevyskytnou žádné konzistentní procesy.</span><span class="sxs-lookup"><span data-stu-id="42f2a-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="42f2a-112">Také je možné nainstalovat skripty pouze v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42f2a-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="42f2a-113">Jiné IDEs muselo napodobovat rozhraní API rozšiřitelnosti sady Visual Studio, aby se pokusilo tyto skripty podporovat, a v běžných editorech a nástrojích příkazového řádku nebyla žádná podpora k dispozici.</span><span class="sxs-lookup"><span data-stu-id="42f2a-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="42f2a-114">Transformace obsahu nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="42f2a-114">Content transforms are not supported</span></span>

<span data-ttu-id="42f2a-115">Podobně jako při instalaci skriptů se transformace spouští při instalaci balíčku a obvykle se neidempotentní.</span><span class="sxs-lookup"><span data-stu-id="42f2a-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="42f2a-116">Vzhledem k tomu, že už není k dispozici žádný čas instalace, transformace XDT a podobné funkce se nepodporují a budou se ignorovat, pokud se takový balíček používá v přenosném scénáři.</span><span class="sxs-lookup"><span data-stu-id="42f2a-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="42f2a-117">Content</span><span class="sxs-lookup"><span data-stu-id="42f2a-117">Content</span></span>

<span data-ttu-id="42f2a-118">Tradiční balíčky NuGet jsou soubory obsahu, jako je zdrojový kód a konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="42f2a-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="42f2a-119">Obvykle se používají ve dvou scénářích:</span><span class="sxs-lookup"><span data-stu-id="42f2a-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="42f2a-120">Počáteční soubory vynechané do projektu, aby ji uživatel mohl později upravit.</span><span class="sxs-lookup"><span data-stu-id="42f2a-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="42f2a-121">Běžným příkladem jsou výchozí konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="42f2a-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="42f2a-122">Soubory obsahu používané jako doprovodné soubory pro sestavení nainstalovaná v projektu.</span><span class="sxs-lookup"><span data-stu-id="42f2a-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="42f2a-123">Příkladem může být obrázek loga používaný sestavením.</span><span class="sxs-lookup"><span data-stu-id="42f2a-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="42f2a-124">Podpora obsahu je v současné době zakázaná pro podobné důvody pro skripty a transformace, ale v procesu navrhování podpory obsahu.</span><span class="sxs-lookup"><span data-stu-id="42f2a-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="42f2a-125">Soubory obsahu je stále možné přenášet uvnitř balíčků a jsou v současné době ignorovány, ale koncový uživatel je stále může zkopírovat do správného místa.</span><span class="sxs-lookup"><span data-stu-id="42f2a-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="42f2a-126">Můžete si prohlédnout jeden z návrhů pro vracení souborů obsahu a postupovat podle jeho průběhu, tady: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627) .</span><span class="sxs-lookup"><span data-stu-id="42f2a-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="42f2a-127">Dopad pro autory balíčku</span><span class="sxs-lookup"><span data-stu-id="42f2a-127">Impact for package authors</span></span>

<span data-ttu-id="42f2a-128">Balíčky používající výše uvedené funkce by musely použít jiný mechanismus.</span><span class="sxs-lookup"><span data-stu-id="42f2a-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="42f2a-129">Nejefektivnějším užitečným mechanismem by byly cíle nebo props nástroje MSBuild, které budou nadále plně podporovány.</span><span class="sxs-lookup"><span data-stu-id="42f2a-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="42f2a-130">Systém sestavení se může rozhodnout v balíčku vybrat jiné konvence.</span><span class="sxs-lookup"><span data-stu-id="42f2a-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="42f2a-131">To je způsob, jakým jsou podporovány cíle nástroje MSBuild i analyzátory Roslyn.</span><span class="sxs-lookup"><span data-stu-id="42f2a-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="42f2a-132">Je možné vytvářet balíčky, které podporují cíle a analyzátory pro `packages.config` scénáře a `project.json` .</span><span class="sxs-lookup"><span data-stu-id="42f2a-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="42f2a-133">Balíčky, které se pokoušejí změnit projekt tak, aby se při spuštění normálně pracovaly v velmi omezené sadě scénářů, a místo toho byste měli zadat soubor Readme nebo pokyny k použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="42f2a-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="42f2a-134">Většina existujících balíčků by neměla vyžadovat použití formátu balíčku popsaného níže.</span><span class="sxs-lookup"><span data-stu-id="42f2a-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="42f2a-135">Formát umožňuje použití nativního obsahu jako první třídy.</span><span class="sxs-lookup"><span data-stu-id="42f2a-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="42f2a-136">To znamená, že spravovaná sestavení jsou závislá na konečné implementaci hardwaru pro dodávání binárních implementací společně se spravovanými sestaveními na základě cílové platformy.</span><span class="sxs-lookup"><span data-stu-id="42f2a-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="42f2a-137">Například System. IO. Compression balíček tuto technologii využívá.</span><span class="sxs-lookup"><span data-stu-id="42f2a-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="42f2a-138">V souhrnu Pokud výše uvedené funkce není nezbytně nutné, doporučujeme použít stávající formát balíčku, protože formát, který je zde popsán, je podporován pouze NuGet 3. x +.</span><span class="sxs-lookup"><span data-stu-id="42f2a-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="42f2a-139">Mohli byste sestavit balíčky, které budou fungovat jak pro scénáře, tak i `packages.config` `project.json` přes překrývá se, ale často je jednodušší jenom strukturovat balíčky tradičním způsobem, bez zastaralých funkcí uvedených výše.</span><span class="sxs-lookup"><span data-stu-id="42f2a-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="42f2a-140">3. x – formát balíčku</span><span class="sxs-lookup"><span data-stu-id="42f2a-140">3.x package format</span></span>

<span data-ttu-id="42f2a-141">Formát balíčku 3. x umožňuje několik dalších funkcí mimo NuGet 2. x:</span><span class="sxs-lookup"><span data-stu-id="42f2a-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="42f2a-142">Definování referenčního sestavení používaného pro kompilaci a sady implementačních sestavení používaných pro modul runtime na různých platformách/zařízeních.</span><span class="sxs-lookup"><span data-stu-id="42f2a-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="42f2a-143">Díky tomu můžete využít výhod rozhraní API specifických pro konkrétní platformu a zároveň zajistit pro svoje zákazníky společnou oblast Surface.</span><span class="sxs-lookup"><span data-stu-id="42f2a-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="42f2a-144">Konkrétně to usnadňuje psaní zprostředkujících přenosných knihoven.</span><span class="sxs-lookup"><span data-stu-id="42f2a-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="42f2a-145">Umožňuje balíčkům vytvářet na platformách, například operační systémy nebo architektura procesoru.</span><span class="sxs-lookup"><span data-stu-id="42f2a-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="42f2a-146">Umožňuje oddělení implementace specifických pro platformu pro doprovodné balíčky.</span><span class="sxs-lookup"><span data-stu-id="42f2a-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="42f2a-147">Podpora nativních závislostí jako první občan třídy.</span><span class="sxs-lookup"><span data-stu-id="42f2a-147">Support Native dependencies as a first class citizen.</span></span>
