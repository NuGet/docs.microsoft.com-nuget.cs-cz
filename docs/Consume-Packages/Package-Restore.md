---
title: "Obnovení balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Popis jak NuGet obnoví balíčky, na kterých závisí na projekt včetně postup zakázání obnovení a omezit verze."
keywords: "Obnovení balíčku NuGet, instalace balíčku NuGet, instalace balíčku, Probíhá obnovení balíčků, verze závislosti, zakázat automatické obnovení chovaly verze balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8af70cff522e1f6c285d17ad0bbc20d23a0734a4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="package-restore"></a>Obnovení balíčku

Ke zvýšení úrovně čisticí vývojového prostředí a zmenšit velikost úložiště, NuGet **obnovení balíčků** nainstaluje všechny odkazované balíčky, než je založený na projekt. Tato funkce se často používá&mdash;k dispozici v sadě Visual Studio .NET Core 2.0 + a xbuild na Mono&mdash;zajistí, že všechny závislosti jsou k dispozici v projektu bez nutnosti tyto balíčky k uložení do správy zdrojového kódu (viz [ Balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) na tom, jak nakonfigurovat úložiště vyloučit binární soubory balíčku). Balíčky můžete obnovit také ručně kdykoli.

Další informace o obnovení balíčků na serverech sestavení v [obnovení balíčků s TFBuild](../consume-packages/team-foundation-build.md).

## <a name="package-restore-overview"></a>Přehled obnovení balíčku

Obnovují se balíčky nejdřív nainstaluje přímé závislosti projektu, podle potřeby, pak instalace všechny závislosti tyto balíčky v rámci celého závislost grafu.

Pokud ještě není nainstalovaný balíček, NuGet se nejprve pokusí načíst z [mezipaměti](../consume-packages/managing-the-nuget-cache.md). Pokud balíček není v mezipaměti, NuGet se potom pokusí stáhnout balíček z povolených zdrojů, jak je uvedeno v **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků**, v pořadí, ve kterém se zobrazí zdroje. Stažené balíčky jsou uloženy v mezipaměti.

> [!Note]
> NuGet neindikuje selhání najít balíčku, dokud nebude provedena kontrola všech zdrojů, po kterých oznámí selhání jenom pro poslední zdroj v seznamu. Nepřímo takové chyby také znamená, že balíček nebyl k dispozici na žádném z jiných zdrojů buď, i v případě, že chyby nebyly zobrazeny pro tyto zdroje jednotlivě.

Obnovení balíčku se aktivuje následujícími způsoby:

- **Uživatelského rozhraní Správce balíčků (Visual Studio v systému Windows)**: balíčky jsou automaticky neobnoví, při vytváření projektů z šablony a při sestavení projektu (s výjimkou možnosti popsané v [povolení a zakázání balíček obnovit](#enabling-and-disabling-package-restore)). V NuGet 4.0 + obnovení také dochází vždy při provedení změn projektu na základě rozhraní .NET Core SDK.

    Chcete-li obnovit ručně, klikněte pravým tlačítkem v Průzkumníku řešení a vyberte **obnovení balíčků NuGet**. Pokud jeden nebo více jednotlivých balíčků jsou stále není správně nainstalován (tj. že Průzkumník řešení se zobrazuje ikona chyby) a pak použít uživatelské rozhraní Správce balíčků odinstalovat a znovu nainstalovat ovlivněných balíčků. V tématu [Reinstalling a aktualizaci balíčků](../Consume-Packages/Reinstalling-and-Updating-Packages.md)

    Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači" nebo "jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas", zapněte automatické obnovení podle pokynů v části [Povolení a zákaz obnovení balíčků](#enabling-and-disabling-package-restore).

- **Rozhraní příkazového řádku NuGet**: použijte [obnovení nuget](../tools/cli-ref-restore.md) příkaz, který obnoví balíčky uvedené v souboru projektu (najdete v části [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)) nebo v [packages.config](../schema/packages-config.md)souboru. Můžete také určit soubor řešení.

- **DotNet rozhraní příkazového řádku**: použijte [dotnet obnovení](/dotnet/core/tools/dotnet-restore.md?tabs=netcore2x) příkaz, který obnoví balíčky uvedené v souboru projektu (najdete v části [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)). S .NET Core 2.0 nebo novější, je automaticky provést obnovení s `dotnet build` a `dotnet run`.

- **MSBuild**: použijte [msbuild /t:restore](../schema/msbuild-targets.md#restore-target) příkaz, který obnovení balíčků balíčky uvedené v souboru projektu (najdete v části [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)). K dispozici pouze v NuGet 4.x+ a MSBuild 15.1 +, které jsou součástí Visual Studio 2017. `nuget restore`a `dotnet restore` obě tento příkaz použijte pro příslušné projekty.

- **Visual Studio Team Services**: při vytváření definice sestavení v Team Services, zahrnují [obnovení NuGet](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) nebo [.NET Core obnovit](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) úloh v definici před všechny úloze sestavení. Tato úloha je zahrnutá ve výchozím nastavení v počet šablony sestavení.

- **Team Foundation Server**: TFS 2013 a novější automaticky obnoví balíčky během vytváření sestavení, za předpokladu, že používáte-li vytvořit šablonu Team sady TFS 2013 nebo novější. Pro starší verzi sady TFS můžete zahrnout krok sestavení vyvolat jeden z výše uvedených možností příkazového řádku obnovení. Volitelně můžete migrovat šablony sestavení TFS 2013. Další informace najdete v tématu [návod obnovení balíčků s Team Foundation Build](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Povolení a zákaz obnovení balíčků

Obnovení balíčku je primárně povolená díky **nástroje > Možnosti > Správce balíčků NuGet** v sadě Visual Studio:

![Řízení chování obnovení balíčku prostřednictvím možnosti Správce balíčků NuGet](media/Restore-01-AutoRestoreOptions.png)

- **Povolit aplikaci NuGet stáhnout chybějící balíčky**: řídí všechny formy obnovení balíčků změnou `packageRestore/enabled` nastavení v `%AppData%\NuGet\NuGet.Config` souboru, jak je uvedeno níže.

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

- **Automaticky Zkontrolujte chybějící balíčky během sestavení v sadě Visual Studio**: ovládací prvky Automatické obnovení změnou `packageRestore/automatic` nastavení v `%AppData%\NuGet\NuGet.Config` souboru, jak je uvedeno níže.

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

Odkaz, najdete v článku [NuGet konfiguračního souboru – část packageRestore](../Schema/nuget-config-file.md#packagerestore-section).

V některých případech vývojáře nebo společnosti chtít povolit nebo zakázat obnovení balíčku pro všechny uživatele v počítači. To se provádí přidáním globální NuGet konfigurační soubor umístěný ve stejné nastavení výše `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Jednotlivým uživatelům můžete selektivně povolte obnovení podle potřeby na úrovni projektu. V tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) přesné informace o tom, jak NuGet upřednostňuje více konfigurační soubory.

## <a name="constraining-package-versions-with-restore"></a>Omezení verze balíčku s obnovením

Při obnovování balíčků pomocí libovolné metody, NuGet ctí žádná omezení, zadaný v `packages.config` nebo souboru projektu:

- `packages.config`: Určete rozsah verze v `allowedVersion` vlastnost závislosti. V tématu [Reinstalling a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Příklad:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference: Zadejte verzi rozsah přímo s číslem verze této závislosti. Příklad:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Ve všech případech, použijte zápis popsané v [Správa verzí balíčku](../reference/package-versioning.md).

## <a name="troubleshooting"></a>Poradce při potížích

V tématu [řešení potíží s obnovení balíčků](Package-restore-troubleshooting.md).