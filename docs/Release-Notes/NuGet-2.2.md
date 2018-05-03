---
title: Poznámky k verzi 2.2 NuGet
description: Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 2.2 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="d4d94-103">Poznámky k verzi 2.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="d4d94-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="d4d94-104">[Poznámky k verzi NuGet 2.1](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 poznámky k verzi](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="d4d94-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="d4d94-105">NuGet 2.2 byla vydána 12 prosinec 2012.</span><span class="sxs-lookup"><span data-stu-id="d4d94-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="d4d94-106">Snadné spuštění sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4d94-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="d4d94-107">Mezi nové funkce, které byl přidán v sadě Visual Studio 2012 byla [dialogové okno Snadné spuštění](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="d4d94-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="d4d94-108">NuGet 2.2 rozšiřuje toto dialogové okno, díky kterému jej k chybě při inicializaci dialogové okno Správce balíčku s podmínkami vyhledávání zadané v Snadné spuštění.</span><span class="sxs-lookup"><span data-stu-id="d4d94-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="d4d94-109">Například zadáte, jquery, snadné spuštění nyní zahrnuje možnost ve výsledcích hledání balíčků NuGet odpovídající 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="d4d94-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet v sadě Visual Studio snadné spuštění](./media/quick-launch.png)

<span data-ttu-id="d4d94-111">Výběrem této možnosti se spustí standardní NuGet balíček správce možnosti vyhledávání pro termín 'jquery'.</span><span class="sxs-lookup"><span data-stu-id="d4d94-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Dialogové okno Správce balíčků NuGet předem vyplněná](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="d4d94-113">Zadejte celou složku pro obsah balíčku</span><span class="sxs-lookup"><span data-stu-id="d4d94-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="d4d94-114">NuGet 2.2 teď umožňuje zadat celou složku v `<file>` element `.nuspec` souboru celý obsah této složky.</span><span class="sxs-lookup"><span data-stu-id="d4d94-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="d4d94-115">Například následující způsobí, že všechny skripty ve složce balíčku skripty mají být přidány do složky contents\scripts při instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="d4d94-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="d4d94-116">**Aktualizace 6/24/16: prázdné složky ve složce "obsah" ignorují při instalaci balíčku.**</span><span class="sxs-lookup"><span data-stu-id="d4d94-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="d4d94-117">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="d4d94-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="d4d94-118">Při použití konzoly Správce balíčků selže instalace balíčku pro projekty F #</span><span class="sxs-lookup"><span data-stu-id="d4d94-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="d4d94-119">Při pokusu o instalaci balíčku NuGet do projektu aplikace F # pomocí konzoly Správce balíčků, je vyvolána výjimkou InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="d4d94-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="d4d94-120">Aktivně Pracujeme s týmem F # k vyřešení problému, ale do té doby, řešením je instalace balíčků NuGet do projektů F # přes dialogové okno Správce balíčků NuGet spíše než konzole.</span><span class="sxs-lookup"><span data-stu-id="d4d94-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="d4d94-121">[Další informace najdete na webu CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="d4d94-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="d4d94-122">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="d4d94-122">Bug Fixes</span></span>
<span data-ttu-id="d4d94-123">NuGet 2.2 obsahuje opravy mnoha chyb.</span><span class="sxs-lookup"><span data-stu-id="d4d94-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="d4d94-124">Úplný seznam pracovní položky pevné v NuGet 2.2 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d4d94-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
