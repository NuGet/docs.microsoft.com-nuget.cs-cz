---
title: "Poznámky k verzi NuGet ve verzi 2.8.2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet ve verzi 2.8.2 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet ve verzi 2.8.2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f50bd1f0c981ef293a4d2ff425e0dffbdf58036c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="e69b5-104">Poznámky k verzi 2.8.2 NuGet</span><span class="sxs-lookup"><span data-stu-id="e69b5-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="e69b5-105">[Poznámky k verzi NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 poznámky k verzi](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="e69b5-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="e69b5-106">NuGet ve verzi 2.8.2 byla vydána 22 může 2014.</span><span class="sxs-lookup"><span data-stu-id="e69b5-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="e69b5-107">Tato verze zahrnuty pouze změny nuget.exe příkazového řádku, balíček NuGet.Server a dalších balíčcích NuGet.</span><span class="sxs-lookup"><span data-stu-id="e69b5-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="e69b5-108">Verze neobsahuje aktualizované rozšíření sady Visual Studio nebo rozšíření nástroje WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e69b5-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="e69b5-109">Upozorňují na důležité aktualizace</span><span class="sxs-lookup"><span data-stu-id="e69b5-109">Notable Updates</span></span>

<span data-ttu-id="e69b5-110">Nejdůležitějším aktualizace byly v nuget.exe příkazového řádku a NuGet.Server balíčku (pro vlastním hostováním kanály NuGet).</span><span class="sxs-lookup"><span data-stu-id="e69b5-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="e69b5-111">Opravy chyb důležité nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e69b5-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="e69b5-112">nuget.exe nabízení selže a udržuje opakování</span><span class="sxs-lookup"><span data-stu-id="e69b5-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="e69b5-113">nuget.exe nabízené neodesílá pověření základního ověřování správně</span><span class="sxs-lookup"><span data-stu-id="e69b5-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="e69b5-114">nuget.exe nabízené nebude podle dočasné přesměrování</span><span class="sxs-lookup"><span data-stu-id="e69b5-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="e69b5-115">Oprava chyby důležité NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e69b5-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="e69b5-116">Nesprávná hodnota IsAbsoluteLatestVersion vrácený NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e69b5-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="e69b5-117">Balíčky aktualizovat</span><span class="sxs-lookup"><span data-stu-id="e69b5-117">Packages Updated</span></span>

<span data-ttu-id="e69b5-118">Nuget.exe příkazového řádku a NuGet.Server oprav je dodávána jako aktualizace balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="e69b5-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="e69b5-119">Došlo k jiným balíčkům aktualizováno také ve verzi 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="e69b5-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="e69b5-120">Tady je seznam aktualizované balíčků:</span><span class="sxs-lookup"><span data-stu-id="e69b5-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="e69b5-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="e69b5-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="e69b5-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="e69b5-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="e69b5-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e69b5-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="e69b5-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="e69b5-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="e69b5-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (balíčku, není rozšíření)</span><span class="sxs-lookup"><span data-stu-id="e69b5-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="e69b5-126">Všechny změny</span><span class="sxs-lookup"><span data-stu-id="e69b5-126">All Changes</span></span>
<span data-ttu-id="e69b5-127">Nebyly 10 problémy řešeny v verze.</span><span class="sxs-lookup"><span data-stu-id="e69b5-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="e69b5-128">Úplný seznam pracovní položky pevná ve NuGet ve verzi 2.8.2, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="e69b5-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
