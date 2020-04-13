---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610535"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 a novější vyžadují .NET Framework 4.7.2 nebo novější ke spuštění.

1. Navštivte [nuget.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3.3 nebo vyšší (2.8.6 není kompatibilní s Mono). Vždy se doporučuje nejnovější verze a 4.1.0+ je nutné publikovat balíčky do nuget.org.
1. Každé stahování `nuget.exe` je soubor přímo. Nařiďte prohlížeči, aby soubor uložil do vybrané složky. Soubor *není* instalačníprogram; pokud jej spustíte přímo z prohlížeče, nic neuvidíte.
1. Přidejte složku, `nuget.exe` do které jste umístili proměnnou prostředí PATH, abyste použili nástroj cli odkudkoli.

#### <a name="macoslinux"></a>macOS/Linux

Chování se může mírně lišit podle distribuce operačního systému.

1. Nainstalujte [Mono 4.4.2 nebo novější](https://www.mono-project.com/docs/getting-started/install/).

1. Na řádku prostředí proveďte následující příkaz:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Vytvořte alias přidáním následujícího skriptu do příslušného `~/.bash_aliases` souboru operačního systému (obvykle nebo `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Znovu nabijte granát.  Otestujte instalaci `nuget` zadáním bez parametrů. NuGet CLI nápověda by se měla zobrazit.
