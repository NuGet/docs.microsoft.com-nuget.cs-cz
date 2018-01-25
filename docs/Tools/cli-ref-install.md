---
title: "Příkaz instalovat NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nuget.exe instalace"
keywords: "nuget nainstalujte odkaz, nainstalujte balíček příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b77e0e6ce045d1a1e59b29f770b5aca13fc4e7e3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="install-command-nuget-cli"></a>nainstalovat příkaz (NuGet CLI)

**Platí pro:** balíček spotřeba &bullet; **podporované verze:** všechny

Stáhne a nainstaluje balíček do projektu, jako výchozí bude použit na aktuální složku, pomocí zadaného balíčku zdroje.

> [!Tip]
> Stažení balíčku přímo mimo kontext projektu, navštivte stránku balíčku na [nuget.org](https://www.nuget.org) a vyberte **Stáhnout** odkaz.

Pokud nejsou zadány žádné zdroje, ty uvedené v souboru globální konfiguraci `%APPDATA%\NuGet\NuGet.Config`, se používají. V tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md) další podrobnosti.

Pokud nejsou zadány žádné konkrétní balíčky, `install` nainstaluje všechny balíčky uvedené v projektu `packages.config` souboru, takže je podobná [ `restore` ](cli-ref-restore.md).

`install` Příkaz nedojde ke změně souboru projektu nebo `packages.config`; tímto způsobem je podobná `restore` v tom pouze přidá balíčky na disk ale nemění závislosti projektu.

Pokud chcete přidat závislost, přidejte projektu přes uživatelské rozhraní Správce balíčků nebo konzoly v sadě Visual Studio nebo upravit `packages.config` a spusťte buď `install` nebo `restore`.

## <a name="usage"></a>Použití

```cli
nuget install <packageID | configFilePath> [options]
```

kde `<packageID>` názvy balíček k instalaci (pomocí nejnovější verze), nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků, chcete-li nainstalovat. Můžete určit, na konkrétní verzi pomocí `-Version` možnost.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá. |
| DependencyVersion | *(4.4 +)*  Určuje konkrétní verzi, přepisování výchozího chování řešení závislostí. |
| DisableParallelProcessing | Zakáže instalaci více balíčků paralelně. |
| ExcludeVersion | Nainstaluje balíček do složky s názvem se pouze název balíčku a není číslo verze. |
| FallbackSource | *(3.2 +)*  Seznam zdroje balíčku pro použití jako případech přejít v případě, že daný balíček nebyl nalezen v primární nebo výchozí zdroj. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze. |
| Rozhraní .NET Framework | *(4.4 +)*  Cílovém Frameworku, který slouží k výběru závislosti. Výchozí hodnota je 'Libovolný' není-li zadána. |
| Nápověda | Zobrazí nápovědu pro příkaz. |
| NoCache | NuGet bránit v použití balíčky z mezipaměti místního počítače. |
| Neinteraktivní | Potlačí výzvy pro vstup uživatele nebo potvrzení. |
| Výstupnísložka | Určuje složku, ve kterém jsou nainstalované balíčky. Pokud není zadaný žádný složky, se používá aktuální složky. |
| PackageSaveMode | Určuje typy souborů, uložte po instalaci balíčku: jeden z `nuspec`, `nupkg`, nebo `nuspec;nupkg`. |
| Předběžné verze | Umožňuje předběžné verze balíčků k instalaci. Tento příznak není požadována, když probíhá obnovení balíčků s `packages.config`. |
| RequireConsent | Ověří, že probíhá obnovení balíčků je zapnutá před stažením a instalací balíčky. Podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md). |
| SolutionDirectory | Určuje kořenové složky řešení pro pro obnovení balíčků. |
| Zdroj | Určuje seznam zdrojů balíčku (jako adresy URL) používat. Pokud tento parametr vynechán, příkaz používá zdrojů, součástí konfigurační soubory, najdete v části [konfigurace NuGet chování](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Podrobnosti | Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*. |
| Version | Určuje verzi balíčku pro instalaci. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
