---
title: Obnovení balíčku NuGet
description: Přehled o tom, jak NuGet obnovuje balíčky, na kterých je projekt závislý, včetně toho, jak zakázat obnovení a omezit verze
author: JonDouglas
ms.author: jodou
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 6cdc826c85f233c7108a53ad244aa8c47df0be67
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901834"
---
# <a name="restore-packages-using-package-restore"></a>Obnovení balíčků pomocí obnovení balíčku

Pro zvýšení úrovně čisticího vývojového prostředí a snížení velikosti úložiště nainstaluje **obnovení balíčku** NuGet všechny závislosti projektu uvedené v souboru projektu nebo `packages.config` . Rozhraní .NET Core 2.0 + `dotnet build` a `dotnet run` provede automatické obnovení balíčku. Visual Studio může automaticky obnovovat balíčky při sestavení projektu a balíčky můžete kdykoli obnovit pomocí sady Visual Studio, `nuget restore` , `dotnet restore` a xbuild na mono.

Obnovení balíčku zajistí, že jsou k dispozici všechny závislosti projektu, aniž by bylo nutné je ukládat do správy zdrojového kódu. Chcete-li konfigurovat úložiště správy zdrojového kódu pro vyloučení binárních souborů balíčku, přečtěte si téma [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Přehled obnovení balíčků

Obnovení balíčků nejprve nainstaluje přímé závislosti projektu podle potřeby a pak nainstaluje všechny závislosti těchto balíčků do celého grafu závislostí.

Pokud balíček ještě není nainstalovaný, NuGet se nejdřív pokusí ho načíst z [mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). Pokud balíček není v mezipaměti, NuGet se pokusí stáhnout balíček ze všech povolených zdrojů v seznamu v části možnosti **nástrojů**  >    >  **Správce balíčků NuGet**  >  **zdroje balíčků** v aplikaci Visual Studio. V průběhu obnovení NuGet ignoruje pořadí zdrojů balíčků a při použití balíčku z libovolného zdroje je nejdříve odpovídat na požadavky. Další informace o tom, jak se NuGet chová, najdete v tématu [běžné konfigurace NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet neindikuje selhání při obnovování balíčku, dokud nebudou všechny zdroje zkontrolovány. V tuto chvíli hlásí NuGet selhání jenom pro poslední zdroj v seznamu. Tato chyba znamená, že balíček nebyl přítomen na *žádném* z ostatních zdrojů, a to i v případě, že chyby nejsou pro každý z těchto zdrojů zobrazovány jednotlivě.

## <a name="restore-packages"></a>Obnovení balíčků

Obnovení balíčku se pokusí nainstalovat všechny závislosti balíčků do správného stavu odpovídajícího odkazům na balíček v souboru projektu (*. csproj*) nebo souboru *packages.config* . (V aplikaci Visual Studio se odkazy zobrazí v Průzkumník řešení pod uzlem **závislosti \ NuGet** nebo **odkazy** .)

1. Pokud jsou odkazy na balíček v souboru projektu správné, použijte k obnovení balíčků preferovaný nástroj.

   - [Visual Studio](#restore-using-visual-studio) ([Automatické obnovení](#restore-packages-automatically-using-visual-studio) nebo [Ruční obnovení](#restore-packages-manually-using-visual-studio))
   - [dotnet CLI](#restore-using-the-dotnet-cli)
   - [nuget.exe CLI](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Pokud balíček odkazuje v souboru projektu (*. csproj*) nebo je soubor *packages.config* nesprávný (neshoduje se s požadovaným stavem po obnovení balíčku), musíte místo toho nainstalovat nebo aktualizovat balíčky.

   Pro projekty používající PackageReference po úspěšném obnovení by měl být balíček přítomen ve složce *Global-Packages* a `obj/project.assets.json` soubor je znovu vytvořen. Pro projekty `packages.config` , které používají, by se měl balíček zobrazit ve `packages` složce projektu. Projekt by se teď měl úspěšně sestavit. 

2. Pokud se po spuštění obnovení balíčku stále setkáte s chybějícími balíčky nebo chybami souvisejícími s balíčkem (jako jsou chybové ikony v Průzkumník řešení v aplikaci Visual Studio), možná budete muset postupovat podle pokynů uvedených v tématu [řešení potíží s chybami při obnovení balíčku](package-restore-troubleshooting.md) nebo případně [přeinstalování a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md).

   V aplikaci Visual Studio konzola správce balíčků nabízí několik flexibilních možností pro přeinstalaci balíčků. Viz [použití balíčku – aktualizace](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Obnovení pomocí sady Visual Studio

V aplikaci Visual Studio ve Windows proveďte jednu z těchto akcí:

- Obnovte balíčky automaticky nebo

- Ruční obnovení balíčků

### <a name="restore-packages-automatically-using-visual-studio"></a>Automaticky obnovovat balíčky pomocí sady Visual Studio

K obnovení balíčku dojde automaticky při vytvoření projektu ze šablony nebo sestavení projektu v závislosti na možnostech v části [Povolit a zakázat obnovení balíčku](#enable-and-disable-package-restore-in-visual-studio). V NuGet 4.0 + dojde k obnovení také automaticky při provádění změn v projektu ve stylu sady SDK (obvykle se jedná o .NET Core nebo .NET Standard projekt).

1. Povolte automatické obnovení balíčku tak, že vyberete možnosti **nástrojů**  >    >  **Správce balíčků NuGet** a potom v části **obnovení balíčku** vyberete možnost **automaticky kontrolovat chybějící balíčky během sestavování v aplikaci Visual Studio** .

   Pro projekty, které nejsou ve stylu sady SDK, musíte nejprve vybrat **Povolit NuGet ke stažení chybějících balíčků** , aby bylo možné povolit možnost automatického obnovení.

1. Sestavte projekt.

   Pokud některé balíčky stále nejsou nainstalované správně, **Průzkumník řešení** zobrazí ikonu chyby. Klikněte pravým tlačítkem a vyberte **Spravovat balíčky NuGet** a pomocí **Správce balíčků** odinstalujte a znovu nainstalujte ovlivněné balíčky. Další informace najdete v tématu [Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md) .

   Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí", "nebo" jeden nebo více balíčků NuGet je nutné obnovit, ale nedala se k udělení souhlasu " [Povolit automatické obnovení](#enable-and-disable-package-restore-in-visual-studio)". Pro starší projekty také viz [migrace na automatické obnovení balíčků](#migrate-to-automatic-package-restore-visual-studio). Viz také [řešení potíží s obnovením balíčku](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Ruční obnovení balíčků pomocí sady Visual Studio

1. Obnovení balíčku povolíte tak, že vyberete možnosti **nástrojů**  >    >  **Správce balíčků NuGet**. V části možnosti **obnovení balíčku** vyberte možnost **povoluje, aby NuGet stahoval chybějící balíčky**.

1. V **Průzkumník řešení** klikněte pravým tlačítkem na řešení a vyberte **obnovit balíčky NuGet**.

   Pokud některé balíčky stále nejsou nainstalované správně, **Průzkumník řešení** zobrazí ikonu chyby. Klikněte pravým tlačítkem a vyberte **Spravovat balíčky NuGet** a pak pomocí **Správce balíčků** odinstalujte a znovu nainstalujte ovlivněné balíčky. Další informace najdete v tématu [Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md) .

   Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí", "nebo" jeden nebo více balíčků NuGet je nutné obnovit, ale nedala se k udělení souhlasu " [Povolit automatické obnovení](#enable-and-disable-package-restore-in-visual-studio)". Pro starší projekty také viz [migrace na automatické obnovení balíčků](#migrate-to-automatic-package-restore-visual-studio). Viz také [řešení potíží s obnovením balíčku](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Povolení a zakázání obnovení balíčku v aplikaci Visual Studio

V aplikaci Visual Studio můžete řídit obnovení balíčků hlavně prostřednictvím **nástrojů**  >  **Možnosti**  >  **Správce balíčků NuGet**:

![Řízení obnovení balíčku pomocí možností Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Umožněte, aby NuGet stáhl chybějící balíčky** řídí všechny formy obnovení balíčku, a to tak, že změníte `packageRestore/enabled` nastavení v [části PackageRestore](../reference/nuget-config-file.md#packagerestore-section) `NuGet.Config` souboru, ve `%AppData%\NuGet\` Windows nebo `~/.nuget/NuGet/` na Mac/Linux. Toto nastavení také povoluje příkaz **obnovit balíčky NuGet** v kontextové nabídce řešení v aplikaci Visual Studio,.

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
  > Chcete-li globálně přepsat `packageRestore/enabled` nastavení, nastavte proměnnou prostředí **EnableNuGetPackageRestore** s hodnotou true nebo false před spuštěním sady Visual Studio nebo spuštěním sestavení.

- **Automaticky kontrolovat chybějící balíčky během sestavování v aplikaci Visual Studio** řídí automatické obnovení změnou `packageRestore/automatic` nastavení v [části packageRestore](../reference/nuget-config-file.md#packagerestore-section) `NuGet.Config` souboru. Pokud je tato možnost nastavena na hodnotu true, spuštění sestavení ze sady Visual Studio automaticky obnoví všechny chybějící balíčky. Toto nastavení nemá vliv na sestavení spouštěná z příkazového řádku MSBuild.

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

Pokud chcete povolit nebo zakázat obnovení balíčků pro všechny uživatele v počítači, může vývojář nebo společnost přidat konfigurační nastavení do globálního `nuget.config` souboru. Globální `nuget.config` je ve Windows v `%ProgramData%\NuGet\Config` , někdy v určité složce sady `\{IDE}\{Version}\{SKU}\` Visual Studio, nebo v systému Mac/Linux na adrese `~/.local/share` . Jednotliví uživatelé pak můžou selektivně povolit obnovení podle potřeby na úrovni projektu. Další podrobnosti o tom, jak NuGet upřednostňuje více konfiguračních souborů, najdete v tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Pokud upravíte `packageRestore` nastavení přímo v `nuget.config` , restartujte Visual Studio, aby se v dialogovém okně **Možnosti** zobrazily aktuální hodnoty.

### <a name="choose-default-package-management-format"></a>Zvolit výchozí formát správy balíčků

![Řízení výchozího formátu správy balíčků i přes možnosti Správce balíčků NuGet](media/Restore-02-PackageFormatOptions.png)

NuGet má dva formáty, ve kterých může projekt používat balíčky: [`PackageReference`](package-references-in-project-files.md) a [`packages.config`](../reference/packages-config.md) . Výchozí formát lze vybrat v rozevíracím seznamu pod nadpisem **Správa balíčků** . Možnost, která se zobrazí po instalaci prvního balíčku v projektu, je k dispozici také.

> [!Note]
> Pokud projekt nepodporuje jak formáty správy balíčků, použije se formát správy balíčků ten, který je kompatibilní s projektem, a proto nemusí být výchozí sadou v možnostech. Kromě toho se NuGet nevyzve k výběru při první instalaci balíčku, a to ani v případě, že je v okně Možnosti vybraná možnost.
>
> Pokud se k instalaci prvního balíčku v projektu používá konzola správce balíčků, NuGet se nezobrazí pro výběr formátu, ani když je v okně Možnosti vybraná možnost.

## <a name="restore-using-the-dotnet-cli"></a>Obnovení pomocí rozhraní příkazového řádku dotnet

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Chcete-li přidat chybějící odkaz na balíček do souboru projektu, použijte příkaz [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), který také spustí `restore` příkaz.

## <a name="restore-using-the-nugetexe-cli"></a>Obnovení pomocí rozhraní příkazového řádku nuget.exe

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> `restore`Příkaz neupraví soubor projektu ani *packages.config*. Chcete-li přidat závislost, přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte *packages.config* a pak spusťte buď `install` nebo `restore` .

## <a name="restore-using-msbuild"></a>Obnovení pomocí MSBuild

Pomocí příkazu [MSBuild-t:Restore](../reference/msbuild-targets.md#restore-target) obnovte balíčky uvedené v souboru projektu (viz [PackageReference](package-references-in-project-files.md)) a začněte s MSBuild 16.5 +, `packages.config` projekty.

 Tento příkaz je k dispozici pouze v NuGet 4. x + a MSBuild 15.1 +, které jsou součástí sady Visual Studio 2017 a novějších verzí.
Počínaje nástrojem MSBuild 16.5 + může tento příkaz také obnovit `packages.config` projekty založené na spuštění s nástrojem `-p:RestorePackagesConfig=true` .

1. Otevřete příkazový řádek pro vývojáře (do **vyhledávacího** pole zadejte **příkaz Developer Command Prompt**).

   Obvykle chcete spustit Developer Command Prompt pro Visual Studio z nabídky **Start** , jak bude nakonfigurován se všemi nezbytnými cestami pro MSBuild.

2. Přepněte do složky obsahující soubor projektu a zadejte následující příkaz.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Zadáním následujícího příkazu znovu sestavte projekt.

   ```cmd
   msbuild
   ```

   Ujistěte se, že výstup nástroje MSBuild označuje, že sestavení bylo úspěšně dokončeno.
   
> [!Note]
> MSBuild má `-restore` přepínač, který se spustí `Restore` , znovu načtěte projekt a pak sestavte. Viz [obnovení a sestavování pomocí jednoho příkazu MSBuild](../reference/msbuild-targets.md#restoring-and-building-with-one-msbuild-command).

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>Obnovit pomocí Azure Pipelines

Při vytváření definice sestavení v Azure Pipelines zahrňte do definice úlohu [obnovení](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) NuGet nebo [obnovení](/azure/devops/pipelines/tasks/build/dotnet-core-cli) .NET Core před všemi úlohami sestavení. Některé šablony sestavení obsahují ve výchozím nastavení úlohu obnovit.

## <a name="restore-using-azure-devops-server"></a>Obnovit pomocí Azure DevOps Server

Azure DevOps Server a TFS 2013 a novější automaticky Obnovují balíčky během sestavování, pokud používáte šablonu týmu sestavení sady TFS 2013 nebo novější. Pro starší verze TFS můžete zahrnout krok sestavení pro spuštění možnosti obnovení z příkazového řádku nebo volitelně migrovat šablonu sestavení na novější verzi. Další informace najdete v tématu [nastavení obnovení balíčku pomocí Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Omezení verzí balíčku s obnovením

Když NuGet obnoví balíčky jakýmkoli způsobem, splní všechna omezení, která jste zadali v `packages.config` souboru, nebo soubor projektu:

- V nástroji `packages.config` můžete zadat rozsah verze ve `allowedVersion` vlastnosti závislosti. Další informace najdete v tématu [omezení verzí upgradu](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) . Například:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- V souboru projektu můžete použít PackageReference k určení rozsahu závislosti přímo. Například:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Ve všech případech použijte zápis popsaný v tématu [Správa verzí balíčku](../concepts/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Vynutit obnovení ze zdrojů balíčku

Ve výchozím nastavení operace obnovení NuGet používají balíčky ze složek *Global-Package* a *HTTP-cache* , které jsou popsány v tématu [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

Chcete-li se vyhnout použití složky *Global-Packages* , proveďte jednu z následujících akcí:

- Vymažte složku pomocí `nuget locals global-packages -clear` nebo `dotnet nuget locals global-packages --clear` .
- Dočasnou změnu umístění složky *Global-Packages* před operací obnovení, a to pomocí jedné z následujících metod:
  - Nastavte proměnnou prostředí NUGET_PACKAGES na jinou složku.
  - Vytvořte `NuGet.Config` soubor, který nastaví `globalPackagesFolder` (Pokud používáte PackageReference) nebo `repositoryPath` (Pokud `packages.config` se používá) do jiné složky. Další informace najdete v tématu [nastavení konfigurace](../reference/nuget-config-file.md#config-section).
  - Pouze nástroj MSBuild: Zadejte jinou složku s `RestorePackagesPath` vlastností.

Chcete-li se vyhnout použití mezipaměti pro zdroje HTTP, proveďte jednu z následujících akcí:

- Použijte `-NoCache` možnost s `nuget restore` nebo `--no-cache` s možností `dotnet restore` . Tyto možnosti neovlivňují operace obnovení prostřednictvím Správce balíčků nebo konzole sady Visual Studio.
- Vymažte mezipaměť pomocí `nuget locals http-cache -clear` nebo `dotnet nuget locals http-cache --clear` .
- Dočasně nastavte proměnnou prostředí NUGET_HTTP_CACHE_PATH na jinou složku.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrace na automatické obnovení balíčku (Visual Studio)

Pro NuGet 2,6 a starší se dřív podporovalo obnovení balíčku integrovaného v MSBuild, ale už není pravdivé. (Obvykle se povolilo tak, že kliknete pravým tlačítkem na řešení v aplikaci Visual Studio a vyberete **Povolit obnovení balíčku NuGet**). Pokud váš projekt používá nepoužívané obnovení balíčku integrované v nástroji MSBuild, proveďte migraci na automatické obnovení balíčku.

Projekty, které používají MSBuild-Integrated obnovení balíčku obvykle obsahují složku *. NuGet* se třemi soubory: *NuGet.config*, *nuget.exe* a *NuGet. targets*. Přítomnost souboru *NuGet. targets* určuje, jestli bude NuGet dál používat přístup integrovaný na MSBuild, takže tento soubor se musí během migrace odebrat.

Migrace na automatické obnovení balíčků:

1. Zavřete Visual Studio.
2. Odstraňte *. NuGet/nuget.exe* a *. NuGet/NuGet. targets*.
3. Pro každý soubor projektu odeberte `<RestorePackages>` prvek a odeberte všechny odkazy na *NuGet. targets*.

Test automatického obnovení balíčků:

1. Odeberte složku *Packages* z řešení.
2. Otevřete řešení v aplikaci Visual Studio a spusťte sestavení.

   Automatické obnovení balíčků by mělo stáhnout a nainstalovat všechny balíčky závislostí, aniž byste je museli přidávat do správy zdrojového kódu.

## <a name="troubleshooting"></a>Řešení potíží

Podívejte se na téma [řešení potíží s obnovením balíčku](Package-restore-troubleshooting.md).
