---
title: Poznámky k verzi NuGet ve verzi 2.8.2
description: Poznámky k verzi pro NuGet ve verzi 2.8.2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780363"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="19c4c-103">Poznámky k verzi NuGet ve verzi 2.8.2</span><span class="sxs-lookup"><span data-stu-id="19c4c-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="19c4c-104">Poznámky k verzi [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Poznámky k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="19c4c-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="19c4c-105">Ve verzi 2.8.2 NuGet byl vydán dne 22. května 2014.</span><span class="sxs-lookup"><span data-stu-id="19c4c-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="19c4c-106">Tato verze obsahuje jenom změny v nuget.exe příkazového řádku, balíček NuGet. Server a další balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="19c4c-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="19c4c-107">Tato verze neobsahovala aktualizované rozšíření sady Visual Studio nebo rozšíření WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="19c4c-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="19c4c-108">Významné aktualizace</span><span class="sxs-lookup"><span data-stu-id="19c4c-108">Notable Updates</span></span>

<span data-ttu-id="19c4c-109">Nejvýznamnější aktualizace byly v příkazovém řádku nuget.exe a balíčku NuGet. Server (pro informační kanály NuGet v místním prostředí).</span><span class="sxs-lookup"><span data-stu-id="19c4c-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="19c4c-110">Důležité opravy chyb nuget.exe</span><span class="sxs-lookup"><span data-stu-id="19c4c-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="19c4c-111"> Nahrávánínuget.exe se nezdařilo a pokračuje se opakováním</span><span class="sxs-lookup"><span data-stu-id="19c4c-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="19c4c-112">nuget.exe push neposílá správně pověření pro základní ověřování</span><span class="sxs-lookup"><span data-stu-id="19c4c-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="19c4c-113">nuget.exe nabízení oznámení nebude následovat po dočasném přesměrování</span><span class="sxs-lookup"><span data-stu-id="19c4c-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="19c4c-114">Důležitá aktualizace NuGet. Server – oprava chyb</span><span class="sxs-lookup"><span data-stu-id="19c4c-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="19c4c-115">NuGet. Server vrátil nesprávnou hodnotu IsAbsoluteLatestVersion.</span><span class="sxs-lookup"><span data-stu-id="19c4c-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="19c4c-116">Aktualizované balíčky</span><span class="sxs-lookup"><span data-stu-id="19c4c-116">Packages Updated</span></span>

<span data-ttu-id="19c4c-117">Opravy nuget.exe příkazového řádku a NuGet. Server jsou dodávány jako aktualizace balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="19c4c-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="19c4c-118">V ve verzi 2.8.2 byly také aktualizovány další balíčky.</span><span class="sxs-lookup"><span data-stu-id="19c4c-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="19c4c-119">Tady je seznam aktualizovaných balíčků:</span><span class="sxs-lookup"><span data-stu-id="19c4c-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="19c4c-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="19c4c-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="19c4c-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="19c4c-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="19c4c-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="19c4c-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="19c4c-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="19c4c-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="19c4c-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (balíček, nikoli rozšíření)</span><span class="sxs-lookup"><span data-stu-id="19c4c-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="19c4c-125">Všechny změny</span><span class="sxs-lookup"><span data-stu-id="19c4c-125">All Changes</span></span>
<span data-ttu-id="19c4c-126">V této verzi bylo vyřešeno 10 problémů.</span><span class="sxs-lookup"><span data-stu-id="19c4c-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="19c4c-127">Úplný seznam pracovních položek opravených ve ve verzi 2.8.2 NuGet najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="19c4c-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
