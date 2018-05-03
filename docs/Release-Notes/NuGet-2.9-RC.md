---
title: Poznámky k verzi 2.9 RC NuGet
description: Poznámky k verzi pro NuGet 2.9 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 15665e7c3f9f638b434b0d7be2f7ff3215c787c6
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-29-rc-release-notes"></a>Poznámky k verzi 2.9 RC NuGet

[Poznámky k verzi NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 poznámky k verzi Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 byla vydána 10 září 2015 jako aktualizace 2.8.7 VSIX pro sadu Visual Studio 2012 a 2013.

### <a name="updates-in-this-release"></a>Aktualizace v této verzi

* Teď přeskočení balíčky zpracování, pokud jejich omezením `.nuspec` dokumentu je poškozený. - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Opraveny multipartwebrequest zpracování \r\n pro scénáře, platformy Unix/Linux - [. 776](https://github.com/NuGet/Home/issues/776)
* Opravě integrace s událostí sestavení v sadě Visual Studio 2013 Community edition – [1180](https://github.com/NuGet/Home/issues/1180)


Úplný seznam opravách v této verzi najdete na Githubu v [2.8.8 milník](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
