---
title: Zpráva k vydání verze NuGet 3.0 Beta
description: Zpráva k vydání verze NuGet 3.0 Beta, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550910"
---
# <a name="nuget-30-beta-release-notes"></a>Zpráva k vydání verze NuGet 3.0 Beta

[Zpráva k vydání verze NuGet 3.0 ve verzi Preview](../release-notes/nuget-3.0-preview.md) | [zpráva k vydání verze NuGet 3.0 RC](../release-notes/nuget-3.0-rc.md)

23. února 2015 byla vydána NuGet 3.0 Beta verzi Visual Studia 2015 CTP 6. Tato verze znamená, že mnohem na náš tým, protože máme několik vylepšení architektury a výkonové sdílet, a My jsme rádi a zahájit vyladění nastavení výkonu v naší službě nuget.org.

Důrazně doporučujeme odinstalovat všechny předchozí verze nástroje rozšíření NuGet sady Visual Studio 2015 před instalací nové verze.  Pokud máte potíže s touto verzí rozšíření, doporučujeme, můžete se vrátit k [dřívější verze](http://nuget.codeplex.com/downloads/get/909582) pro použití se službou Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Této beta verzi 3.0 NuGet je dostupná k instalaci v aplikaci Visual Studio 2015 CTP 6 Galerie rozšíření. Pracujeme na dostat drops ve verzi preview pro sadu Visual Studio 2012 a Visual Studio 2013 velmi brzy. Dříve jste předváděli naše záměr [přestat aktualizace pro sadu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), a jsme obtížná rozhodnutí.

## <a name="new-clientserver-api"></a>Nový klient/Server rozhraní API

Jsme pracovali na některé podrobnosti implementace protokolu Nugetu klient/server. Práce, kterou jsme provedli je vytvoření "Rozhraní API v3" pro NuGet, které jsou navržené s ohledem na vysokou dostupnost důležitých scénářů, jako je obnovení balíčků a instalace balíčků. Nové rozhraní API je postavena na REST a Hypermédia a My jsme vybrali [JSON-LD](http://json-ld.org) jako naše formát prostředku.

V bitech NuGet 3.0 Beta uvidíte nový zdroj balíčků nazývá "api.nuget.org" v rozevírací nabídce zdroje balíčku.   Pokud vyberete tento zdroj balíčku, použijeme spíše pro připojení k nuget.org naše nové rozhraní API. Tento nový zdroj balíčků založená na v3 rozhraní API ve verzi RC: NuGet 3.0, nahradí zdroje balíčku na základě v2 "nuget.org".  Tuto možnost doporučujeme zakázat všechny ostatní zdroje veřejného balíčku jsme ponechte pouze api.nuget.org úložišti pouze veřejné balíčku.

Jsme přidali jsme mnoho času do vytváření rozhraní API v3 a budou i nadále spravovat rozhraní API standard v2 pro staré klienty snaží o přístup k veřejné úložiště.

## <a name="updated-ui"></a>Aktualizace uživatelského rozhraní

Vylepšili jsme uživatelské rozhraní v této verzi zahrnout pole se seznamem, který vám umožní vybrat akci, spolu s balíčkem a tlačítko náhledu převedena do zaškrtávací políčko v oblasti možnosti obrazovky.  Možnosti oblast už není možné sbalit a jsou teď k dispozici odkaz nápovědy, který popisuje dostupné možnosti.

![Nové uživatelské rozhraní NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Operace protokolování

Odebrali jsme modální okno s informací o protokolování, který by rychle zobrazit a skrýt během instalace nebo odinstalace.  Toto okno Přidat žádnou hodnotu, pokud by Opravdu chcete zobrazit informace nebo možné kopírovat a vkládat z něj.  Místo toho jsme teď přesměrování veškerý výstup protokolování do podokna Správce balíčků v okně výstup.  Myslíme si, že toto je pohodlnější a podobně jako typické sestavení sestavu, která byste měli zkontrolovat.


### <a name="focus-on-performance"></a>Zaměřte se na výkon

Provedli jsme spoustu změny názvu zvýšení výkonu vyhledávání NuGet a načte.  To byla naše číslo jedna problém u našich zákazníků, a chceme mít jistotu, že jsme vyřešené v této verzi.  Jsme naše servery vytvořili nové CDN, která je vyladěná a vylepšené odpovídající logiky snad doručí vám relevantnější dotazu a výsledky hledání rychlejší balíčku.

Jak jsme v této fázi vývoje NuGet 3.0 pokračujte, jsme se ladění a monitorování službě nuget.org a ujistěte se, že budeme poskytovat lepší prostředí.  Jsme není plán na žádné výpadky, ale bude přidání a změna prostředky ve službě.  Sledovat na naše [informační kanál twitteru](http://twitter.com/nuget) podrobnosti o když jsme se změní konfiguraci služby.

## <a name="building-nuget-with-nuget"></a>NuGet sestavení nuget

Nyní jsme mají rearchitected našich klientů NuGet do několika komponent, které představují samy o sobě vytváří na balíčky NuGet. Použití našich knihoven vynutí nám vytvořit komponenty, které jsou opakovaně použitelné a, který se dá zabalit správně.  Jsme byli schopni eliminovat duplicitním kódem a naučili jste se lépe konfigurace náš proces vývoje pro podporu potřebné k vytváření balíčků v celém našem řešení.  Pro blogový příspěvek brzy vypadat, kde bude mluvíme o strukturování projektů kódu a jak funguje naše procesu sestavení.

## <a name="stay-tuned"></a>Nenechte si ujít

Prosím dohlížet na [náš blog o](http://blog.nuget.org) další průběh a oznámení pro NuGet 3.0!
