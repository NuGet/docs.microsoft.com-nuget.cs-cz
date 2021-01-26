---
title: Poznámky k verzi NuGet 3.4.4
description: Poznámky k verzi pro NuGet 3.4.4, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780225"
---
# <a name="nuget-344-release-notes"></a>Poznámky k verzi NuGet 3.4.4

Poznámky k verzi [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [NuGet 3,5 – poznámky k verzi beta](../release-notes/nuget-3.5-Beta.md)

Hlavním cílem této verze bylo zvýšení kvality 3.4.3 verze nuget.exe s několika opravami rozšíření sady Visual Studio.

VSIX i nuget.exe si můžete stáhnout [tady](https://dist.nuget.org/index.html).

## <a name="344-rtm-2016-05-19"></a>[3.4.4 – RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Úplný protokol změn](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Změny

- Vylepšení sady: vylepšení zabalení symbolů, balení s `project.json` a dalších [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Zobrazit výjimku, pokud dojde k selhání při hledání projektů v příkazu Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Číst typ balíčku ze vstupu `.nuspec` a `project.json` při balení [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Udělejte NuGet. Shared není projekt. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Použít časový limit nabízených oznámení jako časový limit odpovědi HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- V souborech balíčku s budoucím časem nebudou použity časy [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualizace `NuGet.Core.dll` verze na 2.12.0 pro opravu problému XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Zobrazit chyby při obnovení bez `project.json` nebo `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)
- Oprava verzí závislostí, pokud se požadované verze liší [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)