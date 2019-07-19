---
title: Obnovení balíčku NuGet
description: Přehled o tom, jak NuGet obnovuje balíčky, na kterých je projekt závislý, včetně toho, jak zakázat obnovení a omezit verze
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 0df2b0ebcf438fba99291558f1cf929dcb32618b
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316991"
---
# <a name="package-restore-options"></a>Možnosti obnovení balíčků

Pro zvýšení úrovně čisticího vývojového prostředí a snížení velikosti úložiště nainstaluje **obnovení balíčku** NuGet všechny závislosti projektu uvedené v souboru projektu nebo `packages.config`. Rozhraní .NET Core 2.0 + `dotnet build` a `dotnet run` provede automatické obnovení balíčku. Visual Studio může automaticky obnovovat balíčky při sestavení projektu a balíčky můžete kdykoli obnovit pomocí sady Visual Studio, `nuget restore`, `dotnet restore`a xbuild na mono.

Obnovení balíčku zajistí, že jsou k dispozici všechny závislosti projektu, aniž by bylo nutné je ukládat do správy zdrojového kódu. Chcete-li konfigurovat úložiště správy zdrojového kódu pro vyloučení binárních souborů balíčku, přečtěte si téma [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Přehled obnovení balíčků

Obnovení balíčků nejprve nainstaluje přímé závislosti projektu podle potřeby a pak nainstaluje všechny závislosti těchto balíčků do celého grafu závislostí.

Pokud balíček ještě není nainstalovaný, NuGet se nejdřív pokusí ho načíst z [mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). Pokud balíček v mezipaměti není, nástroj NuGet se pokusí stáhnout balíček ze všech povolených zdrojů v seznamu ve**volbách** >  **nástroje** >  > **Správce balíčků NuGet** **zdroje balíčku** ve vizuálu. Studio. V průběhu obnovení NuGet ignoruje pořadí zdrojů balíčků a při použití balíčku z libovolného zdroje je nejdříve odpovídat na požadavky. Další informace o tom, jak se NuGet chová, najdete v tématu [běžné konfigurace NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet neindikuje selhání při obnovování balíčku, dokud nebudou všechny zdroje zkontrolovány. V tuto chvíli hlásí NuGet selhání jenom pro poslední zdroj v seznamu. Tato chyba znamená, že balíček nebyl přítomen na *žádném* z ostatních zdrojů, a to i v případě, že chyby nejsou pro každý z těchto zdrojů zobrazovány jednotlivě.

## <a name="restore-packages"></a>Obnovit balíčky

Obnovení balíčku můžete aktivovat některým z následujících způsobů:

- **Visual Studio**: V aplikaci Visual Studio ve Windows použijte jednu z následujících metod.

    - Obnovte balíčky automaticky. K obnovení balíčku dojde automaticky při vytvoření projektu ze šablony nebo sestavení projektu v závislosti na možnostech v části [Povolit a zakázat obnovení balíčku](#enable-and-disable-package-restore-visual-studio). V NuGet 4.0 + dojde k obnovení také automaticky při provádění změn v projektu ve stylu sady SDK (obvykle se jedná o .NET Core nebo .NET Standard projekt).

    - Obnovte balíčky ručně. Ruční obnovení získáte tak, že kliknete pravým tlačítkem na řešení v **Průzkumník řešení** a vyberete **obnovit balíčky NuGet**. Pokud některé balíčky stále nejsou nainstalované správně, **Průzkumník řešení** zobrazí ikonu chyby. Klikněte pravým tlačítkem a vyberte **Spravovat balíčky NuGet**a pomocí **Správce balíčků** odinstalujte a znovu nainstalujte ovlivněné balíčky. Další informace najdete v tématu [Přeinstalace a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md) .

    Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí", "nebo" jeden nebo více balíčků NuGet je nutné obnovit, ale nedala se k udělení souhlasu " [Povolit automatické obnovení](#enable-and-disable-package-restore-visual-studio)". Přečtěte si také téma [migrace na automatické obnovení balíčků](#migrate-to-automatic-package-restore-visual-studio) a [řešení potíží s obnovením balíčků](Package-restore-troubleshooting.md).

- **DOTNET CLI**: V příkazovém řádku přejděte do složky, která obsahuje váš projekt, a pak pomocí příkazu [dotnet Restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) obnovte balíčky uvedené v souboru projektu pomocí [PackageReference](../consume-packages/package-references-in-project-files.md). Pomocí .NET Core 2,0 a novějšího se k obnovení dochází automaticky `dotnet build` pomocí `dotnet run` příkazů a.  

- rozhraní příkazového **řádku NuGet. exe**: V příkazovém řádku přejděte do složky, která obsahuje váš projekt, a pak pomocí příkazu [NuGet Restore](../reference/cli-reference/cli-ref-restore.md) obnovte balíčky uvedené v souboru projektu nebo řešení nebo v `packages.config`. 

- **MSBuild**: Pomocí příkazu [MSBuild-t:Restore](../reference/msbuild-targets.md#restore-target) obnovte balíčky uvedené v souboru projektu pomocí PackageReference. Tento příkaz je k dispozici pouze v NuGet 4. x + a MSBuild 15.1 +, které jsou součástí sady Visual Studio 2017 a novějších verzí. `nuget restore` A`dotnet restore` použijte tento příkaz pro příslušné projekty.

- **Azure Pipelines**: Při vytváření definice sestavení v Azure Pipelines zahrňte do definice úlohu [obnovení](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) NuGet nebo [obnovení](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) .NET Core před všemi úlohami sestavení. Některé šablony sestavení obsahují ve výchozím nastavení úlohu obnovit.

- **Azure DevOps Server**: Azure DevOps Server a TFS 2013 a novější automaticky Obnovují balíčky během sestavování, pokud používáte šablonu týmu sestavení sady TFS 2013 nebo novější. Pro starší verze TFS můžete zahrnout krok sestavení pro spuštění možnosti obnovení z příkazového řádku nebo volitelně migrovat šablonu sestavení na novější verzi. Další informace najdete v tématu [nastavení obnovení balíčku pomocí Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore-visual-studio"></a>Povolit a zakázat obnovení balíčku (Visual Studio)

V aplikaci Visual Studio můžete řídit obnovení balíčků hlavně prostřednictvím **nástrojů** > **Možnosti** > **Správce balíčků NuGet**:

![Řízení obnovení balíčku pomocí možností Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Umožněte, aby NuGet stáhl chybějící balíčky** řídí všechny formy obnovení balíčku, a to `packageRestore/enabled` tak, že změníte nastavení v `NuGet.Config` [části packageRestore](../reference/nuget-config-file.md#packagerestore-section) souboru, `%AppData%\NuGet\` ve Windows nebo `~/.nuget/NuGet/` na Mac/Linux. Toto nastavení také povoluje příkaz **obnovit balíčky NuGet** v kontextové nabídce řešení v aplikaci Visual Studio,.

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
  > Chcete-li globálně `packageRestore/enabled` přepsat nastavení, nastavte proměnnou prostředí **EnableNuGetPackageRestore** s hodnotou true nebo false před spuštěním sady Visual Studio nebo spuštěním sestavení.

- **Automaticky kontrolovat chybějící balíčky během sestavování v aplikaci Visual Studio** řídí automatické obnovení změnou `packageRestore/automatic` nastavení v `NuGet.Config` [části packageRestore](../reference/nuget-config-file.md#packagerestore-section) souboru. Pokud je tato možnost nastavena na hodnotu true, spuštění sestavení ze sady Visual Studio automaticky obnoví všechny chybějící balíčky. Toto nastavení nemá vliv na sestavení spouštěná z příkazového řádku MSBuild.

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

Pokud chcete povolit nebo zakázat obnovení balíčků pro všechny uživatele v počítači, může vývojář nebo společnost přidat konfigurační nastavení do globálního `nuget.config` souboru. Globální `nuget.config` je ve `%ProgramData%\NuGet\Config`Windows v, někdy v určité `\{IDE}\{Version}\{SKU}\` složce sady Visual Studio, nebo v systému Mac/Linux na `~/.local/share`adrese. Jednotliví uživatelé pak můžou selektivně povolit obnovení podle potřeby na úrovni projektu. Další podrobnosti o tom, jak NuGet upřednostňuje více konfiguračních souborů, najdete v tématu [běžné konfigurace NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Pokud upravíte `packageRestore` nastavení přímo v `nuget.config`, restartujte Visual Studio, aby se v dialogovém okně **Možnosti** zobrazily aktuální hodnoty.

## <a name="constrain-package-versions-with-restore"></a>Omezení verzí balíčku s obnovením

Když NuGet obnoví balíčky jakýmkoli způsobem, splní všechna omezení, která jste zadali v `packages.config` souboru, nebo soubor projektu:

- V `packages.config`nástroji můžete zadat rozsah verze `allowedVersion` ve vlastnosti závislosti. Další informace najdete v tématu [omezení verzí upgradu](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) . Příklad:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- V souboru projektu můžete použít PackageReference k určení rozsahu závislosti přímo. Příklad:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Ve všech případech použijte zápis popsaný v tématu [Správa verzí balíčku](../reference/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Vynutit obnovení ze zdrojů balíčku

Ve výchozím nastavení operace obnovení NuGet používají balíčky ze složek *Global-Package* a *HTTP-cache* , které jsou popsány v tématu [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

Chcete-li se vyhnout použití složky *Global-Packages* , proveďte jednu z následujících akcí:

- Vymažte složku pomocí `nuget locals global-packages -clear` nebo `dotnet nuget locals global-packages --clear`.
- Dočasnou změnu umístění složky *Global-Packages* před operací obnovení, a to pomocí jedné z následujících metod:
  - Nastavte proměnnou prostředí NUGET_PACKAGES na jinou složku.
  - Vytvořte soubor, který nastaví `globalPackagesFolder` (Pokud používáte PackageReference) nebo `repositoryPath` (Pokud se `packages.config`používá) do jiné složky. `NuGet.Config` Další informace najdete v tématu [nastavení konfigurace](../reference/nuget-config-file.md#config-section).
  - Pouze nástroj MSBuild: Zadejte jinou složku s `RestorePackagesPath` vlastností.

Chcete-li se vyhnout použití mezipaměti pro zdroje HTTP, proveďte jednu z následujících akcí:

- Použijte možnost s `nuget restore`nebo `--no-cache` s`dotnet restore`možností. `-NoCache` Tyto možnosti neovlivňují operace obnovení prostřednictvím Správce balíčků nebo konzole sady Visual Studio.
- Vymažte mezipaměť pomocí `nuget locals http-cache -clear` nebo `dotnet nuget locals http-cache --clear`.
- Dočasně nastavte proměnnou prostředí NUGET_HTTP_CACHE_PATH na jinou složku.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Migrace na automatické obnovení balíčku (Visual Studio)

Pro NuGet 2,6 a starší se dřív podporovalo obnovení balíčku integrovaného v MSBuild, ale už není pravdivé. (Obvykle se povolilo tak, že kliknete pravým tlačítkem na řešení v aplikaci Visual Studio a vyberete **Povolit obnovení balíčku NuGet**). Pokud váš projekt používá nepoužívané obnovení balíčku integrované v nástroji MSBuild, proveďte migraci na automatické obnovení balíčku.

Projekty, které používají nástroj MSBuild – integrované obnovení balíčku obvykle obsahují složku *. NuGet* se třemi soubory: *NuGet. config*, *NuGet. exe*a *NuGet. targets*. Přítomnost souboru *NuGet. targets* určuje, jestli bude NuGet dál používat přístup pomocí nástroje MSBuild-untegrated, takže tento soubor musí být během migrace odebraný.

Migrace na automatické obnovení balíčků:

1. Zavřete Visual Studio.
2. Odstraňte *. NuGet/NuGet. exe* a *. NuGet/NuGet. targets*.
3. Pro každý soubor projektu odeberte `<RestorePackages>` prvek a odeberte všechny odkazy na *NuGet. targets*.

Test automatického obnovení balíčků:

1. Odeberte složku *Packages* z řešení.
2. Otevřete řešení v aplikaci Visual Studio a spusťte sestavení.

   Automatické obnovení balíčků by mělo stáhnout a nainstalovat všechny balíčky závislostí, aniž byste je museli přidávat do správy zdrojového kódu.

## <a name="troubleshooting"></a>Poradce při potížích

Podívejte se na téma [řešení potíží s obnovením balíčku](package-restore-troubleshooting.md).
