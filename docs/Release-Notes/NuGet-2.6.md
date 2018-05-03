---
title: Poznámky k verzi 2.6 NuGet
description: Poznámky k verzi pro NuGet 2.6.1 pro službu WebMatrix, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39ce6ac3d36464d26966b0dabb0893f09ad4afdc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-26-release-notes"></a>Poznámky k verzi 2.6 NuGet

[Poznámky k verzi NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 poznámky k verzi služby WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 byla vydána 26 červen 2013.

## <a name="notable-features-in-the-release"></a>Upozorňují na důležité funkce ve verzi

### <a name="support-for-visual-studio-2013"></a>Podpora pro Visual Studio 2013

NuGet 2.6 je první verze, která poskytuje podporu pro Visual Studio 2013. A jako Visual Studio 2012, je rozšíření Správce balíčků NuGet zahrnuty v každé verzi sady Visual Studio.

Chcete-li poskytovat nejlepší možný podpora pro Visual Studio 2013 při stále podpora Visual Studio 2010 a Visual Studio 2012 a udržování velikosti rozšíření co nejmenší, se vyrábí samostatné rozšíření pro Visual Studio 2013 při původní přípona i nadále cílové sady Visual Studio 2010 a 2012.

Od verze NuGet 2.6, budeme publikovat dvě rozšíření, jak je uvedeno níže:

1. [Správce balíčků NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (platí pro Visual Studio 2010 a 2012)
1. [Správce balíčků NuGet pro Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

S toto rozdělení [nuget.org](https://nuget.org) domovské stránky "Nainstalovat NuGet" tlačítko přejdete k [instalace NuGet](../install-nuget-client-tools.md) stránky, kde můžete najít další informace o instalaci různých klientů NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Podpora transformaci XDT Web.config

Jedna z funkcí nejvíce vysoce požadovaných pro klienta NuGet byl pro podporu výkonnější transformace XML pomocí XDT transformační modul, který se používá v sadě Visual Studio sestavení konfigurace transformace.

V duben 2013 jsme provedli dva big oznámení týkajících se podpory NuGet XDT. První bylo, že samotné knihovny XDT se sám sebe [vydané jako balíčku NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) a [open source na webu CodePlex](http://xdt.codeplex.com/). Tento krok povolit, aby modul XDT volně používat jiné open-source softwaru, včetně klienta NuGet. Druhý oznámení se plán podporovat použití modulu XDT transformace v klientovi NuGet. NuGet 2.6 zahrnuje Tato integrace.

#### <a name="how-it-works"></a>Jak to funguje

Abyste mohli využívat podpory XDT NuGet, vypadat podobně jako u mechanismů [funkce transformace aktuální konfigurace](../create-packages/source-and-config-file-transformations.md).
Transformace soubory budou přidány do složky obsahu balíčku. Ale při transformace konfigurace používat jeden soubor pro instalaci a odinstalaci, XDT transformace povolit jemně odstupňovanou kontrolu nad oba tyto procesy pomocí následující soubory:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Kromě toho NuGet používá přípona souboru k určení které modul pro transformace, aby do balíčky pomocí existující web.config.transforms budou nadále fungovat. Transformace XDT je také možné použít na libovolný soubor XML (nikoli pouze soubor web.config), takže můžete využít to u ostatních aplikací ve vašem projektu.

#### <a name="what-you-can-do-with-xdt"></a>Co můžete dělat s XDT

Jeden z XDT na největší síly je jeho [jednoduchou, ale výkonnou syntaxi](http://msdn.microsoft.com/library/dd465326.aspx) pro manipulaci s strukturu XML modelu DOM. Místo jednoduše překrytí jeden pevný dokumentu struktura na jinou strukturu, poskytuje XDT ovládací prvky pro párování elementů v mnoha různými způsoby, od jednoduchého atribut na plnou podporu jazyka XPath s odpovídajícím názvem. Jakmile je nalezen odpovídající element nebo sadu elementů, XDT poskytuje bohatou sadu funkcí pro manipulaci s prvky, ať to znamená, přidání, aktualizace, nebo odebrání atributů, umístění nového elementu v určitém místě, nebo nahrazení nebo odebrání celý element a její podřízené položky.

### <a name="machine-wide-configuration"></a>Konfigurace celého systému

Jedním z skvělé síly NuGet je, že dělí dolů jinak velká spustitelný soubor nebo knihovny do sady modulární součásti, které můžou být integrované a co je nejdůležitější zachována a verzí nezávisle. Jeden vedlejším účinkem této, je však konvenční představu o produktu nebo produktové řadě stane potenciálně více fragmentace.
Funkce zdroj vlastní balíček NuGet poskytuje jeden způsob organizace balíčky; vlastní balíček zdroje jsou však není zjistitelný na své vlastní.

NuGet 2.6 rozšiřuje logiku pro hledání hierarchii složek na cestě % ProgramData%/NuGet/Config konfiguraci NuGet. Instalační programy produktu můžete přidat vlastní NuGet konfigurační soubory v této složce registrovat zdroj vlastní balíček pro jejich produkty. Struktura složek navíc podporuje sémantiku pro produkt, verzi a i SKU rozhraní IDE. Nastavení z těchto adresářů se použijí v uvedeném pořadí s přednost strategie "poslední ve službě wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{verze}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{verze}\{SKU}\*.config

V tomto seznamu je zástupný symbol {IDE} specifické pro prostředí IDE, ve kterém běží NuGet, tak v případě Visual Studio, bude "Visual Studio". {Version} a {SKU} zástupné symboly jsou poskytovány rozhraní IDE (např.) "11.0" a "WDExpress", "VWDExpress" a "Pro", v uvedeném pořadí). Složka pak může obsahovat mnoho různých *.config souborů.
Proto můžete, společnost součást pokusná jako součást své instalační program produktu, přidat zdroj vlastní balíček, který bude zobrazen pouze verze Professional a Ultimate sady Visual Studio 2012, a to vytvořením následující cesta k souboru:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Při struktura složek provede přehledné pro programy, jako je instalační programy softwaru přidat celého balíčku zdroje do konfigurace NuGet, dialogové okno Konfigurace NuGet má také aktualizovaná tak, aby povolit pro registraci zdroje balíčků jako buď konkrétního uživatele (například registrován v % AppData%/NuGet/NuGet.Config) nebo celého systému.

Tato funkce je využíváno Visual Studio 2013, kde je nainstalován soubor na:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

V rámci tohoto souboru je nakonfigurován nový zdroj balíčků s názvem "Rozhraní .NET Framework Packages".

![Nastavení široké NuGet konfiguračním souboru počítače](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing vyhledávání

Počet balíčků, obsloužených Galerie NuGet stále rostoucí exponenciální rychlostí, vylepšení hledání zůstane někdy v horní části seznamu priorit NuGet. Jeden z plánované funkce pro NuGet je kontextová vyhledávání, což znamená, že NuGet použije informace o verzi a SKU z Visual Studia, která používáte a typu projektu, který vytváříte jako kritéria pro určení důležitosti potenciální hledání výsledky.

Od verze NuGet 2.6, pokaždé, když je balíček nainstalován, kontext pro instalaci se zaznamenává jako součást instalace provozní data.  Hledání také odeslat stejné kontextové informace, které vám umožní Galerie NuGet pro zvýšení výsledků vyhledávání ve vývoji kontextové instalace.  Budoucí aktualizace do Galerie NuGet vám umožní Tato kontextová relevance zvyšovat skóre.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Sledování přímé nainstaluje vs. Nainstaluje závislostí

Autoři balíčku jsou více spoléhat na [balíček statistiky](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) zadaný v galerii NuGet.  Jedna významné chybějící datového bodu, aby autoři žádali je rozdíl mezi přímé balíček nainstaluje a instalaci závislostí.  Dosud klienta NuGet neodeslal žádné kontextu kolem instalační operace pro jestli vývojář přímo daný balíček nainstalován, nebo zda byl nainstalován vyhovět závislost.
Od verze NuGet 2.6, že data se nyní odesílají pro operaci instalace.  Balíček statistiky v galerii NuGet zveřejní dat jako samostatnou instalaci operace s "-závislost" příponu.

* Instalace
* Instalace závislostí
* Aktualizace
* Aktualizace závislostí
* Přeinstalujte
* Přeinstalujte závislostí

Kromě názvu jiné operace se taky zaznamená id závislý balíček pro instalaci.  Budoucí aktualizace do Galerie NuGet zveřejní tato data v rámci sestav, umožňuje autorům balíček plně porozuměli tomu, jak vývojáři instalovaných balíčků.

## <a name="bug-fixes"></a>Opravy chyb

NuGet 2.6 také zahrnuje několik oprav chyb. Úplný seznam pracovní položky pevné ve verzi 2.6 NuGet, prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).