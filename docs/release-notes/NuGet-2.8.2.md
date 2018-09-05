---
title: Zpráva k vydání verze NuGet ve verzi 2.8.2
description: Zpráva k vydání verze pro NuGet ve verzi 2.8.2 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551145"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="450ee-103">Zpráva k vydání verze NuGet ve verzi 2.8.2</span><span class="sxs-lookup"><span data-stu-id="450ee-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="450ee-104">[Zpráva k vydání verze NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [poznámkách k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="450ee-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="450ee-105">NuGet ve verzi 2.8.2 vydaná 22. května 2014.</span><span class="sxs-lookup"><span data-stu-id="450ee-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="450ee-106">Tato verze zahrnuty pouze změny příkazového řádku nuget.exe, balíček NuGet.Server a dalších balíčcích NuGet.</span><span class="sxs-lookup"><span data-stu-id="450ee-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="450ee-107">Vydání neobsahuje k aktualizované rozšíření sady Visual Studio nebo rozšíření nástroje WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="450ee-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="450ee-108">Důležité aktualizace</span><span class="sxs-lookup"><span data-stu-id="450ee-108">Notable Updates</span></span>

<span data-ttu-id="450ee-109">Nejdůležitější aktualizace byly v příkazového řádku nuget.exe a NuGet.Server balíčku (pro kanály NuGet v místním prostředí).</span><span class="sxs-lookup"><span data-stu-id="450ee-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="450ee-110">Opravy chyb důležité nuget.exe</span><span class="sxs-lookup"><span data-stu-id="450ee-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="450ee-111">nuget.exe Push se nezdaří a udržuje opakování</span><span class="sxs-lookup"><span data-stu-id="450ee-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="450ee-112">nuget.exe nabízených neodesílá pověření základního ověřování správně</span><span class="sxs-lookup"><span data-stu-id="450ee-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="450ee-113">nuget.exe nabízených oznámení nebude postupujte podle dočasné přesměrování</span><span class="sxs-lookup"><span data-stu-id="450ee-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="450ee-114">Oprava chyby důležité NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="450ee-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="450ee-115">Nesprávná hodnota IsAbsoluteLatestVersion vrácený NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="450ee-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="450ee-116">Balíčky se aktualizovaly</span><span class="sxs-lookup"><span data-stu-id="450ee-116">Packages Updated</span></span>

<span data-ttu-id="450ee-117">Příkazový řádek nuget.exe a NuGet.Server opravy se dodávají jako aktualizace balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="450ee-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="450ee-118">Došlo k jiné balíčky se aktualizovaly s ve verzi 2.8.2 také.</span><span class="sxs-lookup"><span data-stu-id="450ee-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="450ee-119">Tady je seznam aktualizované balíčky:</span><span class="sxs-lookup"><span data-stu-id="450ee-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="450ee-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="450ee-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="450ee-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="450ee-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="450ee-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="450ee-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="450ee-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="450ee-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="450ee-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (balíčku, není rozšíření)</span><span class="sxs-lookup"><span data-stu-id="450ee-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="450ee-125">Všechny změny</span><span class="sxs-lookup"><span data-stu-id="450ee-125">All Changes</span></span>
<span data-ttu-id="450ee-126">Došlo k 10 problémy zákazníky a vyřešené ve verzi.</span><span class="sxs-lookup"><span data-stu-id="450ee-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="450ee-127">Úplný seznam pracovní položky opravených NuGet ve verzi 2.8.2, prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="450ee-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
