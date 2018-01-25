---
title: "Poznámky k verzi NuGet 1.4 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.4 NuGet."
keywords: "NuGet 1.4 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a69f4f5c7172817d711fa5e995cf6db3875c4810
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-14-release-notes"></a>Poznámky k verzi 1,4 NuGet

[Poznámky k verzi NuGet 1.3](../release-notes/nuget-1.3.md) | [poznámky k verzi NuGet 1.5](../release-notes/nuget-1.5.md)

NuGet 1.4 byla vydána 17 června 2011.

## <a name="features"></a>Funkce

### <a name="update-package-improvements"></a>Vylepšení balíčku aktualizace
NuGet 1.4 představuje mnoho vylepšení příkaz balíčku aktualizace bylo snazší zachovat balíčky na stejnou verzi napříč více projekty v řešení. Například při upgradu na nejnovější verzi balíčku, je velmi běžné na má všechny projekty, ve kterém je tento balíček nainstalován aktualizovat, aby stejné verision.

`Update-Package` Příkaz teď usnadňuje:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualizovat všechny balíčky v jednom projektu

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualizovat balíček ve všech projektech

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aktualizovat všechny balíčky ve všech projektech

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>"Bezpečnou" aktualizaci provést u všech balíčků
`-Safe` Příznak omezí upgrade na pouze verze se stejnou hlavní a vedlejší verze součástí. Například, pokud je nainstalována verze 1.0.0 balíčku a ve informačního kanálu, jsou dostupné verze 1.0.1, 1.0.2 a 1.1 `-Safe` příznak se balíček aktualizuje na verzi 1.0.2. Upgrade bez `-Safe` příznak by upgrade balíčku na nejnovější verzi 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Spravovat balíčky na úrovni řešení
Před NuGet 1.4 instalaci balíčku do více projektů byla náročná, v dialogovém okně. Je vyžadován, spouštění dialogu jednou za projektu.

NuGet 1.4 přidává podporu pro instalaci/odinstalaci nebo aktualizaci balíčků ve více projektech ve stejnou dobu. Jednoduše spustit kliknutím pravým tlačítkem na řešení a výběrem **spravovat balíčky NuGet** možnost nabídky.

![Dialogové okno Spravovat balíčky NuGet úroveň řešení](./media/manage-nuget-packages-solution-dialog.png)

Všimněte si, že v záhlaví okna řešení je zobrazen název, ne název projektu.
Balíček operations teď poskytovat seznam všech políček se seznamem projekty, které by měl použít operaci.

![Spravovat výběr projektu balíčky NuGet](./media/manage-nuget-packages-project-selection.png)

Další podrobnosti naleznete v tématu na [Správa balíčků pro řešení](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Chovaly upgraduje povolené verze
Ve výchozím nastavení při spuštění `Update-Package` na balíček (nebo aktualizaci balíčku v dialogu), ji budou aktualizovány na nejnovější verzi v informačním kanálu. Nové podpory pro aktualizaci všech balíčků můžou nastat případy, ve kterých chcete zamknout balíček na konkrétní verzi rozsah. Například může vědět předem, že vaše aplikace bude fungovat pouze s 2.* verze balíčku, ale není 3.0 nebo vyšší. Prevence omylem aktualizace balíčku na 3 NuGet 1.4 přidává podporu pro omezíte rozsah verze, které balíčky lze přidat k ruční úpravě `packages.config` souboru pomocí možnosti nového `allowedVersions` atribut.

Například následující příklad ukazuje, jak k uzamčení `SomePackage` balíček verze rozsahu 2.0-3.0 (kromě).
`allowedVersions` Atribut přijímá hodnoty pomocí [verze rozsah formátu](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Všimněte si, že v 1.4, uzamčení balíčku na konkrétní verzi rozsah musí být ručně upravovat. V NuGet 1.5 plánujeme přidat podporu pro tento rozsah prostřednictvím umístění `Install-Package` příkaz.

### <a name="package-visualizer"></a>Vizualizér balíčku
Nový balíček vizualizér, spustí prostřednictvím **nástroje** -> **Správce balíčků knihoven** -> **balíček vizualizér** nabídky možnost vám umožňuje snadno zobrazit všechny projekty a závislosti jejich balíčků v rámci řešení.

_**Důležité upozornění:** tato funkce využívá DGML podpory v sadě Visual Studio. Vytváření vizualizace je podporována pouze v sadě nástrojů Visual Studio Ultimate. Zobrazení diagramu DGML je podporována pouze v aplikaci Visual Studio Premium nebo vyššího._

![Vizualizér balíčku](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Kontrola automatické aktualizace pro dialogové okno NuGet
Některé verze NuGet zavádět nové funkce prostřednictvím vyjádřené `.nuspec` souborů, které nejsou rozumí starší verze NuGet dialogového okna.
Jedním z příkladů je zavedení v 1.4 NuGet pro [zadání sestavení architektury](../release-notes/nuget-1.2.md#framework-assembly-refs).
Z toho důvodu je důležité, abyste používali nejnovější verzi balíčku nuget k zajištění, že používáte balíčky s využitím nejnovějších funkcí.
Provádění aktualizací NuGet více viditelných, dialogové okno NuGet obsahuje logiku ke zvýraznění je k dispozici novější verze.

_**Poznámka:**: Kontrola se provádí pouze v případě **Online** karta byla vybrána v aktuální relaci._

![Spravovat balíčky NuGet dialogové okno s dostupná nová verze](./media/manage-nuget-packages-update-notification.png)

Chcete-li vypnout automatickou kontrolu aktualizací, přejděte do dialogového okna nastavení NuGet a zrušte zaškrtnutí políčka **automaticky vyhledávat aktualizace**.

![Nastavení NuGet](./media/nuget-settings.png)

Tato funkce je ve skutečnosti přidaná do NuGet 1.3, ale nebude viditelná, samozřejmě, dokud nebude aktualizace 1.3, jako je například NuGet 1.4, byla k dispozici.

### <a name="package-manager-dialog-improvements"></a>Vylepšení dialogové okno Správce balíčků
* **Názvy nabídek vylepšené**: možnosti nabídky spustit dialogové okno pro přehlednost přejmenovaný. Možnost nabídky je nyní **spravovat balíčky NuGet**.
* **V podokně podrobností se zobrazí datum poslední aktualizace**: NuGet dialogovém okně zobrazí datum poslední aktualizace v podokně podrobností pro balíček při **Online** nebo **aktualizace** vybraná karta.
* **Seznam značek zobrazí**: Nuget dialogovém okně zobrazí značky.

### <a name="powershell-improvements"></a>Vylepšení prostředí PowerShell
* **Podepsané skriptů prostředí PowerShell**: NuGet zahrnuje podepsaných skriptů prostředí Powershell povolení využití v prostředí s více omezením.
* **Výzvy podporu**: konzole Správce balíčků teď podporuje výzvy prostřednictvím `$host.ui.Prompt` a `$host.ui.PromptForChoice` příkazy.
* **Balíček názvy zdrojů**: poskytnutí název zdroje balíčku je podporován při zadávání zdrojový balíček pomocí `-Source` příznak.

### <a name="nugetexe-command-line-improvements"></a>vylepšení nuget.exe příkazového řádku
* **Vlastní příkazy pro balíčky NuGet**: nuget.exe je rozšiřitelný prostřednictvím vlastní příkazy pomocí MEF.
* **Jednodušší pracovního postupu pro vytváření balíčků symbol**: `-Symbols` příznak lze použít pro strukturu složek normální založené na konvenci vytváření balíčku symboly pouze zahrnutím zdroji a `.pdb` soubory ve složce.
* **Zadání více zdrojů**: `NuGet install` příkaz podporuje zadání více zdrojů pomocí středníky jako oddělovač nebo zadáním `-Source` vícekrát.
* **Podpora ověřování proxy**: NuGet 1.4 přidává podporu pro výzvu pro přihlašovací údaje uživatele při použití NuGet za proxy server, který vyžaduje ověření.
* **nuget.exe aktualizovat nejnovější změny**: `-Self` příznak je nyní požadované pro nuget.exe aktualizovalo samo. `nuget.exe Update`Teď má v cestě k `packages.config` soubor a pokusí se aktualizace balíčků. Všimněte si, že tato aktualizace je omezená, v tom, že není nebude: ** aktualizovat, přidat, odebrat obsah v souboru projektu.
** Spouštět skripty prostředí Powershell v rámci balíčku.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Podpora serveru NuGet pro vkládání balíčky pomocí nuget.exe
NuGet obsahuje jednoduchý způsob, jak hostitele [jednoduché webové na základě úložiště NuGet](../hosting-packages/NuGet-Server.md) prostřednictvím `NuGet.Server` balíček NuGet. S NuGet 1.4 lightweight server podporuje vkládání a odstraňování balíčky pomocí nuget.exe.
Nejnovější verzi `NuGet.Server` přidá nový `appSetting`s názvem `apiKey`. Pokud tento parametr vynechán nebo je prázdné, když zavedete balíčků informačního kanálu je zakázána. Nastavení na hodnotu (v ideálním případě silné heslo) apiKey umožňuje vkládání balíčky pomocí nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Podpora pro Windows Phone nástroje Mango Edition
NuGet se teď podporuje v verze release candidate nástrojů pro Windows Phone pro Mango.
V současné době nástroje Windows Phone nemá podporu pro správce rozšíření sady Visual Studio proto k instalaci nástroje NuGet pro Windows Phone, budete muset stáhnout a spustit VSIX ručně.

Odinstalace nástrojů NuGet pro Windows Phone, spusťte následující příkaz.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Opravy chyb
NuGet 1.4 měl celkem 88 pracovní položky, které jsou pevné. 71 těchto byly označeny jako chyby.

Úplný seznam pracovní položky pevné v NuGet 1.4 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb vhodné poznamenat:

* [Problém 603](http://nuget.codeplex.com/workitem/603): závislosti balíčků v různých úložišť přeloží správně při zadávání zdrojové konkrétní balíček.
* [Problém 1036](http://nuget.codeplex.com/workitem/1036): přidání `NuGet Pack SomeProject.csproj` po už vytvořit událost způsobí, že nekonečné smyčce.
* [Problém 961](http://nuget.codeplex.com/workitem/961): `-Source` příznak podporuje relativní cesty.

## <a name="nuget-14-update"></a>Aktualizace NuGet 1.4
Krátce po vydání NuGet 1.4 zjistili jsme několik problémů, které by bylo potřeba opravit.
Číslo konkrétní verze této aktualizace 1.4 je 1.4.20615.9020.

### <a name="bug-fixes"></a>Opravy chyb
* [Problém 1220](http://nuget.codeplex.com/workitem/1220): balíček aktualizace neprovede `install.ps1` / `uninstall.ps1` ve všech projektech po více než jeden projektu
* [Problém 1156](http://nuget.codeplex.com/workitem/1156): konzole Správce balíčků zablokované na W2K3/Windows XP (Pokud není nainstalované prostředí Powershell 2)
