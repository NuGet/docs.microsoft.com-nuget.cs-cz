---
title: Reference k rozhraní příkazového řádku NuGet (CLI)
description: Rejstřík odkazů příkazového řádku pro nuget.exe CLI
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: e9343f1fdddcf839322849925372587e685aef4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623146"
---
# <a name="nuget-cli-reference"></a>Reference k NuGet CLI

Rozhraní příkazového řádku NuGet (CLI), `nuget.exe` poskytuje kompletní rozsah funkcí NuGet pro instalaci, vytváření, publikování a správu balíčků bez provedení změn v souborech projektu.

Chcete-li použít libovolný příkaz, otevřete okno příkazového řádku nebo prostředí bash `nuget` a potom spusťte příkaz a příslušné možnosti, například `nuget help pack` (pro zobrazení pomocníka v příkazu Pack).

Tato dokumentace odráží nejnovější verzi rozhraní příkazového řádku NuGet. Přesné podrobnosti o libovolné verzi, kterou používáte, získáte spuštěním `nuget help` příkazu pro požadovaný příkaz.

Informace o tom, jak používat základní příkazy s rozhraním `nuget.exe` příkazového řádku, najdete v tématu [instalace a použití balíčků pomocí nuget.exe CLI](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Instalace nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Chcete-li zpřístupnit CLI NuGet v rámci konzoly Správce balíčků v sadě Visual Studio, přečtěte si téma [použití nuget.exe CLI v konzole](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Dostupnost

Přesné podrobnosti najdete v tématu [Dostupnost funkce](../install-nuget-client-tools.md#feature-availability) .

- Všechny příkazy jsou k dispozici ve Windows.
- Všechny příkazy pracují s nuget.exe běžící na mono s výjimkou případů `pack` , kde jsou uvedeny pro, `restore` a `update` .
- `pack`Příkazy, `restore` , `delete` , `locals` a `push` jsou také k dispozici v systémech Mac a Linux prostřednictvím rozhraní příkazového řádku dotnet.

## <a name="commands-and-applicability"></a>Příkazy a použitelnost

Dostupné příkazy a použitelnost při vytváření balíčků, spotřebě balíčků nebo publikování balíčku na hostitele:

| Běžné příkazy | Příslušné role | Verze NuGet | Popis |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Vytvoření | 2.7 + | Vytvoří balíček NuGet ze `.nuspec` souboru nebo projektu. Při spuštění na mono se nepodporuje vytváření balíčku ze souboru projektu. |
| [push](cli-reference/cli-ref-push.md) | Publikování | Vše | Publikuje balíček do zdroje balíčku. |
| [config](cli-reference/cli-ref-config.md) | Vše | Vše | Získá nebo nastaví hodnoty konfigurace NuGet. |
| [help or ?](cli-reference/cli-ref-help.md) | Vše | Vše | Zobrazí nápovědu nebo nápovědu k příkazu. |
| [locals](cli-reference/cli-ref-locals.md) | Consumption | 3.3 + | Zobrazí seznam umístění *globálních balíčků*, *HTTP cache*a *dočasných* složek a vymaže obsah těchto složek. |
| [restore](cli-reference/cli-ref-restore.md) | Consumption | 2.7 + | Obnoví všechny balíčky, na které odkazuje formát správy balíčků, který se používá. Při spuštění na mono se nepodporuje obnovení balíčků pomocí formátu PackageReference. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Publikování, spotřeba | Vše | Uloží klíč rozhraní API pro daný zdroj balíčku, když tento zdroj balíčku vyžaduje klíč pro přístup. |
| [spec](cli-reference/cli-ref-spec.md) | Vytvoření | Vše | Vygeneruje `.nuspec` soubor pomocí tokenů při generování souboru z projektu sady Visual Studio. |

| Sekundární příkazy | Příslušné role | Verze NuGet | Popis |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Publikování | 3.3 + | Přidá balíček do zdroje balíčků jiného typu než HTTP pomocí hierarchického rozložení. Pro zdroje HTTP použijte *push*. |
| [delete](cli-reference/cli-ref-delete.md) | Publikování | Vše | Odebere nebo zruší výpis balíčku ze zdroje balíčku. |
| [init](cli-reference/cli-ref-init.md) | Vytvoření | 3.3 + | Přidá balíčky ze složky do zdroje balíčku pomocí hierarchického rozložení. |
| [install](cli-reference/cli-ref-install.md) | Consumption | Vše | Nainstaluje balíček do aktuálního projektu, ale neupraví projekty ani referenční soubory. |
| [list](cli-reference/cli-ref-list.md) | Spotřeba, možná publikování | Vše | Zobrazí balíčky z daného zdroje. |
| [mirror](cli-reference/cli-ref-mirror.md) | Publikování | Zastaralé v 3.2 + | Zrcadlí balíček a jeho závislosti ze zdroje do cílového úložiště. |
| [nápovědě](cli-reference/cli-ref-search.md) | Consumption | 5.8 + | Vyhledá zadaný zdroj pomocí zadaného řetězce dotazu. |
| [sources](cli-reference/cli-ref-sources.md) | Spotřeba, publikování | Vše | Spravuje zdroje balíčků v konfiguračních souborech. |
| [update](cli-reference/cli-ref-update.md) | Consumption | Vše | Aktualizuje balíčky projektu na nejnovější dostupné verze. Nepodporováno při spuštění v mono. |

Různé příkazy využívají různé [proměnné prostředí](cli-reference/cli-ref-environment-variables.md).

Příkazy NuGet CLI podle použitelných rolí:

| Role | Příkazy |
| --- | --- |
| Consumption | `config`, `help`, `install`, `list`, `locals`, `restore`, `search`, `setapikey`, `sources`, `update` |
| Vytvoření | `config`, `help`, `init`, `pack`, `spec` |
| Publikování | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Vývojáři, kteří mají obavy jenom s využitím balíčků, potřebují pochopit jenom tuto podmnožinu příkazů NuGet.

> [!Note]
> V názvech možností příkazu se nerozlišují malá a velká písmena. Nepoužívané možnosti nejsou zahrnuté do tohoto odkazu, jako je například `NoPrompt` (nahrazeno `NonInteractive` ) a `Verbose` (nahrazeno `Verbosity` ).
