---
title: Obnovení balíčků NuGet
description: Přehled, jak balíčky NuGet obnovení projektu závisí na, včetně postup zakázání obnovení a omezení verze.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467800"
---
# <a name="package-restore"></a>Obnovení balíčku

Zvýšit úroveň čištění vývojového prostředí a snížit velikost úložiště, NuGet **obnovení balíčků** instaluje všechny závislosti projektu, které jsou uvedené v souboru projektu nebo `packages.config`. .NET Core 2.0 + `dotnet build` a `dotnet run` příkazy provést obnovení automatické balíčku. Visual Studio můžete balíčky obnovit automaticky při sestavení projektu, a kdykoli prostřednictvím sady Visual Studio, můžete obnovit balíčky `nuget restore`, `dotnet restore`a xbuild v Mono.

Obnovení balíčků zajišťuje, že všechny projektu závislosti jsou k dispozici, bez nutnosti mít uložené ve správě zdrojového kódu. Nakonfigurování svým úložištěm řízení zdrojů pro vyloučení binární soubory balíčku najdete v tématu [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Přehled obnovení balíčků

Obnovení balíčku nejdřív nainstaluje přímé závislosti projektu podle potřeby a potom nainstaluje všechny závislosti tyto balíčky v průběhu graf závislostí pro celé.

Pokud balíček není nainstalovaná, NuGet se nejprve pokusí načíst z [mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). Pokud balíček není v mezipaměti, NuGet se pokusí stáhnout balíček ze všech zdrojů povoleno v seznamu v **nástroje** > **možnosti** > **Správce balíčků NuGet**   >  **Balíček zdroje** v sadě Visual Studio. Během obnovení NuGet ignoruje pořadí zdroje balíčků a používá balíček z libovolným zdrojem je nejprve reagovat na požadavky. Další informace o tom, jak se chová NuGet naleznete v tématu [konfigurace běžných NuGet](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet neukazuje, nepovedlo se obnovit balíček, dokud byly vráceny všechny zdroje. V tu chvíli NuGet hlásí selhání pouze poslední zdroje v seznamu. Chyba znamená, že nebyl k dispozici v balíčku *jakékoli* z jiných zdrojů i v případě chyby se nezobrazují pro každou z těchto zdrojů jednotlivě.

Obnovení balíčků můžete spustit v některém z následujících způsobů:

- **rozhraní příkazového řádku DotNet**: Použití [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) příkazu Obnovit balíčky uvedené v souboru projektu s [PackageReference](../consume-packages/package-references-in-project-files.md). S .NET Core 2.0 nebo novější, obnovení se automaticky stane s `dotnet build` a `dotnet run` příkazy.  

- **Správce balíčků**: V sadě Visual Studio na Windows, obnovení balíčků dojde automaticky při vytvoření projektu ze šablony nebo sestavení projektu, v souladu s možností [povolení a zákaz obnovení balíčku](#enable-and-disable-package-restore). Ve Správci NuGet 4.0 + obnovit také dojde automaticky když provedete změny projektu založeného na .NET Core SDK.

    K obnovení balíčků ručně, klikněte pravým tlačítkem na řešení v **Průzkumníka řešení** a vyberte **obnovit balíčky NuGet**. Pokud jeden nebo více jednotlivých balíčků ještě nejsou nainstalovány správně, **Průzkumníka řešení** se zobrazuje ikona chyba. Klikněte pravým tlačítkem a vyberte **spravovat balíčky NuGet**a použijte **Správce balíčků** odinstalovat a znovu nainstalovat ovlivněné balíčky. Další informace najdete v tématu [znovu nainstalovat a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)

    Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které jsou na tomto počítači chybí" nebo "jeden nebo více balíčků NuGet je nutné obnovit, ale nepodařilo, protože nebyl udělen souhlas," [povolit automatické obnovení](#enable-and-disable-package-restore). Viz také [obnovení balíčků řešení potíží s](Package-restore-troubleshooting.md).

- **nuget.exe CLI**: Použití [obnovení nuget](../tools/cli-ref-restore.md) příkazu Obnovit balíčky uvedené v souboru projektu nebo řešení, nebo v `packages.config`. 

- **MSBuild**: Použití [msbuild - t: restore](../reference/msbuild-targets.md#restore-target) příkazu Obnovit balíčky uvedené v souboru projektu pomocí PackageReference. Tento příkaz je k dispozici pouze v NuGet 4.x+ a MSBuild 15.1 +, které jsou součástí sady Visual Studio 2017 a vyšší verze. Obě `nuget restore` a `dotnet restore` použijte tento příkaz pro příslušné projekty.

- **Kanály Azure**: Při vytváření definice sestavení v kanálech Azure zahrnují NuGet [obnovení](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) nebo .NET Core [obnovení](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages) úloh v definici předtím, než se některé úlohy sestavení. Některé šablony sestavení zahrnout úlohy obnovení ve výchozím nastavení.

- **Azure DevOps Server**: Azure DevOps Server a sadu TFS 2013 a novější automaticky obnovení balíčků během sestavení, pokud používáte TFS 2013 nebo vyšší šablony Team Build. U starších verzí sady TFS můžete zahrnout krok sestavení spustit možnost příkazového řádku obnovení nebo volitelně šablony sestavení migrovat na novější verzi. Další informace najdete v tématu [nastavit obnovení balíčku s Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore"></a>Povolení a zákaz obnovení balíčku

V sadě Visual Studio, můžete řídit obnovení balíčků primárně prostřednictvím **nástroje** > **možnosti** > **Správce balíčků NuGet**:

![Ovládací prvek obnovení balíčků prostřednictvím možnosti Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Umožnit správci balíčků NuGet stáhnout chybějící balíčky** řídí všechny formy obnovení balíčku tak, že změníte `packageRestore/enabled` nastavení [packageRestore části](../reference/nuget-config-file.md#packagerestore-section) z `NuGet.Config` souboru, v `%AppData%\NuGet\` na Windows, nebo `~/.nuget/NuGet/` na Mac/Linux. Toto nastavení také povolí **obnovit balíčky NuGet** příkazu v místní nabídce řešení v sadě Visual Studio.

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
  > Globálně přepsat `packageRestore/enabled` nastavení, nastavte proměnnou prostředí **EnableNuGetPackageRestore** s hodnotou PRAVDA nebo NEPRAVDA před spuštěním aplikace Visual Studio nebo spuštění sestavení.

- **Automaticky zjišťovat pro chybějící balíčky během vytváření v sadě Visual Studio** řídí automatické obnovení tak, že změníte `packageRestore/automatic` nastavení [packageRestore části](../reference/nuget-config-file.md#packagerestore-section) z `NuGet.Config` souboru. Pokud tato možnost nastavená na hodnotu True, systémem sestavení ze sady Visual Studio automaticky obnoví všechny chybějící balíčky. Toto nastavení nemá vliv na sestavení spusťte z příkazového řádku MSBuild.

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

K povolení nebo zakázání obnovení balíčků pro všechny uživatele v počítači, vývojář nebo společnosti můžete přidat nastavení konfigurace na globální `nuget.config` souboru. Globální `nuget.config` je ve Windows na `%ProgramData%\NuGet\Config`, někdy v konkrétní `\{IDE}\{Version}\{SKU}\` složku Visual Studio, nebo v systému Mac/Linux na `~/.local/share`. Jednotlivým uživatelům můžete selektivně povolte obnovení podle potřeby na úrovni projektu. Podrobné informace o tom, jak NuGet upřednostňuje více konfiguračních souborů naleznete v tématu [konfigurace běžných NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Pokud upravíte `packageRestore` přímo v nastavení `nuget.config`, restartujte Visual Studio, tak, aby **možnosti** dialogové okno zobrazuje aktuální hodnoty.

## <a name="constrain-package-versions-with-restore"></a>Omezení verze balíčků pomocí obnovení

Když NuGet obnoví balíčky pomocí libovolné metody, respektuje žádná omezení, které jste zadali v `packages.config` nebo soubor projektu:

- V `packages.config`, můžete zadat rozsah verzí v `allowedVersion` vlastnost závislosti. Zobrazit [verze k upgradu omezit](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) Další informace. Příklad:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- V souboru projektu můžete použít PackageReference přímo určovat rozsah závislostí. Příklad:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Ve všech případech použijte notaci podle [Správa verzí balíčků](../reference/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Vynutit obnovení ze zdroje balíčku

Ve výchozím nastavení, operace obnovení NuGet používat balíčky z *global-packages* a *http-cache* složek, které jsou popsány v [Správa globálních balíčků a ukládat do mezipaměti složky](managing-the-global-packages-and-cache-folders.md).

Abyste se vyhnuli použití *global-packages* složky, proveďte jednu z následujících akcí:

- Zrušte pomocí složky `nuget locals global-packages -clear` nebo `dotnet nuget locals global-packages --clear`.
- Dočasně změnit umístění *global-packages* složky, před provedením operace obnovení, pomocí jedné z následujících metod:
  - Nastavte proměnnou prostředí NUGET_PACKAGES do jiné složky.
  - Vytvoření `NuGet.Config` souboru, který nastaví `globalPackagesFolder` (Pokud se používá PackageReference) nebo `repositoryPath` (Pokud používáte `packages.config`) do jiné složky. Další informace najdete v tématu [nastavení konfigurace](../reference/nuget-config-file.md#config-section).
  - Pouze MSBuild: Zadejte jinou složku s `RestorePackagesPath` vlastnost.

Abyste se vyhnuli použití mezipaměti u zdrojů HTTP, proveďte jednu z následujících akcí:

- Použití `-NoCache` spolu s možností `nuget restore`, nebo `--no-cache` spolu s možností `dotnet restore`. Tyto možnosti nechcete vliv na operace obnovení prostřednictvím správce sady Visual Studio balíček nebo konzoly.
- Vymazání mezipaměti pomocí `nuget locals http-cache -clear` nebo `dotnet nuget locals http-cache --clear`.
- Dočasně nastavte proměnnou prostředí NUGET_HTTP_CACHE_PATH do jiné složky.

## <a name="troubleshooting"></a>Poradce při potížích

Zobrazit [Poradce při potížích s obnovení balíčku](package-restore-troubleshooting.md).
