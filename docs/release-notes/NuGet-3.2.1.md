---
title: Poznámky k verzi NuGet 3.2.1
description: Poznámky k verzi pro NuGet 3.2.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776524"
---
# <a name="nuget-321-release-notes"></a>Poznámky k verzi NuGet 3.2.1

Zpráva k [vydání verze](../release-notes/nuget-3.2.md)  |  NuGet 3,2 Zpráva k [vydání verze NuGet 3,3](../release-notes/nuget-3.3.md)

Verze NuGet 3.2.1 pro příkazový řádek byla vydána 12. října 2015 s několik optimalizacemi a opravami pro vydání 3,2 a je k dispozici z [DIST.NuGet.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Vylepšen

* NuGet teď používá konfigurační soubor s původními velkými písmeny `NuGet.Config` .  To je důležité pro operační systémy s rozlišováním velkých a malých písmen [1427](https://github.com/NuGet/Home/issues/1427)
* Obnovení NuGet teď bude ignorovat projekty DNX ( `*.xproj` ), které by se měly zpracovat pomocí `dnu` [1227](https://github.com/NuGet/Home/issues/1227) .
* Optimalizované využití sítě při práci s `index.json` a registračními daty balíčku [1426](https://github.com/NuGet/Home/issues/1426)
* Vylepšené zpracování stahování prostředků pro zajištění větší robustnosti se službou v2 Services [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Opravy

* Aktualizace NuGet – odkazy jsou správné aktualizace `.csproj` / `.vcxproj` [1483](https://github.com/NuGet/Home/issues/1483)
* Nyní brání vytvoření místní složky. NuGet, když nelze najít SpecialFolders. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* Vylepšené zpracování balíčků v místní mezipaměti, které jsou během stahování poškozené [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Úplný seznam problémů řešených pro rozšíření příkazového řádku a sady Visual Studio najdete v [milníku](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) NuGet GitHubu.

## <a name="known-issues"></a>Známé problémy

Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)