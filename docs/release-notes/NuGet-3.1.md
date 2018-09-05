---
title: Poznámky k verzi 3.1 NuGet
description: Zpráva k vydání verze pro NuGet 3.1, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545344"
---
# <a name="nuget-31-release-notes"></a>Poznámky k verzi 3.1 NuGet

[Zpráva k vydání verze NuGet 3.0](../release-notes/nuget-3.0.0.md) | [zpráva k vydání verze NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 byla vydána 27. července 2015 jako připojené rozšíření pro Universal Windows Platform SDK pro Visual Studio 2015. Tato verze sady Windows Platform SDK jsme doručili tak, že vývojové prostředí Windows by mohla využít výhod práce NuGet napříč platformami, která byla dříve spuštěna. Tato verze rozšíření NuGet dostupná jenom pro Visual Studio 2015.

Doporučujeme, abyste tyto vývojáře, kteří mají přístup ke službě update Galerie sady Visual Studio na nejnovější verzi, která je k dispozici, protože vždy publikujeme aktualizace s opravy chyb a nové funkce.

## <a name="nuget-visual-studio-extension"></a>Rozšíření NuGet Visual Studio

Problémy a funkce v této verzi jsou označené na Githubu s ["3.1 tranzitivní podpora RTM UWP" milník](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) celkem, jsme uzavřeno 67 problémech ve verzi 3.1.

### <a name="new-features"></a>Nové funkce

* `project.json` Podpora pro podporu Windows UPW a ASP.NET 5
* Instalace přenositelné balíčku

Popis a definice těchto funkcích najdete jinde v dokumentaci.

### <a name="deprecated"></a>zastaralé

Následující funkce už nejsou k dispozici pro sadu Visual Studio 2015:

* Již nebude nainstalován úrovně balíčků řešení

Už nejsou k dispozici pro Visual Studio 2015 a projekty, které používají tyto funkce `project.json` specifikace

* `install.ps1` a `uninstall.ps1` – tyto skripty se mají ignorovat během instalace balíčku, obnovení, aktualizovat a odinstalace
* Konfigurace transformace se bude ignorovat.
* Obsah se provádí, ale ne zkopírovat do projektu.
    * Tým pracuje na znovu implementací této funkce, sledovat diskusi a průběh na: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Známé problémy

Došlo k několika problémech doručit v této vydané verzi.

* Instalace verze 3.1 Windows 10 SDK se downgradovat verzi rozšíření NuGet, který byl dříve nainstalován

## <a name="nuget-command-line"></a>NuGet příkazového řádku

Spustitelný soubor příkazového řádku NuGet byla aktualizován a přesunout do nového umístění Distribuovatelný tak, aby historických verzí tohoto nuget.exe nadále být k dispozici.  3.1 beta verze programu nuget.exe můžete stáhnout pro Windows na: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Nové Distribuovatelný umístění nachází na dist.nuget.org hostitel, s struktury složek, která následuje tuto šablonu:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nové funkce

* obnovit a nainstalujte balíčky do projektů, které používají nuget.exe `project.json` souboru.
* nuget.exe můžou připojit k a využívat protokol v3 NuGet na: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Známé problémy ##

1.    Nelze provést pack proti `project.json` soubor – [928](https://github.com/NuGet/Home/issues/928)
2.    Není podporován v Mono - [. 1059](https://github.com/NuGet/Home/issues/1059)
3.    Nelokalizovaný - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Není podepsaný, stejně jako stávající http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
