---
title: Odkaz na NuGet rozhraní příkazového řádku (CLI)
description: Odkaz na příkazový řádek indexu pro rozhraní příkazového řádku nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: a257dbbd9d56b5989e050ed4096d096cd1036184
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426026"
---
# <a name="nuget-cli-reference"></a>Referenční dokumentace rozhraní příkazového řádku NuGet

NuGet rozhraní příkazového řádku (CLI), `nuget.exe`, umožňuje plném rozsahu funkcí NuGet k instalaci, vytvářet, publikovat a spravovat balíčky bez provedení změn v souborech projektu.

Pokud chcete použít jakýkoli příkaz, otevřete okno příkazového řádku nebo prostředí bash a potom spusťte `nuget` následovaný příkazu a vhodné možnosti, například `nuget help pack` (Chcete-li zobrazit nápovědu k příkazu pack).

Tato dokumentace je promítnuto nejnovější verzi rozhraní příkazového řádku NuGet. Kterém najdete přesné informace pro danou verzi, který používáte, spusťte `nuget help` požadovaného příkazu.

Další informace o použití základních příkazů s `nuget.exe` rozhraní příkazového řádku, naleznete v tématu [nainstalovat a používat balíčky pomocí rozhraní příkazového řádku nuget.exe](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalace nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Chcete-li k dispozici v rámci konzoly Správce balíčků NuGet rozhraní příkazového řádku v sadě Visual Studio, naleznete v tématu [pomocí nuget.exe rozhraní příkazového řádku v konzole](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Dostupnost

Zobrazit [dostupnost funkcí](../install-nuget-client-tools.md#feature-availability) najdete přesné informace.

- Všechny příkazy jsou k dispozici na Windows.
- Všechny příkazy pracovat nuget.exe systémem Mono, pokud není uvedeno pro jinak `pack`, `restore`, a `update`.
- `pack`, `restore`, `delete`, `locals`, A `push` příkazy jsou dostupné i na Mac a Linux přes rozhraní příkazového řádku dotnet.

## <a name="commands-and-applicability"></a>Příkazy a použitelnost.

Dostupné příkazy a použitelnost pro vytvoření balíčku, využití balíčků a publikování balíčku na hostitele:

| Běžné příkazy | Příslušné role | NuGet Version | Popis |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Vytvoření | 2.7+ | Vytvoří balíček NuGet `.nuspec` nebo soubor projektu. Při spouštění v Mono, vytvoření balíčku ze souboru projektu se nepodporuje. |
| [push](cli-ref-push.md) | Publikování | Všechny | Publikuje balíček ke zdroji balíčku. |
| [config](cli-ref-config.md) | Všechny | Všechny | Získá nebo nastaví NuGet konfigurační hodnoty. |
| [help or ?](cli-ref-help.md) | Všechny | Všechny | Zobrazí nápovědu informace a nápovědu pro příkaz. |
| [locals](cli-ref-locals.md) | Využití | 3.3+ | Uvádí umístění *global-packages*, *http-cache*, a *temp* složky a vymaže obsah těchto složek. |
| [restore](cli-ref-restore.md) | Využití | 2.7+ | Obnoví všechny balíčky, které odkazuje formát správy balíčků, které používá. Při spouštění v Mono, obnovení balíčků pomocí PackageReference formátu není podporováno. |
| [setapikey](cli-ref-setapikey.md) | Publikování, spotřeby | Všechny | Uloží klíč rozhraní API pro zdroj daného balíčku zdroje tohoto balíčku vyžaduje klíče pro přístup. |
| [spec](cli-ref-spec.md) | Vytvoření | Všechny | Generuje `.nuspec` soubor, pokud soubor se generuje z projektu sady Visual Studio pomocí tokenů. |

| Sekundární příkazy | Příslušné role | NuGet Version | Popis |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Publikování | 3.3+ | Přidá balíček ke zdroji balíčku jiným protokolem než HTTP pomocí hierarchickém rozložení. Pro HTTP zdroji, použijte *nabízených*. |
| [delete](cli-ref-delete.md) | Publikování | Všechny | Odebere nebo unlists balíčku ze zdroje balíčku. |
| [init](cli-ref-init.md) | Vytvoření | 3.3+ | Přidá balíčky ze složky ke zdroji balíčku pomocí hierarchickém rozložení. |
| [install](cli-ref-install.md) | Využití | Všechny | Nainstaluje balíček do aktuálního projektu, ale projekty nebo neodkazuje na soubory. |
| [list](cli-ref-list.md) | Využití, například publikování | Všechny | Zobrazí balíčky z daného zdroje. |
| [mirror](cli-ref-mirror.md) | Publikování | Zastaralé v 3.2 + | Odráží balíček a jeho závislé položky ze zdroje do cílového úložiště. |
| [sources](cli-ref-sources.md) | Spotřeba, publikování | Všechny | Spravuje zdroje balíčků v konfiguračních souborech. |
| [update](cli-ref-update.md) | Využití | Všechny | Projektu balíčky aktualizací na nejnovější dostupné verze. Nejsou podporovány při spouštění v Mono. |

Ujistěte se, různé příkazy pomocí různých [proměnné prostředí](cli-ref-environment-variables.md).

Příkazy rozhraní příkazového řádku NuGet příslušné role:

| Role | Příkazy |
| --- | --- |
| Využití | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Vytvoření | `config`, `help`, `init`, `pack`, `spec` |
| Publikování | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Vývojáři týká pouze využívání balíčků, například potřebovat jenom pochopit tuto dílčí příkazy pro balíčky NuGet.

> [!Note]
> Názvy možností příkazu jsou malá a velká písmena. Možnosti, které jsou zastaralé nejsou součástí tohoto odkazu, například `NoPrompt` (nahrazuje `NonInteractive`) a `Verbose` (nahrazuje `Verbosity`).
