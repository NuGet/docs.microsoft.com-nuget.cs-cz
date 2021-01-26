---
title: Poznámky k verzi pro NuGet 3,0 Preview
description: Poznámky k verzi pro NuGet 3,0 Preview včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780328"
---
# <a name="nuget-30-preview-release-notes"></a>Poznámky k verzi pro NuGet 3,0 Preview

Poznámky k verzi [NuGet 2,9 RC](../release-notes/nuget-2.9-rc.md)  |  [Poznámky k verzi NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)

NuGet 3,0 Preview byl vydán 12. listopadu 2014 jako součást verze Visual Studio 2015 Preview. Vydali jsme NuGet 3,0 Preview. Toto je Velká verze pro nás (i když je to verze Preview) a zajímáme se, abychom mohli začít získávat zpětnou vazbu k našim změnám.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Tato verze NuGet 3,0 Preview je součástí sady Visual Studio 2015 Preview. Pracujeme na získání verze Preview pro Visual Studio 2012 a brzy Visual Studio 2013. Dříve jsme naši záměr ukončili [aktualizace pro Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html)a udělali jsme toto obtížné rozhodnutí.

## <a name="brand-new-ui"></a>Nové uživatelské rozhraní značky

První věc o NuGet 3,0 Preview je naše značka nové uživatelské rozhraní. Už není modální dialog. Teď je to celé okno dokumentu sady Visual Studio. To vám umožní otevřít uživatelské rozhraní pro více projektů (a/nebo řešení) najednou, odtrhnout okno na jiný monitor, ukotvit ho, pokud chcete, atd.

![Nové uživatelské rozhraní NuGet](./media/NuGet-3.0-Preview/new-ui.png)

Mimo rozdíl mezi použitelnostmi z důvodu opuštění modálního dialogového okna máme také spoustu nových funkcí v novém uživatelském rozhraní.

### <a name="version-selection"></a>Výběr verze

Možná nejvíce požadovaná funkce uživatelského rozhraní je to, aby bylo možné vybrat verzi pro instalaci balíčku a aktualizaci – nyní je k dispozici.

![Výběr verze balíčku](./media/NuGet-3.0-Preview/version-selection.png)

Bez ohledu na to, jestli instalujete nebo aktualizujete balíček, vám v rozevírací nabídce verze zobrazíte všechny verze, které jsou pro balíček k dispozici, a některé významné verze se v horní části seznamu povýší pro snadný výběr. Nemusíte už používat konzolu PowerShellu k získání konkrétních verzí, které nejsou nejnovější.

### <a name="combined-installedonlineupdates-workflows"></a>Pracovní postupy kombinované instalace/online/aktualizací

Naše předchozí uživatelské rozhraní obsahovalo 3 karty pro instalaci, online a aktualizace. Uvedené balíčky byly specifické pro tyto pracovní postupy a dostupné akce byly také specifické pro pracovní postupy. I když se to zdálo jako logické, zjistili jsme, že mnohé z nich byste často Trip prostřednictvím tohoto oddělení.

Teď máme kombinované prostředí, kde můžete balíček nainstalovat, aktualizovat nebo odinstalovat, a to bez ohledu na to, jak jste balíček vybrali. Abychom vám pomohli s konkrétními pracovními postupy, teď máme rozevírací seznam filtr, který umožňuje filtrovat balíčky, ale akce dostupné pro balíček jsou konzistentní.

![Odinstalace balíčku](./media/NuGet-3.0-Preview/uninstall-package.png)

Když použijete filtr "installed", můžete snadno zobrazit nainstalované balíčky, u kterých jsou k dispozici aktualizace, a pak můžete balíček odinstalovat nebo aktualizovat změnou výběru verze, aby se zobrazila změna dostupné akce.

![Aktualizace balíčku](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Konsolidace verzí

Je běžné, že máte nainstalovaný stejný balíček do více projektů v rámci vašeho řešení. Někdy se verze nainstalovaná do každého projektu můžou oddělit a je potřeba sjednotit používané verze. NuGet 3,0 Preview zavádí novou funkci jenom pro tento scénář.

Kliknutím pravým tlačítkem na řešení a zvolením možnosti spravovat balíčky NuGet pro řešení lze použít okno pro správu balíčků na úrovni řešení. Odtud platí, že pokud vyberete balíček, který je nainstalovaný do více projektů, ale u různých používaných verzí, bude k dispozici nová akce "konsolidace". V níže uvedeném snímku obrazovky `Newtonsoft.Json` byla nainstalovaná `SamplesClassLibrary` verze s verzí `6.0.4` a nainstalovaná do `SamplesConsoleApp` verze `5.0.4` .

![Konsolidovat verze](./media/NuGet-3.0-Preview/consolidate.png)

Tady je pracovní postup pro konsolidaci do jedné verze.

1. Vybrat `Newtonsoft.Json` balíček v seznamu
1. Zvolit `Consolidate` z `Action` rozevíracího seznamu
1. Pomocí `Version` rozevíracího seznamu vyberte verzi, na kterou se má konsolidovat.
1. Zaškrtněte políčka pro projekty, které by měly být konsolidovány do této verze (Všimněte si, že projekty, které už jsou ve vybrané verzi, budou šedé)
1. Kliknutím na `Consolidate` tlačítko proveďte konsolidaci.

### <a name="operation-previews"></a>Náhledy operací

Bez ohledu na to, jakou operaci provádíte – – instalace/aktualizace/odinstalace – nové uživatelské rozhraní teď nabízí způsob, jak zobrazit náhled změn, které se provedou v projektu. V této verzi Preview se zobrazí všechny nové balíčky, které se budou instalovat, balíčky, které se budou aktualizovat, a balíčky, které se odinstalují, a balíčky, které se během této operace nemění.

V následujícím příkladu vidíte, že instalace Microsoft. AspNet. Signal bude mít za následek poměrně několik změn projektu.

![Instalace signálu Preview](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Možnosti instalace

Pomocí konzoly PowerShellu byste měli mít kontrolu nad několika významnými možnostmi instalace. Tyto funkce jsme teď nastavili i do uživatelského rozhraní. Nyní můžete řídit chování rozlišení závislosti pro způsob, jakým jsou vybrány verze závislostí.

![Chování závislostí](./media/NuGet-3.0-Preview/dependency-behavior.png)

Můžete také zadat akci, která má být provedena, když soubory obsahu z balíčků jsou v konfliktu se soubory, které jsou již v projektu.

![Akce při konfliktu souborů](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Nekonečné posouvání

V našem uživatelském rozhraní se používáme k tomu, abychom při výpisu balíčků měli poměrně značnou část zpětné vazby. Je poměrně běžné, že se posuňte do dolní části krátkého seznamu, kliknete na číslo další stránky a znovu se posuňte. S novým uživatelským rozhraním jsme v seznamu balíčků implementovali nekonečné posouvání, abyste se mohli jenom posouvat jenom o další stránkování.

![Nekonečné posouvání](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Udělejte to jako funkční, rychle se zajistěte, udělejte to v podstatě

Jsme rádi, že vám toto nové uživatelské rozhraní vyzkoušíme. Během tohoto milníku ve verzi Preview jsme povedli dobrý Star pořekadlem o tom, jak to funguje, a to tak, aby bylo v podstatě. " V této verzi Preview jsme provedli většinu tohoto prvního cíle – to funguje. Víme, že ještě není poměrně rychlé a ví, že ještě není poměrně poměrně. Vztah důvěryhodnosti, který budeme pracovat na těchto cílech mezi teď a verzí RC. Mezitím bychom rádi slyšeli svůj názor na *použitelnost* nového uživatelského rozhraní – pracovní postupy, operace a to, jak se *zdá* , že se nové uživatelské rozhraní používá.

Existuje několik funkcí, které jsme odebrali ve srovnání se starým uživatelským rozhraním. Jedna z nich byla úmyslné a druhá z nich se neudělala v čase.

#### <a name="searching-all-package-sources"></a>Hledají se zdroje balíčků "All"

Staré uživatelské rozhraní vám umožnilo provést hledání balíčku se všemi zdroji balíčků. Tuto funkci jsme odebrali v uživatelském rozhraní a my ji nebudeme vracet. Tato funkce se používá k provádění operací vyhledávání u všech zdrojů balíčků, spojování výsledků společně a pokus o řazení výsledků na základě výběru řazení.

Zjistili jsme, že je v zásadě obtížné spojit se vazbou. Mohli byste si představit hledání na Google a Bingu a výsledky tkaní společně? Tato funkce byla navíc pomalá, snadno se *nechtěně* nepoužívá. Domníváme se, že je výjimečně užitečná. Vzhledem k problémům, které zavedla funkce, jsme na ni dostali spoustu zpráv o chybách, které se nikdy neopravily.

#### <a name="update-all"></a>Aktualizovat vše

Použili jsme tlačítko Aktualizovat vše ve starém uživatelském rozhraní, které ještě není v novém uživatelském rozhraní. Tuto funkci budeme obnovení pro naši verzi RC.

## <a name="new-clientserver-api"></a>Nové rozhraní API pro klienty a servery

Kromě všech nových funkcí v naší nové uživatelské rozhraní pro správu balíčků jsme také pracovali na některých podrobnostech implementace pro protokol klienta a serveru NuGet. K práci, kterou jsme dokončili, je vytvoření rozhraní API v3 pro NuGet, které je navržené kolem vysoké dostupnosti pro kritické scénáře, jako je například obnovení balíčků a instalace balíčků. Nové rozhraní API je založené na REST a na médiích a jako náš formát prostředku jsme vybrali [JSON-ld](http://json-ld.org) .

V bitech NuGet 3,0 Preview se v rozevíracím seznamu zdroj balíčků zobrazí nový zdroj balíčku s názvem "preview.nuget.org". Pokud vyberete tento zdroj balíčku, budeme místo toho používat naše nové rozhraní API, abyste se připojili k nuget.org. V uživatelském rozhraní jsme provedli zdroj verze Preview, ale pokračujeme v testování, revizi a vylepšení nového rozhraní API. V NuGet 3,0 RC tento nový zdroj balíčku založený na rozhraní API V3 nahradí zdroj balíčku "nuget.org" na bázi v2.

Navzdory investicím do rozhraní API V3 jsme všechny tyto nové funkce také pracovali s naším stávajícím protokolem API v2, což znamená, že budou fungovat i s existujícími zdroji balíčků kromě nuget.org.

## <a name="new-features-coming"></a>Nové funkce přicházejí

Mezi Now a 3,0 RTM jsme také pracovali na některých základních nových funkcích NuGet, a to nad rámec toho, co vidíte v uživatelském rozhraní. Tady je krátký seznam nejdůležitějšímich investičních oblastí:

1. Spolupracujeme se sadou Visual Studio a týmy MSBuild, abychom mohli získat hlubší přístup k [platformě NuGet](http://blog.nuget.org/20141014/in-the-platform.html).
1. Pracujeme na opuštění konvencí balíčků při instalaci a místo toho se tyto konvence použijí v době balení. zavádí se nový "autoritativní" [manifest balíčku](http://blog.nuget.org/20141023/package-manifests.html).
1. Pracujeme na refaktorování základu NuGet k tomu, aby komponenty klienta a serveru byly opakovaně použitelné v různých doménách, a to i v rámci správy balíčků v sadě Visual Studio.
1. Zkoumáme pojem "privátní závislosti", kde balíček může indikovat, že má závislosti na dalších balíčcích jenom pro podrobnosti o implementaci, a tyto závislosti by neměly být surfované jako závislosti nejvyšší úrovně.

## <a name="stay-tuned"></a>Zůstat vyladěné

Na [našem blogu](http://blog.nuget.org) prosím sledujte, kde najdete další informace o průběhu a oznámeních pro NuGet 3,0!