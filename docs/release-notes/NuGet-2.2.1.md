---
title: Poznámky k verzi NuGet 2.2.1
description: Poznámky k verzi pro NuGet 2.2.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776804"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="f45e2-103">Poznámky k verzi NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="f45e2-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="f45e2-104">Zpráva k [vydání verze](../release-notes/nuget-2.2.md)  |  NuGet 2,2 Zpráva k [vydání verze NuGet 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="f45e2-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="f45e2-105">NuGet 2.2.1 byl vydán 15. února 2013.</span><span class="sxs-lookup"><span data-stu-id="f45e2-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="f45e2-106">Číslo verze rozšíření VS je 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="f45e2-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="f45e2-107">Aktualizace lokalizace</span><span class="sxs-lookup"><span data-stu-id="f45e2-107">Localization Refresh</span></span>
<span data-ttu-id="f45e2-108">V případě, že je NuGet dodávána jako součást sady Visual Studio 2012, je plně lokalizována do jiných jazyků angličtina a 13.</span><span class="sxs-lookup"><span data-stu-id="f45e2-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="f45e2-109">Od té doby byly dodány balíčky NuGet 2,1 a 2,2, ale lokalizace nebyla obnovena.</span><span class="sxs-lookup"><span data-stu-id="f45e2-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="f45e2-110">Verze NuGet 2.2.1 aktualizuje naši lokalizaci.</span><span class="sxs-lookup"><span data-stu-id="f45e2-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="f45e2-111">Uživatelské rozhraní NuGet a konzole PowerShellu jsou lokalizované v následujících jazycích:</span><span class="sxs-lookup"><span data-stu-id="f45e2-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="f45e2-112">Čínština (zjednodušená)</span><span class="sxs-lookup"><span data-stu-id="f45e2-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="f45e2-113">Čínština (tradiční)</span><span class="sxs-lookup"><span data-stu-id="f45e2-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="f45e2-114">Čeština</span><span class="sxs-lookup"><span data-stu-id="f45e2-114">Czech</span></span>
1. <span data-ttu-id="f45e2-115">Angličtina</span><span class="sxs-lookup"><span data-stu-id="f45e2-115">English</span></span>
1. <span data-ttu-id="f45e2-116">Francouzština</span><span class="sxs-lookup"><span data-stu-id="f45e2-116">French</span></span>
1. <span data-ttu-id="f45e2-117">Němčina</span><span class="sxs-lookup"><span data-stu-id="f45e2-117">German</span></span>
1. <span data-ttu-id="f45e2-118">Italština</span><span class="sxs-lookup"><span data-stu-id="f45e2-118">Italian</span></span>
1. <span data-ttu-id="f45e2-119">Japonština</span><span class="sxs-lookup"><span data-stu-id="f45e2-119">Japanese</span></span>
1. <span data-ttu-id="f45e2-120">Korejština</span><span class="sxs-lookup"><span data-stu-id="f45e2-120">Korean</span></span>
1. <span data-ttu-id="f45e2-121">Polština</span><span class="sxs-lookup"><span data-stu-id="f45e2-121">Polish</span></span>
1. <span data-ttu-id="f45e2-122">Portugalština (Brazílie)</span><span class="sxs-lookup"><span data-stu-id="f45e2-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="f45e2-123">Ruština</span><span class="sxs-lookup"><span data-stu-id="f45e2-123">Russian</span></span>
1. <span data-ttu-id="f45e2-124">Španělština</span><span class="sxs-lookup"><span data-stu-id="f45e2-124">Spanish</span></span>
1. <span data-ttu-id="f45e2-125">Turečtina</span><span class="sxs-lookup"><span data-stu-id="f45e2-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="f45e2-126">Šablony sady Visual Studio podporují více předinstalovaných úložišť balíčků</span><span class="sxs-lookup"><span data-stu-id="f45e2-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="f45e2-127">Pokud vytváříte šablony sady Visual Studio, můžete pomocí nástroje NuGet [předinstalovat balíčky](../visual-studio-extensibility/visual-studio-templates.md) jako součást šablony.</span><span class="sxs-lookup"><span data-stu-id="f45e2-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="f45e2-128">Do té doby měla tato funkce omezení, že všechny balíčky potřebné k tomu, aby se daly přijít ze stejného zdroje.</span><span class="sxs-lookup"><span data-stu-id="f45e2-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="f45e2-129">V případě NuGet 2.2.1a můžete mít balíčky nainstalované z několika úložišť (v šabloně, VSIX nebo složky na disku definovaném v registru).</span><span class="sxs-lookup"><span data-stu-id="f45e2-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="f45e2-130">Hlavním scénářem této funkce jsou vlastní šablony projektů ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f45e2-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="f45e2-131">Předdefinované šablony ASP.NET používají předinstalované balíčky a stahují balíčky z místního disku.</span><span class="sxs-lookup"><span data-stu-id="f45e2-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="f45e2-132">Nyní můžete vytvořit vlastní šablonu projektu ASP.NET, která používá existující balíčky nainstalované nástrojem ASP.NET, ale do šablony přidat další balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="f45e2-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="f45e2-133">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="f45e2-133">Bug Fixes</span></span>
<span data-ttu-id="f45e2-134">NuGet 2.2.1 obsahuje několik cílových oprav chyb.</span><span class="sxs-lookup"><span data-stu-id="f45e2-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="f45e2-135">Seznam pracovních položek opravených v NuGet 2.2.1 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="f45e2-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="f45e2-136">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="f45e2-136">Known Issues</span></span>

<span data-ttu-id="f45e2-137">Pokud rozšiřujete šablony projektů ASP.NET, musí všechny předinstalované úložiště balíčků používat stejnou hodnotu `isPreunzipped` atributu.</span><span class="sxs-lookup"><span data-stu-id="f45e2-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
