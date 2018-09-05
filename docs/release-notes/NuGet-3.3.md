---
title: NuGet 3.3 poznámky
description: Zpráva k vydání verze NuGet 3.3 včetně známých problémů, opravy chyb, nové funkce a chcete
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546644"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="ab222-103">NuGet 3.3 poznámky</span><span class="sxs-lookup"><span data-stu-id="ab222-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="ab222-104">[Poznámky k verzi NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC poznámky](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="ab222-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="ab222-105">NuGet 3.3 bylo vydáno 30. listopadu 2015 se velký počet aktualizace uživatelského rozhraní a funkcí příkazového řádku, stejně jako kolekce užitečné opravy klientům NuGet.</span><span class="sxs-lookup"><span data-stu-id="ab222-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="ab222-106">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="ab222-106">New Features</span></span>

* <span data-ttu-id="ab222-107">Byly zavedeny poskytovatelé přihlašovacích údajů, které umožňují klientům příkazového řádku NuGet, abyste mohli bez problému fungují s ověřené informační kanál.</span><span class="sxs-lookup"><span data-stu-id="ab222-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="ab222-108">[Návod, jak nainstalovat Visual Studio Team Services poskytovatele přihlašovacích ](../api/nuget-exe-credential-providers.md) a nakonfigurovat NuGet klientů jsou k dispozici na webu NuGet Docs.</span><span class="sxs-lookup"><span data-stu-id="ab222-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="ab222-109">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="ab222-109">New User Interface Features</span></span>

* <span data-ttu-id="ab222-110">Samostatných kartách procházet, instalace a k dispozici aktualizace</span><span class="sxs-lookup"><span data-stu-id="ab222-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="ab222-111">Aktualizace k dispozici oznámení "BADGE" označující počet balíčků dostupných aktualizací</span><span class="sxs-lookup"><span data-stu-id="ab222-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="ab222-112">Balíček odznaky v seznamu balíčků k označení, zda je nainstalován balíček nebo má k dispozici aktualizace.</span><span class="sxs-lookup"><span data-stu-id="ab222-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="ab222-113">Stáhněte si počet a autor se přidá do seznamu balíčků</span><span class="sxs-lookup"><span data-stu-id="ab222-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="ab222-114">Nejvyšší číslo verze k dispozici a aktuálně nainstalovanou verzi číslo v seznamu balíčků</span><span class="sxs-lookup"><span data-stu-id="ab222-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="ab222-115">Akce tlačítka umožňující rychlé instalace aktualizace i odinstalace ze seznamu balíčků</span><span class="sxs-lookup"><span data-stu-id="ab222-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="ab222-116">Jasnější akce tlačítka na panelu podrobností balíčku</span><span class="sxs-lookup"><span data-stu-id="ab222-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="ab222-117">Datum aktualizace balíčku na panelu podrobností balíčku</span><span class="sxs-lookup"><span data-stu-id="ab222-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="ab222-118">Slučování panelu v zobrazení řešení</span><span class="sxs-lookup"><span data-stu-id="ab222-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="ab222-119">Řazení mřížky projektů a čísel nainstalovaných verzí v zobrazení řešení</span><span class="sxs-lookup"><span data-stu-id="ab222-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="ab222-120">Nové funkce příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="ab222-120">New Command-line Features</span></span>

<span data-ttu-id="ab222-121">V této verzi jsme představili `add` a `init` příkazy inicializace založený na složce úložiště, jak je popsáno v [referenční informace o nuget.exe](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ab222-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="ab222-122">Struktury úložiště, která jsou vytvořena a udržuje k této složce budou [poskytovat výhody výkonu](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) jak je popsáno na našem blogu.</span><span class="sxs-lookup"><span data-stu-id="ab222-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="ab222-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ab222-123">ContentFiles</span></span>

<span data-ttu-id="ab222-124">Obsah je nyní podporována v `project.json` spravované projekty prostřednictvím nového `contentFiles` složky a `.nuspec` `contentFiles` zápisu elementu.</span><span class="sxs-lookup"><span data-stu-id="ab222-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="ab222-125">Tento obsah je možné zadat více přímo tak autora balíčku pro interakce se systémy.</span><span class="sxs-lookup"><span data-stu-id="ab222-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="ab222-126">Další informace o tom, jak nakonfigurovat contentFiles v `.nuspec` najdete v dokumentu [souboru .nuspec odkaz](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ab222-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="ab222-127">Správa mezipaměti NuGet Locals</span><span class="sxs-lookup"><span data-stu-id="ab222-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="ab222-128">Informace o tom, jak spravovat místní mezipaměti na pracovní stanici byla aktualizována NuGet příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="ab222-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="ab222-129">Další informace o místních hodnot příkazu je k dispozici v [odkaz na příkazový řádek NuGet](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="ab222-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="ab222-130">Opravené problémy</span><span class="sxs-lookup"><span data-stu-id="ab222-130">Fixed Issues</span></span>

<span data-ttu-id="ab222-131">**Významné problémy**</span><span class="sxs-lookup"><span data-stu-id="ab222-131">**Notable Issues**</span></span>

* <span data-ttu-id="ab222-132">Příkazový řádek obnovená podpora NuGet pro obnovení balíčků s soubor řešení v Mono - [. 1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="ab222-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="ab222-133">Úplný seznam problémů, které se řeší verze 3.3 najdete na Githubu v části [3.3 milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="ab222-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="ab222-134">Seznam opravených chybách v 3.3 verzi příkazového řádku se zaznamenávají do [3.3 příkazového řádku milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="ab222-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="ab222-135">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="ab222-135">Known Issues</span></span>

<span data-ttu-id="ab222-136">Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="ab222-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>