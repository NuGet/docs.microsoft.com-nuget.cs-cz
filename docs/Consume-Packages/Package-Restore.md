---
title: "Obnovení balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Popis jak NuGet obnoví balíčky, na kterých závisí na projekt včetně postup zakázání obnovení a omezit verze."
keywords: "Obnovení balíčku NuGet, instalace balíčku NuGet, instalace balíčku, Probíhá obnovení balíčků, verze závislosti, zakázat automatické obnovení chovaly verze balíčku"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a>Obnovení balíčku

Ke zvýšení úrovně čisticí vývojového prostředí a zmenšit velikost úložiště, NuGet **obnovení balíčků** nainstaluje všechny odkazované balíčky, než je založený na projekt. Tato funkce se často používá zajistí, že všechny závislosti jsou k dispozici v projektu bez nutnosti tyto balíčky k uložení do správy zdrojového kódu (v tématu [balíčky a Správa zdrojového kódu](../consume-packages/packages-and-source-control.md) na tom, jak nakonfigurovat úložiště k vyloučení binární soubory balíčku).

V tomto tématu:
- [Obnovení Stručná příručka k balíčku](#quick-guide-to-package-restore)
- [Přehled obnovení balíčku](#package-restore-overview)
- [Povolení a zákaz obnovení balíčků](#enabling-and-disabling-package-restore)
- [Omezení verze balíčku s obnovením](#constraining-package-versions-with-restore)
- [Příkazového řádku obnovení](#command-line-restore), pro všechny verze systému NuGet
- [Automatické obnovení v sadě Visual Studio](#automatic-restore-in-visual-studio)pro NuGet 2.7 a později.
- [Integrované nástroje MSBuild obnovení v sadě Visual Studio](#msbuild-integrated-restore)pro NuGet 2.6 a dříve.
- [Obnovení balíčku s Team Foundation Build](#package-restore-with-team-foundation-build)

Obnovit chování se liší podle verze; Pokud chcete zkontrolovat verzi vaší NuGet, jednoduše spusťte `nuget.exe` příkazového řádku a podívejte se na první řádek výstupu.

Další informace o obnovení balíčků na serverech sestavení v [obnovení balíčků s TFBuild](../consume-packages/team-foundation-build.md).

> [!Note]
> Projekty, které jsou nakonfigurované pro balíček obnovit také práci s xbuild na Mono.

## <a name="quick-guide-to-package-restore"></a>Obnovení Stručná příručka k balíčku

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> Pokud se zobrazí chyba "Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači" nebo "jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas", zapněte automatické obnovení podle pokynů v části [Povolení a zákaz obnovení balíčků](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Přehled obnovení balíčku

Nejprve balíček odkazuje udržované v jednom z následujících formátů správu balíčku, v závislosti na typu projektu a verze NuGet. (Všimněte si, že NuGet 4 a MSBuild 15.1 je instalován s Visual Studio 2017.)

| Metoda | Verze NuGet | Popis | 
| --- | --- | --- |
| `packages.config` | 2.x + | Uvádí hloubkové kompletní sadu závislosti. Přidat do balíčků `packages.config` musíte přidat i k souboru projektu a cílů a Props musíte přidat i do souboru projektu. Toto je metoda standardních hodnot pro všechny verze balíčku nuget, ale má nižší výkon ve srovnání s jinými možnostmi. (Viz [souboru packages.config schématu](../schema/packages-config.md).) | 
| `project.json` | 3.x + | Použít pouze ve výchozím nastavení s projekty UWP, ale projekty mohou být převedeny z `packages.config`. `project.json`uvádí jenom nejvyšší úrovně závislosti. Odkazy, cílů a Props se dynamicky k projektu nepřidají během vytváření sestavení, což vede k lepší výkon ve srovnání s `packages.config`. (Viz [project.json schématu](../schema/project-json.md).)|
| PackageReference | 4.x + | Uvádí přímo v souboru projektu v závislosti `<PackageReference>` uzlu, alongside `<Reference>` a `<ProjectReference>`. Podobně jako funguje `project.json`; najdete v části [balíček odkazy v souborech projektu](../Consume-Packages/Package-References-in-Project-Files.md). |

Druhý spustit obnovení pomocí seznamu odkaz v mnoha různými způsoby:

Z příkazového řádku nebo [Konzola správce balíčků](../tools/Package-Manager-Console.md):

| Příkaz | Použít scénáře |
| --- | --- | 
| `nuget restore` | Všechny verze NuGet a všechny odkazové typy. V tématu [příkazového řádku obnovení](#command-line-restore) níže. | 
| `dotnet restore` | Stejné jako `nuget restore` pro projekty .NET Core. V tématu [dotnet obnovení](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Nuget 4.x+ a MSBuild 15.1 + s [balíček odkazy v souborech projektu](../Consume-Packages/Package-References-in-Project-Files.md) pouze. `nuget restore`a `dotnet restore` obě tento příkaz použijte pro příslušné projekty. V tématu [NuGet pack a obnovení jako MSBuild cíle obnovení cíl](../schema/msbuild-targets.md#restore-target).|

Visual Studio, samotné také obnoví balíčky v různých časech:

| Typ | Když se stane obnovení |
| --- | --- |
| Obnovení šablony | Při vytvoření nového projektu jako některé šablony závisí na externí balíčky. |
| Sestavení obnovení | Jako první krok sestavení. |
| Řešení obnovení | Když uživatel klikne pravým tlačítkem myši řešení a vybírá **obnovení balíčků NuGet**. |
| Obnovit na změnu projektu | *(NuGet 4.x pouze)*  Projektu na základě při .NET Core SDK se používá, včetně při projektu změny stavu. |

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
    

- **Automaticky Zkontrolujte chybějící balíčky během sestavení v sadě Visual Studio**: Automatické obnovení NuGet 2.7 a později změnou ovládací prvky `packageRestore/automatic` nastavení v `%AppData%\NuGet\NuGet.Config` souboru, jak je uvedeno níže.
            
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

V některých případech vývojáře nebo společnosti chtít povolit nebo zakázat obnovení balíčku na počítači, ve výchozím nastavení pro všechny uživatele. To lze provést přidáním globální NuGet konfigurační soubor umístěný ve stejné nastavení výše `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Jednotlivým uživatelům můžete selektivně povolte obnovení podle potřeby na úrovni projektu. V tématu [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) přesné informace o tom, jak NuGet upřednostňuje více konfigurační soubory.

## <a name="constraining-package-versions-with-restore"></a>Omezení verze balíčku s obnovením

Když NuGet obnoví balíčky pomocí libovolné metody, dodrží žádná omezení, zadaný v `packages.config`, `project.json`, nebo soubor projektu:

- `packages.config`: Určete rozsah verze v `allowedVersion` vlastnost závislosti. V tématu [přeinstalovat a aktualizaci balíčků](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Příklad:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: Určete rozsah verze přímo s číslem verze této závislosti. Příklad:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Balíček odkazy v souborech projektu: Zadejte verzi rozsah přímo s číslem verze této závislosti. Příklad:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

Ve všech případech, použijte zápis popsané v [Správa verzí balíčku](../reference/package-versioning.md).

## <a name="command-line-restore"></a>Obnovení příkazového řádku

NuGet 2.7 a výše, použijte [obnovení](../tools/cli-ref-restore.md) příkazu obnovte všechny balíčky v řešení (jestli používá `packages.config`, `project.json`, nebo balíčku odkazy v souborech projektu). Pro daný projekt složku jako `c:\proj\app`, běžné varianty níže každý obnovení balíčků:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

Pro NuGet 4.0 + a MSBuild 15.1 +, můžete také použít `MSBuild /t:restore` jak je popsáno na [NuGet pack a obnovit jako cíle MSBuild](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Obnovení době sestavení v sadě Visual Studio

Visual Studio automaticky obnoví chybějící balíčky ve výchozím nastavení na začátku sestavení. Toto chování lze změnit tak, že smažete **nástroje > Možnosti > Správce balíčků NuGet > Obecné > automaticky Zkontrolujte chybějící balíčky během sestavení v sadě Visual Studio**.

Když je povolené, automatické obnovení funguje takto:

1. Po zahájení sestavení sady Visual Studio dá pokyn k obnovení balíčků NuGet.
1. Rekurzivní NuGet hledá všechny `packages.config` soubory v řešení, hledá `project.json`, nebo hledá v souboru projektu.
1. Pro každý balíčky uvedené v referenčních souborů, NuGet kontroly Pokud již existuje v řešení ( `packages` složky, `project.lock.json`, nebo `project.assets.json` v závislosti na tom, jestli je projekt pomocí `packages.config`, `project.json`, nebo na odkazy v balíčku soubory projektu).
1. Pokud daný balíček nebyl nalezen, NuGet pokusí načíst balíček ze své mezipaměti nejprve (viz [Správa mezipaměti NuGet](../consume-packages/managing-the-nuget-cache.md). Pokud balíček není v mezipaměti, NuGet pokusí stáhnout balíček z povolených zdrojů, jak je uvedeno v **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků**, v pořadí, ve kterém se zobrazí zdroje. V takovém případě NuGet neindikuje selhání najít balíčku, dokud nebude provedena kontrola všech zdrojů, po kterých oznámí selhání jenom pro poslední zdroj v seznamu. Nepřímo takové chyby také znamená, že balíček nebyl k dispozici na žádném z jiných zdrojů buď, i v případě, že chyby nebyly zobrazeny pro tyto zdroje jednotlivě.
1. Pokud stahování úspěšné, ukládá do mezipaměti balíček NuGet a nainstaluje do řešení (znovu do buď `packages` složky, `project.lock.json`, nebo `project.assets.json`); jinak selže NuGet a sestavení selže.

Během tohoto procesu se zobrazí dialogové okno průběhu s možností zrušit obnovení balíčků.

## <a name="package-restore-with-team-foundation-build"></a>Obnovení balíčku s Team Foundation Build

Obnovení balíčku se obvykle používá při sestavování projektů na serverech, sestavení, stejně jako u Team Foundation Server (TFS) a Visual Studio Team Services (stejně jako jiné systémy sestavení, které nejsou zde popsané).

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Při vytváření definice sestavení v Team Services, jednoduše zahrnují úlohu obnovení balíčků NuGet v definici před všechny úlohy sestavení. Tato úloha je zahrnutá ve výchozím nastavení v počet šablony sestavení.

![Úloha obnovení balíčku NuGet v definici sestavení Visual Studio Team Service](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Se sadou TFS 2013 a novější balíčky se automaticky obnoví ve výchozím nastavení během vytváření sestavení, za předpokladu, že používáte-li vytvořit šablonu Team pro Team Foundation Server 2013 nebo novější.

Pokud používáte předchozí verzi šablony sestavení (například v projektu, který se migroval z dřívějších verzí sady TFS), budete muset taky migrovat ty sestavení šablony do sady TFS 2013. To v podstatě znamená znovu vytvořit vlastní části šablony sestavení pomocí příslušné šablony pro vašeho zdrojového kódu (TFVC nebo Git).

Pro starší verzi sady TFS, můžete jednoduše zahrnout krok sestavení, který má být vyvolán [příkazového řádku obnovení](#command-line-restore) jak bylo popsáno výše.

Podrobnosti najdete v části pak [návod balíček obnovit pomocí Team Foundation Build](../consume-packages/team-foundation-build.md).    
