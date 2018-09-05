---
title: Poznámky k verzi NuGet 3.2.1
description: Zpráva k vydání verze pro NuGet 3.2.1 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548187"
---
# <a name="nuget-321-release-notes"></a>Poznámky k verzi NuGet 3.2.1

[Zpráva k vydání verze NuGet 3.2](../release-notes/nuget-3.2.md) | [poznámkách k verzi NuGet 3.3](../release-notes/nuget-3.3.md)

Bylo vydáno 12. října 2015 se sadou několik optimalizací a oprav pro 3.2 verzi NuGet 3.2.1 pro příkazový řádek a je k dispozici [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Vylepšení

* NuGet teď používá konfigurační soubor s původní použití malých a velkých `NuGet.Config`.  To je důležité malá a velká písmena v operačních systémech [1427](https://github.com/NuGet/Home/issues/1427)
* Obnovení NuGet teď bude ignorovat projekty dnx (`*.xproj`), který by se měly zpracovat s `dnu` [. 1227](https://github.com/NuGet/Home/issues/1227)
* Optimalizované využití sítě při práci s `index.json` a balíček registrační data [1426](https://github.com/NuGet/Home/issues/1426)
* Stažení vylepšené prostředku zpracování být robustnější službami v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Opravy

* NuGet správně aktualizace `.csproj` / `.vcxproj` odkazy [1483](https://github.com/NuGet/Home/issues/1483)
* Nyní složka .nuget místní brání vytváří při SpecialFolders.UserProfile nejde najít [1531](https://github.com/NuGet/Home/issues/1531)
* Vylepšené zpracování balíčky v místní mezipaměti, které jsou poškozeny během stahování [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Úplný seznam všech problémech, které řeší pro rozšíření příkazového řádku a Visual Studio najdete na webu NuGet GitHub [3.2.1 milník](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Známé problémy

Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)