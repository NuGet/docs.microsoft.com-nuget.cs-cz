---
title: Poznámky k verzi 1.3 NuGet
description: Zpráva k vydání verze pro NuGet 1.3, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551348"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="2478d-103">Poznámky k verzi 1.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="2478d-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="2478d-104">[Zpráva k vydání verze NuGet 1.2](../release-notes/nuget-1.2.md) | [zpráva k vydání verze NuGet 1.4](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="2478d-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="2478d-105">NuGet 1.3 byla vydána 25. dubna 2011.</span><span class="sxs-lookup"><span data-stu-id="2478d-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="2478d-106">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="2478d-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="2478d-107">Zjednodušené vytváření balíčků s integrací serveru symbolů</span><span class="sxs-lookup"><span data-stu-id="2478d-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="2478d-108">Tým NuGet ve spolupráci s lidé na [SymbolSource.org](http://www.symbolsource.org/) nabízí opravdu jednoduchý způsob publikování zdrojů a souboru PDB. spolu s vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="2478d-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="2478d-109">To umožňuje uživatelům balíčku můžete krokovat s vnořením zdroj balíčku v ladicím programu.</span><span class="sxs-lookup"><span data-stu-id="2478d-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="2478d-110">Další podrobnosti najdete v článku [vytváření a publikování balíčku symbolů](../create-packages/symbol-packages.md) snadný způsob, jak publikovat balíčky NuGet se zdroji.</span><span class="sxs-lookup"><span data-stu-id="2478d-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="2478d-111">Můžete také sledovat živé ukázku této funkce jako součást balíčku NuGet do hloubky komunikovat na Mix11.</span><span class="sxs-lookup"><span data-stu-id="2478d-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="2478d-112">Tato funkce je znázorněn plně od 20 minut označte videa.</span><span class="sxs-lookup"><span data-stu-id="2478d-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="2478d-113">`Open-PackagePage` Příkaz</span><span class="sxs-lookup"><span data-stu-id="2478d-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="2478d-114">Tento příkaz umožňuje snadno získat na stránce projektu pro balíček z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="2478d-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="2478d-115">Poskytuje také možnosti Otevřít adresu URL licence a zneužití stránky sestavy pro balíček.</span><span class="sxs-lookup"><span data-stu-id="2478d-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="2478d-116">Syntaxe příkazu je:</span><span class="sxs-lookup"><span data-stu-id="2478d-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="2478d-117">`-PassThru` Možnost se používá k vrácení hodnoty zadané adresy URL.</span><span class="sxs-lookup"><span data-stu-id="2478d-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="2478d-118">Příklady:</span><span class="sxs-lookup"><span data-stu-id="2478d-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="2478d-119">Otevře prohlížeč na adrese URL projektu zadané v balíčku Ninject.</span><span class="sxs-lookup"><span data-stu-id="2478d-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="2478d-120">Otevře prohlížeč na adrese URL licence zadané v balíčku Ninject.</span><span class="sxs-lookup"><span data-stu-id="2478d-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="2478d-121">Otevře prohlížeč na adrese URL u aktuálního zdroje balíčku použitého k oznámení zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="2478d-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="2478d-122">Přiřadí proměnné $url adresu URL licence bez otevření této adresy URL v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="2478d-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="2478d-123">Zvýšení výkonu</span><span class="sxs-lookup"><span data-stu-id="2478d-123">Performance Improvements</span></span>

<span data-ttu-id="2478d-124">NuGet 1.3 přináší spoustu vylepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="2478d-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="2478d-125">NuGet 1.3 se vyhnete stahování stejnou verzi balíčku více než jednou zahrnutím mezipaměti místního uživatele.</span><span class="sxs-lookup"><span data-stu-id="2478d-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="2478d-126">Mezipaměti můžete přistupovat a vymaže přes dialogové okno Nastavení správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="2478d-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Dialogové okno Možnosti NuGet s nastavení mezipaměti balíčku](./media/nuget-options.png)

<span data-ttu-id="2478d-128">Další vylepšení výkonu zahrnují přidání podpory pro kompresi HTTP a vylepšení rychlosti instalaci balíčku sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2478d-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="2478d-129">Visual Studio a nuget.exe používá stejný seznam zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="2478d-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="2478d-130">Před NuGet 1.3 seznam zdroje balíčků, které používají nuget.exe a NuGet Visual Studio Add-In nebyly uloženy na stejném místě.</span><span class="sxs-lookup"><span data-stu-id="2478d-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="2478d-131">NuGet 1.3 nyní používá stejný seznam na obou místech.</span><span class="sxs-lookup"><span data-stu-id="2478d-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="2478d-132">Seznam je uložen v `NuGet.Config` a uložené ve složce data aplikací.</span><span class="sxs-lookup"><span data-stu-id="2478d-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="2478d-133">nuget.exe ignoruje soubory a složky, které začínají znakem '.' ve výchozím nastavení</span><span class="sxs-lookup"><span data-stu-id="2478d-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="2478d-134">Aby NuGet dobře fungují s systémy správy zdrojového kódu takové Subversion nebo Mercurial nuget.exe ignoruje složky a soubory, které začínají "." znaku při vytváření balíčků.</span><span class="sxs-lookup"><span data-stu-id="2478d-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="2478d-135">To lze přepsat pomocí dvou nových příznaky:</span><span class="sxs-lookup"><span data-stu-id="2478d-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="2478d-136">__-NoDefaultExcludes__ se používá pro toto nastavení přepsat a zahrnují všechny soubory.</span><span class="sxs-lookup"><span data-stu-id="2478d-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="2478d-137">__-Vyloučení__ se používá k přidání dalších souborů a složek na vyloučit pomocí vzoru.</span><span class="sxs-lookup"><span data-stu-id="2478d-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="2478d-138">Třeba vyloučit všechny soubory s příponou ".bak.</span><span class="sxs-lookup"><span data-stu-id="2478d-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="2478d-139">_Poznámka: vzor není rekurzivní ve výchozím nastavení._</span><span class="sxs-lookup"><span data-stu-id="2478d-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="2478d-140">Podpora pro projekty WiX a Micro rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2478d-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="2478d-141">Díky příspěvky vytvořené komunitou NuGet zahrnuje podporu pro typy projektů WiX, jakož i rozhraní .NET Framework Micro.</span><span class="sxs-lookup"><span data-stu-id="2478d-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="2478d-142">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="2478d-142">Bug Fixes</span></span>

<span data-ttu-id="2478d-143">Úplný seznam oprav chyb, podívejte se prosím [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="2478d-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="2478d-144">Opravy chyb za zmínku</span><span class="sxs-lookup"><span data-stu-id="2478d-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="2478d-145">Balíčky se zdrojovým souborem fungovat na obou webech a v projektech webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="2478d-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="2478d-146">Pro moduly Websites, zdrojové soubory jsou zkopírovány do `App_Code` složky</span><span class="sxs-lookup"><span data-stu-id="2478d-146">For Websites, source files are copied into the `App_Code` folder</span></span>
