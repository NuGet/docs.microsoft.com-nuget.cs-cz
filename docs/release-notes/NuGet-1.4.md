---
title: Zpráva k vydání verze NuGet 1,4
description: Poznámky k verzi pro NuGet 1,4, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230704"
---
# <a name="nuget-14-release-notes"></a>Zpráva k vydání verze NuGet 1,4

[Poznámky k verzi nuget 1,3](../release-notes/nuget-1.3.md) | zpráva k [vydání verze NuGet 1,5](../release-notes/nuget-1.5.md)

NuGet 1,4 byl vydán 17. června 2011.

## <a name="features"></a>Funkce

### <a name="update-package-improvements"></a>Aktualizace – vylepšení balíčků
NuGet 1,4 představuje mnoho vylepšení příkazu Update-Package, což usnadňuje udržování balíčků ve stejné verzi napříč více projekty v řešení. Například při upgradu balíčku na nejnovější verzi je velmi běžné, aby bylo možné všechny projekty s tímto balíčkem nainstalovat na stejný verision.

Příkaz `Update-Package` teď usnadňuje:

#### <a name="update-all-packages-in-a-single-project"></a>Aktualizovat všechny balíčky v jednom projektu

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aktualizace balíčku ve všech projektech

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aktualizovat všechny balíčky ve všech projektech

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Proveďte bezpečnou aktualizaci u všech balíčků.
Příznak `-Safe` omezuje upgrady pouze na verze se stejnou částí hlavní a dílčí verze. Pokud je například 1.0.0 verze balíčku nainstalován a verze 1.0.1, 1.0.2 a 1,1 jsou k dispozici v informačním kanálu, příznak `-Safe` aktualizuje balíček na 1.0.2. Upgrade bez příznaku `-Safe` by balíček upgradoval na nejnovější verzi 1,1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Správa balíčků na úrovni řešení
Před balíčkem NuGet 1,4 se instalace balíčku do více projektů nenáročných pomocí dialogového okna. Je nutné spustit dialog jednou pro každý projekt.

NuGet 1,4 přidává podporu pro instalaci/odinstalaci/aktualizaci balíčků ve více projektech současně. Stačí spustit kliknutím pravým tlačítkem myši na řešení a výběrem možnosti **Spravovat balíčky NuGet** .

![Dialogové okno Správa balíčků NuGet na úrovni řešení](./media/manage-nuget-packages-solution-dialog.png)

Všimněte si, že v záhlaví dialogového okna se zobrazí název řešení, nikoli název projektu.
Operace balíčku teď poskytují seznam zaškrtávacích políček se seznamem projektů, na které by se měla operace vztahovat.

![Spravovat výběr projektu balíčků NuGet](./media/manage-nuget-packages-project-selection.png)

Další podrobnosti najdete v tématu [Správa balíčků pro řešení](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Omezení upgradu na povolené verze
Ve výchozím nastavení se při spuštění příkazu `Update-Package` na balíčku (nebo aktualizace balíčku pomocí dialogového okna) aktualizuje na nejnovější verzi v informačním kanálu. Díky nové podpoře aktualizace všech balíčků můžou nastat případy, kdy chcete balíček uzamknout do konkrétního rozsahu verzí. Můžete například předem určit, že aplikace bude fungovat pouze s verzí 2. * balíčku, ale ne 3,0 a vyšší. Aby nedocházelo k nechtěné aktualizaci balíčku na 3, NuGet 1,4 přidá podporu pro omezení rozsahu verzí, na které lze balíčky upgradovat, a to ruční úpravou souboru `packages.config` pomocí nového atributu `allowedVersions`.

Například následující příklad ukazuje, jak uzamknout `SomePackage` balíčku rozsah verze 2,0-3,0 (exkluzivní).
Atribut `allowedVersions` akceptuje hodnoty pomocí [formátu rozsahu verzí](../concepts/package-versioning.md#version-ranges).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Všimněte si, že v 1,4 musí být uzamknutí balíčku do konkrétního rozsahu verzí ručně upravováno. V NuGet 1,5 plánujeme přidat podporu pro vložení tohoto rozsahu pomocí příkazu `Install-Package`.

### <a name="package-visualizer"></a>Vizualizér balíčků
Nový Vizualizér balíčků, který se spouští prostřednictvím **nástroje** -> **knihovny správce balíčků** -> možnosti nabídky **Vizualizér balíčků** , umožňuje snadno vizualizovat všechny projekty a jejich závislosti balíčku v rámci řešení.

_**Důležitá Poznámka:** Tato funkce využívá podporu DGML v aplikaci Visual Studio. Vytváření vizualizace se podporuje jenom v Visual Studio Ultimate. Zobrazení diagramu DGML je podporováno pouze v Visual Studio Premium nebo vyšších._

![Vizualizér balíčků](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Automatická aktualizace aktualizací pro dialog NuGet
Některé verze NuGet představují nové funkce vyjádřené pomocí `.nuspec` souboru, které nerozumí starší verze dialogového okna NuGet.
Jedním z příkladů je Úvod do NuGet 1,4 pro [určení sestavení rozhraní](../release-notes/nuget-1.2.md#framework-assembly-refs).
Z tohoto důvodu je důležité použít nejnovější verzi nástroje NuGet, abyste měli jistotu, že budete moci používat balíčky s využitím nejnovějších funkcí.
Aby se aktualizace NuGet zobrazovaly podrobněji, obsahuje dialog NuGet logiku, která zvýrazní, kdy je k dispozici novější verze.

_**Poznámka**: Tato možnost se provádí jenom v případě, že se v aktuální relaci vybrala karta **online** ._

![Dialog spravovat balíčky NuGet s dostupnou novou verzí](./media/manage-nuget-packages-update-notification.png)

Pokud chcete vypnout automatické vyhledávání aktualizací, otevřete dialogové okno nastavení NuGet a zrušte zaškrtnutí políčka **automaticky zjišťovat aktualizace**.

![Nastavení NuGet](./media/nuget-settings.png)

Tato funkce se ve skutečnosti přidala do NuGet 1,3, ale nebude viditelná, dokud nebude k dispozici aktualizace 1,3, jako je třeba NuGet 1,4.

### <a name="package-manager-dialog-improvements"></a>Vylepšení dialogu Správce balíčků
* **Vylepšené názvy nabídek**: možnosti nabídky pro otevření dialogového okna byly pro přehlednost přejmenovány. Možnost nabídky teď **spravuje balíčky NuGet**.
* **Podokno podrobností zobrazuje poslední datum aktualizace**: v dialogovém okně NuGet se v podokně podrobností balíčku zobrazí datum poslední aktualizace, když je vybraná karta **online** nebo **aktualizovat** .
* **Seznam zobrazených značek**: dialogové okno NuGet zobrazí značky.

### <a name="powershell-improvements"></a>Vylepšení PowerShellu
* **Podepsané skripty PowerShellu**: NuGet zahrnuje podepsané skripty PowerShellu, které umožňují použití v přísnějších prostředích.
* **Dotazování na podporu**: konzola správce balíčků teď podporuje zobrazování výzev prostřednictvím příkazů `$host.ui.Prompt` a `$host.ui.PromptForChoice`.
* **Zdrojové názvy balíčků**: zadání názvu zdroje balíčku se podporuje při zadání zdroje balíčku pomocí příznaku `-Source`.

### <a name="nugetexe-command-line-improvements"></a>vylepšení příkazového řádku NuGet. exe
* **Vlastní příkazy NuGet**: NuGet. exe je rozšiřitelný prostřednictvím vlastních příkazů využívajících MEF.
* **Jednodušší pracovní postup pro vytváření balíčků symbolů**: příznak `-Symbols` lze použít pro strukturu složek založenou na běžné konvenci vytvoření balíčku symbolů pouze včetně zdrojových a `.pdb` souborů v rámci složky.
* **Určení více zdrojů**: příkaz `NuGet install` podporuje zadání více zdrojů pomocí středníků jako oddělovače nebo zadáním `-Source` několikrát.
* **Podpora ověřování proxy**: NuGet 1,4 přidává podporu pro výzvy k zadání přihlašovacích údajů uživatele při použití NuGet za proxy serverem, který vyžaduje ověření.
* **NuGet. exe – změna konce aktualizace**: příznak `-Self` se teď vyžaduje, aby se NuGet. exe aktualizoval sám. `nuget.exe Update` nyní používá cestu k souboru `packages.config` a pokusí se aktualizovat balíčky. Všimněte si, že tato aktualizace je omezená, protože se nejedná o: * * aktualizovat, přidat a odebrat obsah v souboru projektu.
* * V rámci balíčku spusťte skripty PowerShellu.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Podpora serveru NuGet pro vkládání balíčků pomocí NuGet. exe
NuGet obsahuje jednoduchý způsob, jak hostovat [zjednodušené úložiště NuGet založené na webu](../hosting-packages/nuget-server.md) prostřednictvím balíčku `NuGet.Server` NuGet. V případě NuGet 1,4 podporuje odlehčený Server doručování a odstraňování balíčků pomocí NuGet. exe.
Nejnovější verze `NuGet.Server` přidá nový `appSetting`s názvem `apiKey`. Pokud je klíč vynechán nebo je ponechán prázdný, je zablokováno vkládání balíčků do informačního kanálu. Nastavení apiKey na hodnotu (v ideálním případě silné heslo) umožňuje zatlačte balíčky pomocí NuGet. exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Podpora pro edice mango Tools pro Windows Phone
V Release Candidate verze Windows Phone nástrojů pro mango se teď podporuje NuGet.
V současné době Windows Phone nástroje nepodporují Správce rozšíření sady Visual Studio, takže pokud chcete nainstalovat NuGet pro Windows Phone nástroje, budete možná muset stáhnout a spustit VSIX ručně.

Pokud chcete odinstalovat NuGet pro nástroje Windows Phone, spusťte následující příkaz.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Opravy chyb
Aktualizace NuGet 1,4 obsahovala celkem 88 pracovních položek. 71 z nich bylo označeno jako chyby.

Úplný seznam pracovních položek opravených v NuGet 1,4 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb zaznamenaly:

* [Problém 603](http://nuget.codeplex.com/workitem/603): při určení konkrétního zdroje balíčků se správně vyřeší závislosti balíčků v různých úložištích.
* [Problém 1036](http://nuget.codeplex.com/workitem/1036): Přidání `NuGet Pack SomeProject.csproj` do události po sestavení už nezpůsobí nekonečnou smyčku.
* [Problém 961](http://nuget.codeplex.com/workitem/961): příznak `-Source` podporuje relativní cesty.

## <a name="nuget-14-update"></a>Aktualizace NuGet 1,4
Krátce po vydání NuGet 1,4 jsme zjistili několik problémů, které byly důležité k opravě.
Konkrétní číslo verze této aktualizace na 1,4 je 1.4.20615.9020.

### <a name="bug-fixes"></a>Opravy chyb
* [Problém 1220](http://nuget.codeplex.com/workitem/1220): aktualizace-Package se nespustí `install.ps1`/`uninstall.ps1` ve všech projektech, pokud existuje víc než jeden projekt.
* [Problém 1156](http://nuget.codeplex.com/workitem/1156): zablokování konsolidace správce balíčků v w2k3/XP (když není nainstalované prostředí PowerShell 2)
