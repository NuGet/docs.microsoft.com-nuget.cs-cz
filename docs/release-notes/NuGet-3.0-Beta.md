---
title: Poznámky k verzi NuGet 3,0 beta
description: Poznámky k verzi pro NuGet 3,0 beta, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776627"
---
# <a name="nuget-30-beta-release-notes"></a>Poznámky k verzi NuGet 3,0 beta

Poznámky k verzi pro [NuGet 3,0 Preview](../release-notes/nuget-3.0-preview.md)  |  [Poznámky k verzi NuGet 3,0 RC](../release-notes/nuget-3.0-rc.md)

NuGet 3,0 Beta byla vydána 23. února 2015 pro vydání sady Visual Studio 2015 CTP 6. Tato verze znamená spoustu našeho týmu, protože máme řadu vylepšení architektury a výkonu ke sdílení a zajímá Vás, jak začít vyladit nastavení výkonu v naší službě nuget.org.

Před instalací této nové verze důrazně doporučujeme odinstalovat všechny předchozí verze rozšíření NuGet pro sadu Visual Studio 2015.  Pokud máte s touto verzí rozšíření nějaké problémy, doporučujeme vrátit se k [předchozí verzi](http://nuget.codeplex.com/downloads/get/909582) pro použití se sadou Visual Studio 2015 Preview.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Tato verze NuGet 3,0 beta je dostupná k instalaci v galerii rozšíření sady Visual Studio 2015 CTP 6. Pracujeme na získání verze Preview pro Visual Studio 2012 a brzy Visual Studio 2013. Dříve jsme naši záměr ukončili [aktualizace pro Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)a udělali jsme toto obtížné rozhodnutí.

## <a name="new-clientserver-api"></a>Nové rozhraní API pro klienty a servery

Pracovali jsme na některých podrobnostech implementace pro protokol klienta a serveru NuGet. K práci, kterou jsme dokončili, je vytvoření rozhraní API v3 pro NuGet, které je navržené kolem vysoké dostupnosti pro kritické scénáře, jako je například obnovení balíčků a instalace balíčků. Nové rozhraní API je založené na REST a na médiích a jako náš formát prostředku jsme vybrali [JSON-ld](http://json-ld.org) .

V bitech NuGet 3,0 beta se v rozevíracím seznamu zdroj balíčků zobrazí nový zdroj balíčku s názvem "api.nuget.org".   Pokud vyberete tento zdroj balíčku, budeme místo toho používat naše nové rozhraní API, abyste se připojili k nuget.org. V NuGet 3,0 RC tento nový zdroj balíčku založený na rozhraní API V3 nahradí zdroj balíčku "nuget.org" na bázi v2.  Doporučujeme, abyste zakázali všechny ostatní zdroje veřejných balíčků a ponechali jenom api.nuget.org jenom jako vaše jediné veřejné úložiště balíčků.

Do sestavení našeho rozhraní API V3 jsme vložili spoustu času a bude dál udržovat Standard v2 API pro staré klienty, kteří hledají přístup k veřejnému úložišti.

## <a name="updated-ui"></a>Aktualizované uživatelské rozhraní

V této vydané verzi jsme vylepšili uživatelské rozhraní, aby zahrnovalo pole se seznamem, které vám umožní vybrat akci, která se má provést s balíčkem, a převést tlačítko Preview na zaškrtávací políčko v oblasti možností obrazovky.  Oblast možností už není sbalitelná a teď poskytuje odkaz na téma, který popisuje dostupné možnosti.

![Nové uživatelské rozhraní NuGet](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>Protokolování operací

Odebrali jsme modální okno s informacemi o protokolování, které se při instalaci nebo odinstalaci rychle zobrazí a skryjí.  Toto okno nepřidalo žádnou hodnotu, pokud byste skutečně chtěli zobrazit informace nebo je kopírovat a vkládat.  Místo toho teď přesměrováváme všechny protokolování výstupu do podokna správce balíčků v okně výstup.  Myslíme si, že to je pohodlnější a podobná se obvyklé sestavě sestavení, kterou chcete zkontrolovat.


### <a name="focus-on-performance"></a>Zaměřit se na výkon

Provedli jsme spoustu změn v názvu zlepšení výkonu hledání NuGet a načítají se.  Toto číslo bylo jedním z našich zákazníků a chtěli jsme se ujistit, že v této verzi jsme ho řešili.  Vystavili jsme naše servery, vytvořili jsme nové CDN a vylepšili dotaz, který odpovídá Logic, aby snad doručování za relevantnější a rychlejší výsledky hledání balíčků.

Jak pokračujeme v této fázi vývoje NuGet 3,0, budeme ladit a monitorovat službu nuget.org, abychom zajistili, že budeme poskytovat vylepšené prostředí.  Neplánujeme zapojit do žádného výpadku, ale přidáváme a měníme prostředky ve službě.  Ponechte si na našem [informačním kanálu na Twitteru](http://twitter.com/nuget) podrobnosti o změně konfigurace služby.

## <a name="building-nuget-with-nuget"></a>Sestavování NuGet pomocí NuGet

Naši klienti NuGet jsme teď změnili na několik součástí, které jsou v balíčcích NuGet integrované. Toto opakované použití našich vlastních knihoven vynutí sestavení komponent, které lze znovu použít a které je možné správně zabalit.  Dokázali jsme eliminovat duplicitní kód a zjistili jsme, jak lépe nakonfigurovat náš vývojový proces tak, aby podporoval nutnost vytváření balíčků v těchto řešeních.  Vyhledáme Blogový příspěvek, kde budeme mluvit o struktuře kódových projektů a o tom, jak náš proces sestavení funguje.

## <a name="stay-tuned"></a>Zůstat vyladěné

Na [našem blogu](http://blog.nuget.org) prosím sledujte, kde najdete další informace o průběhu a oznámeních pro NuGet 3,0!
