---
title: Instalace a Správa balíčků NuGet v aplikaci Visual Studio
description: Pokyny k používání uživatelského rozhraní Správce balíčků NuGet v aplikaci Visual Studio pro práci s balíčky NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 7e4ea59b9954e787e7ab060adc964f3097a8240b
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419969"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Instalace a Správa balíčků v aplikaci Visual Studio pomocí Správce balíčků NuGet

Uživatelské rozhraní Správce balíčků NuGet v aplikaci Visual Studio ve Windows umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních. Informace o zkušenostech v Visual Studio pro Mac najdete v tématu [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). Uživatelské rozhraní Správce balíčků není součástí Visual Studio Code.

> [!NOTE]
> Pokud ve Visual Studiu 2015 chybí správce balíčků NuGet, podívejte se na **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření *Správce balíčků NuGet* . Pokud nemůžete použít instalační program rozšíření v aplikaci Visual Studio, Stáhněte si rozšíření přímo z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).
>
> Od sady Visual Studio 2017 se NuGet a správce balíčků NuGet automaticky nainstalují se všemi. Úlohy týkající se netto. Nainstalujte ji jednotlivě, a to tak, že vyberete **jednotlivé komponenty > nástrojů kódu >** v instalačním programu sady Visual Studio možnost Správce balíčků NuGet.

## <a name="find-and-install-a-package"></a>Vyhledání a instalace balíčku

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši buď na **odkaz** , nebo na projekt a vyberte **Spravovat balíčky NuGet...** .

    ![Možnost spravovat balíčky NuGet – možnost nabídky](media/ManagePackagesUICommand.png)

1. Karta **Procházet** zobrazuje balíčky podle oblíbenosti z aktuálně vybraného zdroje (viz [zdroje balíčků](#package-sources)). Vyhledejte konkrétní balíček pomocí vyhledávacího pole v levém horním rohu. Výběrem balíčku ze seznamu zobrazíte jeho informace, což také umožňuje **nainstalovat tlačítko instalovat** společně s rozevíracím seznamem výběru verze.

    ![Dialogové okno Spravovat balíčky NuGet – karta Procházet](media/Search.png)

1. V rozevíracím seznamu vyberte požadovanou verzi a vyberte **nainstalovat**. Visual Studio nainstaluje balíček a jeho závislosti do projektu. Může se zobrazit výzva, abyste přijali Licenční podmínky. Po dokončení instalace se přidané balíčky zobrazí na kartě **nainstalované** . Balíčky jsou také uvedeny v uzlu **odkazy** Průzkumník řešení, což znamená, že je můžete odkazovat v projektu pomocí `using` příkazů.

    ![Odkazy v Průzkumník řešení](media/References.png)

> [!Tip]
> Chcete-li do hledání zahrnout předběžné verze předprodejní verze a v rozevíracím seznamu verze zpřístupnit předprodejní verze, vyberte možnost **Zahrnout předběžnou** verzi.

## <a name="uninstall-a-package"></a>Odinstalace balíčku

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši buď na **odkaz** , nebo na požadovaný projekt a vyberte **Spravovat balíčky NuGet...** .
1. Vyberte kartu **nainstalované** .
1. Vyberte balíček, který chcete odinstalovat (Pokud je to nutné, pomocí hledání vyfiltrujte seznam) a vyberte **odinstalovat**.

    ![Odinstalace balíčku](media/UninstallPackage.png)

1. Všimněte si, že **zahrnuté předběžné verze** a zdrojové ovládací prvky **balíčku** nemají žádný vliv na odinstalaci balíčků.

## <a name="update-a-package"></a>Aktualizace balíčku

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši buď na **odkaz** , nebo na požadovaný projekt a vyberte **Spravovat balíčky NuGet...** . (V projektech webu klikněte pravým tlačítkem myši na složku **bin** .)
1. Kliknutím na kartu **aktualizace** zobrazíte balíčky, které mají dostupné aktualizace z vybraných zdrojů balíčků. V seznamu aktualizace zvolte **Zahrnout** předprodejní verze pro zahrnutí předprodejních balíčků.
1. Vyberte balíček, který chcete aktualizovat, vyberte požadovanou verzi v rozevíracím seznamu napravo a vyberte **aktualizovat**.

    ![Aktualizace balíčku](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>U některých balíčků je tlačítko **aktualizovat** zakázané a zobrazí se zpráva s oznámením, že se jedná o "implicitně odkazované sadu SDK" (nebo "autoreferenced"). Tato zpráva znamená, že balíček je součástí větší architektury nebo sady SDK a neměli byste ho aktualizovat nezávisle. (Tyto balíčky jsou vnitřně označeny `<IsImplicitlyDefined>True</IsImplicitlyDefined>`pomocí.) Například `Microsoft.NETCore.App` je součástí .NET Core SDK a verze balíčku není stejná jako verze rozhraní modulu runtime používaného aplikací. Musíte [aktualizovat instalaci .NET Core](https://aka.ms/dotnet-download) a získat nové verze ASP.NET Core a modulu runtime .NET Core. [Další podrobnosti o .NET Core metabalíčky a verzích najdete v tomto dokumentu](/dotnet/core/packages). To platí pro následující běžně používané balíčky:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard. Library

    ![Ukázkový balíček označený jako implicitně odkazující nebo automaticky odkazovaný](media/PackageManagerUIAutoReferenced.png)

1. Pokud chcete aktualizovat více balíčků na nejnovější verze, vyberte je v seznamu a klikněte na tlačítko **aktualizovat** nad seznamem.
1. Jednotlivé balíčky můžete také aktualizovat na kartě **nainstalované** . V takovém případě podrobnosti balíčku zahrnují selektor verze (podléhající možnosti předprodejní **zahrnutí** ) a tlačítko **aktualizovat** .

## <a name="manage-packages-for-the-solution"></a>Spravovat balíčky pro řešení

Správa balíčků pro řešení je pohodlný způsob práce s více projekty současně.

1. Vyberte **nástroje > správce balíčků nuget > spravovat balíčky NuGet pro řešení...** příkaz nabídky nebo klikněte pravým tlačítkem na řešení a vyberte **Spravovat balíčky NuGet...** :

    ![Spravovat balíčky NuGet pro řešení](media/ManagePackagesSolutionUICommand.png)

1. Při správě balíčků pro řešení vám uživatelské rozhraní umožní vybrat projekty, které jsou ovlivněné operacemi:

    ![Selektor projektu při správě balíčků pro řešení](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Karta konsolidovat

Vývojáři obvykle považují za chybné postupy použití různých verzí stejného balíčku NuGet v různých projektech ve stejném řešení. Pokud se rozhodnete spravovat balíčky pro řešení, uživatelské rozhraní Správce balíčků poskytuje kartu **konsolidace** , na které můžete snadno zjistit, kde jsou balíčky s různými čísly verzí používány různými projekty v řešení:

![Karta konsolidace uživatelského rozhraní Správce balíčků](media/ConsolidateTab.png)

V tomto příkladu projekt ClassLibrary1 používá EntityFramework 6.2.0, zatímco ConsoleApp1 používá EntityFramework 6.1.0. Chcete-li konsolidovat verze balíčků, postupujte následovně:

- Vyberte projekty, které chcete aktualizovat v seznamu projektu.
- Vyberte verzi, která má být použita ve všech projektech v rámci správy **verzí** , například EntityFramework 6.2.0.
- Vyberte tlačítko **instalovat** .

Správce balíčků nainstaluje vybranou verzi balíčku do všech vybraných projektů, po kterém se balíček už nebude zobrazovat na kartě **konsolidace** .

## <a name="package-sources"></a>Zdroje balíčků

Chcete-li změnit zdroj, ze kterého aplikace Visual Studio získává balíčky, vyberte jeden z voliče zdroje:

![Selektor zdrojů balíčku v uživatelském rozhraní Správce balíčků](media/PackageSourceDropDown.png)

Správa zdrojů balíčků:

1. V uživatelském rozhraní Správce balíčků vyberte ikonu **Nastavení** , která je níže uvedená níže, nebo použijte příkaz **Nástroje > Možnosti** a přejděte na **Správce balíčků NuGet**:

    ![Ikona nastavení uživatelského rozhraní Správce balíčků](media/PackageSourceSettings.png)

1. Vyberte uzel **zdroje balíčků** :

    ![Možnosti zdrojů balíčků](media/options.png)

1. Pokud chcete přidat zdroj, vyberte **+** , upravte název, zadejte adresu URL nebo cestu ve správě **zdrojového kódu** a vyberte **aktualizovat**. Zdroj se nyní zobrazí v rozevíracím seznamu selektoru.
1. Chcete-li změnit zdroj balíčku, vyberte jej, proveďte úpravy v polích **název** a **zdroj** a vyberte možnost **aktualizovat**.
1. Chcete-li zakázat zdroj balíčku, zrušte zaškrtnutí políčka nalevo od názvu v seznamu.
1. Pokud chcete odebrat zdroj balíčku, vyberte ho a pak klikněte na tlačítko **X** .
1. Pomocí tlačítek se šipkami nahoru a dolů se nezmění pořadí priorit zdrojů balíčku. Sada Visual Studio ignoruje pořadí zdrojů balíčku. při použití balíčku z libovolného zdroje je nejprve nutné reagovat na požadavky. Další informace najdete v tématu věnovaném [obnovení balíčků](../consume-packages/package-restore.md).

> [!Tip]
> Pokud se po odstranění zobrazí zdroj balíčku, může být uveden v souborech na úrovni počítače nebo na úrovni `NuGet.Config` uživatele. V tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md) pro umístění těchto souborů odstraňte zdroj úpravou souborů ručně nebo pomocí [příkazu NuGet sources](../reference/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Řízení možností Správce balíčků

Když je vybraný balíček, v uživatelském rozhraní Správce balíčků se pod selektorem verzí zobrazí malý ovládací prvek **možností s možností** rozšíření (tady se zobrazí sbalená i rozbalená). Všimněte si, že u některých typů projektů je k dispozici pouze možnost **Zobrazit okno náhledu** .

![Možnosti Správce balíčků](media/PackageManagerUIOptions.png)

Tyto možnosti jsou vysvětleny v následujících částech.

### <a name="show-preview-window"></a>Zobrazit okno náhledu

Když se tato možnost vybere, otevře se modální okno, které obsahuje závislosti vybraného balíčku před instalací balíčku:

![Ukázka náhledu – dialogové okno](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Možnosti instalace a aktualizace

(Není k dispozici pro všechny typy projektů.)

**Chování závislostí** konfiguruje, jak NuGet určuje, které verze závislých balíčků nainstalovat:

- *Ignorovat závislosti* přeskočí instalaci všech závislostí, což obvykle přeruší instalaci balíčku.
- *Nejnižší* [Výchozí] nainstaluje závislost s minimálním číslem verze, který splňuje požadavky primárního vybraného balíčku.
- *Nejvyšší oprava* nainstaluje verzi se stejnými čísly hlavní verze a podverze, ale nejvyšší číslo opravy. Pokud je například zadána verze 1.2.2, bude nainstalována nejvyšší verze, která začíná 1,2.
- *Nejvyšší* verze nainstaluje verzi se stejným číslem hlavní verze, ale s nejvyšším podčíslem a číslem opravy. Je-li zadána verze 1.2.2, bude nainstalována nejvyšší verze, která začíná 1.
- *Nejvyšší* verze nainstaluje nejvyšší dostupnou verzi balíčku.

**Akce konfliktu souborů** určuje, jak má NuGet zpracovat balíčky, které už existují v projektu nebo na místním počítači:

- *Prompt* vydá pokyn pro dotaz, jestli chcete zachovat nebo přepsat stávající balíčky.
- *Ignorovat všechny* pokyny NuGet pro přeskočení přepsání existujících balíčků
- Příkaz *přepsat vše* instruuje balíček NuGet, aby přepsal všechny existující balíčky.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Možnosti odinstalace

(Není k dispozici pro všechny typy projektů.)

**Odebrat závislosti**: Pokud je vybraná, odebere všechny závislé balíčky, pokud se na ně neodkazují jinde v projektu.

**Vynutit odinstalaci i v případě**, že jsou k dispozici závislosti: Pokud je vybrána, odinstaluje balíček i v případě, že je stále odkazován v projektu. Obvykle se používá v kombinaci s **odebráním závislostí** pro odebrání balíčku a libovolné závislosti, které nainstaloval. Použití této možnosti může však vést k nefunkčním odkazům v projektu. V takových případech bude pravděpodobně nutné přeinstalovat [tyto balíčky](../consume-packages/reinstalling-and-updating-packages.md).
