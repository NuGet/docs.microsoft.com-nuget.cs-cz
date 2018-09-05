---
title: Zpráva k vydání verze NuGet 3.0 RC
description: Zpráva k vydání verze pro NuGet 3.0 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551716"
---
# <a name="nuget-30-rc-release-notes"></a>Zpráva k vydání verze NuGet 3.0 RC

[Zpráva k vydání verze NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [zpráva k vydání verze NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC byla vydána verze Visual Studio 2015 RC 29. dubna 2015. Tato verze obsahuje řadu oprav chyb, vylepšení výkonu a aktualizace pro podporu nového rozhraní.  Je dostupná jenom pro Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Trvalé zaměřením na výkon

Stability a výkonu dotazů NuGet dál, který se Zaměřujeme na žhavým tématem.  V této vydané verzi měli byste začít zobrazit operace velmi rychlé vyhledávání v uživatelském rozhraní NuGet a Web.  Sledujeme, služby a jak použít službu tak, aby nám můžete dále ladit tyto operace.

## <a name="significant-issues-resolved"></a>Vyřešené významné problémy

Stabilizovat klienty NuGet vyřešili jsme řadu problémů jako součást této verze.  Tady je právě krátký seznam některých důležitější vyřešení problémů:

* Jako součást přejmenovat K framework pro ASP.NET 5, byly aktualizovány monikery framework pro zpracování dnx a dnxcore [odkaz](https://github.com/NuGet/Home/issues/215)
* Přidání dokumentaci nápovědy z odkazů v Uživatelském rozhraní aplikace Visual Studio [odkaz](https://github.com/NuGet/Home/issues/232)
* Lepší zpracování složitých odkazů v `.nuspec` s odkazy na rozhraní oddělených čárkou [odkaz](https://github.com/NuGet/Home/issues/276)
* Oprava podporu pro japonské jazykové verze [odkaz](https://github.com/NuGet/Home/issues/253)
* Aktualizace klienta povolit projekty ASP.NET 5 používaly nové koncové body v3 [odkaz](https://github.com/NuGet/Home/issues/219)
* Aktualizováno za účelem lepší popisovač složku packages se správou zdrojového kódu [odkaz](https://github.com/NuGet/Home/issues/56)
* Oprava podporu pro satelitní balíčky [odkaz](https://github.com/NuGet/Home/issues/17)
* Oprava podpory pro soubory obsahu pro konkrétní rozhraní [odkaz](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Generální Githubu přítomnost opravu

Provedli jsme některé změny naše [úložiště zdrojového kódu na Githubu](http://github.com/nuget/home).  Pokud máte nějaké problémy s klienta NuGet sady Visual Studio, příkazy prostředí Powershell nebo příkazového řádku spustitelný soubor můžete protokolovat těchto problémů a sledovat jejich průběh na naše [seznamu problémů na úložiště Domovská stránka úložiště GitHub](http://github.com/nuget/home/issues).  Sledujeme problémy v galerii v našich [úložiště GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Nenechte si ujít

Prosím dohlížet na [náš blog o](http://blog.nuget.org) další průběh a oznámení pro NuGet 3.0!