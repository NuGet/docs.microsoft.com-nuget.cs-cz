---
title: "Poznámky k verzi NuGet 1.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d1c2191-783f-4faa-b72e-356a59323d39
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.3 NuGet."
keywords: "NuGet 1.3 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bc39efd5b9c550c3fdeddf9ad980c0bd9d4dcb3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="30206-104">1.3 poznámky NuGet</span><span class="sxs-lookup"><span data-stu-id="30206-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="30206-105">[Poznámky k verzi NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4 poznámky k verzi](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="30206-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="30206-106">NuGet 1.3 byla vydána 25 Duben 2011.</span><span class="sxs-lookup"><span data-stu-id="30206-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="30206-107">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="30206-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="30206-108">Zjednodušená vytvoření balíčku s integrací serveru – symbol</span><span class="sxs-lookup"><span data-stu-id="30206-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="30206-109">Týmem NuGet ve spolupráci s zaměstnance na [SymbolSource.org](http://www.symbolsource.org/) nabízet skutečně jednoduchý způsob publikování zdrojů a na PDB společně s vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="30206-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="30206-110">To umožňuje příjemci vašeho balíčku na krok do zdroje balíčku v ladicím programu.</span><span class="sxs-lookup"><span data-stu-id="30206-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="30206-111">Další informace najdete v [vytváření a publikování balíčku Symbol](../create-packages/symbol-packages.md) snadný způsob, jak publikovat balíčky NuGet se zdroji.</span><span class="sxs-lookup"><span data-stu-id="30206-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="30206-112">Můžete také shlédnout této funkce jako součást NuGet podrobněji za provozu ukázkový komunikovat v Mix11.</span><span class="sxs-lookup"><span data-stu-id="30206-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="30206-113">Tato funkce je plně ukázán začínající na 20 minut označit videa.</span><span class="sxs-lookup"><span data-stu-id="30206-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="30206-114">`Open-PackagePage`Příkaz</span><span class="sxs-lookup"><span data-stu-id="30206-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="30206-115">Tento příkaz lze snadno získat na stránku projektu pro balíček z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="30206-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="30206-116">Obsahuje také možnosti otevřete adresu URL licence a zneužití stránka sestavy pro daný balíček.</span><span class="sxs-lookup"><span data-stu-id="30206-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="30206-117">Syntaxe příkazu je:</span><span class="sxs-lookup"><span data-stu-id="30206-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="30206-118">`-PassThru` Možnost se používá k vrácení hodnoty zadané adresy URL.</span><span class="sxs-lookup"><span data-stu-id="30206-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="30206-119">Příklady:</span><span class="sxs-lookup"><span data-stu-id="30206-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="30206-120">Otevře prohlížeč na adrese URL projektu zadané v balíčku Ninject.</span><span class="sxs-lookup"><span data-stu-id="30206-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="30206-121">Otevře prohlížeč na adrese URL licence zadané v balíčku Ninject.</span><span class="sxs-lookup"><span data-stu-id="30206-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="30206-122">Otevře prohlížeč na adrese URL u aktuálního zdroje balíčku použitého k oznámení zneužití pro zadaný balíček.</span><span class="sxs-lookup"><span data-stu-id="30206-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="30206-123">Přiřadí proměnné $url adresu URL licence bez otevření této adresy URL v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="30206-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="30206-124">Zvýšení výkonu</span><span class="sxs-lookup"><span data-stu-id="30206-124">Performance Improvements</span></span>

<span data-ttu-id="30206-125">NuGet 1.3 představuje mnoho vylepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="30206-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="30206-126">NuGet 1.3 zabraňuje stahování stejnou verzi balíčku vícekrát zahrnutím mezipaměti místní jednotlivé uživatele.</span><span class="sxs-lookup"><span data-stu-id="30206-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="30206-127">Mezipaměti můžete získat přístup a vymazat prostřednictvím dialogu Nastavení správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="30206-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Dialogové okno Možnosti NuGet s nastavení mezipaměti balíčku](./media/nuget-options.png)

<span data-ttu-id="30206-129">Další vylepšení výkonu zahrnují přidání podpory pro komprese protokolu HTTP a vylepšení rychlosti instalace balíčku Visual Studia.</span><span class="sxs-lookup"><span data-stu-id="30206-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="30206-130">Visual Studio a nuget.exe používá stejný seznam zdroje balíčků</span><span class="sxs-lookup"><span data-stu-id="30206-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="30206-131">Před NuGet 1.3 nebyly uloženy seznam slouží jako nuget.exe a NuGet Visual Studio Add-In zdroje balíčku na stejném místě.</span><span class="sxs-lookup"><span data-stu-id="30206-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="30206-132">NuGet 1.3 teď používá stejný seznam na obou místech.</span><span class="sxs-lookup"><span data-stu-id="30206-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="30206-133">Seznam je uložen v `NuGet.Config` a uložen ve složce data aplikací.</span><span class="sxs-lookup"><span data-stu-id="30206-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="30206-134">nuget.exe ignoruje soubory a složky, které začínají s '.' ve výchozím nastavení</span><span class="sxs-lookup"><span data-stu-id="30206-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="30206-135">Aby bylo možné NuGet tyto Subversion a Mercurial funkce fungují dobře u zdrojových systémů řízení, nuget.exe ignoruje složek a souborů, které začínají '.' znak při vytváření balíčků.</span><span class="sxs-lookup"><span data-stu-id="30206-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="30206-136">To lze přepsat pomocí dva nové příznaky:</span><span class="sxs-lookup"><span data-stu-id="30206-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="30206-137">__-NoDefaultExcludes__ se používá pro toto nastavení přepsat a zahrnují všechny soubory.</span><span class="sxs-lookup"><span data-stu-id="30206-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="30206-138">__-Vyloučit__ se používá k přidání další soubory a složky, které chcete vyloučit pomocí vzoru.</span><span class="sxs-lookup"><span data-stu-id="30206-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="30206-139">Chcete-li například vyloučí všechny soubory s příponou souboru '.bak.</span><span class="sxs-lookup"><span data-stu-id="30206-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="30206-140">_Poznámka: vzoru není rekurzivní ve výchozím nastavení._</span><span class="sxs-lookup"><span data-stu-id="30206-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="30206-141">Podpora pro projekty WiX a malých rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="30206-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="30206-142">Díky komunitní příspěvky NuGet zahrnuje podporu pro typy projektů WiX, jakož i rozhraní .NET Framework Micro.</span><span class="sxs-lookup"><span data-stu-id="30206-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="30206-143">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="30206-143">Bug Fixes</span></span>

<span data-ttu-id="30206-144">Úplný seznam oprav chyb, zobrazte [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="30206-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="30206-145">Opravy chyb vhodné poznamenat</span><span class="sxs-lookup"><span data-stu-id="30206-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="30206-146">Balíčky s zdrojové soubory fungovat v obou webů a projekty webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="30206-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="30206-147">Pro weby, zdrojové soubory jsou kopírovány do `App_Code` složky</span><span class="sxs-lookup"><span data-stu-id="30206-147">For Websites, source files are copied into the `App_Code` folder</span></span>
