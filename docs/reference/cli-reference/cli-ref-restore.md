---
title: NuGet CLI – příkaz obnovení
description: Referenční informace pro příkaz nuget.exe Restore
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780034"
---
# <a name="restore-command-nuget-cli"></a>příkaz Restore (NuGet CLI)

**Platí pro:** &bullet; **podporované verze balíčku:** 2.7 +

Stáhne a nainstaluje ze složky chybějící balíčky `packages` . Při použití s NuGet 4.0 + a formátem PackageReference vygeneruje `<project>.nuget.props` v případě potřeby soubor ve `obj` složce. (Soubor může být vynechán ze správy zdrojového kódu.)

V systému Mac OSX a Linux s rozhraním příkazového řádku pro mono není obnovení balíčků podporováno v PackageReference.

## <a name="usage"></a>Využití

```cli
nuget restore <projectPath> [options]
```

kde `<projectPath>` Určuje umístění řešení nebo `packages.config` souboru. Podrobnosti o chování najdete níže v části [poznámky](#remarks) .

## <a name="options"></a>Možnosti

- **`-ConfigFile`**

  Konfigurační soubor NuGet, který se má použít Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-DirectDownload`**

  *(4.0 +)* Stáhne balíčky přímo bez doplňování mezipamětí s libovolnými binárními soubory nebo metadaty.

- **`-DisableParallelProcessing`**

   Zakáže obnovení více balíčků paralelně.

- **`-FallbackSource`**

  *(3.2 +)* Seznam zdrojů balíčků, které se použijí jako záložní pro případ, že se balíček nenajde v primárním nebo výchozím zdroji. K oddělení položek seznamu použijte středník.

- **`-Force`**

  V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné. Zadání tohoto příznaku se podobá odstranění `project.assets.json` souboru. To neobejde mezipaměť HTTP-cache.

- **`-ForceEnglishOutput`**

  *(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.

- **`-ForceEvaluate`**

  Vynutí obnovení, aby se znovu vyhodnotily všechny závislosti i v případě, že soubor zámku již existuje.

- **`-?|-help`**

  Zobrazí informace o nápovědě k příkazu.

- **`-LockFilePath`**

  Výstupní umístění, kde je zapsán soubor zámku projektu. Ve výchozím nastavení je to `PROJECT_ROOT\packages.lock.json` .

- **`-LockedMode`**

  Nepovolujte aktualizaci souboru zámku projektu.

- **`-MSBuildPath`**

   *(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž přednost využije `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem. Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild.

- **`-NoCache`**

  Zabraňuje balíčku NuGet v použití balíčků v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Potlačí výzvy pro vstup uživatele nebo potvrzení.

- **`-OutputDirectory`**

  Určuje složku, ve které jsou balíčky nainstalované. Pokud není zadána žádná složka, je použita aktuální složka. Vyžaduje se při obnovení `packages.config` souboru se souborem, pokud `PackagesDirectory` `SolutionDirectory` se nepoužívá nebo.

- **`-PackageSaveMode`**

  Určuje typy souborů, které se uloží po instalaci balíčku: jedna z hodnot `nuspec` , `nupkg` nebo `nuspec;nupkg` .

- **`-PackagesDirectory`**

  Stejné jako `OutputDirectory` . Vyžaduje se při obnovení `packages.config` souboru se souborem, pokud `OutputDirectory` `SolutionDirectory` se nepoužívá nebo.

- **`-Project2ProjectTimeOut`**

  Časový limit v sekundách pro řešení odkazů mezi projekty.

- **`-Recursive`**

  *(4.0 +)* Obnoví všechny odkazy na projekty UWP a .NET Core. Neplatí pro projekty používající `packages.config` .

- **`-RequireConsent`**

  Ověřuje, jestli je před stažením a instalací balíčků povolený obnovování balíčků. Podrobnosti najdete v tématu věnovaném [obnovení balíčků](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Určuje složku řešení. Neplatný při obnovování balíčků pro řešení. Vyžaduje se při obnovení `packages.config` souboru se souborem, pokud `PackagesDirectory` `OutputDirectory` se nepoužívá nebo.

- **`-Source`**

  Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít pro obnovení. Pokud tento příkaz vynecháte, použije se zdroje zadané v konfiguračních souborech, viz téma [Konfigurace chování NuGet](../../consume-packages/configuring-nuget-behavior.md). K oddělení položek seznamu použijte středník.

- **`-UseLockFile`**

  Povoluje vygenerování souboru zámku projektu a jeho použití s obnovením.

- **`-Verbosity [normal|quiet|detailed]`**

  Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="remarks"></a>Poznámky

Příkaz Restore provede následující kroky:

1. Určete režim operace příkazu Restore.

   | typ souboru projectPath | Chování |
   | --- | --- |
   | Řešení (složka) | NuGet vyhledá `.sln` soubor a použije ho, pokud se najde. v opačném případě se zobrazí chyba. `(SolutionDir)\.nuget` slouží jako spouštěcí složka. |
   | `.sln` souborů | Obnovit balíčky identifikované řešením; obsahuje chybu, pokud `-SolutionDirectory` se používá. `$(SolutionDir)\.nuget` slouží jako spouštěcí složka. |
   | `packages.config` nebo soubor projektu | Obnovte balíčky uvedené v souboru, vyřešte je a nainstalujte závislosti. |
   | Jiný typ souboru | Předpokládá se, že se jedná o `.sln` soubor, který je uvedený výše. Pokud se nejedná o řešení, NuGet vyvolá chybu. |
   | (projectPath není zadáno) | <ul><li>NuGet vyhledá soubory řešení v aktuální složce. Pokud se najde jeden soubor, použije se k obnovení balíčků. Pokud je nalezeno více řešení, NuGet vyvolá chybu.</li><li>Pokud neexistují žádné soubory řešení, NuGet vyhledá `packages.config` a použije k obnovení balíčků.</li><li>Pokud se nenajde žádné řešení nebo `packages.config` soubor, NuGet vyvolá chybu.</ul> |

2. Určení složky balíčků pomocí následujícího pořadí priorit (Pokud žádná z těchto složek nenalezne, vyvolá chybu NuGet):

    - Složka zadaná s parametrem `-PackagesDirectory` .
    - `repositoryPath`Hodnota v`Nuget.Config`
    - Složka zadaná s `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Při obnovování balíčků pro řešení provede NuGet následující:
    - Načte soubor řešení.
    - Obnoví balíčky na úrovni řešení uvedené v `$(SolutionDir)\.nuget\packages.config` části do `packages` složky.
    - Obnovte balíčky uvedené v `$(ProjectDir)\packages.config` části do `packages` složky. Pro každý zadaný balíček obnovte balíček paralelně, pokud `-DisableParallelProcessing` není zadaný.

## <a name="examples"></a>Příklady

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
