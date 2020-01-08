---
title: Zpráva k vydání verze NuGet 2,6
description: Poznámky k verzi NuGet 2.6.1 pro WebMatrix, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384121"
---
# <a name="nuget-26-release-notes"></a>Zpráva k vydání verze NuGet 2,6

Zpráva k [vydání verze nuget 2,5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 pro poznámky k verzi WebMatrixu](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2,6 byl vydán 26. června 2013.

## <a name="notable-features-in-the-release"></a>Významné funkce v této verzi

### <a name="support-for-visual-studio-2013"></a>Podpora Visual Studio 2013

NuGet 2,6 je první verze, která poskytuje podporu pro Visual Studio 2013. A podobně jako v případě sady Visual Studio 2012 je rozšíření Správce balíčků NuGet součástí každé edice sady Visual Studio.

Abychom zajistili nejlepší možnou podporu pro Visual Studio 2013 a zároveň stále podporovali sadu Visual Studio 2010 i Visual Studio 2012 a co nejmenší velikost rozšíření, vytvoříme pro Visual Studio 2013 samostatné rozšíření. původní rozšíření i nadále cílí na sady Visual Studio 2010 a 2012.

Počínaje verzí NuGet 2,6 budeme publikovat dvě rozšíření níže:

1. [Správce balíčků NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (platí pro Visual Studio 2010 a 2012)
1. [Správce balíčků NuGet pro Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

V tomto rozdělení vám tlačítko pro instalaci NuGet domovské stránky [NuGet.org](https://nuget.org) přejde na stránku [instalace NuGet](../install-nuget-client-tools.md) , kde najdete další informace o instalaci různých klientů NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Podpora transformace Web. config XDT

Jednou z nejvysoce požadovaných funkcí pro klienta NuGet byla podpora výkonnějších transformací XML pomocí transformačního modulu XDT, který se používá při transformaci konfigurace sady Visual Studio.

V dubnu 2013 jsme vytvořili dvě velké oznámení týkající se podpory NuGet pro XDT. První je, že samotná knihovna XDT se samostatně [uvolnila jako balíček NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) a [Open source na webu CodePlex](http://xdt.codeplex.com/). Tento krok umožňuje, aby modul XDT byl volně využit jiným Open Source softwarem, včetně klienta NuGet. Druhé oznámení bylo plán, který podporuje použití modulu XDT k transformaci v klientovi NuGet. NuGet 2,6 zahrnuje tuto integraci.

#### <a name="how-it-works"></a>Jak to funguje

Aby bylo možné využít podporu XDT NuGet, mechanismus vypadá podobně jako u [aktuální funkce transformace konfigurace](../create-packages/source-and-config-file-transformations.md).
Transformační soubory jsou přidány do složky obsahu balíčku. Nicméně zatímco transformace konfigurace používají pro instalaci i odinstalaci jeden soubor, transformace XDT umožňují jemně odstupňovanou kontrolu nad oběma těmito procesy pomocí následujících souborů:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Kromě toho nástroj NuGet používá příponu souboru k určení, který modul se má spustit pro transformace, takže balíčky používající existující soubor Web. config. transformes budou fungovat i nadále. Transformace XDT lze také použít pro libovolný soubor XML (nikoli pouze Web. config), takže to můžete využít pro jiné aplikace v projektu.

#### <a name="what-you-can-do-with-xdt"></a>Co můžete dělat s XDT

Jednou z největších XDT je [jednoduchá, ale účinná syntaxe](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110)) pro manipulaci s STRUKTUROU modelu DOM XML. Místo pouhého překrytí jedné pevné struktury dokumentu do jiné struktury XDT poskytuje ovládací prvky pro vyhovující prvky různými způsoby, od jednoduchého názvu atributu, který odpovídá úplné podpoře XPath. Po nalezení odpovídajícího prvku nebo sady prvků XDT poskytuje bohatou sadu funkcí pro manipulaci s prvky, ať už to znamená přidání, aktualizaci nebo odebrání atributů, umístění nového prvku do konkrétního umístění nebo nahrazení nebo odebrání celé prvek a jeho podřízené položky.

### <a name="machine-wide-configuration"></a>Konfigurace na úrovni počítače

Jednou z skvělých silných funkcí NuGet je to, že rozděluje jinak velký spustitelný soubor nebo knihovnu do sady modulárních komponent, které se dají integrovat, a s nejdůležitější údržbou a nezávisle na sobě. Jedním z nich však je, že konvenční nápad produktové nebo produktové řady se bude potenciálně více fragmentovat.
Funkce vlastního zdroje balíčků NuGet nabízí jeden ze způsobů uspořádání balíčků. vlastní zdroje balíčků ale nepůjde zjistit sami.

NuGet 2,6 rozšiřuje logiku pro konfiguraci sady NuGet tím, že hledá hierarchii složek v cestě% Složka ProgramData%/NuGet/Config. Instalační programy produktu můžou do této složky přidat vlastní konfigurační soubory NuGet, aby si zaregistrovali vlastní zdroj balíčku pro svoje produkty. Kromě toho struktura složek podporuje sémantiku pro produkt, verzi a dokonce SKU rozhraní IDE. Nastavení z těchto adresářů se aplikují v následujícím pořadí s prioritou "poslední v WINS".

1. %ProgramData%\NuGet\Config\*. config
2. %ProgramData%\NuGet\Config\{IDE}\*. config
3. %ProgramData%\NuGet\Config\{IDE}\{verze}\*. config
4. %ProgramData%\NuGet\Config\{IDE}\{verze}\{SKU}\*. config

V tomto seznamu je zástupný symbol {IDE} specifický pro integrované vývojové prostředí (IDE), ve kterém je spuštěná aplikace NuGet, takže v případě sady Visual Studio se bude jednat o "VisualStudio". Zástupné symboly {Version} a {SKU} poskytuje IDE (např. "11,0" a "WDExpress", "VWDExpress" a "pro" v uvedeném pořadí). Složka pak může obsahovat mnoho různých souborů *. config.
Proto může společnost ACME Component jako součást instalačního programu produktu přidat vlastní zdroj balíčku, který bude viditelný pouze v edicích Professional a Ultimate sady Visual Studio 2012 vytvořením následující cesty k souboru:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Přestože struktura složek usnadňuje programům, jako jsou instalační programy pro přidání zdrojů balíčku do konfigurace NuGet, Aktualizovali jsme také dialogové okno Konfigurace NuGet, které umožňuje registraci zdrojů balíčků buď jako specifických pro uživatele (například zaregistrovaných v%/NuGet/NuGet.Config) nebo v rámci počítače.

Tato funkce je využívána nástrojem Visual Studio 2013, kde je nainstalován soubor v:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

V tomto souboru je nakonfigurovaný nový zdroj balíčku s názvem ".NET Framework balíčky".

![Nastavení konfiguračního souboru NuGet pro počítač](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing vyhledávání

Jelikož počet balíčků poskytovaných galerií NuGet stále roste v exponenciálním tempu, vylepšení hledání zůstane v horní části seznamu priorit NuGet. Jednou z plánovaných funkcí pro NuGet je kontextové hledání, což znamená, že NuGet bude používat informace o verzi a SKU sady Visual Studio, kterou používáte, a typu projektu, který sestavíte jako kritéria pro určení závažnosti potenciálního vyhledávání. důsledk.

Počínaje verzí NuGet 2,6 se při každém instalaci balíčku zaznamená kontext instalace jako součást dat operace instalace.  Hledání také odesílá stejné kontextové informace, což umožní galerii NuGet zvýšit výsledky hledání pomocí kontextových trendů instalace.  Budoucí aktualizace galerie NuGet umožní tuto kontextovou zvyšování relevance rozlišovat.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Sledování instalací s přímým přístupem vs. instalace závislostí

Autoři balíčků využívají více a další informace o [statistice balíčků](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) , které jsou k dispozici v galerii NuGet.  Jeden významný chybějící datový bod, na který autor požádal, je rozdíl mezi instalací přímých balíčků a instalací závislostí.  Až do této chvíle klient NuGet neodeslal žádný kontext kolem operace instalace, aby mohl vývojář přímo nainstalovat balíček nebo jestli byl nainstalovaný, aby vyhověl závislosti.
Počínaje verzí NuGet 2,6 budou data nyní odeslána k instalaci.  Statistika balíčku na galerii NuGet zveřejňuje tato data jako samostatné operace instalace s příponou "-Dependency".

* Instalace produktu
* Instalace – závislost
* Aktualizovat
* Aktualizace – závislost
* Přeinstalace
* Opětovná instalace – závislost

Kromě názvu jiné operace se pro instalaci zaznamená i ID závislého balíčku.  Budoucí aktualizace galerie NuGet zveřejňuje tato data v sestavách a umožní autorům balíčků plně pochopit, jak vývojáři instalují své balíčky.

## <a name="bug-fixes"></a>Opravy chyb

NuGet 2,6 obsahuje také několik oprav chyb. Úplný seznam pracovních položek opravených v NuGet 2,6 najdete v [přehledu problémů NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).