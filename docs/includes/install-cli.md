---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610535"
---
#### <a name="windows"></a><span data-ttu-id="4eaa8-101">Windows</span><span class="sxs-lookup"><span data-stu-id="4eaa8-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="4eaa8-102">NuGet. exe 5,0 a novější vyžaduje spuštění .NET Framework 4.7.2 nebo novějším.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="4eaa8-103">Přejděte na [NuGet.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3,3 nebo vyšší (2.8.6 není kompatibilní s mono).</span><span class="sxs-lookup"><span data-stu-id="4eaa8-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="4eaa8-104">Nejnovější verze se vždycky doporučuje a k publikování balíčků do nuget.org se vyžaduje 4.1.0 +.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="4eaa8-105">Každé stažení je `nuget.exe` soubor přímo.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="4eaa8-106">Řekněte prohlížeči, aby soubor uložil do složky podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="4eaa8-107">Soubor *není instalační* program. Pokud ji spustíte přímo z prohlížeče, nezobrazí se žádná.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="4eaa8-108">Přidejte složku, do které jste umístili `nuget.exe` do proměnné prostředí PATH pro použití nástroje CLI odkudkoli.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="4eaa8-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="4eaa8-109">macOS/Linux</span></span>

<span data-ttu-id="4eaa8-110">V případě distribuce operačního systému se může chování mírně lišit.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="4eaa8-111">Nainstalujte [mono 4.4.2 nebo novější](https://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="4eaa8-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="4eaa8-112">Na příkazovém řádku prostředí spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="4eaa8-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="4eaa8-113">Vytvořte alias přidáním následujícího skriptu do příslušného souboru pro váš operační systém (obvykle `~/.bash_aliases` nebo `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="4eaa8-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="4eaa8-114">Znovu načtěte prostředí.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-114">Reload the shell.</span></span>  <span data-ttu-id="4eaa8-115">Otestujte instalaci zadáním `nuget` bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="4eaa8-116">Měla by se zobrazit Help CLI NuGet.</span><span class="sxs-lookup"><span data-stu-id="4eaa8-116">NuGet CLI help should display.</span></span>
