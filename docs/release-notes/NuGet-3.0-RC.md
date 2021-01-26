---
title: Poznámky k verzi NuGet 3,0 RC
description: Poznámky k verzi pro NuGet 3,0 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776572"
---
# <a name="nuget-30-rc-release-notes"></a>Poznámky k verzi NuGet 3,0 RC

Poznámky k verzi [NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Poznámky k verzi NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)

NuGet 3,0 RC byl vydán 29. dubna 2015 s vydáním sady Visual Studio 2015 RC. Tato verze přináší řadu důležitých oprav chyb, vylepšení výkonu a aktualizace pro podporu nových rozhraní.  Je k dispozici pouze pro Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Pokračující zaměření na výkon

Stabilita a výkon dotazů NuGet dál představují aktivní téma, které se zaměřujeme na.  V této verzi byste měli začít zobrazovat velmi rychlé operace vyhledávání v uživatelském rozhraní a na webu NuGet.  Sledujeme službu a jak službu používáte, abychom mohli i nadále ladit tyto operace.

## <a name="significant-issues-resolved"></a>Vyřešené významné problémy

Za účelem stabilizace klientů NuGet jsme v rámci této verze vyřešili spoustu problémů.  Tady je jenom stručný seznam některých z důležitějších problémů, které jsme vyřešili:

* V rámci přejmenování rozhraní K Framework pro ASP.NET 5 byly monikery rozhraní aktualizované pro zpracování [propojení](https://github.com/NuGet/Home/issues/215) DNX a dnxcore.
* Přidání dokumentace k nápovědě z odkazů v rámci [odkazu](https://github.com/NuGet/Home/issues/232) na uživatelské rozhraní sady Visual Studio
* Lepší zacházení se složitými odkazy v `.nuspec` rámci [odkazu](https://github.com/NuGet/Home/issues/276) na odkazy rozhraní s oddělovači
* Pevná podpora pro japonské [odkazy](https://github.com/NuGet/Home/issues/253) na japonštinu
* Aktualizovaný klient, aby povoloval ASP.NET 5 projektů používat nové [odkazy](https://github.com/NuGet/Home/issues/219) na koncové body V3
* Aktualizováno pro lepší zpracování složky balíčků pomocí [odkazu](https://github.com/NuGet/Home/issues/56) správy zdrojového kódu
* [Odkaz](https://github.com/NuGet/Home/issues/17) na fixní podporu pro satelitní balíčky
* Opravená podpora pro [odkaz](https://github.com/NuGet/Home/issues/18) soubory obsahu pro konkrétní rozhraní

## <a name="github-presence-overhaul"></a>Renovace stavu GitHubu

Provedli jsme některé změny našich [úložišť zdrojového kódu na GitHubu](http://github.com/nuget/home).  Pokud máte nějaké problémy s klientem nástroje NuGet pro aplikaci Visual Studio, příkazy prostředí PowerShell nebo spustitelný soubor příkazového řádku, můžete tyto problémy zaprotokolovat a sledovat jejich průběh v našem [seznamu problémů domovského úložiště GitHub](http://github.com/nuget/home/issues).  Sledujeme problémy pro galerii v našem [úložišti GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Zůstat vyladěné

Na [našem blogu](http://blog.nuget.org) prosím sledujte, kde najdete další informace o průběhu a oznámeních pro NuGet 3,0!