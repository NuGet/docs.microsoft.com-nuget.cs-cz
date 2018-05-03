---
title: Poznámky k verzi 3.0 Beta NuGet
description: Poznámky k verzi pro NuGet 3.0 Beta včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4608b196d19f95410f9fe20f6a22e31c15955b89
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-beta-release-notes"></a>Poznámky k verzi 3.0 Beta NuGet

[Poznámky k verzi Preview NuGet 3.0](../release-notes/nuget-3.0-preview.md) | [poznámky k verzi RC NuGet 3.0](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta byla vydána 23 únor 2015 pro verze Visual Studio 2015 CTP 6. Tato verze znamená mnoho náš tým, jak máme několik architektura a vylepšení výkonu pro sdílení a máme nadšení a zahájit vyladění výkonu nastavení v naší službě nuget.org.

Důrazně doporučujeme, abyste před instalací této nové verzi odinstalovali všechny předchozí verze rozšíření NuGet sady Visual Studio 2015.  Pokud máte potíže s touto verzí rozšíření, doporučujeme vrátit k [předchozí verze](http://nuget.codeplex.com/downloads/get/909582) pro použití s Visual Studio 2015 preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Této beta verzi 3.0 NuGet je k dispozici pro instalaci ve Visual Studio 2015 CTP 6 Galerie rozšíření. Pracujeme na velmi brzy získat vyřazuje preview pro sadu Visual Studio 2012 a Visual Studio 2013. Jsme předtím sdílené naše záměr [přestali aktualizace pro sadu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), a jsme Ujistěte se, že obtížné rozhodnutí.

## <a name="new-clientserver-api"></a>Nový klient Server rozhraní API

Jste byla pracujeme na některé podrobnosti implementace pro protokol klienta nebo serveru NuGet. Práci, kterou jsme krok je vytvoření "API v3" pro NuGet, který je určený kolem vysoké dostupnosti u kritických scénářů, jako je obnovení balíčků a instalaci balíčků. Nové rozhraní API je založena na REST a hypermédií a jsme vybrali [JSON-LD](http://json-ld.org) jako formát naše prostředku.

V bitech NuGet 3.0 Beta uvidíte nový zdroj balíčků s názvem "api.nuget.org" v rozevírací nabídce zdroje balíčku.   Pokud vyberete tento zdroj balíčku, použijeme místo pro připojení k nuget.org naší nové rozhraní API. Tento nový zdroj balíčků na základě v3 rozhraní API v NuGet 3.0 RC, nahradí zdroje balíčku na základě v2 "nuget.org".  Doporučujeme zakázání všechny ostatní zdroje veřejné balíček a ponechat jenom api.nuget.org jako úložiště pouze veřejné balíčku.

Jsme jste vložena vytváření našem rozhraní API v3 mnoho času a budou nadále udržovat standardní v2 rozhraní API pro žádosti pro přístup k úložišti veřejné staré klientů.

## <a name="updated-ui"></a>Aktualizované uživatelského rozhraní

Jsme jste rozšířeného uživatelského rozhraní v této verzi zahrnout combobox, která vám umožní vybrat akci, s tímto balíčkem a přešla do zaškrtávací políčko v oblasti možnosti obrazovky tlačítka Náhled.  Oblasti možnosti již není sbalitelné a teď poskytuje odkaz nápovědy popisuje možnosti dostupné.

![Nové uživatelské rozhraní NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Operace protokolování

Jsme odebrali modální okno s informacemi o protokolování, který by rychle zobrazit a skrýt během instalace nebo odinstalace.  Toto okno Přidat žádná hodnota, pokud by Opravdu chcete zobrazit informace o nebo moct kopírovat a vkládat z něj.  Místo toho jsme veškerý výstup protokolování tak, aby podokně Správce balíčků ve výstupním okně jsou nyní přesměrování.  Myslíme si, že toto je pohodlnější a podobná typické sestavení sestavy, které chcete prověřit.


### <a name="focus-on-performance"></a>Zaměřit se na výkon

Jsme provedli spoustu změny názvu zvýšení výkonu vyhledávání NuGet a načtení.  Bylo naše číslo jeden problém od našich zákazníků, jsme chtěli jistotu, že jsme řešili v této verzi.  Jsme přizpůsobená naše servery, vytvořené na nové CDN a vylepšené dotaz logiku zpravidla dodávat vám relevantnější porovnávání a výsledky hledání budou rychlejší balíčku.

Jak jsme pokračovat prostřednictvím této fáze vývoje NuGet 3.0, jsme bude ladění a sledování služby nuget.org zajistit, že jsme poskytovat lepší prostředí.  Jsme nezadávejte plánujete používat na žádné výpadky, ale bude se přidání a změna prostředky ve službě.  Dohlížet na našem [twitter informačního kanálu](http://twitter.com/nuget) podrobnost, když se nám změnit konfiguraci služby.

## <a name="building-nuget-with-nuget"></a>Vytváření NuGet s NuGet

Nyní jsme mít rearchitected naše klienty NuGet do několika součásti, které jsou sami sestavuje do balíčků NuGet. Tato znovu používat naše vlastní knihovny vynutí nám sestavení součásti, které jsou opakovaně použitelné a který se dá správně zabalit.  Intenzivně jsme může eliminovat duplicitní kódu a dozvěděli, jak nakonfigurovat lépe naše procesu vývoje pro podporu potřeba sestavovat balíčky v našich řešení.  Vyhledejte příspěvku na blogu brzy kde bude mluvíme o tom, jak jsou strukturovaná projekty kódu a jak funguje naše procesu sestavení.

## <a name="stay-tuned"></a>Nenechte ujít

Prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a hlášení pro NuGet 3.0!
