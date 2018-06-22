---
title: Poznámky k verzi NuGet 3.2.1
description: Poznámky k verzi pro NuGet 3.2.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820141"
---
# <a name="nuget-321-release-notes"></a>Poznámky k verzi NuGet 3.2.1

[Poznámky k verzi NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 poznámky k verzi](../release-notes/nuget-3.3.md)

3.2.1 NuGet pro příkazového řádku byla vydána 12. října 2015 s několik optimalizací a opravy pro verzi 3.2 a je dostupné v [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Vylepšení

* NuGet teď používá konfigurační soubor s původní malá a velká písmena `NuGet.Config`.  To je důležité malá a velká písmena v operačních systémech [1427](https://github.com/NuGet/Home/issues/1427)
* Obnovení NuGet teď bude ignorovat projektů dnx (`*.xproj`), měla by být zpracována s `dnu` [. 1227](https://github.com/NuGet/Home/issues/1227)
* Optimalizované využití sítě při práci s `index.json` a balíčku registrační data [1426](https://github.com/NuGet/Home/issues/1426)
* Stahování prostředků vylepšené zpracování být robustnější službou v2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Opravy

* Aktualizace NuGet správně aktualizuje `.csproj` / `.vcxproj` odkazy [1483](https://github.com/NuGet/Home/issues/1483)
* Nyní složka místní .nuget brání vytváří při SpecialFolders.UserProfile nejde najít [1531](https://github.com/NuGet/Home/issues/1531)
* Vylepšené zpracování balíčky v místní mezipaměti, které jsou poškozené během stahování [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Úplný seznam problémů řešit pro rozšíření příkazového řádku a Visual Studio naleznete na webu NuGet GitHub [3.2.1 milník](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Známé problémy

Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)