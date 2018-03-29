---
title: Odkaz uživatelského rozhraní Správce balíčků NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: Pokyny k používání uživatelského rozhraní Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky NuGet.
keywords: NuGet, uživatelského rozhraní Správce balíčků NuGet uživatelského rozhraní, NuGet v sadě Visual Studio, Správa balíčků NuGet, NuGet uživatelské rozhraní Správce balíčků v sadě Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ad36c2ab0c6e62c7fe624b35d92e852303ecfdfb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-package-manager-ui"></a>Uživatelského rozhraní Správce balíčků NuGet

Uživatelské rozhraní Správce balíčků NuGet v sadě Visual Studio v systému Windows umožňuje snadno nainstalování, odinstalování a aktualizovat balíčky NuGet ve projekty a řešení. Pro prostředí v sadě Visual Studio pro Mac, najdete v části [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough). Uživatelské rozhraní Správce balíčků není součástí Visual Studio Code.

V tomto tématu:

- [Hledání a instalaci balíčku (Procházet karta)](#finding-and-installing-a-package)
- [Odinstalace balíčku (karta nainstalovaná)](#uninstalling-a-package)
- [Aktualizace balíčku (karty nainstalovaná a aktualizace)](#updating-a-package) (zahrnuje ["Implicitně odkazuje sady SDK" nebo "AutoReferenced" zprávy](#implicit_reference))
- [Spravovat balíčky pro řešení](#managing-packages-for-the-solution) (práce s více projektů současně).
- [Zdroje balíčků](#package-sources)
- [Ovládání možnosti Správce balíčku](#package-manager-options-control)

> [!Note]
> Pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015, zkontrolujte **nástroje > rozšíření a aktualizace...**  a vyhledejte *Správce balíčků NuGet* rozšíření. Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, stáhněte si rozšíření přímo z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> V aplikaci Visual Studio 2017 jsou NuGet a Správce balíčků NuGet automaticky nainstalovány s žádným. NET související úlohy. Nainstalujte ji jednotlivě výběrem **jednotlivých součástí > Code nástroje > Správce balíčků NuGet** možnosti v instalačním programu Visual Studio 2017.

## <a name="finding-and-installing-a-package"></a>Hledání a instalaci balíčku

1. V **Průzkumníku řešení**, klikněte pravým tlačítkem na buď **odkazy** nebo projekt a vyberte **spravovat balíčky NuGet...** .

    ![Spravovat balíčky NuGet nabídky](media/ManagePackagesUICommand.png)

1. **Procházet** karta zobrazí balíčky podle oblíbenosti z aktuálně vybraného zdroje (najdete v části [balíček zdroje](#package-sources)). Vyhledejte konkrétní balíček pomocí vyhledávacího pole v levé horní části. Vyberte balíček ze seznamu zobrazíte její informace, které taky umožňuje **nainstalovat** tlačítko společně s rozevírací výběr verze.

    ![Spravovat kartu Procházet dialogové okno balíčky NuGet](media/Search.png)

1. Vyberte požadovanou verzi z rozevíracího seznamu a vyberte **nainstalovat**. Visual Studio nainstaluje do projektu balíček a jeho závislosti. Můžete být vyzváni k potvrzení licenčních podmínek. Po dokončení instalace se přidané balíčky zobrazí na **nainstalovaná** kartě. Balíčky jsou také uvedeny v **odkazy** uzlu Průzkumníka řešení, která určuje, zda mohou odkazovat na ně v projektu s `using` příkazy.

    ![Odkazy v Průzkumníku řešení](media/References.png)

> [!Tip]
    > Při hledání zahrnout předprodejní verze a aby předprodejní verze dostupné ve verzi rozevíracího seznamu, vyberte **zahrnout předběžné verze** možnost.

## <a name="uninstalling-a-package"></a>Odinstalace balíčku

1. V **Průzkumníku řešení**, klikněte pravým tlačítkem na buď **odkazy** nebo požadovaný projekt a vyberte **spravovat balíčky NuGet...** .
1. Vyberte **nainstalovaná** kartě.
1. Vyberte balíček, který chcete odinstalovat (pomocí vyhledávání pro filtrování seznamu v případě potřeby) a vyberte **odinstalovat**.

    ![Odinstalace balíčku](media/UninstallPackage.png)

1. Všimněte si, že **zahrnout předběžné verze** a **zdroj balíčku** ovládací prvky mít žádný vliv, při odinstalaci balíčků.

## <a name="updating-a-package"></a>Aktualizace balíčku

1. V **Průzkumníku řešení**, klikněte pravým tlačítkem na buď **odkazy** nebo požadovaný projekt a vyberte **spravovat balíčky NuGet...** . (V projektech webových stránek, klikněte pravým tlačítkem myši **Bin** složky.)
1. Vyberte **aktualizace** karty zobrazíte balíčky, které jsou k dispozici aktualizace ze zdroje vybraný balíček. Vyberte **zahrnout předběžné verze** zahrnout předběžné verze balíčků v seznamu aktualizací.
1. Vyberte balíček, který chcete aktualizovat, vyberte požadovanou verzi z rozevíracího seznamu na pravé straně a vyberte **aktualizace**.

    ![Aktualizace balíčku](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Pro některé balíčky **aktualizace** tlačítko je zakázané a zobrazí se zpráva s informacemi o tom, že ji "implicitně odkazuje sady SDK" (nebo "AutoReferenced"). Zpráva označuje, že balíčku, například Microsoft.NETCore.App nebo Microsoft.NETStandard.Library, je součástí větší framework nebo sady SDK a nesmí být aktualizovány nezávisle. (Tyto balíčky jsou interně označené `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Pokud chcete aktualizovat balíček, aktualizujte sadu SDK, do které patří.

    ![Příklad balíček označen jako implicitně odkazy nebo AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Chcete-li aktualizovat více balíčků jejich nejnovější verze, vyberte je v seznamu a vyberte **aktualizace** tlačítko výše v seznamu.
1. Můžete také aktualizovat individuální balíčku z **nainstalovaná** kartě. V takovém případě podrobnosti balíčku zahrnout selektor verze (podléhají **zahrnout předběžné verze** možnost) a **aktualizace** tlačítko.

## <a name="managing-packages-for-the-solution"></a>Spravovat balíčky pro řešení

Spravovat balíčky pro řešení je pohodlný způsob pro práci s více projektů současně.

1. Vyberte **nástroje > Správce balíčků NuGet > Správa balíčků NuGet pro řešení...**  nabídky příkazu, nebo klikněte pravým tlačítkem na řešení a vyberte **spravovat balíčky NuGet...** :

    ![Správa balíčků NuGet pro řešení](media/ManagePackagesSolutionUICommand.png)

1. Při správě balíčky pro řešení, uživatelské rozhraní umožní vám vybrat projektů, které jsou ovlivněné operace:

    ![Selektor projektu při správě balíčky pro řešení](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Konsolidovat karta

Vývojáři obvykle považuje za chybný postup používat různé verze stejného balíčku NuGet v různých projektů ve stejném řešení. Pokud zvolíte možnost spravovat balíčky pro řešení, poskytuje uživatelské rozhraní Správce balíčků **konsolidace** karty, na které můžete snadno zobrazit kde balíčky s čísla různých verzí používají různé projekty v řešení:

![Karta konsolidovat uživatelského rozhraní Správce balíčků](media/ConsolidateTab.png)

V tomto příkladu je projektu ClassLibrary1 využitím objektu EntityFramework 6.2.0, zatímco ConsoleApp1 je s využitím objektu EntityFramework 6.1.0. Pro konsolidaci verze balíčku, postupujte takto:

- Vyberte projekty k aktualizaci v seznamu projektu.
- Vyberte verze se má použít na všechny projekty v **verze** ovládací prvek, jako je například EntityFramework 6.2.0.
- Vyberte **nainstalovat** tlačítko.

Správce balíčků nainstaluje verzi vybraný balíček do všech vybraných projektů, po které balíčku již nadále nebude zobrazovat na **konsolidace** kartě.

## <a name="package-sources"></a>Zdroje balíčků

Chcete-li změnit zdroj, ze kterého Visual Studio získá balíčky, vyberte jednu z modulu pro výběr zdroje:

![Výběr zdroje balíčku v uživatelské rozhraní Správce balíčků](media/PackageSourceDropDown.png)

Správa zdrojů balíčků:

1. Vyberte **nastavení** ikony v uživatelském rozhraní Správce balíčků uvedených níže nebo používat **nástroje > Možnosti** příkazů a přejděte k položce **Správce balíčků NuGet**:

    ![Ikona nastavení uživatelského rozhraní správce balíčku](media/PackageSourceSettings.png)

1. Vyberte **zdroje balíčků** uzlu:

    ![Možnosti zdroje balíčku](media/options.png)

1. Přidat zdroj, vyberte **+**, upravit název, zadejte adresu URL nebo cestu **zdroj** řízení a vyberte **aktualizace**. Zdroj se teď zobrazí v modulu pro výběr rozevíracího seznamu.
1. Chcete-li změnit zdroj balíčku, vyberte ho, proveďte úpravy v **název** a **zdroj** pole a vyberte **aktualizace**.
1. Zakázat zdroj balíčku, zrušte zaškrtnutí políčka nalevo od názvu v seznamu.
1. Pokud chcete odebrat zdroj balíčku, vyberte ho a pak vyberte **X** tlačítko.
1. Pomocí nahoru a dolů tlačítek Chcete-li změnit pořadí priority zdroje balíčku. Při obnovování balíčků pro projekt sady Visual Studio vyhledá tyto zdroje v pořadí podle priority. Další informace najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md).

> [!Tip]
> Pokud je zdroj balíčku se znovu zobrazí po odstranění, nemusí být zobrazeny v úrovni počítače nebo individuální `NuGet.Config` soubory. V tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md) pro umístění tyto soubory pak odebrat zdroj upravit soubory ručně nebo pomocí [nuget zdroje příkaz](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Ovládání možnosti Správce balíčku

Pokud je vybraná balíčku, uživatelské rozhraní Správce balíčků zobrazí malá, rozšíření **možnosti** řízení níže modulu pro výběr verze (viz zde i sbalené a rozbalené). Všimněte si, že pro některé projekt typy pouze **zobrazit okno náhledu** možnost je k dispozici.

![Možnosti správce balíčku](media/PackageManagerUIOptions.png)

Následující části popisují tyto možnosti.

### <a name="show-preview-window"></a>Zobrazit okno náhledu

Při výběru modální okna zobrazí který závislosti zvolené balíčku před instalací balíčku:

![Dialogové okno náhledu příklad](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Možnosti instalace a aktualizace

(Není k dispozici pro všechny typy projektů.)

**Chování závislostí** konfiguruje, jak NuGet rozhodne, která verze závislé balíčky pro instalaci:

- *Ignorovat závislosti* přeskočí instalaci všechny závislosti, které obvykle dělí instalovaného balíčku.
- *Nejnižší* [výchozí] nainstaluje závislost číslo minimální verze, který splňuje požadavky na primární zvolené balíčku.
- *Nejvyšší oprava* nainstaluje verzi s stejná hlavní verze a podverze čísla, ale nejvyšší číslo opravy. Například pokud je zadaná verze 1.2.2 pak nejvyšší verzi, která začíná 1.2 bude nainstalována
- *Nejvyšší vedlejší* nainstaluje verze se stejnou hlavní číslo verze, ale číslem a oprava číslo. Pokud je určená verze 1.2.2, pak nejvyšší verzi, která začíná 1 budou nainstalovány
- *Nejvyšší* nainstaluje nejvyšší dostupné verze balíčku.

**Soubor konflikt akce** určuje způsob zpracování NuGet balíčky, které již existují v projektu nebo místního počítače:

- *Výzva* dá pokyn k dotaz, zda chcete zachovat nebo přepsat existující balíčky NuGet.
- *Ignorovat všechny* dá pokyn tak, aby přeskočil přepsal všechny existující balíčky NuGet.
- *Přepsat všechny* dá pokyn k přepsání všechny existující balíčky NuGet.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Odinstalování možností

(Není k dispozici pro všechny typy projektů.)

**Odebrání závislostí**: při výběru odebere všechny závislé balíčky, pokud nejsou jinde odkazovaná v projektu.

**Vynutit odinstalaci i v případě, že neexistují závislosti na něm**: při výběru Odinstaluje balíček i v případě, že je stále odkazováno v projektu. To se obvykle používá v kombinaci s **odebrání závislostí** odebrat balíček a to bez ohledu závislostí je nainstalovat. Pomocí této možnosti může, ale vést ke poškozenými odkazy v projektu. V takových případech budete muset [znovu nainstalujte tyto další balíčky](../consume-packages/reinstalling-and-updating-packages.md).
