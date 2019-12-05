---
title: Zpráva k vydání verze NuGet 1,3
description: Poznámky k verzi pro NuGet 1,3, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825261"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="5a18f-103">Zpráva k vydání verze NuGet 1,3</span><span class="sxs-lookup"><span data-stu-id="5a18f-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="5a18f-104">[Poznámky k verzi nuget 1,2](../release-notes/nuget-1.2.md) | zpráva k [vydání verze NuGet 1,4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="5a18f-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="5a18f-105">NuGet 1,3 byl vydán 25. dubna 2011.</span><span class="sxs-lookup"><span data-stu-id="5a18f-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="5a18f-106">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="5a18f-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="5a18f-107">Zjednodušené vytváření balíčků s integrací serveru symbolů</span><span class="sxs-lookup"><span data-stu-id="5a18f-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="5a18f-108">Tým NuGet spolupracuje s lidé na [SymbolSource.org](http://www.symbolsource.org/) , který nabízí opravdu jednoduchý způsob publikování vašich zdrojů a PDB spolu s balíčkem.</span><span class="sxs-lookup"><span data-stu-id="5a18f-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="5a18f-109">To umožňuje uživatelům vašeho balíčku krokovat se se zdrojem balíčku v ladicím programu.</span><span class="sxs-lookup"><span data-stu-id="5a18f-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="5a18f-110">Další podrobnosti najdete v [tématu Vytvoření a publikování balíčku symbolů](../create-packages/symbol-packages.md) snadný způsob, jak publikovat balíčky NuGet se zdroji.</span><span class="sxs-lookup"><span data-stu-id="5a18f-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="5a18f-111">Můžete také sledovat živou ukázku této funkce jako součást NuGet v podrobném hovoru na Mix11.</span><span class="sxs-lookup"><span data-stu-id="5a18f-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="5a18f-112">Tato funkce je plně znázorněna na začátku 20 minut videa.</span><span class="sxs-lookup"><span data-stu-id="5a18f-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="5a18f-113">`Open-PackagePage` – příkaz</span><span class="sxs-lookup"><span data-stu-id="5a18f-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="5a18f-114">Tento příkaz usnadňuje zobrazení stránky projektu pro balíček v konzole správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="5a18f-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="5a18f-115">Poskytuje taky možnosti pro otevření adresy URL licence a stránky pro zneužití sestav pro daný balíček.</span><span class="sxs-lookup"><span data-stu-id="5a18f-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="5a18f-116">Syntaxe příkazu je:</span><span class="sxs-lookup"><span data-stu-id="5a18f-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="5a18f-117">Možnost `-PassThru` slouží k vrácení hodnoty zadané adresy URL.</span><span class="sxs-lookup"><span data-stu-id="5a18f-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="5a18f-118">Příklady:</span><span class="sxs-lookup"><span data-stu-id="5a18f-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="5a18f-119">Otevře prohlížeč na adrese URL projektu zadané v balíčku Ninject.</span><span class="sxs-lookup"><span data-stu-id="5a18f-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="5a18f-120">Otevře prohlížeč na adrese URL licence zadané v balíčku Ninject.</span><span class="sxs-lookup"><span data-stu-id="5a18f-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="5a18f-121">Otevře prohlížeč na adrese URL v aktuálním zdroji balíčků, který se používá k nahlášení zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="5a18f-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="5a18f-122">Přiřadí adresu URL licence k proměnné, $url, bez otevření adresy URL v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="5a18f-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="5a18f-123">Zvýšení výkonu</span><span class="sxs-lookup"><span data-stu-id="5a18f-123">Performance Improvements</span></span>

<span data-ttu-id="5a18f-124">NuGet 1,3 zavádí spoustu vylepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="5a18f-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="5a18f-125">NuGet 1,3 vylučuje stažení stejné verze balíčku několikrát zahrnutím místní mezipaměti pro jednotlivé uživatele.</span><span class="sxs-lookup"><span data-stu-id="5a18f-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="5a18f-126">Mezipaměť je k dispozici a vymazána prostřednictvím dialogového okna nastavení správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="5a18f-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Dialogové okno Možnosti NuGet s nastavením mezipaměti pro balíčky](./media/nuget-options.png)

<span data-ttu-id="5a18f-128">Další vylepšení výkonu zahrnuje přidání podpory pro kompresi HTTP a vylepšení rychlosti instalace balíčku v rámci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a18f-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="5a18f-129">Sada Visual Studio a nástroj NuGet. exe používá stejný seznam zdrojů balíčků</span><span class="sxs-lookup"><span data-stu-id="5a18f-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="5a18f-130">Před NuGet 1,3 se seznam zdrojů balíčků používaných nástrojem NuGet. exe a doplňku NuGet pro Visual Studio neuložil na stejném místě.</span><span class="sxs-lookup"><span data-stu-id="5a18f-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="5a18f-131">NuGet 1,3 teď používá stejný seznam na obou místech.</span><span class="sxs-lookup"><span data-stu-id="5a18f-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="5a18f-132">Seznam je uložený v `NuGet.Config` a uložený ve složce sady data.</span><span class="sxs-lookup"><span data-stu-id="5a18f-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="5a18f-133">NuGet. exe ignoruje soubory a složky, které ve výchozím nastavení začínají na.</span><span class="sxs-lookup"><span data-stu-id="5a18f-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="5a18f-134">Aby mohla aplikace NuGet dobře fungovat se systémy správy zdrojového kódu, například s podverzemi a Mercurial, nástroje NuGet. exe při vytváření balíčků ignoruje složky a soubory, které začínají znakem ".".</span><span class="sxs-lookup"><span data-stu-id="5a18f-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="5a18f-135">To lze přepsat pomocí dvou nových příznaků:</span><span class="sxs-lookup"><span data-stu-id="5a18f-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="5a18f-136">__-NoDefaultExcludes__ se používá k přepsání tohoto nastavení a zahrnutí všech souborů.</span><span class="sxs-lookup"><span data-stu-id="5a18f-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="5a18f-137">__– Vyloučení__ se používá k přidání dalších souborů nebo složek, které se mají vyloučit pomocí vzoru.</span><span class="sxs-lookup"><span data-stu-id="5a18f-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="5a18f-138">Například pro vyloučení všech souborů s příponou souboru. bak</span><span class="sxs-lookup"><span data-stu-id="5a18f-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="5a18f-139">_Poznámka: vzor není ve výchozím nastavení rekurzivní._</span><span class="sxs-lookup"><span data-stu-id="5a18f-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="5a18f-140">Podpora pro projekty WiX a rozhraní .NET Micro Framework</span><span class="sxs-lookup"><span data-stu-id="5a18f-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="5a18f-141">Díky komunitním příspěvkům zahrnuje NuGet podporu typů projektů WiX i rozhraní .NET Micro Framework.</span><span class="sxs-lookup"><span data-stu-id="5a18f-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="5a18f-142">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="5a18f-142">Bug Fixes</span></span>

<span data-ttu-id="5a18f-143">Úplný seznam oprav chyb najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="5a18f-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="5a18f-144">Opravy chyb zaznamenaly</span><span class="sxs-lookup"><span data-stu-id="5a18f-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="5a18f-145">Balíčky se zdrojovými soubory fungují na webech i v projektech webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="5a18f-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="5a18f-146">Zdrojové soubory pro websites se zkopírují do složky `App_Code`</span><span class="sxs-lookup"><span data-stu-id="5a18f-146">For Websites, source files are copied into the `App_Code` folder</span></span>
