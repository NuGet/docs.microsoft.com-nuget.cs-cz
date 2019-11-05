---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610535"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet. exe 5,0 a novější vyžaduje spuštění .NET Framework 4.7.2 nebo novějším.

1. Přejděte na [NuGet.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3,3 nebo vyšší (2.8.6 není kompatibilní s mono). Nejnovější verze se vždycky doporučuje a k publikování balíčků do nuget.org se vyžaduje 4.1.0 +.
1. Každé stažení je `nuget.exe` soubor přímo. Řekněte prohlížeči, aby soubor uložil do složky podle vašeho výběru. Soubor *není instalační* program. Pokud ji spustíte přímo z prohlížeče, nezobrazí se žádná.
1. Přidejte složku, do které jste umístili `nuget.exe` do proměnné prostředí PATH pro použití nástroje CLI odkudkoli.

#### <a name="macoslinux"></a>macOS/Linux

V případě distribuce operačního systému se může chování mírně lišit.

1. Nainstalujte [mono 4.4.2 nebo novější](https://www.mono-project.com/docs/getting-started/install/).

1. Na příkazovém řádku prostředí spusťte následující příkaz:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Vytvořte alias přidáním následujícího skriptu do příslušného souboru pro váš operační systém (obvykle `~/.bash_aliases` nebo `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Znovu načtěte prostředí.  Otestujte instalaci zadáním `nuget` bez parametrů. Měla by se zobrazit Help CLI NuGet.
