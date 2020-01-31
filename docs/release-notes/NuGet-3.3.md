---
title: Zpráva k vydání verze NuGet 3,3
description: Poznámky k verzi pro NuGet 3,3, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813777"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="d5e58-103">Zpráva k vydání verze NuGet 3,3</span><span class="sxs-lookup"><span data-stu-id="d5e58-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="d5e58-104">[Poznámky k verzi NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NUGET 3,4 – RC – poznámky k verzi](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="d5e58-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="d5e58-105">NuGet 3,3 byl vydán 30. listopadu 2015 s významným počtem aktualizací uživatelského rozhraní a funkcí příkazového řádku a také kolekce užitečných oprav klientů NuGet.</span><span class="sxs-lookup"><span data-stu-id="d5e58-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="d5e58-106">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="d5e58-106">New Features</span></span>

* <span data-ttu-id="d5e58-107">Poskytovatelé přihlašovacích údajů se zavedli, aby klienti příkazového řádku NuGet mohli bez problémů pracovat s ověřeným informačním kanálem.</span><span class="sxs-lookup"><span data-stu-id="d5e58-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="d5e58-108">[Pokyny k instalaci poskytovatele přihlašovacích údajů Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) a konfiguraci klientů NuGet, aby je používali, jsou k dispozici v dokumentaci NuGet.</span><span class="sxs-lookup"><span data-stu-id="d5e58-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="d5e58-109">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="d5e58-109">New User Interface Features</span></span>

* <span data-ttu-id="d5e58-110">Samostatné procházení, instalace a aktualizace karet k dispozici</span><span class="sxs-lookup"><span data-stu-id="d5e58-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="d5e58-111">Dostupné aktualizace upozorňující na počet balíčků s dostupnými aktualizacemi</span><span class="sxs-lookup"><span data-stu-id="d5e58-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="d5e58-112">Označení balíčků v seznamu balíčků, aby označovaly, jestli je balíček nainstalovaný nebo má k dispozici aktualizace</span><span class="sxs-lookup"><span data-stu-id="d5e58-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="d5e58-113">Počet stažení a autor přidaný do seznamu balíčků</span><span class="sxs-lookup"><span data-stu-id="d5e58-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="d5e58-114">Nejvyšší dostupné číslo verze a aktuálně nainstalované číslo verze v seznamu balíčků</span><span class="sxs-lookup"><span data-stu-id="d5e58-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="d5e58-115">Tlačítka akcí umožňující rychlou instalaci, aktualizaci a odinstalaci ze seznamu balíčků</span><span class="sxs-lookup"><span data-stu-id="d5e58-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="d5e58-116">Tlačítka pro vymazání akcí na panelu podrobností balíčku</span><span class="sxs-lookup"><span data-stu-id="d5e58-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="d5e58-117">Datum aktualizace balíčku na panelu podrobností balíčku</span><span class="sxs-lookup"><span data-stu-id="d5e58-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="d5e58-118">Sloučit panel v zobrazení řešení</span><span class="sxs-lookup"><span data-stu-id="d5e58-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="d5e58-119">V zobrazení řešení lze seřaditelné mřížky projektů a čísla nainstalovaných verzí.</span><span class="sxs-lookup"><span data-stu-id="d5e58-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="d5e58-120">Nové funkce příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="d5e58-120">New Command-line Features</span></span>

<span data-ttu-id="d5e58-121">V této verzi jsme zavedli příkazy `add` a `init` k inicializaci úložišť založených na složkách, jak je popsáno v [referenčních informacích k NuGet. exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d5e58-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="d5e58-122">Úložiště, která jsou vytvořená a spravovaná pomocí této struktury složek, budou [poskytovat významné výhody](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) z hlediska výkonu, jak je uvedeno na našem blogu.</span><span class="sxs-lookup"><span data-stu-id="d5e58-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="d5e58-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="d5e58-123">ContentFiles</span></span>

<span data-ttu-id="d5e58-124">Obsah je nyní podporován v `project.json` spravovaných projektů prostřednictvím nové složky `contentFiles` a `.nuspec` `contentFiles` Notation elementu.</span><span class="sxs-lookup"><span data-stu-id="d5e58-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="d5e58-125">Tento obsah může být přímo určen autorem balíčku pro interakce se systémy projektu.</span><span class="sxs-lookup"><span data-stu-id="d5e58-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="d5e58-126">Další informace o tom, jak nakonfigurovat contentFiles v dokumentu `.nuspec`, najdete v [odkazu. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="d5e58-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="d5e58-127">Správa mezipaměti místních prostředí NuGet</span><span class="sxs-lookup"><span data-stu-id="d5e58-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="d5e58-128">Příkazový řádek NuGet byl aktualizován tak, aby obsahoval informace o tom, jak spravovat místní mezipaměti v pracovní stanici.</span><span class="sxs-lookup"><span data-stu-id="d5e58-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="d5e58-129">Další informace o příkazu místní hodnoty jsou k dispozici v [Referenční příručce k příkazovému řádku NuGet](../reference/cli-reference/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="d5e58-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="d5e58-130">Opravené problémy</span><span class="sxs-lookup"><span data-stu-id="d5e58-130">Fixed Issues</span></span>

<span data-ttu-id="d5e58-131">**Významné problémy**</span><span class="sxs-lookup"><span data-stu-id="d5e58-131">**Notable Issues**</span></span>

* <span data-ttu-id="d5e58-132">Obnovená podpora příkazového řádku NuGet pro obnovení balíčků se souborem řešení v mono- [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="d5e58-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="d5e58-133">Úplný seznam problémů, které byly řešeny ve verzi 3,3, najdete na webu GitHub pod [milníkem 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="d5e58-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="d5e58-134">Seznam problémů opravených ve verzi příkazového řádku 3,3 se zaznamenávají do [řádku 3,3 příkazového řádku](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="d5e58-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="d5e58-135">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="d5e58-135">Known Issues</span></span>

<span data-ttu-id="d5e58-136">Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="d5e58-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>