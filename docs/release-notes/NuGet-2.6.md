---
title: Poznámky k verzi 2.6 NuGet
description: Zpráva k vydání verze pro NuGet 2.6.1 pro WebMatrix, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551940"
---
# <a name="nuget-26-release-notes"></a>Poznámky k verzi 2.6 NuGet

[Zpráva k vydání verze NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 pro WebMatrix poznámky](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 byla vydána 26. června 2013.

## <a name="notable-features-in-the-release"></a>Důležité funkce ve verzi

### <a name="support-for-visual-studio-2013"></a>Podpora pro sadu Visual Studio 2013

NuGet 2.6 je první verze, která poskytuje podporu pro sadu Visual Studio 2013. A jako je Visual Studio 2012, rozšíření Správce balíčků NuGet je zahrnuto v každé edici sady Visual Studio.

Aby bylo možné poskytnout nejlepší možné podpory pro Visual Studio 2013 stále podporuje Visual Studio 2010 a Visual Studio 2012 a udržovala co nejmenší rozšíření velikosti, jsme se vytváření používat samostatné rozšíření pro Visual Studio 2013 při původní přípona pokračuje k cílení na Visual Studio 2010 a 2012.

Od verze NuGet 2.6, budeme publikovat dvě rozšíření, jak je uvedeno níže:

1. [Správce balíčků NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (platí pro Visual Studio 2010 a 2012)
1. [Správce balíčků NuGet pro Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Pomocí tohoto rozdělení [nuget.org](https://nuget.org) Domovská stránka "Nainstalovat NuGet" tlačítko vás přesměruje na [instalace NuGet](../install-nuget-client-tools.md) stránku, kde najdete další informace o instalaci různých klientů NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Podpora transformace XDT Web.config

Jednou z nejvíce velmi žádaných funkcí pro klienta NuGet bylo pro podporu výkonnější transformace XML pomocí XDT transformační modul, který se používá v transformacích konfigurace sestavení sady Visual Studio.

V dubnu 2013 se jsme provedli dvě velké objemy oznámení ohledně podpory NuGet XDT. První je, že samotné knihovny XDT se sám [vydané jako balíček NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) a [open source na webu CodePlex](http://xdt.codeplex.com/). Tento krok povolen modul XDT k volně používat jiný software open source, včetně klienta NuGet. Druhý oznámení byla plán podporovat použití XDT stroj pro transformace v klienta NuGet. NuGet 2.6 obsahuje tato integrační.

#### <a name="how-it-works"></a>Jak to funguje

Výhod podpory NuGet XDT mechanismu vypadat podobně jako u těch, které [aktuální funkce transformace config](../create-packages/source-and-config-file-transformations.md).
Soubory transformace jsou přidány do složky balíčku obsahu. Při konfiguraci transformace používat jediný soubor instalaci a odinstalaci, však XDT transformace povolit velice přesně kontrolovat, oba tyto procesy pomocí následující soubory:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Kromě toho NuGet používá příponu souboru k určení, které modul pro spuštění pro transformace, takže balíčky pomocí existující web.config.transforms budou nadále fungovat. Transformace XDT lze také použít k jakémukoli souboru XML (ne jenom web.config), takže můžete využít to u ostatních aplikací ve vašem projektu.

#### <a name="what-you-can-do-with-xdt"></a>Co můžete dělat s XDT

Jednou z jeho XDT největší předností je jeho [jednoduchou, ale výkonnou syntaxi](http://msdn.microsoft.com/library/dd465326.aspx) pro manipulaci s strukturu DOM XML Místo jednoduše zakreslovat jednu strukturu pevné dokumentu na jinou strukturu, XDT poskytuje ovládací prvky pro porovnání prvků v různými způsoby, od jednoduchého atribut název vzorů pro plnou podporu jazyka XPath. Po nalezení odpovídající prvek nebo sadu elementů XDT poskytuje bohatou sadu funkcí pro zpracování elementů, ať už to znamená, že přidání, aktualizace nebo odebrání atributů, uvedení nového elementu v konkrétním umístění, nebo nahrazení nebo odebrání celý element a jeho podřízené položky.

### <a name="machine-wide-configuration"></a>Konfiguraci celého počítače

Jednou z skvělé výhody NuGet je, že ho boří jinak velká spustitelný soubor nebo knihovny do sady modulární komponenty, které může být integrované a co je nejdůležitější udržované a verzuje nezávisle na sobě. Jeden vedlejším účinkem této, ale je, že konvenční představu o produktu nebo produktové řady potenciálně vypsalo.
Funkce zdroj vlastní balíček NuGet poskytuje jeden způsob uspořádání balíčky; zdroje balíčků vlastní však nejsou zjistitelné na své vlastní.

NuGet 2.6 rozšiřuje logiku pro konfiguraci NuGet tak, že na cestě % ProgramData%/NuGet/Config hierarchii složek. Instalační programy produktu můžete přidat vlastní NuGet konfigurační soubory v této složce k registraci balíčku vlastní zdroje pro své produkty. Struktura složek navíc podporuje sémantiku pro produkt, verze a dokonce i SKU integrovaného vývojového prostředí. Nastavení z těchto adresářů se použijí v uvedeném pořadí s prioritou strategie "poslední ve službě wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{verze}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{verze}\{SKU}\*.config

V tomto seznamu je zástupný symbol {IDE} specifické pro integrované vývojové prostředí, ve kterém je spuštěná NuGet, takže v případě sady Visual Studio, budou "Visual Studio". {Version} a {SKU} zástupné symboly jsou k dispozici v integrovaném vývojovém prostředí (např.) "11.0" a "WDExpress", "VWDExpress" a "Pro", v uvedeném pořadí). Složka pak může obsahovat mnoho různých *.config souborů.
Proto můžete, společnosti ACME komponenty jako součást svého instalačního programu produktu, přidat zdroj vlastní balíček, který bude viditelná pouze v verze Professional a Ultimate sady Visual Studio 2012, a to tak, že vytvoříte následující cesta k souboru:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Zatímco strukturu složek je jednoduché pro programů, jako je instalační programy softwaru přidat zdroje celého balíčku NuGet konfigurace, dialogové okno Konfigurace NuGet aktualizovali jsme také povolit pro registraci zdroje balíčků jako buď specifické pro uživatele (například registrace v % AppData%/NuGet/NuGet.Config) nebo celý počítač.

Tato funkce je využíváno Visual Studio 2013, kde je soubor nainstalovat na:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

V tomto souboru je nakonfigurovat nový zdroj balíčků nazývá "Rozhraní .NET Framework Packages".

![Nastavení v celé NuGet konfiguračního souboru počítače](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing vyhledávání

Počet balíčků, které jsou obsluhovány Galerie NuGet se stále rozrůstá exponenciální rychlostí, vylepšení hledání stále zůstává v horní části seznamu priorit NuGet. Mezi plánované funkce pro NuGet je kontextové vyhledávání, což znamená, že NuGet použije informace o verzi a SKU sady Visual Studio, kterou používáte a typu projektu, kterou vytváříte jako kritéria pro určení důležitosti potenciální vyhledávání výsledky.

Od verze NuGet 2.6, pokaždé, když je balíček nainstalován, kontext pro instalaci se zaznamenává jako část dat operace instalace.  Hledání také odeslat stejné kontextové informace, které vám umožní Galerie NuGet pro zvýšení výsledky hledání ve vývoji kontextové instalace.  Budoucí aktualizace Galerie NuGet vám umožní Tato kontextová relevance zvýšení skóre.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Sledování vs s přímým přístupem nainstaluje. Instalace závislostí

Autoři balíčku jsou čím dál tím víc spoléhat na [balíček statistiky](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) k dispozici v galerii NuGet.  Jednou z významné chybí datový bod, že autoři žádali je rozlišovat nainstaluje balíček s přímým přístupem a instalace závislostí.  Až doteď NuGet klient neodeslal jakýkoli kontext operace instalace, jestli pro vývojáře přímo nainstalovaný balíček nebo zda byl nainstalován splňovat závislost.
Od verze NuGet 2.6, že data se budou odesílat teď pro operaci instalace.  Statistiky balíčku v galerii NuGet zpřístupní tato data jako samostatné instalační operace s "-závislost" příponu.

* Instalace
* Instalace závislostí
* Aktualizace
* Aktualizace závislostí
* Znovu nainstalujte
* Znovu nainstalovat závislost

Kromě názvu jiné operace závislý balíček id také zaznamenána pro instalaci.  Budoucí aktualizace Galerie NuGet zpřístupní tato data v rámci sestavy, umožňuje autorům balíčků abyste úplně pochopili, jak vývojáři instalaci balíčků.

## <a name="bug-fixes"></a>Opravy chyb

NuGet 2.6 zahrnuje také několik oprav chyb. Úplný seznam pracovních položek opraveno ve verzi 2.6 NuGet, prosím zobrazení [NuGet sledování problémů pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).