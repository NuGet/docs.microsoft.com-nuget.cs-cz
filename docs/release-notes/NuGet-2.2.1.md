---
title: Zpráva k vydání verze NuGet 2.2.1
description: Zpráva k vydání verze pro NuGet 2.2.1 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550695"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="d8a78-103">Zpráva k vydání verze NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="d8a78-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="d8a78-104">[Zpráva k vydání verze NuGet 2.2](../release-notes/nuget-2.2.md) | [zpráva k vydání verze NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="d8a78-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="d8a78-105">15. února 2013 byla vydána NuGet 2.2.1.</span><span class="sxs-lookup"><span data-stu-id="d8a78-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="d8a78-106">Číslo verze rozšíření VS je 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="d8a78-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="d8a78-107">Lokalizace aktualizace</span><span class="sxs-lookup"><span data-stu-id="d8a78-107">Localization Refresh</span></span>
<span data-ttu-id="d8a78-108">NuGet dodán jako součást sady Visual Studio 2012, byl plně lokalizované do angličtiny + 13 jiných jazycích.</span><span class="sxs-lookup"><span data-stu-id="d8a78-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="d8a78-109">Od té doby byly dodány NuGet 2.1, tak i 2.2 ale lokalizace kdyby byly aktualizovány.</span><span class="sxs-lookup"><span data-stu-id="d8a78-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="d8a78-110">Vydání verze NuGet 2.2.1 aktualizuje naše lokalizace.</span><span class="sxs-lookup"><span data-stu-id="d8a78-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="d8a78-111">Uživatelské rozhraní a konzolu Powershellu Nugetu jsou lokalizovány do následujících jazycích:</span><span class="sxs-lookup"><span data-stu-id="d8a78-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="d8a78-112">Čínština (zjednodušená)</span><span class="sxs-lookup"><span data-stu-id="d8a78-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="d8a78-113">Čínština (tradiční)</span><span class="sxs-lookup"><span data-stu-id="d8a78-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="d8a78-114">Čeština</span><span class="sxs-lookup"><span data-stu-id="d8a78-114">Czech</span></span>
1. <span data-ttu-id="d8a78-115">Angličtina</span><span class="sxs-lookup"><span data-stu-id="d8a78-115">English</span></span>
1. <span data-ttu-id="d8a78-116">Francouzština</span><span class="sxs-lookup"><span data-stu-id="d8a78-116">French</span></span>
1. <span data-ttu-id="d8a78-117">Němčina</span><span class="sxs-lookup"><span data-stu-id="d8a78-117">German</span></span>
1. <span data-ttu-id="d8a78-118">Italština</span><span class="sxs-lookup"><span data-stu-id="d8a78-118">Italian</span></span>
1. <span data-ttu-id="d8a78-119">Japonština</span><span class="sxs-lookup"><span data-stu-id="d8a78-119">Japanese</span></span>
1. <span data-ttu-id="d8a78-120">Korejština</span><span class="sxs-lookup"><span data-stu-id="d8a78-120">Korean</span></span>
1. <span data-ttu-id="d8a78-121">Polština</span><span class="sxs-lookup"><span data-stu-id="d8a78-121">Polish</span></span>
1. <span data-ttu-id="d8a78-122">Portugalština (Brazílie)</span><span class="sxs-lookup"><span data-stu-id="d8a78-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="d8a78-123">Ruština</span><span class="sxs-lookup"><span data-stu-id="d8a78-123">Russian</span></span>
1. <span data-ttu-id="d8a78-124">Španělština</span><span class="sxs-lookup"><span data-stu-id="d8a78-124">Spanish</span></span>
1. <span data-ttu-id="d8a78-125">Turečtina</span><span class="sxs-lookup"><span data-stu-id="d8a78-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="d8a78-126">Šablony sady Visual Studio podporují více úložišť předinstalovaný balíček</span><span class="sxs-lookup"><span data-stu-id="d8a78-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="d8a78-127">Pokud na základě šablony sady Visual Studio, můžete správci balíčků NuGet [předinstalovat balíčky](../visual-studio-extensibility/visual-studio-templates.md) jako součást šablony.</span><span class="sxs-lookup"><span data-stu-id="d8a78-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="d8a78-128">Až doteď, tato funkce má omezení, že všechny balíčky potřebné k pocházet ze stejného zdroje.</span><span class="sxs-lookup"><span data-stu-id="d8a78-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="d8a78-129">Nuget 2.2.1 však může mít balíčky nainstalované z více úložišť (v rámci šablony, VSIX nebo složku na disku, které jsou definovány v registru).</span><span class="sxs-lookup"><span data-stu-id="d8a78-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="d8a78-130">Hlavní scénáře pro tuto funkci je vlastní šablony projektů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d8a78-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="d8a78-131">Předinstalované balíčky, stahování balíčků z místního disku použít předdefinované šablony ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d8a78-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="d8a78-132">Nyní můžete vytvořit vlastní šablonu projektu ASP.NET, která využívá existující balíčky nainstalované pomocí technologie ASP.NET, ale přidání dalších balíčků NuGet do šablony.</span><span class="sxs-lookup"><span data-stu-id="d8a78-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="d8a78-133">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="d8a78-133">Bug Fixes</span></span>
<span data-ttu-id="d8a78-134">NuGet 2.2.1 obsahuje několik cílová opravy chyb.</span><span class="sxs-lookup"><span data-stu-id="d8a78-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="d8a78-135">Seznam pracovních položek opravených NuGet 2.2.1 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d8a78-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="d8a78-136">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="d8a78-136">Known Issues</span></span>

<span data-ttu-id="d8a78-137">Pokud rozšiřujete šablony projektů ASP.NET, všechna úložiště předinstalovaný balíček musí používat stejnou hodnotu pro `isPreunzipped` atribut.</span><span class="sxs-lookup"><span data-stu-id="d8a78-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
