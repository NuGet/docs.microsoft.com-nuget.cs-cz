---
title: Referenční informace o NuGet rozhraní příkazového řádku (CLI)
description: Reference k příkazovému řádku index pro nuget.exe rozhraní příkazového řádku
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: ed91a31505ab1de9447cdbeb87c8ad08f7ba56d8
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-cli-reference"></a>Referenční dokumentace rozhraní příkazového řádku NuGet

NuGet rozhraní příkazového řádku (CLI) `nuget.exe`, poskytuje bude celkový rozsah funkcí NuGet k instalaci, vytvářet, publikovat a spravovat balíčky bez jakýchkoli změn souborů projektu.

Chcete-li používat všechny příkazy, otevřete okno příkazového řádku nebo prostředí bash a potom spusťte `nuget` následovaný příkazu a požadované možnosti, jako například `nuget help pack` (Chcete-li zobrazit nápovědu k příkazu pack).

Tato dokumentace odráží nejnovější verzi rozhraní příkazového řádku NuGet. Pro přesné podrobnosti libovolné dané verze, kterou používáte, spusťte `nuget help` pro požadovaný příkaz.

## <a name="installing-nugetexe"></a>Instalace nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Chcete-li k dispozici v konzoli správce balíčků NuGet příkazového řádku v sadě Visual Studio, najdete v části [pomocí nuget.exe rozhraní příkazového řádku v konzole](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Dostupnost

V tématu [dostupnost funkcí](../install-nuget-client-tools.md#feature-availability) najdete přesné informace.

- Všechny příkazy jsou k dispozici v systému Windows.
- Všechny příkazy pro práci s nuget.exe systémem Mono, pokud není uvedeno pro jinak `pack`, `restore`, a `update`.
- `pack`, `restore`, `delete`, `locals`, A `push` příkazy jsou také k dispozici na Mac a Linux pomocí rozhraní příkazového řádku dotnet.

## <a name="commands-and-applicability"></a>Příkazy a použitelnosti

Dostupné příkazy a použitelnost k vytvoření balíčku, balíčku spotřebu nebo publikování balíčku na hostitele:

| Běžné příkazy | Platných rolí | Verze NuGet | Popis |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Vytvoření | 2.7+ | Vytvoří z balíčku NuGet `.nuspec` nebo soubor projektu. Při spuštění na Mono, vytváření balíčku ze souboru projektu není podporován. |
| [push](cli-ref-push.md) | Publikování | Všechny | Publikuje balíček ke zdroji balíčku. |
| [config](cli-ref-config.md) | Všechny | Všechny | Získá nebo nastaví hodnoty konfigurace NuGet. |
| [help nebo ?](cli-ref-help.md) | Všechny | Všechny | Zobrazí nápovědu informace nebo nápovědu pro příkaz. |
| [locals](cli-ref-locals.md) | Spotřeba | 3.3+ | Uvádí umístění *globální balíčky*, *http mezipaměti*, a *temp* složek a vymaže obsah těchto složek. |
| [restore](cli-ref-restore.md) | Spotřeba | 2.7+ | Obnoví všechny balíčky odkazuje formátu balíček správy používá. Při spuštění na Mono, Probíhá obnovení balíčků formátu PackageReference není podporována. |
| [setapikey](cli-ref-setapikey.md) | Publikování, spotřeba | Všechny | Pokud tento zdroj balíčku vyžaduje klíče pro přístup, uloží klíč rozhraní API pro zdroj daného balíčku. |
| [spec](cli-ref-spec.md) | Vytvoření | Všechny | Generuje `.nuspec` souboru pomocí tokenů, je-li generování souboru z projektu sady Visual Studio. |

| Sekundární příkazy | Platných rolí | Verze NuGet | Popis |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publikování | 3.3+ | Přidá balíček ke zdroji balíčku jiným protokolem než HTTP pomocí hierarchickém rozložení. Pro HTTP zdrojů, použijte *nabízené*. |
| [delete](cli-ref-delete.md) | Publikování | Všechny | Odebere nebo unlists balíčku ze zdroje balíčku. |
| [init](cli-ref-init.md) | Vytvoření | 3.3+ | Přidá balíčky ze složky ke zdroji balíčku pomocí hierarchickém rozložení. |
| [install](cli-ref-install.md) | Spotřeba | Všechny | Nainstaluje balíček do aktuálního projektu, ale neupravuje projekty ani odkazovat soubory. |
| [list](cli-ref-list.md) | Využívání, případně publikování | Všechny | Zobrazí balíčky z daného zdroje. |
| [mirror](cli-ref-mirror.md) | Publikování | Zastaralé v 3.2 + | Odráží balíček a jeho závislé součásti ze zdroje do cílového úložiště. |
| [sources](cli-ref-sources.md) | Spotřeba, publikování | Všechny | Spravuje zdroje balíčků v konfiguračních souborech. |
| [update](cli-ref-update.md) | Spotřeba | Všechny | Projektu balíčky aktualizací na nejnovější verze k dispozici. Není podporováno, když se používá Mono. |

Ujistěte se, jiné příkazy použití různých [proměnné prostředí](cli-ref-environment-variables.md).

Příkazy rozhraní příkazového řádku NuGet příslušné role:

| Role | Příkazy |
| --- | --- |
| Spotřeba | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Vytvoření | `config`, `help`, `init`, `pack`, `spec` |
| Publikování | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Vývojáři pouze nevadí využívání balíčků, například potřebovat pouze pochopit tuto podmnožinu příkazy pro balíčky NuGet.

> [!Note]
> Příkaz možnost názvy jsou velká a malá písmena. Možnosti, které jsou zastaralé nejsou součástí tohoto odkazu, jako například `NoPrompt` (nahrazuje `NonInteractive`) a `Verbose` (nahrazuje `Verbosity`).
