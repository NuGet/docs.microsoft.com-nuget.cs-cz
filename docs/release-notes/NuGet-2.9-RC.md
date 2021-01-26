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
# <a name="nuget-29-rc-release-notes"></a>Poznámky k verzi pro NuGet 2,9 – RC

Poznámky k verzi [NuGet 2.8.7](../release-notes/nuget-2.8.7.md)  |  [Poznámky k verzi pro NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2,9 byl vydán 10. září 2015 jako aktualizace 2.8.7 VSIX pro Visual Studio 2012 a 2013.

### <a name="updates-in-this-release"></a>Aktualizace v této verzi

* Teď se přeskočí zpracování balíčků, pokud `.nuspec` je jejich dokument s omezením poškozený – [PR8](https://github.com/NuGet/NuGet2/pull/8) .
* Opravené zpracování multipartwebrequest ve scénářích \r\n pro systémy UNIX a Linux – [776](https://github.com/NuGet/Home/issues/776)
* Opravená integrace s událostmi sestavení v Visual Studio 2013 Community Edition – [1180](https://github.com/NuGet/Home/issues/1180)


Úplný seznam oprav v této verzi najdete na GitHubu v [2.8.8ém milníku](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) .
