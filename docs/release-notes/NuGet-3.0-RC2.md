---
title: Poznámky k verzi NuGet 3,0 RC2
description: Poznámky k verzi pro NuGet 3,0 RC2 včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780278"
---
# <a name="nuget-30-rc2-release-notes"></a>Poznámky k verzi NuGet 3,0 RC2

Poznámky k verzi [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  Zpráva k [vydání verze NuGet 3,0](../release-notes/nuget-3.0.0.md)

NuGet 3,0 RC2 byla vydána 3. června 2015 jako dočasná verze, která je k dispozici v galerii rozšíření sady Visual Studio 2015 a [CodePlex](https://nuget.codeplex.com/releases/view/615507). Tato verze obsahuje řadu důležitých oprav chyb a vylepšení výkonu, které jsme zjistili, že byly důležité k vydání před dokončením sady Visual Studio 2015. Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.

V této verzi jsme uzavřeli 158 problémů a můžete si prohlédnout [úplný seznam problémů na GitHubu](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

## <a name="summary-of-top-issues-resolved"></a>Shrnutí nejdůležitějších vyřešených problémů

* [Častá volání síťové aktualizace po aktualizaci okna Správce balíčků](https://github.com/NuGet/Home/issues/515)
* [Zpožděný posun při změně na nainstalované zobrazení ve Správci balíčků](https://github.com/NuGet/Home/issues/519)
* [Síťová volání by se měla spustit ve vlákně na pozadí.](https://github.com/NuGet/Home/issues/516)
* [Přidáno zaškrtávací políčko nezobrazit Náhled okna](https://github.com/NuGet/Home/issues/566)
* [Přidání omezení procesů pro snížení využití procesoru](https://github.com/NuGet/Home/issues/356)
* Vylepšené zpracování odkazů na přenositelné knihovny tříd
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Služba automatického dokončování rozlišuje velká a malá písmena.](https://github.com/NuGet/Home/issues/198)
* [Aktualizace pro znovu zavedení přihlašovacích údajů základního ověřování](https://github.com/NuGet/Home/issues/456)
* [Vylepšené protokolování chyb](https://github.com/NuGet/Home/issues/407)
* [Vylepšené chybové zprávy PowerShellu při volání rutiny Update-Package](https://github.com/NuGet/Home/issues/5)

Stáhněte si tuto [aktualizaci do rozšíření NuGet](https://nuget.codeplex.com/releases/view/615507) z webu CodePlex a podívejte se na [náš blog](http://blog.nuget.org) , abyste mohli další postup a oznámení pro NuGet 3,0!