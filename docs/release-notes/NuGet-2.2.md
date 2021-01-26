---
title: Zpráva k vydání verze NuGet 2,2
description: Poznámky k verzi pro NuGet 2,2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780436"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="817fb-103">Zpráva k vydání verze NuGet 2,2</span><span class="sxs-lookup"><span data-stu-id="817fb-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="817fb-104">Zpráva k [vydání verze](../release-notes/nuget-2.1.md)  |  NuGet 2,1 [Poznámky k verzi NuGet 2.2.1](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="817fb-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="817fb-105">NuGet 2,2 byl vydaný 12. prosince 2012.</span><span class="sxs-lookup"><span data-stu-id="817fb-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="817fb-106">Snadné spuštění sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="817fb-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="817fb-107">Jednou z nových funkcí, které byly přidány v aplikaci Visual Studio 2012, bylo [dialogové okno snadné spuštění](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="817fb-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="817fb-108">NuGet 2,2 rozšiřuje toto dialogové okno, aby bylo možné inicializovat dialog správce balíčků s hledanými výrazy uvedenými v panelu snadného spuštění.</span><span class="sxs-lookup"><span data-stu-id="817fb-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="817fb-109">Například když zadáte jQuery v okně rychlé spuštění, ve výsledcích se zobrazí možnost vyhledat balíčky NuGet, které odpovídají "jQuery".</span><span class="sxs-lookup"><span data-stu-id="817fb-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Balíčky NuGet v aplikaci Visual Studio – snadné spuštění](./media/quick-launch.png)

<span data-ttu-id="817fb-111">Výběrem této možnosti se spustí standardní možnosti vyhledávání správce balíčků NuGet pro termín "jQuery".</span><span class="sxs-lookup"><span data-stu-id="817fb-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Dialog správce balíčků NuGet předem naplněný](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="817fb-113">Zadat celou složku pro obsah balíčku</span><span class="sxs-lookup"><span data-stu-id="817fb-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="817fb-114">NuGet 2,2 teď umožňuje zadat celou složku v `<file>` prvku `.nuspec` souboru, aby zahrnovala celý obsah této složky.</span><span class="sxs-lookup"><span data-stu-id="817fb-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="817fb-115">Například následující příkaz způsobí, že všechny skripty ve složce Scripts balíčku budou přidány do složky contents\scripts při instalaci balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="817fb-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="817fb-116">**Aktualizace 6/24/16: prázdné složky ve složce Content se při instalaci balíčku ignorují.**</span><span class="sxs-lookup"><span data-stu-id="817fb-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="817fb-117">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="817fb-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="817fb-118">Instalace balíčku pro projekty F # při použití konzoly Správce balíčků se nezdařila</span><span class="sxs-lookup"><span data-stu-id="817fb-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="817fb-119">Při pokusu o instalaci balíčku NuGet do projektu F # pomocí konzoly Správce balíčků je vyvolána událost InvalidOperationException.</span><span class="sxs-lookup"><span data-stu-id="817fb-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="817fb-120">Aktivně spolupracujeme s týmem F # k vyřešení problému, ale mezitím je k dispozici alternativní řešení pro instalaci balíčků NuGet do projektů F # prostřednictvím dialogového okna Správce balíčků NuGet místo konzoly.</span><span class="sxs-lookup"><span data-stu-id="817fb-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="817fb-121">[Další informace jsou k dispozici na webu CodePlex](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="817fb-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="817fb-122">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="817fb-122">Bug Fixes</span></span>
<span data-ttu-id="817fb-123">NuGet 2,2 obsahuje mnoho oprav chyb.</span><span class="sxs-lookup"><span data-stu-id="817fb-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="817fb-124">Úplný seznam pracovních položek opravených v NuGet 2,2 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="817fb-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
