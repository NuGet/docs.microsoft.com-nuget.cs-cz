---
title: Obnovení balíčků NuGet
description: Přehled o tom, jak NuGet obnoví balíčky, na které projekt závisí, včetně postup zakázání obnovení a omezení verze.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: da69181aebe3bebcea6acd6e15fde6b77dd33452
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580295"
---
# <a name="package-restore"></a>Obnovení balíčku

Zvýšit úroveň čištění vývojového prostředí a snížit velikost úložiště, NuGet **obnovení balíčků** nainstaluje všechny projektu závislosti, jak je uvedeno v jednom souboru projektu nebo `packages.config`. Visual Studio můžete obnovit balíčky automaticky při vytváření projektu. `dotnet build` a `dotnet run` příkazy (.NET Core 2.0 +) také provést automatické obnovování. Můžete také obnovit balíčky v každém okamžiku prostřednictvím sady Visual Studio `nuget restore`, `dotnet restore`a xbuild v Mono.

Obnovení balíčků zajišťuje, že všechny projektu závislosti jsou k dispozici bez ukládání těchto balíčků ve správě zdrojového kódu. Zobrazit [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) o tom, jak nakonfigurovat úložiště k vyloučení binární soubory balíčku.

## <a name="package-restore-overview"></a>Přehled obnovení balíčků

Obnovují se balíčky nejdřív nainstaluje přímé závislosti projektu podle potřeby a potom nainstaluje všechny závislosti tyto balíčky v průběhu graf závislostí pro celé.

Pokud balíček není nainstalovaná, NuGet se nejprve pokusí načíst z [mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). Pokud balíček není v mezipaměti, NuGet se pak pokusí stáhnout balíček ze všech zdrojů povolené (naleznete v tématu [konfigurace NuGet chování](Configuring-NuGet-Behavior.md); zdroje se zobrazí také v **nástroje > Možnosti > Správce balíčků NuGet > Zdroje balíčků** seznamu v sadě Visual Studio). Během obnovení NuGet ignoruje pořadí zdroje balíčků pomocí balíčku od toho zdroje je nejprve reagovat na požadavky.

> [!Note]
> NuGet neznamená neúspěšného obnovení balíčku, dokud byly vráceny všechny zdroje. V tu chvíli NuGet hlásí selhání pouze poslední zdroje v seznamu. Chyba znamená, že nebyl k dispozici v balíčku *jakékoli* z jiných zdrojů i v případě chyby se nezobrazují pro každou z těchto zdrojů jednotlivě.

Obnovení balíčku se aktivuje následujícími způsoby:

- **rozhraní příkazového řádku DotNet**: použijte [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) příkaz, který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../consume-packages/package-references-in-project-files.md)). S .NET Core 2.0 nebo novější, obnovení se provádí automaticky pomocí `dotnet build` a `dotnet run`.

- **Uživatelské rozhraní Správce balíčků (Visual Studio na Windows)**: obnovení balíčků automaticky při vytvoření projektu ze šablony a při sestavování projektu (v souladu s možnosti popsané v [povolení a zakázání balíček obnovení](#enabling-and-disabling-package-restore)). Ve Správci NuGet 4.0 + obnovit také dojde automaticky při změn projektu založeného na .NET Core SDK.

    Chcete-li obnovit ručně, klikněte pravým tlačítkem na řešení v Průzkumníku řešení a vyberte **obnovit balíčky NuGet**. Pokud jeden nebo více jednotlivých balíčků se stále není správně nainstalován (tj., Průzkumník řešení zobrazuje ikona chyby) a pak použijte uživatelské rozhraní Správce balíčků odinstalovat a znovu nainstalovat ovlivněné balíčky. Zobrazit [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md)

    Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které jsou na tomto počítači chybí" nebo "jeden nebo více balíčků NuGet je nutné obnovit, ale nepodařilo, protože nebyl udělen souhlas", zapněte automatické obnovení podle pokynů v části [Povolení a zákaz obnovení balíčku](#enabling-and-disabling-package-restore). Viz také [odstraňování problémů obnovení balíčku](Package-restore-troubleshooting.md).

- **Rozhraní příkazového řádku NuGet**: použijte [obnovení nuget](../tools/cli-ref-restore.md) příkaz, který obnoví balíčky uvedené v souboru projektu nebo v `packages.config`. Můžete také určit soubor řešení.

- **Nástroj MSBuild**: použijte [msbuild/t: Restore](../reference/msbuild-targets.md#restore-target) příkaz, který obnoví balíčky balíčky uvedené v souboru projektu (pouze PackageReference). K dispozici pouze v NuGet 4.x+ a MSBuild 15.1 +, které jsou součástí sady Visual Studio 2017. `nuget restore` a `dotnet restore` obě použijte tento příkaz pro příslušné projekty.

- **Visual Studio Team Services**: při vytváření definice sestavení ve službě Team Services, patří [obnovení NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) nebo [obnovení aplikace .NET Core](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) úloh v definici před libovolná sestavení úkolu. Tato úloha je zahrnuté ve výchozím nastavení v počtu šablon sestavení.

- **Team Foundation Server**: TFS 2013 a novější automatické obnovení balíčků během sestavení, za předpokladu, že používáte týmového sestavení šablony pro TFS 2013 nebo novější. Pro starší verze TFS můžete zahrnout krok sestavení k vyvolání jednu z výše uvedených možností příkazového řádku obnovení. Volitelně můžete migrovat šablony sestavení do TFS 2013. Další informace najdete v tématu [návod k obnovení balíčků pomocí procesu Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Povolení a zakázání obnovení balíčku

Obnovení balíčku především zajišťuje **nástroje > Možnosti > Správce balíčků NuGet** v sadě Visual Studio:

![Řízení chování balíčku obnovení prostřednictvím možnosti Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Umožnit správci balíčků NuGet stáhnout chybějící balíčky**: Určuje všechny formy obnovení balíčku tak, že změníte `packageRestore/enabled` nastavení `NuGet.Config` sdílené, jak je znázorněno níže (`%AppData%\NuGet\NuGet.Config` na Windows, `~/.nuget/NuGet/NuGet.Config` na Mac/Linux). V sadě Visual Studio, toto nastavení umožňuje **obnovit balíčky NuGet** příkazu v místní nabídce řešení pro práci.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  `packageRestore/enabled` Nastavení se dá přepsat globální nastavení proměnné prostředí volá **EnableNuGetPackageRestore** s hodnotou PRAVDA nebo NEPRAVDA před spuštěním aplikace Visual Studio nebo spuštění sestavení.

- **Automaticky zjišťovat pro chybějící balíčky během vytváření v sadě Visual Studio**: řídí automatické obnovení tak, že změníte `packageRestore/automatic` nastavení `NuGet.Config` sdílené, jak je znázorněno níže (`%AppData%\NuGet\NuGet.Config` na Windows, `~/.nuget/NuGet/NuGet.Config` na Mac/Linux). Když nastavíte tuto možnost, systémem sestavení ze sady Visual Studio automaticky obnoví všechny chybějící balíčky. Možnost nemá vliv na sestavení, spusťte z příkazového řádku pomocí nástroje MSBuild.

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

Odkaz, najdete v článku [NuGet konfiguračního souboru – část packageRestore](../reference/nuget-config-file.md#packagerestore-section).

V některých případech může být vhodné pro vývojáře nebo společnosti k povolení nebo zakázání obnovení balíčků pro všechny uživatele v počítači. K tomuto účelu přidat do globální NuGet konfigurační soubor umístěný ve stejné nastavení výše `%ProgramData%\NuGet\Config` (Windows, potenciálně v rámci konkrétní `\{IDE}\{Version}\{SKU}\` složka pro sadu Visual Studio) nebo `~/.local/share` (Mac/Linux). Jednotlivým uživatelům můžete selektivně povolte obnovení podle potřeby na úrovni projektu. Zobrazit [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) najdete přesné informace o tom, jak NuGet upřednostňuje více konfiguračních souborů.

> [!Important]
> Pokud upravíte `packageRestore` přímo v nastavení `nuget.config`, restartujte aplikaci Visual Studio tak, aby se dialogové okno Možnosti zobrazuje aktuální hodnoty.

## <a name="constraining-package-versions-with-restore"></a>Omezující verze balíčků pomocí obnovení

Při obnovování balíčků pomocí libovolné metody, NuGet respektuje omezeními podle `packages.config` nebo soubor projektu:

- `packages.config`: Zadejte rozsah verzí v `allowedVersion` vlastnost závislosti. Zobrazit [Reinstalling a aktualizace balíčků](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Příklad:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Soubor projektu (PackageReference): přímo s číslem verze závislosti uvádět rozsah verzí. Příklad:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Ve všech případech použijte notaci podle [Správa verzí balíčků](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Vynucení obnovení ze zdroje balíčku

Ve výchozím nastavení, operace obnovení NuGet používat balíčky z *global-packages* a *http-cache* složkách, které jsou popsány v [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).

Abyste se vyhnuli použití *global-packages* složky, proveďte jednu z následujících akcí:

- Zrušte pomocí složky `nuget locals global-packages -clear` nebo `dotnet nuget locals global-packages --clear`
- Dočasně změnit umístění *global-packages* složky, před provedením operace obnovení pomocí jedné z následujících metod:
  - Nastavte proměnnou prostředí NUGET_PACKAGES do jiné složky.
  - Vytvoření `NuGet.Config` souboru, který nastaví `globalPackagesFolder` (Pokud se používá PackageReference) nebo `repositoryPath` (Pokud používáte `packages.config`) do jiné složky (naleznete v tématu [nastavení konfigurace](../reference/nuget-config-file.md#config-section)
  - Pouze nástroj MSBuild: zadat jinou složku s `RestorePackagesPath` vlastnost.

Abyste se vyhnuli použití mezipaměti u zdrojů HTTP, proveďte jednu z následujících akcí:

- Použití `-NoCache` spolu s možností `nuget restore` nebo `--no-cache` spolu s možností `dotnet restore`. Tyto možnosti nemají vliv na operace obnovení, ať už Visual Studio uživatelské rozhraní Správce balíčků nebo konzoly.
- Vymazání mezipaměti pomocí `nuget locals http-cache -clear` nebo `dotnet nuget locals http-cache --clear`.
- Dočasně nastaví proměnné prostředí NUGET_HTTP_CACHE_PATH do jiné složky.

## <a name="troubleshooting"></a>Poradce při potížích

Zobrazit [odstraňování problémů obnovení balíčku](package-restore-troubleshooting.md).
