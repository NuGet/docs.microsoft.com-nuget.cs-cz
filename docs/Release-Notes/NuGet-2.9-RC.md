---
title: "Poznámky k verzi 2.9 RC NuGet | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 2.9 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.9 k vydání verze RC, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0e73b54ab7bbf97806269834c67ad0a159c9065b
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="49820-104">Poznámky k verzi 2.9 RC NuGet</span><span class="sxs-lookup"><span data-stu-id="49820-104">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="49820-105">[Poznámky k verzi NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 poznámky k verzi Preview](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="49820-105">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="49820-106">NuGet 2.9 byla vydána 10 září 2015 jako aktualizace 2.8.7 VSIX pro sadu Visual Studio 2012 a 2013.</span><span class="sxs-lookup"><span data-stu-id="49820-106">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="49820-107">Aktualizace v této verzi</span><span class="sxs-lookup"><span data-stu-id="49820-107">Updates in this release</span></span>

* <span data-ttu-id="49820-108">Teď přeskočení balíčky zpracování, pokud jejich omezením `.nuspec` dokumentu je poškozený. - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="49820-108">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="49820-109">Opraveny multipartwebrequest zpracování \r\n pro scénáře, platformy Unix/Linux - [. 776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="49820-109">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="49820-110">Opravě integrace s událostí sestavení v sadě Visual Studio 2013 Community edition – [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="49820-110">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="49820-111">Úplný seznam opravách v této verzi najdete na Githubu v [2.8.8 milník](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="49820-111">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
