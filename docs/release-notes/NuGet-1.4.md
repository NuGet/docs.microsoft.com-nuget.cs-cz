---
title: Zpráva k vydání verze 1.4 NuGet
description: Zpráva k vydání verze pro NuGet 1.4, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550628"
---
# <a name="nuget-14-release-notes"></a>Zpráva k vydání verze 1.4 NuGet

[Zpráva k vydání verze NuGet 1.3](../release-notes/nuget-1.3.md) | [zpráva k vydání verze NuGet 1.5](../release-notes/nuget-1.5.md)

NuGet 1.4 byla vydána 17 dne 2011.

## <a name="features"></a>Funkce

### <a name="update-package-improvements"></a>Vylepšení aktualizace balíčků
NuGet 1.4 přináší spoustu vylepšení příkazu Update-Package to usnadňuje zachovat balíčky na stejnou verzi více projektů v řešení. Například při upgradu na nejnovější verzi balíčku, je velmi běžné vyžadovat všechny projekty se tento balíček aktualizovat tak, aby stejné verision.

`Update-Package` Příkaz nyní usnadňuje:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualizovat všechny balíčky v jednom projektu

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualizovat balíček ve všech projektech

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aktualizovat všechny balíčky ve všech projektech

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Provádění "bezpečné" aktualizace na všechny balíčky
`-Safe` Příznak omezí upgrade na pouze verze pomocí stejné verze komponenty hlavní a podverze. Pokud je nainstalována verze 1.0.0 balíčku a verze 1.0.1, 1.0.2 a 1.1, jsou k dispozici v informačním kanálu, například `-Safe` příznak je balíček aktualizován na 1.0.2. Bez upgradu `-Safe` příznak by balíček upgradu na nejnovější verze 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Správa balíčků na úrovni řešení
Před NuGet 1.4 instalaci balíčku do více projektů byla náročná, pomocí dialogového okna. To nutné, spouští se dialogové okno jednou za projektu.

NuGet 1.4 přidává podporu pro instalace/odinstalace/aktualizuje balíčky v několika projektech současně. Jednoduše spustit tak, že kliknete pravým tlačítkem řešení a vyberete **spravovat balíčky NuGet** nabídky.

![Dialogové okno řešení úroveň spravovat balíčky NuGet](./media/manage-nuget-packages-solution-dialog.png)

Všimněte si, že v záhlaví dialogového okna, název řešení se zobrazí, nikoli název projektu.
Operace balíčků teď poskytují seznam zaškrtávacích políček seznam projektů, které se má použít operaci.

![Správa výběr projektu balíčky NuGet](./media/manage-nuget-packages-project-selection.png)

Další podrobnosti naleznete v tématu o [Správa balíčků pro řešení](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Omezení upgraduje povolené verze
Ve výchozím nastavení při spuštění `Update-Package` příkaz balíčku (nebo aktualizaci balíčku pomocí dialogového okna), se aktualizují na nejnovější verzi v informačním kanálu. S novou podporu pro všechny balíčky aktualizací můžou nastat případy, ve kterých chcete zamknout balíček na rozsah konkrétní verze. Například můžete vědět předem, že vaše aplikace bude fungovat jenom s 2.* verze balíčku, ale ne 3.0 a novějších. Aby nedošlo k neúmyslné balíček aktualizace na 3, NuGet 1.4 přidává podporu pro omezení rozsahu verzí, které balíčky je možné upgradovat na tak, že ručně upravíte `packages.config` souborů pomocí nové `allowedVersions` atribut.

Například následující příklad ukazuje, jak uzamknout `SomePackage` 2.0-3.0 (výhradní) v rozsahu balíčku verze.
`allowedVersions` Atribut je možné zadat hodnoty pomocí [formát rozsahu verze](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Mějte na paměti, že 1.4, uzamčení balíček na rozsah konkrétní verze musí být ručně upravit. 1.5 NuGet plánujeme přidat podporu pro uvedení tento rozsah prostřednictvím `Install-Package` příkazu.

### <a name="package-visualizer"></a>Balíček Vizualizéru
Nový balíček vizualizéru, spustí prostřednictvím **nástroje** -> **Správce balíčků knihoven** -> **balíčku Vizualizéru** klikněte na možnost vám umožní snadno Vizualizujte všechny projekty a závislosti jejich balíčků v rámci řešení.

_**Důležitá poznámka:** tato funkce využívá výhod podpory DGML v sadě Visual Studio. Vytvoření vizualizace je podporována pouze v sadě Visual Studio Ultimate. Zobrazení diagramu DGML je podporována pouze v aplikaci Visual Studio Premium nebo vyšší._

![Balíček Vizualizéru](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Kontrola automatické aktualizace v dialogovém okně NuGet
Některé verze NuGet zavádět nové funkce vyjádřena `.nuspec` souborů, které nebudou srozumitelné pro starší verze NuGet dialogového okna.
Jedním z příkladů je zavedení 1.4 NuGet pro [zadání sestavení rozhraní](../release-notes/nuget-1.2.md#framework-assembly-refs).
Z toho důvodu je důležité, abyste používali nejnovější verzi balíčku nuget k zajištění, že může používat balíčky, které využívají nejnovější funkce.
Provádění aktualizací NuGet viditelnější, dialogové okno NuGet obsahuje logiku a zvýraznit, když je dostupná novější verze.

_**Poznámka:**: Kontrola se provádí pouze v případě **Online** kartu byla vybrána v aktuální relaci._

![Spravovat balíčky NuGet dialogové okno s dostupná nová verze](./media/manage-nuget-packages-update-notification.png)

Chcete-li vypnout automatickou kontrolu aktualizací, přejděte do dialogového okna nastavení NuGet a zrušte zaškrtnutí políčka **automaticky vyhledávat aktualizace**.

![Nastavení NuGet](./media/nuget-settings.png)

Tuto funkci ve skutečnosti byl přidán NuGet 1.3, ale nebude viditelné, samozřejmě, až do aktualizace 1.3, jako je NuGet 1.4, byl k dispozici.

### <a name="package-manager-dialog-improvements"></a>Vylepšení dialogového okna Správce balíčků
* **Názvy nabídek vylepšené**: spuštění dialogového okna Možnosti nabídky byly přejmenovány nejasnostem. Možnost nabídky je nyní **spravovat balíčky NuGet**.
* **V podokně podrobností se zobrazí nejnovější data aktualizací**: Zobrazí se dialogové okno NuGet datum poslední aktualizace v podokně podrobností pro balíček při **Online** nebo **aktualizuje** vybraná karta.
* **Seznam značek zobrazí**: Nuget dialogové okno zobrazí značky.

### <a name="powershell-improvements"></a>Vylepšení prostředí PowerShell
* **Podepsané skripty prostředí PowerShell**: NuGet zahrnuje podepsaných skriptů prostředí Powershell umožňuje využití v prostředích s více omezující.
* **Dotazování podporu**: konzoly Správce balíčků teď podporuje dotazování přes `$host.ui.Prompt` a `$host.ui.PromptForChoice` příkazy.
* **Balíček názvy zdrojů**: poskytnutí název zdroje balíčku je podporováno, pokud zadáte zdroj balíčku pomocí `-Source` příznak.

### <a name="nugetexe-command-line-improvements"></a>vylepšení příkazového řádku nuget.exe
* **Vlastní příkazy pro balíčky NuGet**: nuget.exe je rozšiřitelný prostřednictvím vlastní příkazy pomocí MEF.
* **Jednodušší pracovního postupu pro vytváření balíčků symbolů**: `-Symbols` příznak lze použít k vytvoření balíčku symbolů pouze zahrnutím zdroj struktury složek normální založené na konvenci a `.pdb` soubory ve složce.
* **Zadání více zdrojů**: `NuGet install` příkaz podporuje zadání více zdrojů pomocí středníkem jako oddělovač nebo zadáním `-Source` více než jednou.
* **Podpora proxy serveru ověřování**: NuGet 1.4 přidává podporu pro vás vyzve k zadání přihlašovacích údajů uživatele při použití NuGet za proxy serverem, který vyžaduje ověření.
* **nuget.exe aktualizovat zásadní změna**: `-Self` příznak je nyní nutné zahrnout nuget.exe aktualizovalo samo. `nuget.exe Update` nyní přijímá cesty k `packages.config` soubor a pokusí se aktualizace balíčků. Všimněte si, že tato aktualizace je omezený v tom, že se tak nestane: ** aktualizaci, přidání, odebrání obsahu v souboru projektu.
** Spouštění Powershellových skriptů v rámci balíčku.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Podpora serveru NuGet pro vkládání balíčků pomocí nuget.exe
NuGet obsahuje jednoduchý způsob, jak hostitele [jednoduché webové na základě úložiště NuGet](../hosting-packages/nuget-server.md) prostřednictvím `NuGet.Server` balíček NuGet. S NuGet 1.4 jednoduchý server podporuje vkládání a odstraňování balíčků s využitím nuget.exe.
Nejnovější verzi `NuGet.Server` přidá nový `appSetting`s názvem `apiKey`. Když tento parametr vynechán nebo je prázdné, nahráním balíčky do informačního kanálu se vypne. Nastavení apiKey na hodnotu (v ideálním případě silné heslo) umožňuje vložit balíčky pomocí nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Podpora pro Windows Phone Tools Mango Edition
NuGet se teď podporuje ve verzi Release candidate nástroje Windows Phone pro Mango.
V současné době nástroje Windows Phone nemá podporu pro správce rozšíření sady Visual Studio, proto k instalaci nástroje NuGet pro Windows Phone, budete muset stáhnout a spustit ručně VSIX.

Odinstalace nástroje NuGet pro Windows Phone, spusťte následující příkaz.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.4 bylo celkem 88 pracovní položky opraveno. 71 z nich byly označeny jako chyby.

Úplný seznam pracovních položek opravených NuGet 1.4 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb za zmínku:

* [Problém 603](http://nuget.codeplex.com/workitem/603): závislosti balíčků v různých úložištích řeší správně při zadávání zdroj konkrétního balíčku.
* [Problém 1036](http://nuget.codeplex.com/workitem/1036): přidání `NuGet Pack SomeProject.csproj` na událost po sestavení už způsobuje nekonečnou smyčku.
* [Problém 961](http://nuget.codeplex.com/workitem/961): `-Source` příznak podporuje relativní cesty.

## <a name="nuget-14-update"></a>Aktualizace NuGet 1.4
Krátce po vydání NuGet 1.4 našli jsme několik problémů, které byly potřeba opravit.
Počet konkrétní verzi této aktualizace 1.4 je 1.4.20615.9020.

### <a name="bug-fixes"></a>Opravy chyb
* [Problém 1220](http://nuget.codeplex.com/workitem/1220): Update-Package neprovede `install.ps1` / `uninstall.ps1` ve všech projektech po více než jeden projekt
* [Problém 1156](http://nuget.codeplex.com/workitem/1156): konzole Správce balíčků zablokované W2K3/XP (Pokud není nainstalovaný Powershell 2)
