---
title: "Poznámky k verzi NuGet 2.2.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 2.2.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.2.1 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="47095-104">Poznámky k verzi NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="47095-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="47095-105">[Poznámky k verzi NuGet 2.2](../release-notes/nuget-2.2.md) | [NuGet 2.5 poznámky k verzi](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="47095-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="47095-106">NuGet 2.2.1 byla vydána 15. února 2013.</span><span class="sxs-lookup"><span data-stu-id="47095-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="47095-107">Číslo verze rozšíření sady Visual Studio je 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="47095-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="47095-108">Lokalizace aktualizace</span><span class="sxs-lookup"><span data-stu-id="47095-108">Localization Refresh</span></span>
<span data-ttu-id="47095-109">NuGet dodávána jako součást sady Visual Studio 2012, byla plně lokalizované do angličtina + 13 další jazyky.</span><span class="sxs-lookup"><span data-stu-id="47095-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="47095-110">Od té doby byly součástí NuGet 2.1 a 2.2 ale lokalizace kdyby byla aktualizována.</span><span class="sxs-lookup"><span data-stu-id="47095-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="47095-111">Verze NuGet 2.2.1 aktualizuje naše lokalizace.</span><span class="sxs-lookup"><span data-stu-id="47095-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="47095-112">Lokalizace uživatelského rozhraní a prostředí PowerShell konzoly NuGet do následující jazyky:</span><span class="sxs-lookup"><span data-stu-id="47095-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="47095-113">Čínština (zjednodušená)</span><span class="sxs-lookup"><span data-stu-id="47095-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="47095-114">Čínština (tradiční)</span><span class="sxs-lookup"><span data-stu-id="47095-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="47095-115">Čeština</span><span class="sxs-lookup"><span data-stu-id="47095-115">Czech</span></span>
1. <span data-ttu-id="47095-116">Angličtina</span><span class="sxs-lookup"><span data-stu-id="47095-116">English</span></span>
1. <span data-ttu-id="47095-117">Francouzština</span><span class="sxs-lookup"><span data-stu-id="47095-117">French</span></span>
1. <span data-ttu-id="47095-118">Němčina</span><span class="sxs-lookup"><span data-stu-id="47095-118">German</span></span>
1. <span data-ttu-id="47095-119">Italština</span><span class="sxs-lookup"><span data-stu-id="47095-119">Italian</span></span>
1. <span data-ttu-id="47095-120">Japonština</span><span class="sxs-lookup"><span data-stu-id="47095-120">Japanese</span></span>
1. <span data-ttu-id="47095-121">Korejština</span><span class="sxs-lookup"><span data-stu-id="47095-121">Korean</span></span>
1. <span data-ttu-id="47095-122">Polština</span><span class="sxs-lookup"><span data-stu-id="47095-122">Polish</span></span>
1. <span data-ttu-id="47095-123">Portugalština (Brazílie)</span><span class="sxs-lookup"><span data-stu-id="47095-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="47095-124">Ruština</span><span class="sxs-lookup"><span data-stu-id="47095-124">Russian</span></span>
1. <span data-ttu-id="47095-125">Španělština</span><span class="sxs-lookup"><span data-stu-id="47095-125">Spanish</span></span>
1. <span data-ttu-id="47095-126">Turečtina</span><span class="sxs-lookup"><span data-stu-id="47095-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="47095-127">Šablony sady Visual Studio podporují několik předinstalovaných balíček úložiště</span><span class="sxs-lookup"><span data-stu-id="47095-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="47095-128">Pokud můžete vytvořit šablony sady Visual Studio, můžete použít NuGet [předinstalovat balíčky](../visual-studio-extensibility/visual-studio-templates.md) v rámci šablony.</span><span class="sxs-lookup"><span data-stu-id="47095-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="47095-129">Až do této chvíle, tato funkce obsahovala omezení všech balíčků potřeby pocházet ze stejného zdroje.</span><span class="sxs-lookup"><span data-stu-id="47095-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="47095-130">U balíčku NuGet 2.2.1 ale může mít balíčky nainstalované z více úložiště (v šabloně, VSIX nebo složky na disku, které jsou definované v registru).</span><span class="sxs-lookup"><span data-stu-id="47095-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="47095-131">Hlavní scénáře pro tuto funkci je vlastní šablony projektů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="47095-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="47095-132">Předinstalované balíčky, stahování balíčků z místního disku použít předdefinované šablony ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="47095-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="47095-133">Nyní můžete vytvořit vlastní šablony projektu ASP.NET, která používá existující balíčky nainstalované technologií ASP.NET, ale do šablony přidat další balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="47095-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="47095-134">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="47095-134">Bug Fixes</span></span>
<span data-ttu-id="47095-135">NuGet 2.2.1 zahrnuje několik cílových opravy chyb.</span><span class="sxs-lookup"><span data-stu-id="47095-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="47095-136">Seznam pracovní položky pevná ve NuGet 2.2.1, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="47095-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="47095-137">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="47095-137">Known Issues</span></span>

<span data-ttu-id="47095-138">Pokud jsou rozšíření šablony projektu ASP.NET, všechny úložiště předinstalované balíčku musíte použít stejné hodnoty `isPreunzipped` atribut.</span><span class="sxs-lookup"><span data-stu-id="47095-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
