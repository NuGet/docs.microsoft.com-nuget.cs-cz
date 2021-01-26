---
title: Poznámky k verzi pro NuGet 2,9 – RC
description: Poznámky k verzi pro NuGet 2,9 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780315"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="04781-103">Poznámky k verzi pro NuGet 2,9 – RC</span><span class="sxs-lookup"><span data-stu-id="04781-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="04781-104">Poznámky k verzi [NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Poznámky k verzi pro NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="04781-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="04781-105">NuGet 2,9 byl vydán 10. září 2015 jako aktualizace 2.8.7 VSIX pro Visual Studio 2012 a 2013.</span><span class="sxs-lookup"><span data-stu-id="04781-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="04781-106">Aktualizace v této verzi</span><span class="sxs-lookup"><span data-stu-id="04781-106">Updates in this release</span></span>

* <span data-ttu-id="04781-107">Teď se přeskočí zpracování balíčků, pokud `.nuspec` je jejich dokument s omezením poškozený – [PR8](https://github.com/NuGet/NuGet2/pull/8) .</span><span class="sxs-lookup"><span data-stu-id="04781-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="04781-108">Opravené zpracování multipartwebrequest ve scénářích \r\n pro systémy UNIX a Linux – [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="04781-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="04781-109">Opravená integrace s událostmi sestavení v Visual Studio 2013 Community Edition – [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="04781-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="04781-110">Úplný seznam oprav v této verzi najdete na GitHubu v [2.8.8ém milníku](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) .</span><span class="sxs-lookup"><span data-stu-id="04781-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
