---
title: Poznámky k verzi NuGet 3.4.4
description: Poznámky k verzi pro včetně NuGet 3.4.4 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820858"
---
# <a name="nuget-344-release-notes"></a>Poznámky k verzi NuGet 3.4.4

[Poznámky k verzi NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [poznámky k verzi 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)

Hlavním cílem této verze byla vylepšení kvality 3.4.3 verzi nuget.exe s několika opravy také rozšíření sady Visual Studio.

Si můžete stáhnout VSIX i nuget.exe [zde](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Úplné protokol změn](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Změny

- Vylepšení aktualizací Service Pack: Vylepšení balení symboly, balení s `project.json` a další [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Zobrazit výjimky, když dojde k selhání hledání projekty v příkazu update [\#605](https://github.com/NuGet/NuGet.Client/pull/605)
- Typ balíčku číst ze vstupu `.nuspec` a `project.json` při balení [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Zkontrolujte NuGet.Shared není projektu. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Použít nabízenou časový limit jako časový limit odpovědi HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Soubory balíčků s budoucí časy nebude mít časy jejich použít [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualizace `NuGet.Core.dll` verzi 2.12.0 opravu problému XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Podpora./NuGet.CommandLine.XPlat - v \<podrobností\> \<režimu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Zobrazení Chyba při obnově bez `project.json` nebo `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Stanovení závislost verze při požadované verze se liší [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)