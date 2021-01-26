---
title: Poznámky k verzi pro NuGet 3,4 – RC
description: Poznámky k verzi pro NuGet 3,4 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780239"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="c1b96-103">Poznámky k verzi pro NuGet 3,4 – RC</span><span class="sxs-lookup"><span data-stu-id="c1b96-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="c1b96-104">Zpráva k [vydání verze](../release-notes/nuget-3.3.md)  |  NuGet 3,3 Zpráva k [vydání verze NuGet 3,4](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="c1b96-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="c1b96-105">NuGet 3,4 – RC byla vydána 3. března 2016 společně se sadou Visual Studio 2015 Update 2 RC a byla sestavena s několika principy v mozky:</span><span class="sxs-lookup"><span data-stu-id="c1b96-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="c1b96-106">Podpora pro různé platformy</span><span class="sxs-lookup"><span data-stu-id="c1b96-106">Cross-Platform support</span></span>
* <span data-ttu-id="c1b96-107">Vylepšení výkonu</span><span class="sxs-lookup"><span data-stu-id="c1b96-107">Performance improvements</span></span>
* <span data-ttu-id="c1b96-108">Vylepšení dílčího uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="c1b96-108">Minor UI improvements</span></span>

<span data-ttu-id="c1b96-109">V této verzi RC jsou k dispozici následující funkce s vyšším plánovaným vydáním pro 3,4 finální verzi.</span><span class="sxs-lookup"><span data-stu-id="c1b96-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="c1b96-110">Nové funkce</span><span class="sxs-lookup"><span data-stu-id="c1b96-110">New Features</span></span>

* <span data-ttu-id="c1b96-111">Klienti NuGet teď podporují kódování obsahu gzip z úložišť.</span><span class="sxs-lookup"><span data-stu-id="c1b96-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="c1b96-112">Podpora soubory PDB z balíčků v projektech xproj</span><span class="sxs-lookup"><span data-stu-id="c1b96-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="c1b96-113">Podpora pro akce sestavení pro iOS a Android v elementu contentFiles</span><span class="sxs-lookup"><span data-stu-id="c1b96-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="c1b96-114">Podpora pro monikery rozhraní netstandard a netstandardapp</span><span class="sxs-lookup"><span data-stu-id="c1b96-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="c1b96-115">Nové funkce uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="c1b96-115">New User Interface Features</span></span>

* <span data-ttu-id="c1b96-116">Významná vylepšení výkonu, zejména na kartách nainstalované, aktualizace a konsolidace</span><span class="sxs-lookup"><span data-stu-id="c1b96-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="c1b96-117">Nainstalované a aktualizované karty jsou nyní seřazené abecedně.</span><span class="sxs-lookup"><span data-stu-id="c1b96-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="c1b96-118">Přidání tlačítka aktualizovat, které umožňuje aktualizovat hledání</span><span class="sxs-lookup"><span data-stu-id="c1b96-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="c1b96-119">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="c1b96-119">Updates and Improvements</span></span>

* <span data-ttu-id="c1b96-120">Balíčky, na které se odkazuje v `project.json` plovoucí verzi, se v každém sestavení neaktualizují.</span><span class="sxs-lookup"><span data-stu-id="c1b96-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="c1b96-121">Místo toho se aktualizují pouze v případě, že je vynuceno obnovení, vyčištění, opětovné sestavení nebo změna `project.json` .</span><span class="sxs-lookup"><span data-stu-id="c1b96-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="c1b96-122">zdroje úložiště nuget.org již nejsou vynuceny do konfigurace projektu, když použijete uživatelské rozhraní konfigurace NuGet.</span><span class="sxs-lookup"><span data-stu-id="c1b96-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="c1b96-123">NuGet už neobnovuje balíčky ve sdílených projektech ani nezapisuje soubor zámku.</span><span class="sxs-lookup"><span data-stu-id="c1b96-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="c1b96-124">Vylepšili jsme selhání sítě a zpracování opakování pro nedosažitelné nebo pomalé servery.</span><span class="sxs-lookup"><span data-stu-id="c1b96-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="c1b96-125">Vylepšení chování klávesnice a myši jsou vylepšena v uživatelském rozhraní Správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1b96-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="c1b96-126">Nyní podporujeme nejnovější `project.json` schéma v DNX.</span><span class="sxs-lookup"><span data-stu-id="c1b96-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c1b96-127">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="c1b96-127">Known Issues</span></span>

<span data-ttu-id="c1b96-128">Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="c1b96-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>