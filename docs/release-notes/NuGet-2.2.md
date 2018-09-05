---
title: Poznámky k verzi 2.2 NuGet
description: Zpráva k vydání verze pro NuGet 2.2 včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545989"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="a6d34-103">Poznámky k verzi 2.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="a6d34-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="a6d34-104">[Zpráva k vydání verze NuGet 2.1](../release-notes/nuget-2.1.md) | [zpráva k vydání verze NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="a6d34-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="a6d34-105">12. prosince 2012 byla vydána NuGet 2.2.</span><span class="sxs-lookup"><span data-stu-id="a6d34-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="a6d34-106">Snadné spuštění sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6d34-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="a6d34-107">Mezi nové funkce přidané v sadě Visual Studio 2012 byl [dialogové okno Snadné spuštění](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="a6d34-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="a6d34-108">NuGet 2.2 rozšiřuje toto dialogové okno, což umožňuje inicializovat dialogové okno Správce balíčků s hledaným výrazům zadali rychlé uvedení na trh.</span><span class="sxs-lookup"><span data-stu-id="a6d34-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="a6d34-109">Například zadání 'jquery' v panelu Snadné spuštění nyní zahrnuje možnost ve výsledcích hledání balíčků NuGet odpovídajících řetězci "jquery".</span><span class="sxs-lookup"><span data-stu-id="a6d34-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet v sadě Visual Studio snadného spuštění](./media/quick-launch.png)

<span data-ttu-id="a6d34-111">Výběrem této možnosti se spustí standardní NuGet package manager vyhledávání pro termín "jquery".</span><span class="sxs-lookup"><span data-stu-id="a6d34-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Dialogové okno Správce balíčků NuGet předvyplněný](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="a6d34-113">Zadejte celou složku pro obsah balíčku</span><span class="sxs-lookup"><span data-stu-id="a6d34-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="a6d34-114">NuGet 2.2 teď umožňuje zadat celou složku v `<file>` elementu `.nuspec` soubor obsahovat veškerý obsah této složky.</span><span class="sxs-lookup"><span data-stu-id="a6d34-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="a6d34-115">Například následující způsobí, že všechny skripty ve složce balíčku skripty mají být přidány do složky contents\scripts při instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="a6d34-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="a6d34-116">**Aktualizace 6/24/16: prázdné složky ve složce "obsah" jsou ignorovány při instalaci balíčku.**</span><span class="sxs-lookup"><span data-stu-id="a6d34-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="a6d34-117">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="a6d34-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="a6d34-118">Selhání instalace balíčku pro projekty F # při používání konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="a6d34-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="a6d34-119">Při pokusu o instalaci balíčku NuGet do projektu F # pomocí konzoly Správce balíčků, je vyvolána výjimka InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="a6d34-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="a6d34-120">Aktivně Pracujeme s týmem F # k vyřešení problému, ale do té doby alternativním řešením je instalace balíčků NuGet do projektů F # přes dialogové okno Správce balíčků NuGet, nikoli konzole.</span><span class="sxs-lookup"><span data-stu-id="a6d34-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="a6d34-121">[Další informace jsou k dispozici na webu CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="a6d34-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="a6d34-122">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="a6d34-122">Bug Fixes</span></span>
<span data-ttu-id="a6d34-123">NuGet 2.2 zahrnuje opravy mnoha chyb.</span><span class="sxs-lookup"><span data-stu-id="a6d34-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="a6d34-124">Úplný seznam pracovních položek opravených NuGet 2.2 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a6d34-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
