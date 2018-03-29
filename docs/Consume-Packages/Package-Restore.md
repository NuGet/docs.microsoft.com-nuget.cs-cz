---
title: Obnovení balíčku NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Přehled o tom, jak NuGet obnoví balíčky, na kterých závisí na projekt včetně postup zakázání obnovení a omezit verze.
keywords: Obnovení balíčku NuGet, instalace balíčku NuGet, instalace balíčku, Probíhá obnovení balíčků, verze závislosti, zakázat automatické obnovení chovaly verze balíčku
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: d5c9c9f571ea25f8877f78c3fba114562d31fcd8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="package-restore"></a>Obnovení balíčku

Ke zvýšení úrovně čisticí vývojového prostředí a zmenšit velikost úložiště, NuGet **obnovení balíčků** nainstaluje všechny projektu závislosti, jak je uvedeno v některém souboru projektu nebo `packages.config`. Visual Studio můžete obnovit balíčky automaticky, když je založený na projekt. `dotnet build` a `dotnet run` příkazy (.NET Core 2.0 +) také provést automatické obnovení. Můžete také obnovit balíčky kdykoli pomocí sady Visual Studio, `nuget restore`, `dotnet restore`a xbuild na Mono.

Obnovení balíčku je zajištěno, že všechny projektu závislosti jsou k dispozici bez ukládání těchto balíčků ve správě zdrojového kódu. V tématu [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) na tom, jak nakonfigurovat úložiště vyloučit binární soubory balíčku.

## <a name="package-restore-overview"></a>Přehled obnovení balíčku

Obnovují se balíčky nejprve nainstaluje přímé závislosti projektu podle potřeby, a poté nainstaluje všechny závislosti tyto balíčky v rámci celého závislost grafu.

Pokud ještě není nainstalovaný balíček, NuGet se nejprve pokusí načíst z [mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). Pokud balíček není v mezipaměti, NuGet se potom pokusí stáhnout balíček ze všech zdrojů povoleno (najdete v části [konfigurace NuGet chování](Configuring-NuGet-Behavior.md); zdrojů se zobrazí také v **nástroje > Možnosti > Správce balíčků NuGet > Zdroje balíčků** seznamu v sadě Visual Studio). Během obnovení NuGet ignoruje pořadí zdroje balíčků pomocí balíčku z libovolného zdroj je nejdřív reagovat na požadavky.

> [!Note]
> NuGet neindikuje neúspěšného obnovení balíčku, dokud nebude provedena kontrola všech zdrojů. V té době NuGet ohlásí chybu pouze poslední zdroje v seznamu. Chyba znamená, že balíček nebyl k dispozici na *žádné* z jiných zdrojů, i když chyby nejsou zobrazeny pro každou z těchto zdrojů jednotlivě.

Obnovení balíčku se aktivuje následujícími způsoby:

- **DotNet rozhraní příkazového řádku**: použijte [dotnet obnovení](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) příkaz, který obnoví balíčky uvedené v souboru projektu (najdete v části [PackageReference](../consume-packages/package-references-in-project-files.md)). S .NET Core 2.0 nebo novější, je automaticky provést obnovení s `dotnet build` a `dotnet run`.

- **Uživatelského rozhraní Správce balíčků (Visual Studio v systému Windows)**: balíčky jsou automaticky neobnoví, při vytváření projektů z šablony a při sestavení projektu (s výjimkou možnosti popsané v [povolení a zakázání balíček obnovit](#enabling-and-disabling-package-restore)). V NuGet 4.0 + obnovení také dochází vždy při provedení změn projektu na základě rozhraní .NET Core SDK.

    Chcete-li obnovit ručně, klikněte pravým tlačítkem v Průzkumníku řešení a vyberte **obnovení balíčků NuGet**. Pokud jeden nebo více jednotlivých balíčků jsou stále není správně nainstalován (tj. že Průzkumník řešení se zobrazuje ikona chyby) a pak použít uživatelské rozhraní Správce balíčků odinstalovat a znovu nainstalovat ovlivněných balíčků. V tématu [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md)

    Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači" nebo "jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas", zapněte automatické obnovení podle pokynů v části [Povolení a zákaz obnovení balíčků](#enabling-and-disabling-package-restore). Viz také [řešení potíží s balíček obnovení](Package-restore-troubleshooting.md).

- **Rozhraní příkazového řádku NuGet**: použijte [obnovení nuget](../tools/cli-ref-restore.md) příkaz, který obnoví balíčky uvedené v souboru projektu nebo v `packages.config`. Můžete také určit soubor řešení.

- **MSBuild**: použití [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) příkaz, který obnovení balíčků balíčky uvedené v souboru projektu (pouze PackageReference). K dispozici pouze v NuGet 4.x+ a MSBuild 15.1 +, které jsou součástí Visual Studio 2017. `nuget restore` a `dotnet restore` obě tento příkaz použijte pro příslušné projekty.

- **Visual Studio Team Services**: při vytváření definice sestavení v Team Services, zahrnují [obnovení NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) nebo [.NET Core obnovit](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) úloh v definici před všechny úloze sestavení. Tato úloha je zahrnutá ve výchozím nastavení v počet šablony sestavení.

- **Team Foundation Server**: TFS 2013 a novější automaticky obnoví balíčky během vytváření sestavení, za předpokladu, že používáte-li vytvořit šablonu Team sady TFS 2013 nebo novější. Pro starší verzi sady TFS můžete zahrnout krok sestavení vyvolat jeden z výše uvedených možností příkazového řádku obnovení. Volitelně můžete migrovat šablony sestavení TFS 2013. Další informace najdete v tématu [návod obnovení balíčků s Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Povolení a zákaz obnovení balíčků

Obnovení balíčku je primárně povolená díky **nástroje > Možnosti > Správce balíčků NuGet** v sadě Visual Studio:

![Řízení chování obnovení balíčku prostřednictvím možnosti Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Povolit aplikaci NuGet stáhnout chybějící balíčky**: řídí všechny formy obnovení balíčků změnou `packageRestore/enabled` nastavení v `NuGet.Config` souboru, jak je uvedeno níže (`%AppData%\NuGet\NuGet.Config` v systému Windows, `~/.nuget/NuGet/NuGet.Config` na Mac/Linux). V sadě Visual Studio, toto nastavení umožňuje **obnovení balíčků NuGet** příkaz v místní nabídce na řešení pro práci.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  `packageRestore/enabled` Nastavení je možné přepsat globálně nastavením proměnné prostředí názvem **EnableNuGetPackageRestore** s hodnotou PRAVDA nebo NEPRAVDA před spuštění sady Visual Studio nebo spuštění sestavení.

- **Automaticky Zkontrolujte chybějící balíčky během sestavení v sadě Visual Studio**: ovládací prvky Automatické obnovení změnou `packageRestore/automatic` nastavení v `NuGet.Config` souboru, jak je uvedeno níže (`%AppData%\NuGet\NuGet.Config` v systému Windows, `~/.nuget/NuGet/NuGet.Config` na Mac/Linux). Pokud je tato možnost nastavená, spuštění sestavení ze sady Visual Studio automaticky obnoví všechny chybějící balíčky. Možnost nemá vliv na sestavení, spusťte z příkazového řádku pomocí nástroje MSBuild.

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

V některých případech vývojáře nebo společnosti chtít povolit nebo zakázat obnovení balíčku pro všechny uživatele v počítači. K tomuto účelu přidat do globální NuGet konfigurační soubor umístěný ve stejné nastavení výše `%ProgramData%\NuGet\Config` (Windows potenciálně v konkrétní `\{IDE}\{Version}\{SKU}\` složku pro sadu Visual Studio) nebo `~/.local/share` (Mac/Linux). Jednotlivým uživatelům můžete selektivně povolte obnovení podle potřeby na úrovni projektu. V tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) přesné informace o tom, jak NuGet upřednostňuje více konfigurační soubory.

> [!Important]
> Pokud chcete upravit `packageRestore` nastavení přímo v `nuget.config`, restartujte Visual Studio, aby se dialogové okno Možnosti zobrazuje aktuální hodnoty.

## <a name="constraining-package-versions-with-restore"></a>Omezení verze balíčku s obnovením

Při obnovování balíčků pomocí libovolné metody, NuGet ctí žádná omezení, zadaný v `packages.config` nebo souboru projektu:

- `packages.config`: Určete rozsah verze v `allowedVersion` vlastnost závislosti. V tématu [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Příklad:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Soubor projektu (PackageReference): Zadejte verzi rozsah přímo s číslem verze této závislosti. Příklad:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Ve všech případech, použijte zápis popsané v [Správa verzí balíčku](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Vynutit obnovení ze zdroje balíčků

Ve výchozím nastavení používají operace obnovení NuGet balíčky z *globální balíčky* a *http mezipaměti* složkách, které jsou popsané na [správy globální balíčky a složky mezipaměti](managing-the-global-packages-and-cache-folders.md).

Aby se zabránilo pomocí *globální balíčky* složku, proveďte jednu z následujících:

- Vymazat složky použitím `nuget locals global-packages -clear` nebo `dotnet nuget locals global-packages --clear`
- Dočasně změnit umístění *globální balíčky* složky a potom operaci obnovení pomocí jedné z následujících metod:
  - Nastavte proměnnou prostředí NUGET_PACKAGES do jiné složky.
  - Vytvoření `NuGet.Config` soubor, který nastaví `globalPackagesFolder` (Pokud se používá PackageReference) nebo `repositoryPath` (Pokud používáte `packages.config`) do jiné složky (najdete v části [nastavení konfigurace](../reference/nuget-config-file.md#config-section)
  - MSBuild pouze: zadat jinou složku, pomocí `RestorePackagesPath` vlastnost.

Chcete-li Vyhněte se použití mezipaměti pro zdrojů HTTP, proveďte jednu z následujících:

- Použití `-NoCache` možnost s `nuget restore` nebo `--no-cache` možnost s `dotnet restore`. Tyto možnosti neovlivní operace obnovení prostřednictvím konzoly nebo Visual Studio uživatelské rozhraní Správce balíčků.
- Vymazání mezipaměti pomocí `nuget locals http-cache -clear` nebo `dotnet nuget locals http-cache --clear`.
- Dočasně nastavte proměnné prostředí NUGET_HTTP_CACHE_PATH do jiné složky.

## <a name="troubleshooting"></a>Poradce při potížích

V tématu [řešení potíží s obnovení balíčků](package-restore-troubleshooting.md).