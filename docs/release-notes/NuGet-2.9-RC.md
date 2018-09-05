---
title: Poznámky k verzi 2.9 RC NuGet
description: Zpráva k vydání verze pro NuGet 2.9 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548321"
---
# <a name="nuget-29-rc-release-notes"></a>Poznámky k verzi 2.9 RC NuGet

[Zpráva k vydání verze NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [zpráva k vydání verze NuGet 3.0 ve verzi Preview](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 byla vydána jako aktualizace 2.8.7 10. září 2015 VSIX pro Visual Studio 2012 a 2013.

### <a name="updates-in-this-release"></a>Aktualizace v této verzi

* Nyní vynechává zpracování balíčky, pokud jejich omezením `.nuspec` dokumentu má chybný formát - [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Opravit multipartwebrequest zpracování \r\n pro scénáře, platformy Unix/Linux - [776](https://github.com/NuGet/Home/issues/776)
* Opravit integrace s událostí sestavení v aplikaci Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)


Úplný seznam opravách v této verzi najdete na Githubu v [2.8.8 milník](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
