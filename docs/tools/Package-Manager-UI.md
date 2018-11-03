---
title: Odkaz uživatelského rozhraní Správce balíčků NuGet
description: Pokyny k používání uživatelského rozhraní Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky NuGet.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 1de6ddeca6295c621a90409807af198bc3c7a068
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981181"
---
# <a name="nuget-package-manager-ui"></a>Uživatelské rozhraní Správce balíčků NuGet

Uživatelské rozhraní Správce balíčků NuGet v sadě Visual Studio ve Windows umožňuje snadno nainstalování, odinstalování a aktualizace balíčků NuGet do projektů a řešení. Prostředí sady Visual Studio pro Mac, najdete v části [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough). Uživatelské rozhraní Správce balíčků není součástí systému Visual Studio Code.

V tomto tématu:

- [Vyhledání a instalace balíčku (Karta Procházet)](#finding-and-installing-a-package)
- [Odinstalovává se balíček (stiskněte klávesu tab nainstalováno)](#uninstalling-a-package)
- [Aktualizuje se balíček (karty nainstalováno a aktualizace)](#updating-a-package) (zahrnuje ["Implicitně odkazovaná sadu SDK" nebo "AutoReferenced" zpráva](#implicit_reference))
- [Správa balíčků pro řešení](#managing-packages-for-the-solution) (práce s více projektů současně).
- [Zdroje balíčků](#package-sources)
- [Ovládací prvek možnosti Správce balíčků](#package-manager-options-control)

> [!Note]
> Pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015, zkontrolujte **nástroje > rozšíření a aktualizace...**  , vyhledejte *Správce balíčků NuGet* rozšíření. Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, stáhněte si rozšíření přímo z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> V sadě Visual Studio 2017 NuGet a Správce balíčků NuGet se instalují automaticky s žádné. NET související úlohy. Instalovat jednotlivě tak, že vyberete **jednotlivé komponenty > kód nástroje > Správce balíčků NuGet** možnost v instalačním programu sady Visual Studio 2017.

## <a name="finding-and-installing-a-package"></a>Vyhledání a instalace balíčku

1. V **Průzkumníka řešení**, pravým tlačítkem myši buď **odkazy** nebo projekt a vyberte **spravovat balíčky NuGet...** .

    ![Spravovat balíčky NuGet nabídky](media/ManagePackagesUICommand.png)

1. **Procházet** karta zobrazuje i podle popularity z aktuálně vybraného zdroje balíčků (naleznete v tématu [balíček zdroje](#package-sources)). Vyhledejte konkrétní balíček pomocí vyhledávacího pole v levém horním rohu. Vyberte balíček ze seznamu zobrazíte její informace, které umožňuje **nainstalovat** tlačítko spolu s rozevírací výběr verze.

    ![Správa kartu Procházet dialogové okno balíčků NuGet](media/Search.png)

1. Vyberte požadovanou verzi z rozevíracího seznamu a vyberte **nainstalovat**. Visual Studio nainstaluje do projektu balíček a jeho závislosti. Můžete být vyzváni k potvrzení licenčních podmínek. Po dokončení instalace se zobrazí přidání balíčků na **nainstalováno** kartu. Balíčky jsou uvedené také na **odkazy** uzlu Průzkumníka řešení, která udává, najdete je v projektu s `using` příkazy.

    ![Odkazy v Průzkumníku řešení](media/References.png)

> [!Tip]
> Chcete-li do hledání zahrnout předběžné verze a aby předběžné verze k dispozici ve verzi rozevíracího seznamu, vyberte **zahrnout předběžné verze** možnost.

## <a name="uninstalling-a-package"></a>Odinstalace balíčku

1. V **Průzkumníka řešení**, pravým tlačítkem myši buď **odkazy** nebo požadovaný projekt a vyberte **spravovat balíčky NuGet...** .
1. Vyberte **nainstalováno** kartu.
1. Vyberte balíček odinstalovat (použití vyhledávání k filtrování seznamu v případě potřeby) a vyberte **odinstalovat**.

    ![Odinstalace balíčku](media/UninstallPackage.png)

1. Všimněte si, že **zahrnout předběžné verze** a **zdroj balíčku** ovládací prvky nemají žádný vliv při odinstalaci balíčků.

## <a name="updating-a-package"></a>Aktualizace balíčku

1. V **Průzkumníka řešení**, pravým tlačítkem myši buď **odkazy** nebo požadovaný projekt a vyberte **spravovat balíčky NuGet...** . (V projektech webových stránek, klikněte pravým tlačítkem myši **Bin** složky.)
1. Vyberte **aktualizace** kartu pro zobrazení balíčky, které jsou dostupné aktualizace z vybraného balíčku zdrojů. Vyberte **zahrnout předběžné verze** zahrnout předběžné verze balíčků v seznamu aktualizací.
1. Vyberte balíček, který chcete aktualizovat, vyberte požadovanou verzi z rozevíracího seznamu na pravé straně a vyberte **aktualizovat**.

    ![Aktualizace balíčku](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Pro některé balíčky **aktualizace** je tlačítko neaktivní a zobrazí se zpráva s informacemi o tom, že jej je "implicitně odkazovat pomocí sady SDK" (nebo "AutoReferenced"). Tato zpráva znamená, že balíček je součástí větší platforma nebo sada SDK a by neměly být aktualizovány nezávisle na sobě. (Tyto balíčky jsou označené interně `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Například `Microsoft.NETCore.App` je součástí sady .NET Core SDK, a verze balíčku není stejná jako verze rozhraní framework modulu runtime aplikace používá. Je potřeba [aktualizaci instalace .NET Core](https://aka.ms/dotnet-download) získat nové verze modulu runtime ASP.NET Core a .NET Core. [Najdete v tomto dokumentu podrobné informace o .NET Core metabalíčky a správy verzí](/dotnet/core/packages). To platí pro běžně používané následujících balíčků:
    * Metabalíček
    * Microsoft.AspNetCore.App
    * Balíčky Microsoft.NETCore.App
    * NETStandard.Library

    ![Příklad balíček označen jako implicitně odkazy nebo AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. K aktualizaci více balíčků na jejich nejnovější verze, vyberte je v seznamu a vyberte **aktualizovat** tlačítko nad seznamem.
1. Můžete také aktualizovat v nějakém balíčku **nainstalováno** kartu. V takovém případě podrobnosti balíčku zahrnují volič verze (vztahuje **zahrnout předběžné verze** možnost) a **aktualizace** tlačítko.

## <a name="managing-packages-for-the-solution"></a>Správa balíčků pro řešení

Správa balíčků pro řešení je pohodlný způsob pro práci s více projektů současně.

1. Vyberte **nástroje > Správce balíčků NuGet > spravovat balíčky NuGet pro řešení...**  nabídky příkazu, nebo klikněte pravým tlačítkem na řešení a vyberte **spravovat balíčky NuGet...** :

    ![Spravovat balíčky NuGet pro řešení](media/ManagePackagesSolutionUICommand.png)

1. Při správě balíčků pro řešení, uživatelské rozhraní vám umožní vybrat projekty, které jsou ovlivněny operace:

    ![Selektor projektu při správě balíčků řešení](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Konsolidace kartu

Vývojáři obvykle považuje za špatný postup používají různé verze stejného balíčku NuGet v různých projektech ve stejném řešení. Pokud budete chtít spravovat balíčky pro řešení, poskytuje uživatelské rozhraní Správce balíčků **konsolidovat** karta, na které můžete snadno zobrazit kde balíčky s čísly odlišné verze používají různé projekty v řešení:

![Karta konsolidovat uživatelského rozhraní Správce balíčků](media/ConsolidateTab.png)

V tomto příkladu je projekt ClassLibrary1 využitím objektu EntityFramework 6.2.0, zatímco ConsoleApp1 je využitím objektu EntityFramework 6.1.0. Pro konsolidaci verze balíčků, postupujte takto:

- Vyberte projekty, které chcete aktualizovat v seznamu projektu.
- Vyberte verze se má použít ve všech projektech v **verze** ovládacího prvku, třeba 6.2.0 objektu EntityFramework.
- Vyberte **nainstalovat** tlačítko.

Správce balíčků nainstaluje do všech vybraných projektů, po jejichž uplynutí již nezobrazuje balíček na verze vybraného balíčku **konsolidovat** kartu.

## <a name="package-sources"></a>Zdroje balíčků

Chcete-li změnit zdroj, ze kterého sady Visual Studio získá balíčky, vyberte jednu z modulu pro výběr zdroje:

![Výběr zdroje balíčku v uživatelské rozhraní Správce balíčků](media/PackageSourceDropDown.png)

Správa zdroje balíčků:

1. Vyberte **nastavení** ikony v Uživatelském rozhraní Správce balíčků uvedených níže nebo pomocí **nástroje > Možnosti** příkazů a přejděte k položce **Správce balíčků NuGet**:

    ![Ikona nastavení uživatelského rozhraní Správce balíčků](media/PackageSourceSettings.png)

1. Vyberte **zdroje balíčků** uzlu:

    ![Možnosti zdroje balíčku](media/options.png)

1. Chcete-li přidat zdroj **+**, upravte název, zadejte adresu URL nebo cestu **zdroj** ovládací prvek a vyberte **aktualizace**. Zdroj se teď zobrazí v rozevírací seznam pro výběr.
1. Chcete-li změnit zdroj balíčku, vyberte ho, proveďte úpravy v **název** a **zdroj** pole a vyberte **aktualizace**.
1. Zakázat zdroje balíčku, zrušte zaškrtnutí políčka nalevo od názvu v seznamu.
1. Odebrat zdroj balíčku, vyberte ho a pak vyberte **X** tlačítko.
1. Nahoru a Šipka dolů změňte pořadí priority zdroje balíčků. Při obnovování balíčků pro projekt sady Visual Studio vyhledá tyto zdroje v pořadí podle priority. Další informace najdete v tématu [obnovení balíčku](../consume-packages/package-restore.md).

> [!Tip]
> Pokud po jejím odstranění znovu objeví zdroj balíčku, mohou být uvedeny v úrovni počítače nebo individuální `NuGet.Config` soubory. Naleznete v tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md) pro umístění tyto soubory pak odebrat zdrojový úprava souborů ručně nebo pomocí [nuget zdrojů příkaz](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Ovládací prvek možnosti Správce balíčků

Při výběru balíčku, uživatelské rozhraní Správce balíčků zobrazí malá, rozšiřitelné **možnosti** ovládacího prvku pod volič verze (zobrazuje se zde i sbalení a rozbalení). Všimněte si, že některé projektu typy pouze **zobrazit okno náhledu** možnost je k dispozici.

![Možnosti Správce balíčků](media/PackageManagerUIOptions.png)

Následující části popisují tyto možnosti.

### <a name="show-preview-window"></a>Zobrazit okno náhledu

Vyberete-li, modální okno zobrazí které závislosti zvolené balíček před instalací balíčku:

![Dialogové okno náhledu příklad](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Možnosti instalace a aktualizace

(Není k dispozici pro všechny typy projektů.)

**Chování závislostí** konfiguruje jak NuGet rozhodne, která verze závislé balíčky pro instalaci:

- *Ignorovat závislosti* přeskočí instalaci všechny závislosti, přerušíte obvykle probíhá instalace balíčku.
- *Nejnižší* [výchozí] instaluje závislost s minimální verze číslo, které splňuje požadavky na primární zvolené balíčku.
- *Nejvyšší oprava* nainstaluje verzi s stejná čísla hlavní verze a podverze, ale nejvyšší číslo opravy. Například pokud je zadaná verze 1.2.2 klikněte nejvyšší, který začíná 1.2 budou nainstalovány jejich verze
- *Nejvyšší podverze* nainstaluje verzi stejné číslo hlavní verze, ale nejvyšší číslo podverze a oprava číslo. Pokud je zadaná verze 1.2.2, pak nejvyšší začínající hodnotou 1 budou nainstalovány jejich verze
- *Nejvyšší* nainstaluje nejvyšší dostupnou verzi balíčku.

**Akce při konfliktu souborů** Určuje, jak NuGet pracovat s balíčky, které již existují v projektu nebo v místním počítači:

- *Příkazový řádek* dává pokyn k dotaz, jestli chcete zachovat nebo přepsat existující balíčky NuGet.
- *Přeskakovat vše* dá pokyn, chcete-li přeskočit přepíše všechny stávající balíčky NuGet.
- *Přepsat vše* dává pokyn k přepsání existujících balíčků NuGet.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Možnosti odinstalace

(Není k dispozici pro všechny typy projektů.)

**Odebrat závislosti**: Pokud je vybráno, odebere všechny závislé balíčky, pokud nejsou odkazovat kdekoli v projektu.

**Vynutit odinstalaci i v případě, že jsou na něm závislosti**: Pokud je vybráno, odinstaluje balíček i v případě, že je stále odkazovaný v projektu. To se obvykle používá v kombinaci s **odebrat závislosti** odebrat balíček a cokoli, co je nainstalovat závislosti. Pomocí této možnosti může, ale vést k poškození odkazů v projektu. V takovém případě budete muset [znovu nainstalujte tyto balíčky](../consume-packages/reinstalling-and-updating-packages.md).
