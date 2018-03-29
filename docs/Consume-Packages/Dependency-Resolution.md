---
title: Balíček NuGet závislostí řešení | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Informace o procesu, pomocí kterého se balíček NuGet závislosti vyřešen a nainstalované v obou NuGet 2.x a NuGet 3.x+.
keywords: Závislosti balíčků NuGet, Správa verzí NuGet, verze závislosti, verze grafu, verze rozlišení, přenositelné obnovení
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: d387acd369c88a64abaa2cb94a913fe211df8da1
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="56211-104">Jak NuGet řeší závislosti balíčků</span><span class="sxs-lookup"><span data-stu-id="56211-104">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="56211-105">Vždy, když je balíček nainstalován, nebo přeinstalovat, včetně instaluje jako součást [obnovení](../consume-packages/package-restore.md) procesu NuGet nainstaluje také všechny další balíčky, na kterých závisí tento první balíček.</span><span class="sxs-lookup"><span data-stu-id="56211-105">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="56211-106">Tyto okamžité závislosti potom také může mít závislosti na jejich vlastní, které můžete pokračovat v libovolné hloubka.</span><span class="sxs-lookup"><span data-stu-id="56211-106">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="56211-107">To vytváří, co se nazývá *graf závislostí* která popisuje vztahy mezi balíčky na všech úrovních.</span><span class="sxs-lookup"><span data-stu-id="56211-107">This produces what's called a *dependency graph* that describes the relationships between packages at all levels.</span></span>

<span data-ttu-id="56211-108">Pokud více balíčků stejné závislosti, pak stejné ID balíčku může vyskytovat v grafu vícekrát, potenciálně s omezeními jinou verzi.</span><span class="sxs-lookup"><span data-stu-id="56211-108">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="56211-109">Jenom jedna verze nástroje daného balíčku můžete však použít v projektu, tak NuGet, musíte zvolit, která verze se má použít.</span><span class="sxs-lookup"><span data-stu-id="56211-109">However, only one version of a given package can be used in a project, so NuGet must choose which version is used.</span></span> <span data-ttu-id="56211-110">Přesný postup závisí na formátu správu balíčku, který je používán.</span><span class="sxs-lookup"><span data-stu-id="56211-110">The exact process depends on the package management format being used.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="56211-111">Řešení závislostí s PackageReference</span><span class="sxs-lookup"><span data-stu-id="56211-111">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="56211-112">Při instalaci balíčků do projektů formátu PackageReference, NuGet přidá reference na graf ploché balíčku v příslušný soubor a řeší konflikty předem.</span><span class="sxs-lookup"><span data-stu-id="56211-112">When installing packages into projects using the PackageReference format, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="56211-113">Tento proces se označuje jako *přenositelné obnovení*.</span><span class="sxs-lookup"><span data-stu-id="56211-113">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="56211-114">Přeinstalovat nebo při obnovování balíčků je pak proces stahování balíčky uvedené v tomto grafu, výsledkem je rychlejší a předvídatelnější sestavení.</span><span class="sxs-lookup"><span data-stu-id="56211-114">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="56211-115">Můžete také využít výhod zástupný znak (plovoucí) verze, jako je například 2.8. \*, zabraňující nákladné a Chyba volání náchylné k chybám `nuget update` na klientské počítače a servery sestavení.</span><span class="sxs-lookup"><span data-stu-id="56211-115">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="56211-116">Když je proces obnovení NuGet spuštěna před sestavení, nejprve přeloží závislosti v paměti a pak zapíše výsledný grafu do souboru s názvem `project.assets.json` v `obj` složky projektu pomocí PackageReference.</span><span class="sxs-lookup"><span data-stu-id="56211-116">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json` in the `obj` folder of a project using PackageReference.</span></span> <span data-ttu-id="56211-117">MSBuild pak přečte tento soubor a překládá do sady složek, kde naleznete potenciální odkazy a přidá je do stromu projektu v paměti.</span><span class="sxs-lookup"><span data-stu-id="56211-117">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="56211-118">Soubor zámků je dočasný a by neměly být přidávány do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="56211-118">The lock file is temporary and should not be added to source control.</span></span> <span data-ttu-id="56211-119">Je uvedena ve výchozím nastavení v obou `.gitignore` a `.tfignore`.</span><span class="sxs-lookup"><span data-stu-id="56211-119">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="56211-120">V tématu [balíčky a Správa zdrojového kódu](packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="56211-120">See [Packages and source control](packages-and-source-control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="56211-121">Pravidla řešení závislostí</span><span class="sxs-lookup"><span data-stu-id="56211-121">Dependency resolution rules</span></span>

<span data-ttu-id="56211-122">Přenositelné obnovení používá čtyři hlavní pravidla o vyřešení závislostí: nejnižší příslušné verze, plovoucí verze, nejbližší wins a cousin závislosti.</span><span class="sxs-lookup"><span data-stu-id="56211-122">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="56211-123">Nejnižší příslušné verze</span><span class="sxs-lookup"><span data-stu-id="56211-123">Lowest applicable version</span></span>

<span data-ttu-id="56211-124">Nejnižší verze příslušné pravidlo obnoví nejnižší verzi balíčku podle definice jeho závislé součásti.</span><span class="sxs-lookup"><span data-stu-id="56211-124">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="56211-125">Platí také pro závislosti na aplikaci nebo knihovny tříd Pokud deklarovaný jako [plovoucí](#floating-versions).</span><span class="sxs-lookup"><span data-stu-id="56211-125">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="56211-126">Na následujícím obrázku například 1.0 beta je považováno za nižší než 1.0, NuGet zvolí 1.0 verze:</span><span class="sxs-lookup"><span data-stu-id="56211-126">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![Výběr nejnižší příslušné verze](media/projectJson-dependency-1.png)

<span data-ttu-id="56211-128">Na obrázku další verze 2.1 není k dispozici na informační kanál, ale protože je omezení verze > = 2.1 vyskladnění NuGet další nejnižší verze můžete najít v tomto případě 2.2:</span><span class="sxs-lookup"><span data-stu-id="56211-128">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![Výběr další dostupná na informační kanál nejnižší verze](media/projectJson-dependency-2.png)

<span data-ttu-id="56211-130">Pokud aplikace určuje přesné číslo verze protokolu, například 1.2, který není k dispozici na informační kanál, NuGet selže s chybou při pokusu o instalaci nebo obnovení balíčku:</span><span class="sxs-lookup"><span data-stu-id="56211-130">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![NuGet vygeneruje chybu, když je přesný balíčku verze není k dispozici](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="56211-132">Plovoucí verze (zástupný znak)</span><span class="sxs-lookup"><span data-stu-id="56211-132">Floating (wildcard) versions</span></span>

<span data-ttu-id="56211-133">Číslo s plovoucí čárkou nebo zástupné verze závislosti zadaný \* zástupný znak, stejně jako u 6.0.\*.</span><span class="sxs-lookup"><span data-stu-id="56211-133">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="56211-134">Tato verze specifikace říká "použít nejnovější verzi 6.0.x"; 4.\* znamená "pomocí nejnovější verze 4.x."</span><span class="sxs-lookup"><span data-stu-id="56211-134">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="56211-135">Pomocí zástupného znaku umožňuje závislost balíčku pokračujte vyvíjející se bez nutnosti změny spotřebitelskou aplikaci (nebo balíček).</span><span class="sxs-lookup"><span data-stu-id="56211-135">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="56211-136">Pokud používáte zástupný znak, NuGet řeší nejvyšší verzi balíčku, který odpovídá vzorku verze, například 6.0. \* získá nejvyšší verzi balíčku, který začíná 6.0:</span><span class="sxs-lookup"><span data-stu-id="56211-136">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![Výběr verze 6.0.1 při plovoucí verze 6.0. \* se požaduje](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="56211-138">Informace o chování zástupné znaky a předběžných verzí, naleznete v části [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="56211-138">For information on the behavior of wildcards and pre-release versions, see [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="56211-139">Nejbližší wins</span><span class="sxs-lookup"><span data-stu-id="56211-139">Nearest wins</span></span>

<span data-ttu-id="56211-140">Když graf balíčku pro aplikace obsahuje různé verze stejného balíčku, NuGet zvolí balíček, který je nejblíže k aplikaci v grafu a všechny ostatní ignoruje.</span><span class="sxs-lookup"><span data-stu-id="56211-140">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="56211-141">Toto chování umožňuje aplikaci přepsat všechny verze konkrétní balíček v grafu závislostí.</span><span class="sxs-lookup"><span data-stu-id="56211-141">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="56211-142">V následujícím příkladu je aplikace závislá přímo na balíček B s omezením na verzi > = 2.0.</span><span class="sxs-lookup"><span data-stu-id="56211-142">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="56211-143">Aplikace také závisí na balíčku A, což pak také závisí na balíčku B, ale s > = 1.0 omezení.</span><span class="sxs-lookup"><span data-stu-id="56211-143">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="56211-144">Protože závislost na balíček B 2.0 je blíže aplikace v grafu, že verze se má použít:</span><span class="sxs-lookup"><span data-stu-id="56211-144">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![Aplikace pomocí pravidla nejbližší služby Wins](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="56211-146">Pravidlo nejbližší Wins může způsobit přechod na nižší verzi balíčku, proto potenciálně nejnovější Další závislosti v grafu.</span><span class="sxs-lookup"><span data-stu-id="56211-146">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="56211-147">Proto je použito toto pravidlo upozornění k upozornění uživatele.</span><span class="sxs-lookup"><span data-stu-id="56211-147">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="56211-148">Toto pravidlo také výsledkem vyšší efektivity s velké závislost grafu (jako jsou ty balíčky BCL), protože po dané závislost je ignorován, NuGet ignoruje všechny zbývající závislosti na tuto větev grafu.</span><span class="sxs-lookup"><span data-stu-id="56211-148">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="56211-149">V následujícím diagramu například, protože se používá balíček C 2.0, NuGet ignoruje větve v grafu, které odkazují na starší verzi balíčku C:</span><span class="sxs-lookup"><span data-stu-id="56211-149">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![Při NuGet ignoruje balíček v grafu, je ignorováno uvedené celý pobočky](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="56211-151">Cousin závislosti</span><span class="sxs-lookup"><span data-stu-id="56211-151">Cousin dependencies</span></span>

<span data-ttu-id="56211-152">Pokud jiný balíček verze jsou uvedené ve stejné vzdálenosti v grafu z aplikace, NuGet použije nejnižší verze, která splňuje všechny požadavky verze (stejně jako u [nejnižší příslušné verze](#lowest-applicable-version) a [ plovoucí verze](#floating-versions) pravidla).</span><span class="sxs-lookup"><span data-stu-id="56211-152">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="56211-153">Na obrázku níže například verze 2.0 balíček B splňuje dalších > = 1.0 omezení a je tedy používá:</span><span class="sxs-lookup"><span data-stu-id="56211-153">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![Řešení závislostí cousin pomocí nižší verzi, která splňuje všechna omezení](media/projectJson-dependency-7.png)

<span data-ttu-id="56211-155">V některých případech není možné splňují všechny požadavky verze.</span><span class="sxs-lookup"><span data-stu-id="56211-155">In some cases, it's not possible to meet all version requirements.</span></span> <span data-ttu-id="56211-156">Jak je uvedeno níže, pokud balíček A vyžaduje přesně balíček B 1.0 a C balíčku vyžaduje balíček B > = 2.0, pak NuGet nelze vyřešit závislosti a ohlásí chybu.</span><span class="sxs-lookup"><span data-stu-id="56211-156">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![Nepřeložitelný závislosti z důvodu požadavku na přesnou verzi](media/projectJson-dependency-8.png)

<span data-ttu-id="56211-158">V těchto situacích nejvyšší úrovně příjemce (aplikace nebo balíčku) přidejte vlastní přímé závislost na balíček B tak, aby [nejbližší Wins](#nearest-wins) pravidlo vztahuje.</span><span class="sxs-lookup"><span data-stu-id="56211-158">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="56211-159">Řešení závislostí s souboru Packages.config je.</span><span class="sxs-lookup"><span data-stu-id="56211-159">Dependency resolution with packages.config</span></span>

<span data-ttu-id="56211-160">S `packages.config`, závislosti projektu se zapisují do `packages.config` jako plochý seznam.</span><span class="sxs-lookup"><span data-stu-id="56211-160">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="56211-161">Všechny závislosti tyto balíčky se zapisují taky ve stejném seznamu.</span><span class="sxs-lookup"><span data-stu-id="56211-161">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="56211-162">Při instalaci balíčků NuGet může také upravit `.csproj` souboru `app.config`, `web.config`a další jednotlivé soubory.</span><span class="sxs-lookup"><span data-stu-id="56211-162">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="56211-163">S `packages.config`, NuGet pokusí o řešení konfliktů závislostí při instalaci jednotlivých jednotlivých balíčků.</span><span class="sxs-lookup"><span data-stu-id="56211-163">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="56211-164">To znamená, pokud balíček A probíhá instalace a závisí na balíčku B a B balíček je již uveden v `packages.config` jako závislost něco jiného, porovná verze balíčku B požadovanou NuGet a pokusí se najít na verzi, která splňuje všechny verze omezení.</span><span class="sxs-lookup"><span data-stu-id="56211-164">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="56211-165">Konkrétně NuGet vybere dolní *major.minor* verzi, která splňuje závislosti.</span><span class="sxs-lookup"><span data-stu-id="56211-165">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="56211-166">Ve výchozím nastavení, NuGet 2.8 vyhledá nejnižší verze oprava (najdete v části [poznámky k verzi NuGet 2.8](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span><span class="sxs-lookup"><span data-stu-id="56211-166">By default, NuGet 2.8 looks for the lowest patch version (see [NuGet 2.8 release notes](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span></span> <span data-ttu-id="56211-167">Můžete řídit prostřednictvím toto nastavení `DependencyVersion` atribut `Nuget.Config` a `-DependencyVersion` přepnout na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="56211-167">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="56211-168">`packages.config` Zpracování pro řešení závislostí získá složitý pro větší grafy závislostí.</span><span class="sxs-lookup"><span data-stu-id="56211-168">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="56211-169">Každé nové instalace balíčku vyžaduje přecházení přes celou grafu a vyvolá riziko pro konflikty verzí.</span><span class="sxs-lookup"><span data-stu-id="56211-169">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="56211-170">Když dojde ke konfliktu, instalace se zastaví, nechat projektu v neurčitém stavu, zejména s potenciální úpravy samotný soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="56211-170">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="56211-171">Nejedná se o problém při použití jiných formátů balíček správy.</span><span class="sxs-lookup"><span data-stu-id="56211-171">This is not an issue when using other package management formats.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="56211-172">Správa závislostí prostředky</span><span class="sxs-lookup"><span data-stu-id="56211-172">Managing dependency assets</span></span>

<span data-ttu-id="56211-173">Při použití formátu PackageReference, můžete určit, které prostředky z toku závislosti do nejvyšší úrovně projektu.</span><span class="sxs-lookup"><span data-stu-id="56211-173">When using the PackageReference format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="56211-174">Podrobnosti najdete v tématu [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="56211-174">For details, see [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="56211-175">Pokud nejvyšší úrovně projektu samotné je balíček, máte také kontrolu nad tento tok pomocí `include` a `exclude` atributy s uvedené v závislosti `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="56211-175">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="56211-176">V tématu [příponou .nuspec odkaz - závislosti](../reference/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="56211-176">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="56211-177">S výjimkou odkazy</span><span class="sxs-lookup"><span data-stu-id="56211-177">Excluding references</span></span>

<span data-ttu-id="56211-178">Existují scénáře, ve kterých sestavení se stejným názvem může odkazovat více než jednou v projektu generovala chyby při návrhu a čase vytvoření buildu.</span><span class="sxs-lookup"><span data-stu-id="56211-178">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="56211-179">Zvažte projekt, který obsahuje vlastní verzi `C.dll`a odkazuje na C balíček, který také obsahuje `C.dll`.</span><span class="sxs-lookup"><span data-stu-id="56211-179">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="56211-180">Ve stejnou dobu, projekt také závisí na balíčku B, který také závisí na balíčku C a `C.dll`.</span><span class="sxs-lookup"><span data-stu-id="56211-180">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="56211-181">V důsledku toho by který NuGet nelze určit `C.dll` chcete použít, ale projektu závislost na balíček C nelze právě odebrat, protože balíček B také na něm závisí.</span><span class="sxs-lookup"><span data-stu-id="56211-181">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="56211-182">Chcete-li tento problém vyřešili, musíte přímý odkaz `C.dll` mají (nebo použijte jiný balíček, který odkazuje na ten správný) a potom ho přidat závislost na C balíček, který vyloučí všechny její prostředky.</span><span class="sxs-lookup"><span data-stu-id="56211-182">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="56211-183">To v závislosti na formátu balíček správy používá provádí následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="56211-183">This is done as follows depending on the package management format in use:</span></span>

- <span data-ttu-id="56211-184">[PackageReference](../consume-packages/package-references-in-project-files.md): Přidejte `Exclude="All"` v závislost:</span><span class="sxs-lookup"><span data-stu-id="56211-184">[PackageReference](../consume-packages/package-references-in-project-files.md): add `Exclude="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- <span data-ttu-id="56211-185">`packages.config`: odeberte odkaz na PackageC z `.csproj` tak, aby odkazuje jenom verze `C.dll` , které chcete.</span><span class="sxs-lookup"><span data-stu-id="56211-185">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="56211-186">Instalace aktualizací závislostí během balíčku</span><span class="sxs-lookup"><span data-stu-id="56211-186">Dependency updates during package install</span></span> 

<span data-ttu-id="56211-187">Pokud už je splnit verze závislosti, není během instalace dalších balíčků aktualizovat závislost.</span><span class="sxs-lookup"><span data-stu-id="56211-187">If a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> <span data-ttu-id="56211-188">Představte si třeba balíček A, který závisí na balíčku B a určuje 1.0 pro číslo verze.</span><span class="sxs-lookup"><span data-stu-id="56211-188">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="56211-189">Zdrojové úložiště obsahuje verze 1.0, 1.1 a 1.2 balíčku B. Pokud A je nainstalován v projektu, který již obsahuje B verze 1.0, pak B 1.0 dál používá vzhledem k tomu, že splňují omezení verze.</span><span class="sxs-lookup"><span data-stu-id="56211-189">The source repository contains versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B 1.0 remains in use because it satisfies the version constraint.</span></span> <span data-ttu-id="56211-190">Ale pokud balíček A měli požadavky verze 1.1 nebo vyšší b, B 1.2 by možné nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="56211-190">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="56211-191">Řešení chyb při nekompatibilní balíčku</span><span class="sxs-lookup"><span data-stu-id="56211-191">Resolving incompatible package errors</span></span>

<span data-ttu-id="56211-192">Během balíček operaci obnovení, mohou se zobrazit chyba "jeden nebo více balíčků nejsou kompatibilní...", nebo balíček "není kompatibilní" s cílový framework projektu na.</span><span class="sxs-lookup"><span data-stu-id="56211-192">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="56211-193">K této chybě dojde, když jeden nebo více balíčků, kterou se odkazuje v projektu neoznačují podporují cílový framework projektu na; To znamená, balíček neobsahuje vhodný knihovny DLL v jeho `lib` složku pro cílové rozhraní, které je kompatibilní s projektu.</span><span class="sxs-lookup"><span data-stu-id="56211-193">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="56211-194">(Viz [cílové architektury](../reference/target-frameworks.md) seznam.)</span><span class="sxs-lookup"><span data-stu-id="56211-194">(See [Target frameworks](../reference/target-frameworks.md) for a list.)</span></span> 

<span data-ttu-id="56211-195">Například, pokud cíle projektu `netstandard1.6` a zkusíte nainstalovat balíček, který obsahuje knihovny DLL v pouze `lib\net20` a `\lib\net45` složky a potom zobrazit zprávy jako pro balíček a případně jeho položky závislé na následující:</span><span class="sxs-lookup"><span data-stu-id="56211-195">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you see messages like the following for the package and possibly its dependents:</span></span>

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

<span data-ttu-id="56211-196">Pro vyřešení problémům s kompatibilitou, proveďte jednu z těchto možností:</span><span class="sxs-lookup"><span data-stu-id="56211-196">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="56211-197">Změňte cíl projektu pro rozhraní, které podporuje balíčky, které chcete použít.</span><span class="sxs-lookup"><span data-stu-id="56211-197">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="56211-198">Obraťte se na autora balíčků a pracovat s nimi přidání podpory pro vaši zvolenou framework.</span><span class="sxs-lookup"><span data-stu-id="56211-198">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="56211-199">Každý balíček výpis stránky na [nuget.org](https://www.nuget.org/) má **kontaktujte vlastníky** odkaz pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="56211-199">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>

