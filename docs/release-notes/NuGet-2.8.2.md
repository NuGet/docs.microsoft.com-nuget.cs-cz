---
title: Poznámky k verzi 2.8.2 NuGet
description: Poznámky k verzi pro NuGet ve verzi 2.8.2 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821327"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="d5967-103">Poznámky k verzi 2.8.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="d5967-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="d5967-104">[Poznámky k verzi NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 poznámky k verzi](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="d5967-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="d5967-105">NuGet ve verzi 2.8.2 byla vydána 22 může 2014.</span><span class="sxs-lookup"><span data-stu-id="d5967-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="d5967-106">Tato verze zahrnuty pouze změny nuget.exe příkazového řádku, balíček NuGet.Server a dalších balíčcích NuGet.</span><span class="sxs-lookup"><span data-stu-id="d5967-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="d5967-107">Verze neobsahuje aktualizované rozšíření sady Visual Studio nebo rozšíření nástroje WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="d5967-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="d5967-108">Upozorňují na důležité aktualizace</span><span class="sxs-lookup"><span data-stu-id="d5967-108">Notable Updates</span></span>

<span data-ttu-id="d5967-109">Nejdůležitějším aktualizace byly v nuget.exe příkazového řádku a NuGet.Server balíčku (pro vlastním hostováním kanály NuGet).</span><span class="sxs-lookup"><span data-stu-id="d5967-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="d5967-110">Opravy chyb důležité nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d5967-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="d5967-111">nuget.exe nabízení selže a udržuje opakování</span><span class="sxs-lookup"><span data-stu-id="d5967-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="d5967-112">nuget.exe nabízené neodesílá pověření základního ověřování správně</span><span class="sxs-lookup"><span data-stu-id="d5967-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="d5967-113">nuget.exe nabízené nebude podle dočasné přesměrování</span><span class="sxs-lookup"><span data-stu-id="d5967-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="d5967-114">Oprava chyby důležité NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="d5967-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="d5967-115">Nesprávná hodnota IsAbsoluteLatestVersion vrácený NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="d5967-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="d5967-116">Balíčky aktualizovat</span><span class="sxs-lookup"><span data-stu-id="d5967-116">Packages Updated</span></span>

<span data-ttu-id="d5967-117">Nuget.exe příkazového řádku a NuGet.Server oprav je dodávána jako aktualizace balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="d5967-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="d5967-118">Došlo k jiným balíčkům aktualizováno také ve verzi 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="d5967-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="d5967-119">Tady je seznam aktualizované balíčků:</span><span class="sxs-lookup"><span data-stu-id="d5967-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="d5967-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="d5967-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="d5967-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="d5967-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="d5967-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="d5967-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="d5967-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="d5967-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="d5967-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (balíčku, není rozšíření)</span><span class="sxs-lookup"><span data-stu-id="d5967-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="d5967-125">Všechny změny</span><span class="sxs-lookup"><span data-stu-id="d5967-125">All Changes</span></span>
<span data-ttu-id="d5967-126">Nebyly 10 problémy řešeny v verze.</span><span class="sxs-lookup"><span data-stu-id="d5967-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="d5967-127">Úplný seznam pracovní položky pevná ve NuGet ve verzi 2.8.2, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="d5967-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
