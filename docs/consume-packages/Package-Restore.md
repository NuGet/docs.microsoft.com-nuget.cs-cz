---
title: Obnovení balíčku NuGet
description: Přehled o tom, jak NuGet obnovuje balíčky projektu závisí na, včetně jak zakázat obnovení a omezit verze.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428742"
---
# <a name="restore-packages-using-package-restore"></a>Obnovení balíčků pomocí nástroje Obnovení balíčků

Chcete-li podpořit čistší vývojové prostředí a zmenšit velikost úložiště, NuGet **Package Restore** nainstaluje `packages.config`všechny závislosti projektu uvedené v souboru projektu nebo . Rozhraní .NET Core 2.0+ `dotnet build` a `dotnet run` příkazy provést automatické obnovení balíčku. Visual Studio můžete obnovit balíčky automaticky při vytváření projektu a můžete obnovit `nuget restore`balíčky kdykoliprostřednictvím Sady Visual Studio, , `dotnet restore`a xbuild na Mono.

Obnovení balíčku zajišťuje, že všechny závislosti projektu jsou k dispozici, aniž by bylo třeba je ukládat do správy zdrojového kódu. Chcete-li nakonfigurovat úložiště správy zdrojového kódu tak, aby vylučovalo binární soubory balíčků, přečtěte si informace [o balíčcích a slučování zdrojů](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Přehled obnovení balíčku

Obnovení balíčku nejprve nainstaluje přímé závislosti projektu podle potřeby, pak nainstaluje všechny závislosti těchto balíčků v celém grafu závislostí.

Pokud balíček ještě není nainstalován, NuGet nejprve pokusí načíst z [mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). Pokud balíček není v mezipaměti, NuGet se pokusí stáhnout balíček ze všech povolených zdrojů v seznamu na **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** v sadě Visual Studio. Během obnovení NuGet ignoruje pořadí zdrojů balíčku a používá balíček z toho, který zdroj je první reagovat na požadavky. Další informace o tom, jak se nuget chová, naleznete [v tématu Common NuGet konfigurace](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet neznamená selhání obnovení balíčku, dokud všechny zdroje byly zkontrolovány. V té době NuGet hlásí selhání pouze pro poslední zdroj v seznamu. Chyba znamená, že balíček nebyl přítomen na *žádném* z jiných zdrojů, i když chyby nejsou zobrazeny pro každý z těchto zdrojů jednotlivě.

## <a name="restore-packages"></a>Obnovení balíčků

Nástroj Restore package restore se pokusí nainstalovat všechny závislosti balíčků do správného stavu, který odpovídá odkazům na balíček v souboru projektu (*csproj*) nebo souboru *packages.config.* (V sadě Visual Studio se odkazy zobrazí v Průzkumníku řešení pod **závislostmi \ NuGet** nebo **uzel Reference.)**

1. Pokud jsou odkazy na balíček v souboru projektu správné, obnovte balíčky pomocí upřednostňovaného nástroje.

   - [Visual Studio](#restore-using-visual-studio) [(automatické obnovení](#restore-packages-automatically-using-visual-studio) nebo ruční [obnovení)](#restore-packages-manually-using-visual-studio)
   - [Rozhraní příkazového řádku dotnet](#restore-using-the-dotnet-cli)
   - [Rozhraní příkazového řádku nuget.exe](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Pokud jsou odkazy na balíček v souboru projektu (*.csproj*) nebo soubor *packages.config* nesprávné (neodpovídají požadovanému stavu po obnovení balíčku), musíte místo toho nainstalovat nebo aktualizovat balíčky.

   Pro projekty pomocí PackageReference po úspěšném obnovení balíček by měl `obj/project.assets.json` být přítomen ve složce *globální balíčky* a soubor je znovu vytvořen. Pro projekty pomocí `packages.config`balíček by měl `packages` být uveden ve složce projektu. Projekt by měl nyní úspěšně sestavit. 

2. Pokud se po spuštění nástroje Restore package restore zobrazí stále chybějící balíčky nebo chyby související s balíčky (například ikony chyb v Průzkumníkovi řešení v sadě Visual Studio), budete možná muset postupovat podle pokynů popsaných v [části Poradce při potížích s chybami obnovení balíčků](package-restore-troubleshooting.md) nebo případně [přeinstalovat a aktualizovat balíčky](../consume-packages/reinstalling-and-updating-packages.md).

   V sadě Visual Studio nabízí konzola Správce balíčků několik flexibilních možností pro přeinstalaci balíčků. Viz [Použití aktualizace balíčků](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Obnovení pomocí sady Visual Studio

V sadě Visual Studio v systému Windows:

- Obnovit balíčky automaticky, nebo

- Ruční obnovení balíčků

### <a name="restore-packages-automatically-using-visual-studio"></a>Automatické obnovení balíčků pomocí sady Visual Studio

Obnovení balíčku se stane automaticky při vytváření projektu ze šablony nebo sestavení projektu, s výhradou možností v [povolit a zakázat obnovení balíčku](#enable-and-disable-package-restore-in-visual-studio). V NuGet 4.0+ obnovení také probíhá automaticky, když provedete změny v projektu ve stylu sady SDK (obvykle projekt .NET Core nebo .NET Standard).

1. Povolte automatické obnovení balíčků výběrem **nástroje** > **Možnosti** > **NuGet Správce balíčků**a potom vyberte automaticky zkontrolovat chybějící **balíčky během sestavení v sadě Visual Studio v** části Obnovení **balíčků**.

   Pro projekty, které nejsou ve stylu sady SDK, musíte nejprve vybrat **možnost Povolit nuget ke stažení chybějících balíčků,** abyste povolili možnost automatického obnovení.

1. Sestavte projekt.

   Pokud jeden nebo více jednotlivých balíčků stále není správně nainstalováno, **Průzkumník řešení** zobrazí ikonu chyby. Klepněte pravým tlačítkem myši a vyberte **spravovat balíčky NuGet**a odinstalujte a znovu nainstalujte ohrožené balíčky pomocí **Správce balíčků.** Další informace naleznete v [tématu Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)

   Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí", nebo "Jeden nebo více balíčků NuGet je třeba obnovit, ale nemohlo být, protože nebyl udělen souhlas," [povolte automatické obnovení](#enable-and-disable-package-restore-in-visual-studio). U starších projektů naleznete také [v tématu Migrace na automatické obnovení balíčků](#migrate-to-automatic-package-restore-visual-studio). Viz také [řešení potíží s obnovením balíčků](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Ruční obnovení balíčků pomocí sady Visual Studio

1. Povolte obnovení balíčku výběrem **nástroje** > **Možnosti** > **NuGet Správce balíčků**. V části **Možnosti obnovení balíčků** vyberte **Povolit aplikaci NuGet stahovat chybějící balíčky**.

1. V **Průzkumníku řešení**klepněte pravým tlačítkem myši na řešení a vyberte **příkaz Obnovit balíčky NuGet**.

   Pokud jeden nebo více jednotlivých balíčků stále není správně nainstalováno, **Průzkumník řešení** zobrazí ikonu chyby. Klepněte pravým tlačítkem myši a vyberte **spravovat balíčky NuGet**a potom pomocí **Správce balíčků** odinstalujte a znovu nainstalujte ohrožené balíčky. Další informace naleznete v [tématu Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)

   Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí", nebo "Jeden nebo více balíčků NuGet je třeba obnovit, ale nemohlo být, protože nebyl udělen souhlas," [povolte automatické obnovení](#enable-and-disable-package-restore-in-visual-studio). U starších projektů naleznete také [v tématu Migrace na automatické obnovení balíčků](#migrate-to-automatic-package-restore-visual-studio). Viz také [řešení potíží s obnovením balíčků](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Povolení a zakázání obnovení balíčků v sadě Visual Studio

V sadě Visual Studio řídíte obnovení balíčků především prostřednictvím **nástroje** > **Možnosti** > **NuGet Správce balíčků**:

![Správa obnovení balíčku prostřednictvím možností správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Povolit NuGet ke stažení chybějící balíčky** řídí `packageRestore/enabled` všechny formy obnovení balíčku `NuGet.Config` změnou `%AppData%\NuGet\` nastavení v `~/.nuget/NuGet/` [balíčkuObnovit části](../reference/nuget-config-file.md#packagerestore-section) souboru, na Windows nebo na Mac/Linux. Toto nastavení také umožňuje **příkaz Obnovit balíčky NuGet** v kontextové nabídce řešení v sadě Visual Studio .

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > Chcete-li globálně `packageRestore/enabled` přepsat nastavení, nastavte proměnnou prostředí **EnableNuGetPackageRestore** s hodnotou True nebo False před spuštěním sady Visual Studio nebo spuštěním sestavení.

- **Automaticky zkontrolujte chybějící balíčky během sestavení v** `packageRestore/automatic` sadě Visual Studio řídí automatické obnovení změnou nastavení v [části packageRestore](../reference/nuget-config-file.md#packagerestore-section) souboru. `NuGet.Config` Pokud je tato možnost nastavena na hodnotu True, spuštění sestavení z sady Visual Studio automaticky obnoví všechny chybějící balíčky. Toto nastavení nemá vliv na sestavení spuštěná z příkazového řádku MSBuild.

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Chcete-li povolit nebo zakázat obnovení balíčků pro všechny uživatele v počítači, může vývojář nebo společnost přidat nastavení konfigurace do globálního `nuget.config` souboru. Globální `nuget.config` je v `%ProgramData%\NuGet\Config`systému Windows `\{IDE}\{Version}\{SKU}\` na , někdy pod konkrétní `~/.local/share`složku Visual Studio nebo v Mac/Linux na . Jednotliví uživatelé pak mohou selektivně povolit obnovení podle potřeby na úrovni projektu. Další podrobnosti o tom, jak NuGet upřednostňuje více konfiguračních souborů, naleznete [v tématu Běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Pokud upravujete `packageRestore` nastavení `nuget.config`přímo v aplikaci , restartujte aplikaci Visual Studio tak, aby dialogové okno **Možnosti** zobrazovaly aktuální hodnoty.

### <a name="choose-default-package-management-format"></a>Zvolit výchozí formát správy balíčků

![Řídit výchozí formát správy balíčků pomocí možností Správce balíčků NuGet](media/Restore-02-PackageFormatOptions.png)

NuGet má dva formáty, ve kterých může projekt používat balíčky: [`PackageReference`](package-references-in-project-files.md) a [`packages.config`](../reference/packages-config.md). Výchozí formát lze vybrat z rozevíracího souboru v záhlaví **Správa balíčků.** Možnost, která má být vyzvána při instalaci prvního balíčku v projektu je také k dispozici.

> [!Note]
> Pokud projekt nepodporuje oba formáty správy balíčků, bude použitý formát správy balíčků ten, který je kompatibilní s projektem, a proto nemusí být výchozí sadou v možnostech. Kromě toho NuGet nebude výzvu k výběru na první instalaci balíčku, i v případě, že možnost je vybrána v okně možností.
>
> Pokud správce balíčků Konzola slouží k instalaci první balíček v projektu, NuGet nebude výzvu k výběru formátu, i v případě, že možnost je vybrána v okně možností.

## <a name="restore-using-the-dotnet-cli"></a>Obnovení pomocí rozhraní se konstruujícím rozhraní DOTNet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Chcete-li přidat chybějící odkaz na balíček do souboru projektu, `restore` použijte [balíček dotnet add](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), který také spustí příkaz.

## <a name="restore-using-the-nugetexe-cli"></a>Obnovení pomocí cli nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> Příkaz `restore`nemění soubor projektu nebo *soubor packages.config*. Chcete-li přidat závislost, přidejte balíček prostřednictvím uzly Správce balíčků nebo konzoly v `install` `restore`sadě Visual Studio nebo upravte *soubor packages.config* a spusťte buď nebo .

## <a name="restore-using-msbuild"></a>Obnovení pomocí nástroje MSBuild

Chcete-li obnovit balíčky uvedené v souboru projektu s PackageReference, použijte příkaz [msbuild -t:restore.](../reference/msbuild-targets.md#restore-target) Tento příkaz je k dispozici pouze v NuGet 4.x+ a MSBuild 15.1+, které jsou součástí Visual Studio 2017 a vyšší verze. Oba `nuget restore` `dotnet restore` a použít tento příkaz pro příslušné projekty.

1. Otevřete příkazový řádek Vývojář (Do **vyhledávacího** pole zadejte **příkazový řádek Vývojář**).

   Obvykle chcete spustit příkazový řádek pro vývojáře pro Visual Studio z nabídky **Start,** protože bude nakonfigurován se všemi potřebnými cestami pro MSBuild.

2. Přepněte do složky obsahující soubor projektu a zadejte následující příkaz.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Zadejte následující příkaz pro opětovné sestavení projektu.

   ```cmd
   msbuild
   ```

   Ujistěte se, že výstup MSBuild označuje, že sestavení bylo úspěšně dokončeno.

## <a name="restore-using-azure-pipelines"></a>Obnovení pomocí Azure Pipelines

Při vytváření definice sestavení v Azure Pipelines, zahrnout NuGet [obnovení](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) nebo .NET Core [obnovení](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) úlohy v definici před všechny úlohy sestavení. Některé šablony sestavení zahrnují úlohu obnovení ve výchozím nastavení.

## <a name="restore-using-azure-devops-server"></a>Obnovení pomocí serveru Azure DevOps

Azure DevOps Server a TFS 2013 a novější automaticky obnovit balíčky během sestavení, pokud používáte šablonu TFS 2013 nebo novější team build. Pro starší verze TFS můžete zahrnout krok sestavení pro spuštění možnosti obnovení příkazového řádku nebo volitelně migrovat šablonu sestavení na novější verzi. Další informace naleznete v [tématu Nastavení obnovení balíčku pomocí team foundation buildu](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Omezit verze balíčků s obnovením

Když NuGet obnoví balíčky prostřednictvím libovolné metody, respektuje `packages.config` všechna omezení, která jste zadali v souboru projektu:

- V `packages.config`programu můžete zadat rozsah `allowedVersion` verzí ve vlastnosti závislosti. Další informace naleznete [v tématu Omezit verze upgradu.](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) Příklad:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- V souboru projektu můžete použít PackageReference k určení rozsahu závislosti přímo. Příklad:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Ve všech případech použijte zápis popsaný v [package versioning](../concepts/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Vynutit obnovení ze zdrojů balíčků

Ve výchozím nastavení používají operace obnovení NuGet balíčky ze složek *globálních balíčků* a *http-cache,* které jsou popsány v části [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

Chcete-li se vyhnout použití složky *globálních balíčků,* proveďte jeden z následujících akcí:

- Zrušte zaškrtnutí složky pomocí `nuget locals global-packages -clear` aplikace nebo `dotnet nuget locals global-packages --clear`.
- Dočasně změňte umístění složky *globálních balíčků* před operací obnovení pomocí jedné z následujících metod:
  - Nastavte proměnnou prostředí NUGET_PACKAGES na jinou složku.
  - Vytvořte `NuGet.Config` soubor, `globalPackagesFolder` který nastaví (pokud používáte PackageReference) nebo `repositoryPath` (pokud používáte) `packages.config`do jiné složky. Další informace naleznete v [tématu nastavení konfigurace](../reference/nuget-config-file.md#config-section).
  - Pouze MSBuild: Zadejte jinou složku s vlastností. `RestorePackagesPath`

Chcete-li se vyhnout použití mezipaměti pro zdroje HTTP, proveďte jeden z následujících akcí:

- Použijte `-NoCache` možnost `nuget restore`s , `--no-cache` nebo `dotnet restore`možnost s . Tyto možnosti nemají vliv na operace obnovení prostřednictvím Správce balíčků sady Visual Studio nebo konzoly.
- Vymazání mezipaměti pomocí `nuget locals http-cache -clear` nebo `dotnet nuget locals http-cache --clear`.
- Dočasně nastavte proměnnou prostředí NUGET_HTTP_CACHE_PATH na jinou složku.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrace na automatické obnovení balíčků (Visual Studio)

Pro NuGet 2.6 a starší msbuild integrovaný balíček obnovení byla dříve podporována, ale to již není pravda. (Obvykle byla povolena klepnutím pravým tlačítkem myši na řešení v sadě Visual Studio a výběrem **možnosti Povolit obnovení balíčku NuGet).** Pokud váš projekt používá zastaralé obnovení balíčku integrované msbuild, migrujte na automatické obnovení balíčku.

Projekty, které používají obnovení balíčku MSBuild-Integrated, obvykle obsahují složku *Nuget* se třemi soubory: *NuGet.config*, *nuget.exe*a *NuGet.targets*. Přítomnost souboru *NuGet.targets* určuje, zda NuGet bude nadále používat přístup MSBuild-untegrated, takže tento soubor musí být odebránběhem migrace.

Migrace na automatické obnovení balíčků:

1. Zavřete Visual Studio.
2. Odstranit *.nuget/nuget.exe* a *.nuget/NuGet.targets*.
3. Pro každý soubor projektu `<RestorePackages>` odeberte prvek a odeberte všechny odkazy na *NuGet.targets*.

Chcete-li otestovat automatické obnovení balíčku:

1. Odeberte složku *balíčků* z řešení.
2. Otevřete řešení v sadě Visual Studio a spusťte sestavení.

   Automatické obnovení balíčku by měl stáhnout a nainstalovat každý balíček závislostí, bez jejich přidání do správy zdrojového kódu.

## <a name="troubleshooting"></a>Řešení potíží

Viz [Poradce při potížích s obnovením balíčku](package-restore-troubleshooting.md).
