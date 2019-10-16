---
title: NuGet CLI – příkaz obnovení
description: Referenční informace o příkazu NuGet. exe Restore
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8ba61fa87118108c36e9dc73f30d964380d02dab
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380460"
---
# <a name="restore-command-nuget-cli"></a>příkaz Restore (NuGet CLI)

**Platí pro:** spotřeba balíčku &bullet; **podporované verze:** 2.7 +

Stáhne a nainstaluje do složky `packages` žádné chybějící balíčky. Při použití s NuGet 4.0 + a formátem PackageReference vygeneruje soubor `<project>.nuget.props`, pokud je to potřeba, do složky `obj`. (Soubor může být vynechán ze správy zdrojového kódu.)

V systému Mac OSX a Linux s rozhraním příkazového řádku pro mono není obnovení balíčků podporováno v PackageReference.

## <a name="usage"></a>Použití

```cli
nuget restore <projectPath> [options]
```

kde `<projectPath>` určuje umístění řešení nebo souboru `packages.config`. Podrobnosti o chování najdete níže v části [poznámky](#remarks) .

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet, který se má použít Pokud není zadaný, použije se `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).|
| DirectDownload | *(4.0 +)* Stáhne balíčky přímo bez doplňování mezipamětí s libovolnými binárními soubory nebo metadaty. |
| DisableParallelProcessing | Zakáže obnovení více balíčků paralelně. |
| FallbackSource | *(3.2 +)* Seznam zdrojů balíčků, které se použijí jako záložní pro případ, že se balíček nenajde v primárním nebo výchozím zdroji. K oddělení položek seznamu použijte středník. |
| ForceEnglishOutput | *(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu. |
| Nápověda | Zobrazí informace o nápovědě k příkazu. |
| MSBuildPath | *(4.0 +)* Určuje cestu nástroje MSBuild, který má být použit s příkazem, přičemž má přednost před `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)* Určuje verzi nástroje MSBuild, která má být použita s tímto příkazem. Podporované hodnoty jsou 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9. Ve výchozím nastavení je nástroj MSBuild v cestě vybrán, jinak má výchozí nejvyšší nainstalovanou verzi nástroje MSBuild. |
| NoCache | Zabraňuje balíčku NuGet v použití balíčků v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| OutputDirectory | Určuje složku, ve které jsou balíčky nainstalované. Pokud není zadána žádná složka, je použita aktuální složka. Vyžaduje se při obnovení souboru `packages.config`, pokud se nepoužívá `PackagesDirectory` nebo `SolutionDirectory`.|
| PackageSaveMode | Určuje typy souborů, které se uloží po instalaci balíčku: jedna z `nuspec`, `nupkg` nebo `nuspec;nupkg`. |
| PackagesDirectory | Stejné jako `OutputDirectory`. Vyžaduje se při obnovení souboru `packages.config`, pokud se nepoužívá `OutputDirectory` nebo `SolutionDirectory`. |
| Project2ProjectTimeOut | Časový limit v sekundách pro řešení odkazů mezi projekty. |
| zahrnout | *(4.0 +)* Obnoví všechny odkazy na projekty UWP a .NET Core. Neplatí pro projekty používající `packages.config`. |
| RequireConsent | Ověřuje, jestli je před stažením a instalací balíčků povolený obnovování balíčků. Podrobnosti najdete v tématu věnovaném [obnovení balíčků](../../consume-packages/package-restore.md). |
| SolutionDirectory | Určuje složku řešení. Neplatný při obnovování balíčků pro řešení. Vyžaduje se při obnovení souboru `packages.config`, pokud se nepoužívá `PackagesDirectory` nebo `OutputDirectory`. |
| Zdroj | Určuje seznam zdrojů balíčků (jako adresy URL), které se mají použít pro obnovení. Pokud tento příkaz vynecháte, použije se zdroje zadané v konfiguračních souborech, viz téma [Konfigurace chování NuGet](../../consume-packages/configuring-nuget-behavior.md). K oddělení položek seznamu použijte středník. |
| Ode | V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné. Zadání tohoto příznaku se podobá odstranění souboru `project.assets.json`. To neobejde mezipaměť HTTP-cache. |
| Podrobnosti | Určuje množství podrobností zobrazených ve výstupu: *normální*, *tiché*a *podrobné*. |

Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .

## <a name="remarks"></a>Poznámky

Příkaz Restore provede následující kroky:

1. Určete režim operace příkazu Restore.

   | typ souboru projectPath | Předvídatelně |
   | --- | --- |
   | Řešení (složka) | NuGet vyhledá soubor `.sln` a použije ho, pokud se našel. v opačném případě obsahuje chybu. jako spouštěcí složka se používá `(SolutionDir)\.nuget`. |
   | soubor `.sln` | Obnovit balíčky identifikované řešením; obsahuje chybu, pokud se používá `-SolutionDirectory`. jako spouštěcí složka se používá `$(SolutionDir)\.nuget`. |
   | `packages.config` nebo soubor projektu | Obnovte balíčky uvedené v souboru, vyřešte je a nainstalujte závislosti. |
   | Jiný typ souboru | Předpokládá se, že se jedná o soubor `.sln`, jak je uvedeno výše. Pokud se nejedná o řešení, NuGet vyvolá chybu. |
   | (projectPath není zadáno) | <ul><li>NuGet vyhledá soubory řešení v aktuální složce. Pokud se najde jeden soubor, použije se k obnovení balíčků. Pokud je nalezeno více řešení, NuGet vyvolá chybu.</li><li>Pokud neexistují žádné soubory řešení, NuGet vyhledá `packages.config` a použije ho k obnovení balíčků.</li><li>Pokud se nenajde žádné řešení ani soubor `packages.config`, NuGet vyvolá chybu.</ul> |

2. Určení složky balíčků pomocí následujícího pořadí priorit (Pokud žádná z těchto složek nenalezne, vyvolá chybu NuGet):

    - Složka zadaná s `-PackagesDirectory`.
    - Hodnota `repositoryPath` v `Nuget.Config`
    - Složka zadaná s `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. Při obnovování balíčků pro řešení provede NuGet následující:
    - Načte soubor řešení.
    - Obnoví balíčky na úrovni řešení uvedené v `$(SolutionDir)\.nuget\packages.config` do složky `packages`.
    - Obnovte balíčky uvedené v `$(ProjectDir)\packages.config` do složky `packages`. U každého zadaného balíčku obnovte balíček paralelně, pokud není zadaný parametr `-DisableParallelProcessing`.

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
