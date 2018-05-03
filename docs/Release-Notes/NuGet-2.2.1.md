---
title: Poznámky k verzi NuGet 2.2.1
description: Poznámky k verzi pro NuGet 2.2.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="9ee07-103">Poznámky k verzi NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="9ee07-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="9ee07-104">[Poznámky k verzi NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 poznámky k verzi](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="9ee07-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="9ee07-105">NuGet 2.2.1 byla vydána 15. února 2013.</span><span class="sxs-lookup"><span data-stu-id="9ee07-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="9ee07-106">Číslo verze rozšíření sady Visual Studio je 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="9ee07-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="9ee07-107">Lokalizace aktualizace</span><span class="sxs-lookup"><span data-stu-id="9ee07-107">Localization Refresh</span></span>
<span data-ttu-id="9ee07-108">NuGet dodávána jako součást sady Visual Studio 2012, byla plně lokalizované do angličtina + 13 další jazyky.</span><span class="sxs-lookup"><span data-stu-id="9ee07-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="9ee07-109">Od té doby byly součástí NuGet 2.1 a 2.2 ale lokalizace kdyby byla aktualizována.</span><span class="sxs-lookup"><span data-stu-id="9ee07-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="9ee07-110">Verze NuGet 2.2.1 aktualizuje naše lokalizace.</span><span class="sxs-lookup"><span data-stu-id="9ee07-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="9ee07-111">Lokalizace uživatelského rozhraní a prostředí PowerShell konzoly NuGet do následující jazyky:</span><span class="sxs-lookup"><span data-stu-id="9ee07-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="9ee07-112">Čínština (zjednodušená)</span><span class="sxs-lookup"><span data-stu-id="9ee07-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="9ee07-113">Čínština (tradiční)</span><span class="sxs-lookup"><span data-stu-id="9ee07-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="9ee07-114">Čeština</span><span class="sxs-lookup"><span data-stu-id="9ee07-114">Czech</span></span>
1. <span data-ttu-id="9ee07-115">Angličtina</span><span class="sxs-lookup"><span data-stu-id="9ee07-115">English</span></span>
1. <span data-ttu-id="9ee07-116">Francouzština</span><span class="sxs-lookup"><span data-stu-id="9ee07-116">French</span></span>
1. <span data-ttu-id="9ee07-117">Němčina</span><span class="sxs-lookup"><span data-stu-id="9ee07-117">German</span></span>
1. <span data-ttu-id="9ee07-118">Italština</span><span class="sxs-lookup"><span data-stu-id="9ee07-118">Italian</span></span>
1. <span data-ttu-id="9ee07-119">Japonština</span><span class="sxs-lookup"><span data-stu-id="9ee07-119">Japanese</span></span>
1. <span data-ttu-id="9ee07-120">Korejština</span><span class="sxs-lookup"><span data-stu-id="9ee07-120">Korean</span></span>
1. <span data-ttu-id="9ee07-121">Polština</span><span class="sxs-lookup"><span data-stu-id="9ee07-121">Polish</span></span>
1. <span data-ttu-id="9ee07-122">Portugalština (Brazílie)</span><span class="sxs-lookup"><span data-stu-id="9ee07-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="9ee07-123">Ruština</span><span class="sxs-lookup"><span data-stu-id="9ee07-123">Russian</span></span>
1. <span data-ttu-id="9ee07-124">Španělština</span><span class="sxs-lookup"><span data-stu-id="9ee07-124">Spanish</span></span>
1. <span data-ttu-id="9ee07-125">Turečtina</span><span class="sxs-lookup"><span data-stu-id="9ee07-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="9ee07-126">Šablony sady Visual Studio podporují několik předinstalovaných balíček úložiště</span><span class="sxs-lookup"><span data-stu-id="9ee07-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="9ee07-127">Pokud můžete vytvořit šablony sady Visual Studio, můžete použít NuGet [předinstalovat balíčky](../visual-studio-extensibility/visual-studio-templates.md) v rámci šablony.</span><span class="sxs-lookup"><span data-stu-id="9ee07-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="9ee07-128">Až do této chvíle, tato funkce obsahovala omezení všech balíčků potřeby pocházet ze stejného zdroje.</span><span class="sxs-lookup"><span data-stu-id="9ee07-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="9ee07-129">U balíčku NuGet 2.2.1 ale může mít balíčky nainstalované z více úložiště (v šabloně, VSIX nebo složky na disku, které jsou definované v registru).</span><span class="sxs-lookup"><span data-stu-id="9ee07-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="9ee07-130">Hlavní scénáře pro tuto funkci je vlastní šablony projektů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9ee07-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="9ee07-131">Předinstalované balíčky, stahování balíčků z místního disku použít předdefinované šablony ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9ee07-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="9ee07-132">Nyní můžete vytvořit vlastní šablony projektu ASP.NET, která používá existující balíčky nainstalované technologií ASP.NET, ale do šablony přidat další balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="9ee07-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="9ee07-133">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="9ee07-133">Bug Fixes</span></span>
<span data-ttu-id="9ee07-134">NuGet 2.2.1 zahrnuje několik cílových opravy chyb.</span><span class="sxs-lookup"><span data-stu-id="9ee07-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="9ee07-135">Seznam pracovní položky pevná ve NuGet 2.2.1, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9ee07-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="9ee07-136">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="9ee07-136">Known Issues</span></span>

<span data-ttu-id="9ee07-137">Pokud jsou rozšíření šablony projektu ASP.NET, všechny úložiště předinstalované balíčku musíte použít stejné hodnoty `isPreunzipped` atribut.</span><span class="sxs-lookup"><span data-stu-id="9ee07-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
