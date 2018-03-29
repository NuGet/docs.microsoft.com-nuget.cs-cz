---
title: Poznámky k verzi Preview NuGet 3.0 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Poznámky k verzi pro náhled 3.0 NuGet včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
keywords: Náhled 3.0 NuGet poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f9f979e041ea6c7ba2f61603b1ea5848edc28f0c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-30-preview-release-notes"></a>Poznámky k verzi 3.0 Preview NuGet

[Poznámky k verzi RC NuGet 2.9](../release-notes/nuget-2.9-rc.md) | [poznámky k verzi NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 Preview byla vydána 12. listopadu 2014 jako součást Visual Studiu 2015 Preview verze. Jsme vydali NuGet 3.0 Preview. Toto je velký verze pro nás (i když náhled), a máme nadšení zahájíte získávání názory na naše změny.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Tato verze Preview NuGet 3.0 je součástí Visual Studiu 2015 Preview. Pracujeme na velmi brzy získat vyřazuje preview pro sadu Visual Studio 2012 a Visual Studio 2013. Jsme předtím sdílené naše záměr [přestali aktualizace pro sadu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), a jsme Ujistěte se, že obtížné rozhodnutí.

## <a name="brand-new-ui"></a>Nové uživatelské rozhraní

První věcí, kterou jste si všimli o NuGet 3.0 Preview je naše nové uživatelské rozhraní. Je už modální dialogové okno; Teď je úplná okna dokumentu sady Visual Studio. Můžete tak otevřít uživatelské rozhraní pro více projektů (nebo řešení) jednou, oddělení okna na druhém monitoru, ukotvení ho ale byste jako atd.

![Nové uživatelské rozhraní NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Nad rámec rozdílů použitelnost kvůli zrušení modální dialogové okno máme také mnoha nových funkcí v novém uživatelském rozhraní.

### <a name="version-selection"></a>Výběr verze

Pravděpodobně nejvíc požadované funkce uživatelského rozhraní je umožnit výběr verze pro instalaci balíčku a aktualizace – to je nyní k dispozici.

![Výběr verze balíčku](./media/NuGet-3.0-Preview/version-selection.png)

Ať už jsou instalace nebo aktualizace balíčku, verzi rozevíracího seznamu vám umožní vidět všechny verze k dispozici pro balíček s některé významné verze povýšen na začátku seznamu pro výběr snadné. Již nepotřebujete k získání konkrétních verzí, které nejsou na nejnovější použít konzolu prostředí PowerShell.

### <a name="combined-installedonlineupdates-workflows"></a>Kombinovaná pracovních nainstalován/Online/aktualizace

Naše předchozí uživatelské rozhraní umožňovaly 3 karty nainstalovaná, Online a aktualizace. Balíčky uvedené byly specifické pro dané pracovní postupy a specifické pro pracovní postupy a byly dostupné akce. Při který mailech vypadalo logické že Slyšeli jsme, že řada z vás by často získat přerušovačů toto oddělení.

Nyní je k dispozici kombinované prostředí, kde můžete nainstalovat, aktualizovat nebo odinstalovat balíček bez ohledu na to, jak jste získali vybraný balíček. Jako pomoc s konkrétní pracovní postupy, nyní je k dispozici rozevírací filtru, která vám umožní filtrovat zobrazené balíčků, ale pak akce dostupné pro balíček jsou konzistentní.

![Odinstalace balíčku](./media/NuGet-3.0-Preview/uninstall-package.png)

Pomocí filtru "Nainstalovaná", můžete snadno zobrazí vaše nainstalované balíčky, které jsou dostupné aktualizace, a pak můžete odinstalovat nebo aktualizovat balíček změnou výběr verze zobrazíte změnit akce k dispozici.

![Aktualizace balíčku](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Konsolidace verze

Je běžné tak, aby měl stejné balíček nainstalován do více projektů v rámci vašeho řešení. Někdy může verze nainstalované do každého projektu soubor od sebe a je nutné konsolidovat verze používán. NuGet 3.0 Preview zavádí novou funkci právě v tomto scénáři.

Okno Správa řešení úrovni balíčku přístupná pomocí pravým tlačítkem myši na řešení a zvolte spravovat balíčky NuGet pro řešení. Odtud Pokud vyberete balíček, který je nainstalován do více projektů, ale s různými verzemi používá, a novou akci "Konsolidace" k dispozici. Na obrazovce snímek níže `Newtonsoft.Json` byl nainstalován do `SamplesClassLibrary` s verzí `6.0.4` a nainstalované do `SamplesConsoleApp` s verzí `5.0.4`.

![Konsolidovat verze](./media/NuGet-3.0-Preview/consolidate.png)

Zde je pracovní postup pro konsolidaci do jedné verze.

1. Vyberte `Newtonsoft.Json` balíčku v seznamu
1. Zvolte `Consolidate` z `Action` rozevíracího seznamu
1. Použití `Version` rozevíracího seznamu vyberte verzi, které se mají konsolidovat do
1. Zaškrtněte políčka pro projekty, které by měly být konsolidovány do této verze (Všimněte si, že bude projekty už ve vybrané verzi šedá)
1. Klikněte `Consolidate` tlačítko provádět konsolidací

### <a name="operation-previews"></a>Operace verze Preview

Bez ohledu na to, kterou operaci, kterou právě provádíte--instalace nebo aktualizace/odinstalace – nové uživatelské rozhraní teď nabízí způsob, jak zobrazení náhledu změn, které budou provedeny do projektu. Tato verze preview se zobrazí všechny nové balíčky, které se nainstalují, balíčky, které budou aktualizovány a balíčky, které bude odinstalován, společně s balíčky, které budou během operace beze změny.

V následujícím příkladu jsme uvidí, že instalace Microsoft.AspNet.SignalR dojde v mnoha změny do projektu.

![Náhled instalaci SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Možnosti instalace

Pomocí konzoly Powershellu, jste měli kontrolu nad několika možností významné instalace. Tyto funkce jsme teď jste začlenění do uživatelského rozhraní také. Nyní můžete řídit chování řešení závislostí pro jak jsou vybrané verze ze závislostí.

![Chování závislostí](./media/NuGet-3.0-Preview/dependency-behavior.png)

Můžete také zadat akce, které se má provést při soubory obsahu z balíčků v konfliktu s soubory už v projektu.

![Soubor konflikt akce](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Nekonečné posouvání

Jsme použili k získání odlišují zpětné vazby na naše uživatelské rozhraní s i posouvání a stránkování vzorů při výpisu balíčků. Bylo poměrně běžně používají přejděte do dolní části seznamu krátké, klikněte na tlačítko Další číslo stránky a posuňte se znovu. Pomocí nového uživatelského rozhraní implementovali jsme nekonečné posouvání v seznamu balíčků tak, že potřebujete posuňte – žádné další stránkování.

![Nekonečné posouvání](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Nastavit jej jako pracovní, zkontrolujte je rychlý, zkontrolujte jej Pretty

Snažíme se nadšení získat toto nové uživatelské rozhraní můžete vyzkoušet. Během této milník Preview jsme jsme následující funkční staré adage z "Díky práce, zkontrolujte rychlé, ujistěte se, je poměrně." V této verzi preview jsme jste provést většinu z této prvním cílem – funguje. Víme poměrně rychle ještě není a víme, že poměrně poměrně ještě není. Vztah důvěryhodnosti, který budete mít pracujeme na tyto cíle od tohoto okamžiku verze RC. Do té doby, budeme rádi uslyšíme vaše názory *použitelnost* nového uživatelského rozhraní – pracovní postupy, operace a jak ho *funguje* pomocí nového uživatelského rozhraní.

Existuje několik funkcí, které jsme odebrali ve srovnání s původním uživatelského rozhraní. Jednu z těchto byl úmyslné a jiného právě nebyla získat provádějí v čase.

#### <a name="searching-all-package-sources"></a>Hledání "Vše" zdroje balíčků

Rozhraní staré povoleno můžete provádět vyhledávání balíčku pro všechny vaše zdroje balíčku. Odebrali jsme tuto funkci v uživatelském rozhraní a jsme nebude možné převedení zpět. Tato funkce používá k provádění operací hledání pro všechny vaše zdroje balíčku weave výsledky společně a pokus o řazení výsledků na základě řazení výběru.

Zjistili jsme, že závažnost hledání je skutečně obtížné weave společně. Může vám Představte si prohledávání proti Google a Bing a společně tkaní výsledky? Kromě toho tato funkce byla pomalé, snadno *omylem* použití a My domníváte se zřídka ve skutečnosti užitečné. Z důvodu problémů funkce zavedená, dostali jsme řadu sestav chyb v něm, které by mohly nikdy byly opraveny.

#### <a name="update-all"></a>Aktualizuje všechny

Použili jsme "Aktualizovat vše" tlačítko k dispozici v původním uživatelské rozhraní, které nejsou v novém uživatelském rozhraní ještě. Tato funkce jsme se resurrect pro naše verzi RC.

## <a name="new-clientserver-api"></a>Nový klient Server rozhraní API

Kromě všech těchto nových funkcí v našich nové uživatelské rozhraní správy balíčků jste také byla pracujeme na některé podrobnosti implementace pro protokol klienta nebo serveru NuGet. Práci, kterou jsme krok je vytvoření "API v3" pro NuGet, který je určený kolem vysoké dostupnosti u kritických scénářů, jako je obnovení balíčků a instalaci balíčků. Nové rozhraní API je založena na REST a hypermédií a jsme vybrali [JSON-LD](http://json-ld.org) jako formát naše prostředku.

V bitech NuGet 3.0 Preview zobrazí nový zdroj balíčků s názvem "preview.nuget.org" v rozevírací nabídce zdroje balíčku. Pokud vyberete tento zdroj balíčku, použijeme místo pro připojení k nuget.org naší nové rozhraní API. Jsme provedli jsme zdroji preview k dispozici v uživatelském rozhraní při budeme nadále otestovat, zkontrolovat, jestli a zlepšit nového rozhraní API. Tento nový zdroj balíčků na základě v3 rozhraní API v NuGet 3.0 RC, nahradí zdroje balíčku na základě v2 "nuget.org".

Navzdory investice, které začne do rozhraní API v3 jsme provedli všechny tyto nové funkce se naše existující rozhraní API v2 protokol, což znamená, že bude fungovat s existující zdroje balíčku než nuget.org také fungovat.

## <a name="new-features-coming"></a>Nové funkce, než dorazí

Od tohoto okamžiku 3.0 RTM také pracujeme na některé základní NuGet kromě funkcí funkcí, co se zobrazí v uživatelském rozhraní. Tady je seznam krátké nejdůležitějšími investice oblastí:

1. Nemůžeme se partnerství se sady Visual Studio a nástroje MSBuild týmy získat [NuGet hlubší do platformy](http://blog.nuget.org/20141014/in-the-platform.html).
1. Pracujeme na abandon konvence doba instalace balíčku a místo toho použijte tyto konvence během balení zavedením nové "autoritativní" [manifest balíčku](http://blog.nuget.org/20141023/package-manifests.html).
1. Pracujeme na refactor NuGet codebase – Chcete-li znovu použitelné součásti klienta a server v různých doménách nad rámec správy balíčků v sadě Visual Studio.
1. Zkoumán představu o "privátní závislosti", kde balíček můžete určit, které se má závislosti na dalších balíčků pouze podrobnosti implementace a tyto závislosti by neměl být prezentované jako závislosti nejvyšší úrovně.

## <a name="stay-tuned"></a>Nenechte ujít

Prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a hlášení pro NuGet 3.0!