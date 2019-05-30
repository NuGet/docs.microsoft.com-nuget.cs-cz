---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271499"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 nebo novější vyžaduje rozhraní .NET Framework 4.7.2 nebo později ke spuštění.

1. Navštivte [nuget.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3.3 nebo novější (2.8.6 přílohy není kompatibilní s Mono). Doporučujeme vždy na nejnovější verzi a 4.1.0+ je potřeba publikovat balíčky nuget.org.
1. Každý soubor ke stažení je `nuget.exe` přímo soubor. Dáte pokyn, aby prohlížeč k uložení souboru do složky podle vašeho výběru. Soubor je *není* příslušný instalační program; vám nic neuvidí, je-li spustit přímo z prohlížeče.
1. Přidat složku, kam jste umístili `nuget.exe` do proměnné prostředí PATH použít nástroj příkazového řádku z libovolného místa.

#### <a name="macoslinux"></a>macOS/Linux

Chování se může mírně lišit podle distribuce operačního systému.

1. Nainstalujte [Mono 4.4.2 nebo novější](http://www.mono-project.com/docs/getting-started/install/).

1. Spuštěním následujícího příkazu v příkazovém řádku shell:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Vytvořit alias, přidejte následující skript k příslušnému souboru pro váš operační systém (obvykle `~/.bash_aliases` nebo `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Znovu načte prostředí.  Otestujte instalaci tak, že zadáte `nuget` bez parametrů. Zobrazit nápovědu příkazového řádku NuGet.
