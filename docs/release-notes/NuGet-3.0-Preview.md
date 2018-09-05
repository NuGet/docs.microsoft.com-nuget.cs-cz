---
title: Zpráva k vydání verze NuGet 3.0 ve verzi Preview
description: Poznámky k verzi NuGet 3.0 Preview, včetně známých problémů, opravy chyb, přidány nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546462"
---
# <a name="nuget-30-preview-release-notes"></a>Zpráva k vydání verze NuGet 3.0 ve verzi Preview

[Zpráva k vydání verze NuGet 2.9 RC](../release-notes/nuget-2.9-rc.md) | [zpráva k vydání verze NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 ve verzi Preview byla vydána 12. listopadu 2014 jako součást Visual Studio 2015 Preview verzi. Jsme vydali NuGet 3.0 ve verzi Preview. Toto je významným vydáním pro nás (byť ve verzi preview), a My jsme rádi začít získávat zpětnou vazbu na naše změny.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

V této verzi Preview NuGet 3.0 je součástí sady Visual Studio 2015 Preview. Pracujeme na dostat drops ve verzi preview pro sadu Visual Studio 2012 a Visual Studio 2013 velmi brzy. Dříve jste předváděli naše záměr [přestat aktualizace pro sadu Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), a jsme obtížná rozhodnutí.

## <a name="brand-new-ui"></a>Úplně nové uživatelské rozhraní

První, co zjistíte o NuGet 3.0 ve verzi Preview je naše zcela nové uživatelské rozhraní. Již není modální dialogové okno; Nyní je úplné okna dokumentu sady Visual Studio. Tímto způsobem lze najednou otevřít uživatelské rozhraní pro více projektů (a/nebo řešení), odtrhnout okna na jiný monitor, ukotvit ale byste to líbí, atd.

![Nové uživatelské rozhraní NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Nad rámec rozdíly použitelnost kvůli opuštění modální dialogové okno máme také řadu nových funkcí v nové uživatelské rozhraní.

### <a name="version-selection"></a>Výběr verze

Možná nejčastěji požadované funkce uživatelského rozhraní umožňující výběr verze pro balíček instalace a aktualizace – tato funkce je teď k dispozici.

![Výběr verze balíčku](./media/NuGet-3.0-Preview/version-selection.png)

Zda jsou instalujete nebo aktualizujete balíček, rozevírací seznam verzí vám umožní vidět všechny verze k dispozici pro balíček, se některé důležité verze přesunuty do horní části seznamu pro výběr snadno. Už nepotřebujete k získání konkrétních verzí, které nejsou na nejnovější verzi použijte konzolu Powershellu.

### <a name="combined-installedonlineupdates-workflows"></a>Kombinované nainstalované/Online/aktualizace pracovní postupy

Naše předchozí uživatelské rozhraní bylo nainstalováno, Online, a aktualizace 3 kartách. Balíčky uvedené byly specifické pro dané pracovní postupy a byly specifické pro pracovní postupy a akce, které jsou k dispozici. Zatímco, který vypadal jako logické Slyšeli jsme, že celá řada z vás bude často získat zasekne podle oddělení.

Teď máme kombinované prostředí, kde můžete nainstalovat, aktualizovat nebo odinstalovat balíček bez ohledu na to, jak jste získali balíčku vybrané. Jako pomoc s konkrétní pracovní postupy, nyní je k dispozici rozevírací seznam filtru, který vám umožní filtrovat viditelné balíčků, ale pak akce, které jsou k dispozici pro balíček jsou k dispozici konzistentní vzhledem k aplikacím.

![Odinstalovat balíček](./media/NuGet-3.0-Preview/uninstall-package.png)

Pomocí filtru "Nainstalováno", může potom snadno zobrazit nainstalované balíčky, které jsou dostupné aktualizace, a pak můžete odinstalovat nebo aktualizovat balíček tak, že změníte výběr verze zobrazíte změnit akce k dispozici.

![Aktualizace balíčku](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Konsolidace verze

Je běžné mít stejný balíček nainstalovat do více projektů v rámci vašeho řešení. Někdy verze nainstalované do jednotlivých projektů můžete odchylek od sebe a je nutné konsolidovat verze používá. NuGet 3.0 ve verzi Preview zavádí novou funkci pouze v tomto scénáři.

Okno správy balíčků úrovni řešení je přístupný kliknutím pravým tlačítkem na řešení a vyberete spravovat balíčky NuGet pro řešení. Odtud Pokud vyberte balíček, který je nainstalován do více projektů, ale s různými verzemi používá, novou akci "Konsolidovat" k dispozici. Na snímku níže, obrazovky `Newtonsoft.Json` byl nainstalován do `SamplesClassLibrary` s verzí `6.0.4` a jsou nainstalovaná do `SamplesConsoleApp` s verzí `5.0.4`.

![Konsolidace verze](./media/NuGet-3.0-Preview/consolidate.png)

Tady je pracovní postup pro konsolidaci do jedné verze.

1. Vyberte `Newtonsoft.Json` balíčku v seznamu
1. Zvolte `Consolidate` z `Action` rozevíracího seznamu
1. Použití `Version` rozevíracího seznamu vyberte verzi, které se mají konsolidovat do
1. Zaškrtněte políčka pro projekty, které by měly být konsolidovány do této verze (Všimněte si, že projekty už ve vybrané verzi zapnutá)
1. Klikněte na tlačítko `Consolidate` tlačítko provést sloučení

### <a name="operation-previews"></a>Operace verze Preview

Bez ohledu na to, kterou operaci provádíte – instalace/aktualizace/odinstalace – nové uživatelské rozhraní teď nabízí způsob, jak zobrazit náhled změn, které se pošle do vašeho projektu. V této verzi preview se zobrazí všechny nové balíčky, které nainstaluje balíčky, které se aktualizuje a balíčky, které bude odinstalován, společně s balíčky, které bude v průběhu operace beze změny.

V následujícím příkladu vidíme, že instalace Microsoft.AspNet.SignalR způsobí mnoho změn do projektu.

![Instalace funkce SignalR ve verzi Preview](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Možnosti instalace

Pomocí konzoly Powershellu, jste měli kontrolu nad několika možností významné instalace. Tyto funkce jsme teď jste zařazení do systému i uživatelského rozhraní. Nyní můžete řídit chování řešení závislostí pro jak se vybírají verze závislosti.

![Chování závislostí](./media/NuGet-3.0-Preview/dependency-behavior.png)

Můžete také zadat akce má být provedena, pokud soubory obsahu z balíčků jsou v konfliktu se soubory, které již ve vašem projektu.

![Akce při konfliktu souborů](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Nekonečné posouvání

Jsme použili k získání odlišují zpětné vazby na naše uživatelské rozhraní s oběma posouvání a stránkování paradigmat při výpisu balíčky. Bylo poměrně běžných muset posunout na konec krátký seznam, klikněte na tlačítko Další číslo stránky a posuňte se znovu. Pomocí nové uživatelské rozhraní implementovali jsme nekonečné posouvání v seznamu balíčků tak, že budete muset posunout – už nemusíte stránkování.

![Nekonečné posouvání](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Usnadnit práci, usnadňují rychlé, nastavte ji Pretty

Jsme nadšeni, abyste toto nové uživatelské rozhraní pro vás k vyzkoušení. Během této milník ve verzi Preview jsme následující funkční staré adage z "usnadňují práce, usnadňují rychlé, hodně usnadňují." V této verzi preview jsme dosažené výsledky většinu tento první cíle – to funguje. Víme, že se poměrně rychle ještě není a víme, že poměrně hodně ještě není. Vztah důvěryhodnosti, který budeme pracovat na tyto cíle a verzi RC. Do té doby, rádi uslyšíme vaše názory *použitelnost* nové uživatelské rozhraní – pracovní postupy, operace a jak ho *pracuje* používat nové uživatelské rozhraní.

Existuje několik funkcí, které jste odebrali jsme ve srovnání s původní uživatelské rozhraní. Jeden z nich je to tak úmyslně, a druhé právě neměli udělat v čase.

#### <a name="searching-all-package-sources"></a>Hledání "Vše" zdroje balíčků

Staré uživatelské rozhraní umožňují vyhledávat v balíčku pro všemi zdroji balíčku. Odebrali jsme funkci v uživatelském rozhraní a můžeme nesmí být převedení zpět. Tato funkce používá k provádění operací vyhledávání pro všemi zdroji balíčku, příběhů výsledky dohromady a pokus o řazení výsledků na základě vašeho výběru řazení.

Zjistili jsme, že je velmi obtížné příběhů společně hledání podle relevance. Může si představit prohledávání proti Google a Bing a společně tkaní výsledky? Kromě toho tato funkce byla pomalé a snadno *omylem* použití a My myslíte, že se jen zřídka skutečně užitečné. Z důvodu problémů funkce zavedená, dostali jsme řadu sestavy chyb na to, které by mohly nikdy jsme opravili.

#### <a name="update-all"></a>Aktualizovat vše

Mívali jsme "Aktualizovat vše" tlačítko v původní uživatelské rozhraní, která existuje v nové uživatelské rozhraní ještě není. Pro naše verzi RC jsme se resurrect tuto funkci.

## <a name="new-clientserver-api"></a>Nový klient/Server rozhraní API

Kromě všech těchto nových funkcí v naší nové uživatelské rozhraní správy balíčků jsme také pracovali na některé podrobnosti implementace protokolu Nugetu klient/server. Práce, kterou jsme provedli je vytvoření "Rozhraní API v3" pro NuGet, které jsou navržené s ohledem na vysokou dostupnost důležitých scénářů, jako je obnovení balíčků a instalace balíčků. Nové rozhraní API je postavena na REST a Hypermédia a My jsme vybrali [JSON-LD](http://json-ld.org) jako naše formát prostředku.

V bitech NuGet 3.0 ve verzi Preview uvidíte nový zdroj balíčků nazývá "preview.nuget.org" v rozevírací nabídce zdroje balíčku. Pokud vyberete tento zdroj balíčku, použijeme spíše pro připojení k nuget.org naše nové rozhraní API. Zpřístupnili jsme náhled zdroje v uživatelském rozhraní a dál budeme testování, opravit a zlepšit nové rozhraní API. Tento nový zdroj balíčků založená na v3 rozhraní API ve verzi RC: NuGet 3.0, nahradí zdroje balíčku na základě v2 "nuget.org".

Bez ohledu na investic, kterou jsme už vložení do rozhraní API v3 jsme provedli všechny tyto nové funkce fungovat i pro naše stávající rozhraní API v2 protokolu, to znamená, že bude fungovat s existující zdroje balíčků než nuget.org také.

## <a name="new-features-coming"></a>Novou funkcí produktů

Od tohoto okamžiku 3.0 RTM pracujeme také na některé základní nové NuGet, víc funkcí zobrazí v uživatelském rozhraní. Tady je krátký seznam charakteristiky investičních oblastí:

1. Naše partnerství s Visual Studio a nástroje MSBuild týmy, které chcete-li získat [NuGet do platformy pro hlubší](http://blog.nuget.org/20141014/in-the-platform.html).
1. Pracujeme na opustit konvence čas instalace balíčku a místo toho použít tyto konvence v době vytváření balíčků zavedením nového "autoritativní" [manifest balíčku](http://blog.nuget.org/20141023/package-manifests.html).
1. Pracujeme na Refaktorujte NuGet základu kódu provést opakovaně použitelné součásti klienta a serveru v různých doménách nad rámec správy balíčků v sadě Visual Studio.
1. Prošetřujeme pojem "soukromé závislosti" balíček můžete určit, kam se má závislosti na ostatní balíčky pouze podrobnosti implementace, a tyto závislosti by neměl být prezentované jako závislosti nejvyšší úrovně.

## <a name="stay-tuned"></a>Nenechte si ujít

Prosím dohlížet na [náš blog o](http://blog.nuget.org) další průběh a oznámení pro NuGet 3.0!