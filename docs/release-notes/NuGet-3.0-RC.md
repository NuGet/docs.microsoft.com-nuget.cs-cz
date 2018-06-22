---
title: Poznámky k verzi RC NuGet 3.0
description: Poznámky k verzi pro RC 3.0 NuGet včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819595"
---
# <a name="nuget-30-rc-release-notes"></a>Poznámky k verzi RC NuGet 3.0

[Poznámky k verzi Beta NuGet 3.0](../release-notes/nuget-3.0-beta.md) | [poznámky k verzi RC2 NuGet 3.0](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC byla vydána 29. dubna 2015 ve verzi Visual Studio 2015 RC. Tato verze obsahuje několik důležitých oprav chyb, vylepšení výkonu a aktualizace pro podporu nového rozhraní.  Je k dispozici pouze pro Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Trvalá zaměřit se na výkon

Stability a výkonu dotazů NuGet nadále aktivní téma, které jsme se zaměřením na.  V této verzi měli byste začít zobrazíte operace velmi rychlé hledání v NuGet uživatelského rozhraní a webu.  Probíhá sledování služby a jak používat službu, aby jsme můžete nadále vyladění těchto operací.

## <a name="significant-issues-resolved"></a>Významné vyřešení problémů

Stabilizovat klienty NuGet jsme vyřešit řadu problémů v rámci této verze.  Tady je právě stručný seznam některých důležitější vyřešení problémů:

* Jako součást přejmenování tisíc framework pro ASP.NET 5, byly aktualizovány monikery framework pro zpracování dnx a dnxcore [odkaz](https://github.com/NuGet/Home/issues/215)
* Nápovědě přidají odkazy ve Visual Studiu [odkaz](https://github.com/NuGet/Home/issues/232)
* Lepší zpracování složitých odkazů v `.nuspec` s oddělovači framework odkazy [odkaz](https://github.com/NuGet/Home/issues/276)
* Pevné podporu pro jazykové japonské verze [odkaz](https://github.com/NuGet/Home/issues/253)
* Aktualizovaného klienta povolit projekty ASP.NET 5, aby používaly nové koncové body v3 [odkaz](https://github.com/NuGet/Home/issues/219)
* Aktualizováno za účelem lepší popisovač balíčky složka se správa zdrojového kódu [odkaz](https://github.com/NuGet/Home/issues/56)
* Pevné podporu pro balíčky satelitní [odkaz](https://github.com/NuGet/Home/issues/17)
* Opravě podporu pro soubory obsahu pro konkrétní rozhraní [odkaz](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Generální opravu přítomnosti Githubu

Provedli jsme některé změny naše [zdrojového kódu úložiště na Githubu](http://github.com/nuget/home).  Pokud máte problémy s klienta NuGet sady Visual Studio, příkazy prostředí Powershell nebo příkazového řádku spustitelného souboru můžete protokolu tyto problémy a jejich průběh sledovat na našem [seznam problémů úložiště GitHub domovské](http://github.com/nuget/home/issues).  Sledujeme problémy pro galerii v našem [úložiště GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Nenechte ujít

Prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a hlášení pro NuGet 3.0!