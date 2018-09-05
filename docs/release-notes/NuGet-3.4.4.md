---
title: Zpráva k vydání verze NuGet 3.4.4
description: Zpráva k vydání verze pro NuGet 3.4.4 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547470"
---
# <a name="nuget-344-release-notes"></a>Zpráva k vydání verze NuGet 3.4.4

[Zpráva k vydání verze NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 betaverze poznámky](../release-notes/nuget-3.5-Beta.md)

Hlavním cílem této verzi byla vylepšení kvality 3.4.3 verze programu nuget.exe pomocí rozšíření sady Visual Studio také několik oprav.

Si můžete stáhnout VSIX i nuget.exe [tady](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Úplný protokol změn](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Změny

- Vylepšení aktualizací Service Pack: Vylepšení balení symbolů, balení s `project.json` a další [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Zobrazit výjimky, když dojde k selhání hledání projekty v příkazu update [\#605](https://github.com/NuGet/NuGet.Client/pull/605)
- Přečíst typ balíčku ze vstupu `.nuspec` a `project.json` při balení [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Ujistěte se, NuGet.Shared ne k projektu. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Použít časový limit nabízených oznámení jako vypršení časového limitu odpovědi HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Soubory balíčku s budoucích časů nebude mít s úspěšností použít [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualizuje se `NuGet.Core.dll` verze, kterou chcete 2.12.0 k vyřešení problému XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Podpora./NuGet.CommandLine.XPlat - v \<podrobností\> \<režimu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Zobrazení chyby obnovení bez `project.json` nebo `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Stanovení verzí závislosti při požadované verze se liší [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)