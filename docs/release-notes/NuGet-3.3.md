---
title: Poznámky k verzi 3.3 NuGet
description: Poznámky k verzi pro NuGet 3.3 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821561"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="a0906-103">Poznámky k verzi 3.3 NuGet</span><span class="sxs-lookup"><span data-stu-id="a0906-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="a0906-104">[Poznámky k verzi NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC poznámky](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="a0906-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="a0906-105">NuGet 3.3 byla vydána 30. listopadu 2015 se velký počet aktualizace uživatelského rozhraní a funkcí příkazového řádku, jakož i kolekce užitečné opravy pro klienty NuGet.</span><span class="sxs-lookup"><span data-stu-id="a0906-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="a0906-106">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="a0906-106">New Features</span></span>

* <span data-ttu-id="a0906-107">Byly zavedeny poskytovatelé přihlašovacích údajů, které umožňují klienty NuGet příkazového řádku moct pracovat s ověřené informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="a0906-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="a0906-108">[Pokyny k instalaci Visual Studio Team Services přihlašovací údaje poskytovatele ](../api/nuget-exe-credential-providers.md) a nakonfigurujte NuGet klientům použít je k dispozici v NuGet dokumentace.</span><span class="sxs-lookup"><span data-stu-id="a0906-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="a0906-109">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="a0906-109">New User Interface Features</span></span>

* <span data-ttu-id="a0906-110">Samostatné karty Procházet, nainstalovaná a k dispozici aktualizace</span><span class="sxs-lookup"><span data-stu-id="a0906-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="a0906-111">Aktualizace k dispozici oznámení, která určuje počet balíčků, které jsou dostupné aktualizace</span><span class="sxs-lookup"><span data-stu-id="a0906-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="a0906-112">Balíček odznaky v seznamu balíček k označení, pokud je balíček nainstalován, nebo má k dispozici aktualizace.</span><span class="sxs-lookup"><span data-stu-id="a0906-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="a0906-113">Stáhněte si počet a Autor přidán do seznamu balíčku</span><span class="sxs-lookup"><span data-stu-id="a0906-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="a0906-114">Nejvyšší číslo verze k dispozici a aktuálně nainstalované verze číslo na seznam balíčků</span><span class="sxs-lookup"><span data-stu-id="a0906-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="a0906-115">Akce tlačítka umožňující rychlé instalace, aktualizovat a odinstalovat ze seznamu balíčku</span><span class="sxs-lookup"><span data-stu-id="a0906-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="a0906-116">Jasnější akce tlačítka na panelu podrobností balíčku</span><span class="sxs-lookup"><span data-stu-id="a0906-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="a0906-117">Datum aktualizace balíčku na panelu podrobností balíčku</span><span class="sxs-lookup"><span data-stu-id="a0906-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="a0906-118">Konsolidovat panelu v zobrazení řešení</span><span class="sxs-lookup"><span data-stu-id="a0906-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="a0906-119">Řazení mřížky projekty a nainstalovaná verze číslic v zobrazení řešení</span><span class="sxs-lookup"><span data-stu-id="a0906-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="a0906-120">Nové funkce příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="a0906-120">New Command-line Features</span></span>

<span data-ttu-id="a0906-121">V této verzi zavedli jsme `add` a `init` příkazy k chybě při inicializaci úložiště založené na složku, jak je popsáno v [nuget.exe odkaz](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a0906-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="a0906-122">Struktury úložiště, které jsou vytvořená a udržovaná tato složka se [poskytovat výrazný výkon](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) jak je uvedeno v našem blogu.</span><span class="sxs-lookup"><span data-stu-id="a0906-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="a0906-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a0906-123">ContentFiles</span></span>

<span data-ttu-id="a0906-124">Obsah se teď podporuje v `project.json` spravované projekty prostřednictvím nové `contentFiles` složky a `.nuspec` `contentFiles` element zápis.</span><span class="sxs-lookup"><span data-stu-id="a0906-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="a0906-125">Tento obsah může být více přímo určena autora balíčku pro interakce se systémy projektu.</span><span class="sxs-lookup"><span data-stu-id="a0906-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="a0906-126">Další informace o tom, jak nakonfigurovat contentFiles v `.nuspec` dokument lze najít v [příponou .nuspec odkaz](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="a0906-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="a0906-127">Místní hodnoty – NuGet mezipaměti správy</span><span class="sxs-lookup"><span data-stu-id="a0906-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="a0906-128">Informace o tom, jak spravovat místní mezipaměti na pracovní stanici je aktualizovaná NuGet příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="a0906-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="a0906-129">Další informace o příkazu místní hodnoty – je k dispozici v [reference k příkazovému řádku NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="a0906-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="a0906-130">Opravené problémy</span><span class="sxs-lookup"><span data-stu-id="a0906-130">Fixed Issues</span></span>

<span data-ttu-id="a0906-131">**Významné problémy**</span><span class="sxs-lookup"><span data-stu-id="a0906-131">**Notable Issues**</span></span>

* <span data-ttu-id="a0906-132">Nástroje příkazového řádku obnovené NuGet pro obnovení balíčků s soubor řešení na Mono - [. 1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="a0906-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="a0906-133">Úplný seznam problémů, které byly vyřešeny ve verzi 3.3 najdete na Githubu v části [3.3 milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="a0906-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="a0906-134">Seznam chyby v 3.3 příkazového řádku verze se zaznamenávají [3.3 příkazového řádku milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="a0906-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="a0906-135">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="a0906-135">Known Issues</span></span>

<span data-ttu-id="a0906-136">Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="a0906-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>