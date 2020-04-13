---
title: Instalace a správa balíčků NuGet v sadě Visual Studio
description: Pokyny pro použití nuget správce balíčků ui v sadě Visual Studio pro práci s balíčky NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428693"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Instalace a správa balíčků v sadě Visual Studio pomocí Správce balíčků NuGet

NuGet Package Manager UI v sadě Visual Studio v systému Windows umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních. Zkušenosti v Visual Studiu pro Mac najdete [v tématu zahrnutí balíčku NuGet v projektu](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). Ui Správce balíčků není součástí kódu sady Visual Studio.

> [!NOTE]
> Pokud vám chybí Správce balíčků NuGet ve Visual Studiu 2015, zkontrolujte **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření *NuGet Package Manager.* Pokud se vám nedaří použít instalační program rozšíření v sadě [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Visual Studio, stáhněte si rozšíření přímo z aplikace .
>
> Počínaje Visual Studio 2017, NuGet a NuGet Správce balíčků jsou automaticky nainstalovány s libovolným . NET související s úlohami. Nainstalujte ji jednotlivě výběrem **jednotlivých součástí > nástroje Code >** možnost i správce balíčků NuGet v instalačním programu sady Visual Studio.

## <a name="find-and-install-a-package"></a>Vyhledání a instalace balíčku

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na **odkazy** nebo na projekt a vyberte **spravovat balíčky NuGet...**.

    ![Možnost nabídky Spravovat balíčky NuGet](media/ManagePackagesUICommand.png)

1. Na kartě **Procházet** se zobrazí balíčky podle oblíbenosti z aktuálně vybraného zdroje (viz [zdroje balíčků](#package-sources)). Vyhledejte konkrétní balíček pomocí vyhledávacího pole v levém horním rohu. Vyberte balíček ze seznamu, chcete-li zobrazit jeho informace, což také umožňuje **tlačítko Instalovat** spolu s rozevíracím seznamem výběr verze.

    ![Karta Procházet dialogové okno Spravovat balíčky nugetů](media/Search.png)

1. V rozevíracím souboru vyberte požadovanou verzi a vyberte **Instalovat**. Visual Studio nainstaluje balíček a jeho závislosti do projektu. Můžete být požádáni o přijetí licenčních podmínek. Po dokončení instalace se přidané balíčky zobrazí na kartě **Nainstalováno.** Balíčky jsou také **uvedeny** v uzlu Reference `using` průzkumníka řešení, což znamená, že na ně můžete odkazovat v projektu s příkazy.

    ![Odkazy v Průzkumníku řešení](media/References.png)

> [!Tip]
> Chcete-li do hledání zahrnout předběžné verze a zpřístupnit předběžné verze v rozevíracím souboru verze, vyberte možnost **Zahrnout předběžnou verzi.**

> [!Note]
> NuGet má dva formáty, ve kterých může projekt používat balíčky: [`PackageReference`](package-references-in-project-files.md) a [`packages.config`](../reference/packages-config.md). [Výchozí nastavení lze nastavit v okně možností sady Visual Studio](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>Odinstalace balíčku

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na **odkazy** nebo na požadovaný projekt a vyberte **spravovat balíčky NuGet...**.
1. Vyberte kartu **Nainstalováno**.
1. Vyberte balíček, který chcete odinstalovat (v případě potřeby pomocí hledání seznam vyfiltrujte) a vyberte **Odinstalovat**.

    ![Odinstalace balíčku](media/UninstallPackage.png)

1. Všimněte si, že **zahrnout předběžné verze** a **balíček zdrojové** ovládací prvky nemají žádný vliv při odinstalaci balíčků.

## <a name="update-a-package"></a>Aktualizace balíčku

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na **odkazy** nebo na požadovaný projekt a vyberte **spravovat balíčky NuGet...**. (V projektech webu klikněte pravým tlačítkem myši na složku **Bin.)**
1. Výběrem karty **Aktualizace** zobrazíte balíčky, které mají k dispozici aktualizace z vybraných zdrojů balíčků. Vyberte **Zahrnout předběžnou verzi,** chcete-li do seznamu aktualizací zahrnout předběžné balíčky.
1. Vyberte balíček, který chcete aktualizovat, vyberte požadovanou verzi z rozevíracího balíčku vpravo a vyberte **Aktualizovat**.

    ![Aktualizace balíčku](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>U některých balíčků je zakázáno tlačítko **Aktualizovat** a zobrazí se zpráva, že je "Implicitně odkazováno sadou SDK" (nebo "AutoReferenced"). Tato zpráva označuje, že balíček je součástí větší rozhraní nebo sady SDK a by neměly být aktualizovány nezávisle. (Tyto balíčky jsou `<IsImplicitlyDefined>True</IsImplicitlyDefined>`vnitřně označeny .) Například `Microsoft.NETCore.App` je součástí sady .NET Core SDK a verze balíčku není stejná jako verze rozhraní runtime, kterou používá aplikace. Chcete-li získat nové verze ASP.NET core a .NET Core runtime, musíte [aktualizovat instalaci jádra .NET.](https://aka.ms/dotnet-download) [Další podrobnosti o metabalíčcích .NET Core a správě verzí](/dotnet/core/packages)naleznete v tomto dokumentu. To platí pro následující běžně používané balíčky:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Aplikace Microsoft.NETCore.App
    * NETStandard.Knihovna

    ![Ukázkový balíček označený jako implicitně odkazy nebo AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. Chcete-li aktualizovat více balíčků na jejich nejnovější verze, vyberte je v seznamu a vyberte tlačítko **Aktualizovat** nad seznamem.
1. Jednotlivé balíčky můžete také aktualizovat na kartě **Nainstalováno.** V tomto případě podrobnosti o balíčku zahrnují volič verze (s výhradou **include předběžné verze** možnost) a tlačítko **Aktualizovat.**

## <a name="manage-packages-for-the-solution"></a>Správa balíčků pro řešení

Správa balíčků pro řešení je pohodlným prostředkem pro práci s více projekty současně.

1. Vyberte **příkaz nabídky Nástroje > NuGet > Spravovat balíčky NuGet pro řešení...** nebo klepněte pravým tlačítkem myši na řešení a vyberte spravovat **balíčky NuGet...**:

    ![Správa balíčků NuGet pro řešení](media/ManagePackagesSolutionUICommand.png)

1. Při správě balíčků pro řešení umožňuje unové oi vybrat projekty, které jsou ovlivněny operacemi:

    ![Výběr projektu při správě balíčků pro řešení](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Karta Konsolidovat

Vývojáři obvykle považují za špatné praxe používat různé verze stejného balíčku NuGet napříč různými projekty ve stejném řešení. Pokud se rozhodnete spravovat balíčky pro řešení, ui Správce balíčků poskytuje **kartu Konsolidovat,** na které můžete snadno zjistit, kde balíčky s odlišnými čísly verzí jsou používány různými projekty v řešení:

![Karta Konsolidovat ui správce balíčků](media/ConsolidateTab.png)

V tomto příkladu classlibrary1 projekt používá EntityFramework 6.2.0, vzhledem k tomu, ConsoleApp1 používá EntityFramework 6.1.0. Chcete-li konsolidovat verze balíčku, postupujte takto:

- Vyberte projekty, které chcete aktualizovat v seznamu projektů.
- Vyberte verzi, která se má použít ve všech těchto projektech v ovládacím **prvku verze,** například EntityFramework 6.2.0.
- Vyberte tlačítko **Instalovat.**

Správce balíčků nainstaluje vybranou verzi balíčku do všech vybraných projektů, po kterých se balíček již nezobrazí na kartě **Konsolidovat.**

## <a name="package-sources"></a>Zdroje balíčků

Chcete-li změnit zdroj, ze kterého Visual Studio získává balíčky, vyberte jeden z voliče zdroje:

![Výběr zdroje balíčků v uzdu správce balíčků](media/PackageSourceDropDown.png)

Správa zdrojů balíčků:

1. Vyberte ikonu **Nastavení** v hlavním uživateli Správce balíčků uvedenéníže nebo použijte příkaz **Nástroje > možnosti** a přejděte na **NuGet Package Manager**:

    ![Ikona nastavení ui správce balíčků](media/PackageSourceSettings.png)

1. Vyberte uzel **Zdroje balíčků:**

    ![Možnosti zdrojů balíčků](media/options.png)

1. Chcete-li přidat **+** zdroj, vyberte , upravte název, zadejte adresu URL nebo cestu **do ovládacího prvku Zdroj** a vyberte **Aktualizovat**. Zdroj se nyní zobrazí v rozevíracím okně voliče.
1. Chcete-li změnit zdroj balíčku, vyberte jej, proveďte úpravy v polích **Název** a **Zdroj** a vyberte **Aktualizovat**.
1. Chcete-li zakázat zdroj balíčku, zrušte zaškrtnutí políčka nalevo od názvu v seznamu.
1. Chcete-li odebrat zdroj balíčku, vyberte jej a pak vyberte tlačítko **X.**
1. Použití tlačítek se šipkami nahoru a dolů nezmění pořadí priorit zdrojů balíčků. Visual Studio ignoruje pořadí zdrojů balíčků, pomocí balíčku z toho, který zdroj je první reagovat na požadavky. Další informace naleznete v [tématu Obnovení balíčku](../consume-packages/package-restore.md).

> [!Tip]
> Pokud se zdroj balíčku po jeho odstranění znovu zobrazí, může být uveden `NuGet.Config` v souborech na úrovni počítače nebo na úrovni uživatele. Viz [Běžné Konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md) pro umístění těchto souborů, potom odebrat zdroj úpravou souborů ručně nebo pomocí [nuget zdroje příkazu](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Ovládací prvek Možnosti správce balíčků

Když je vybrán balíček, ui Správce balíčků zobrazí malý, rozbalitelný ovládací prvek **Možnosti** pod voličem verze (zobrazeno zde sbalené i rozšířené). Všimněte si, že pro některé typy projektů je k dispozici pouze možnost **Zobrazit okno náhledu.**

![Možnosti správce balíčků](media/PackageManagerUIOptions.png)

Následující části vysvětlují tyto možnosti.

### <a name="show-preview-window"></a>Zobrazit okno náhledu

Je-li tato možnost vybrána, zobrazí se modální okno, které jsou závislosti vybraného balíčku před instalací balíčku:

![Dialogové okno Náhled na příklad](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Možnosti instalace a aktualizace

(Není k dispozici pro všechny typy projektů.)

**Chování závislostí** konfiguruje způsob, jakým nuget rozhoduje o tom, které verze závislých balíčků mají být nainstalovány:

- *Ignorovat závislosti přeskočí* instalaci všech závislostí, které obvykle přeruší balíček, který je nainstalován.
- *Nejnižší* [Výchozí] nainstaluje závislost s minimálním číslem verze, které splňuje požadavky primárního vybraného balíčku.
- *Nejvyšší oprava* nainstaluje verzi se stejnými hlavními a dílčími čísly verzí, ale s nejvyšším číslem opravy. Pokud je například zadána verze 1.2.2, bude nainstalována nejvyšší verze začínající verzí 1.2.
- *Nejvyšší vedlejší* nainstaluje verzi se stejným číslem hlavní verze, ale nejvyšší dílčí číslo a číslo opravy. Pokud je zadána verze 1.2.2, bude nainstalována nejvyšší verze začínající na 1.
- *Nejvyšší* nainstaluje nejvyšší dostupnou verzi balíčku.

**Akce konfliktu souborů** určuje, jak by měl NuGet zpracovávat balíčky, které již existují v projektu nebo místním počítači:

- *Výzva* pokyn NuGet se zeptat, zda zachovat nebo přepsat existující balíčky.
- *Ignorovat všechny* pokyny NuGet přeskočit přepsání všechny existující balíčky.
- *Přepsat všechny* pokyny NuGet přepsat všechny existující balíčky.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Možnosti odinstalace

(Není k dispozici pro všechny typy projektů.)

**Odebrat závislosti**: Pokud je tato možnost vybrána, odebere všechny závislé balíčky, pokud nejsou odkazovány jinde v projektu.

**Vynutit odinstalaci i v případě, že jsou na něm závislosti**: pokud je vybrána, odinstaluje balíček, i když je stále odkazován v projektu. To se obvykle používá v kombinaci s **Remove závislosti** odebrat balíček a bez ohledu na závislosti, které nainstalován. Použití této možnosti však může vést k přerušené odkazy v projektu. V takových případech může být nutné [přeinstalovat tyto další balíčky](../consume-packages/reinstalling-and-updating-packages.md).
