---
title: "Poznámky k verzi NuGet 3.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 3.1 NuGet."
keywords: "NuGet 3.1 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-31-release-notes"></a>Poznámky k verzi 3.1 NuGet

[Poznámky k verzi NuGet 3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 poznámky k verzi](../release-notes/nuget-3.1.1.md)

NuGet 3.1 byla vydána 27. července 2015 jako připojené rozšíření pro univerzální platformu Windows SDK pro Visual Studio 2015. Tato verze sada Windows SDK pro platformu poskytneme tak, aby vývojového prostředí systému Windows může využít pracovní NuGet a platformy, která již byla dříve spuštěna. Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.

Doporučujeme, abyste tyto vývojáři, kteří mají přístup k sadě Visual Studio Galerie aktualizaci na nejnovější verzi, která je k dispozici, protože jsme se vždy publikování aktualizace s oprav chyb a nové funkce.

## <a name="nuget-visual-studio-extension"></a>Rozšíření NuGet Visual Studio

Problémy a funkce v této verzi jsou označené na Githubu se ["3.1 přenositelné podpora RTM UWP" milník](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) celkem, jsme uzavřený 67 problémů v 3.1 vydání.

### <a name="new-features"></a>Nové funkce

* `project.json`Podpora pro podporu Windows UWP a ASP.NET 5
* Instalace přenositelné balíčku

Popis a definice těchto funkcí jinde v dokumentaci.

### <a name="deprecated"></a>Zastaralé

Již nejsou k dispozici pro Visual Studio 2015 následující funkce:

* Úrovně balíčků řešení už ji instalovat

Již nejsou k dispozici pro Visual Studio 2015 a projekty, které používají následující funkce `project.json` specifikace

* `install.ps1`a `uninstall.ps1` -tyto skripty během instalace balíčku se bude ignorovat, obnovit, aktualizovat a odinstalace
* Konfigurace transformací budou ignorovány.
* Obsah se provádí, ale není zkopírovat do projektu.
    * Tým pracuje na znovu implementací této funkce, postupujte podle diskuse a v průběhu: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Známé problémy

Došlo k několika známých problémů doručit v této verzi.

* Instalace verze 3.1 s Windows 10 SDK se downgradovat verzi rozšíření NuGet, který byl dříve nainstalován

## <a name="nuget-command-line"></a>NuGet příkazového řádku

Spustitelný soubor příkazového řádku NuGet byl aktualizován a přesunout do nového umístění distribuovatelného, aby mohl pokračovat historických verzích nuget.exe bylo k dispozici.  3.1 beta verzi nuget.exe můžete stáhnout pro Windows v: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Nové distribuovatelného umístění se nachází na hostiteli dist.nuget.org s strukturu složek, která následuje tuto šablonu:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Nové funkce

* můžete obnovit a nainstalovat balíčky do projektů, které používají nuget.exe `project.json` souboru.
* připojení a využívat protokol NuGet v3 na nuget.exe lze: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Známé problémy ##

1.    Nelze provést pack proti `project.json` soubor - [928](https://github.com/NuGet/Home/issues/928)
2.    Není podporována na Mono - [. 1059](https://github.com/NuGet/Home/issues/1059)
3.    Nelokalizovaný - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Není podepsaný, stejně jako existující http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)
