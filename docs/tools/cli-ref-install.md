---
title: Instalace rozhraní příkazového řádku NuGet
description: Referenční informace pro příkaz install nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8088c6dcb7d453650950c219e1cc4dd047a64417
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425998"
---
# <a name="install-command-nuget-cli"></a>Příkaz install (NuGet CLI)

**Platí pro:** balíček spotřeby &bullet; **podporované verze:** všechny

Stáhne a nainstaluje balíček do projektu, jako výchozí se použije aktuální složku, pomocí zadaného balíčku zdroje.

> [!Tip]
> Chcete-li stáhnout balíček přímo mimo kontext projektu, navštivte stránku balíčku na [nuget.org](https://www.nuget.org) a vyberte **Stáhnout** odkaz.

Pokud nejsou zadány žádné zdroje, jsou uvedeny v souboru globální konfiguraci `%appdata%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), se používají. Zobrazit [konfigurace běžných NuGet](../consume-packages/configuring-nuget-behavior.md) další podrobnosti.

Pokud nejsou zadány žádné konkrétní balíčky, `install` nainstaluje všechny balíčky uvedené v projektu `packages.config` souboru, takže podobný [ `restore` ](cli-ref-restore.md).

`install` Příkaz neprovede žádné změny souboru projektu nebo `packages.config`; tímto způsobem je podobný `restore` , pouze na disk přidá balíčky ale nedojde ke změně závislosti projektu.

Můžete přidat závislost, přidejte balíček přes uživatelské rozhraní Správce balíčků nebo konzoly v sadě Visual Studio, nebo upravte `packages.config` a spustit některý `install` nebo `restore`.

## <a name="usage"></a>Použití

```cli
nuget install <packageID | configFilePath> [options]
```

kde `<packageID>` názvy balíček nainstalovat (pomocí nejnovější verze), nebo `<configFilePath>` identifikuje `packages.config` soubor, který uvádí balíčky pro instalaci. Můžete určit konkrétní verzi s `-Version` možnost.

## <a name="options"></a>Možnosti

| Možnost | Popis |
| --- | --- |
| ConfigFile | Konfigurační soubor NuGet použít. Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.|
| DependencyVersion | *(4.4 +)*  Verzi závislosti balíčků chcete použít, které může být jedna z následujících akcí:<br/><ul><li>*Nejnižší* (výchozí): nejnižší verze</li><li>*HighestPatch*: verze s nejnižší hlavní, vedlejší nejnižší, nejvyšší oprava</li><li>*HighestMinor*: verze s hlavní nejnižší, nejvyšší podverze, nejvyšší oprava</li><li>*Nejvyšší*: nejvyšší verze</li></ul> |
| DisableParallelProcessing | Zakáže instalaci více balíčků paralelně. |
| ExcludeVersion | Nainstaluje balíček do složky s názvem se pouze název balíčku, nikoli číslo verze. |
| FallbackSource | *(3.2 +)*  Seznam zdrojů balíčků, které má být použit jako náhrad balíček nebyl nalezen v primární nebo výchozí zdroj. |
| ForceEnglishOutput | *(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze. |
| Rozhraní .NET Framework | *(4.4 +)*  Cílové rozhraní framework slouží k výběru závislosti. Výchozí hodnota je "Žádný" Pokud nejsou zadané. |
| Help | Zobrazí nápovědu pro příkaz. |
| NoCache | Brání použití mezipaměti balíčků NuGet. Zobrazit [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Potlačí vyzve k zadání uživatele o vstup ani potvrzení. |
| OutputDirectory | Určuje složku, ve kterém jsou nainstalované balíčky. Pokud není zadána žádná složka, použije se aktuální složce. |
| PackageSaveMode | Určuje typy souborů, uložte po instalaci balíčku: jeden z `nuspec`, `nupkg`, nebo `nuspec;nupkg`. |
| Platnost předběžné verze | Umožňuje předběžné verze balíčků k instalaci. Tento příznak není vyžadován obnovují se balíčky s `packages.config`. |
| RequireConsent | Ověří, zda je povoleno obnovují se balíčky před stažením a instalací balíčků. Podrobnosti najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md). |
| SolutionDirectory | Určuje kořenovou složku řešení, pro které se mají balíčky obnovit. |
| Source | Určuje seznam zdrojů balíčků (jako adresy URL) používat. Pokud tento parametr vynechán, příkaz používá zdroje k dispozici v konfiguračních souborech naleznete v tématu [konfigurace běžných NuGet](../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*. |
| Version | Určuje verzi balíčku pro instalaci. |

Viz také [proměnné prostředí](cli-ref-environment-variables.md)

## <a name="examples"></a>Příklady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
