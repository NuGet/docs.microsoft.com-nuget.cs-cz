---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610535"
---
#### <a name="windows"></a><span data-ttu-id="287cd-101">Windows</span><span class="sxs-lookup"><span data-stu-id="287cd-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="287cd-102">NuGet.exe 5.0 a novější vyžadují .NET Framework 4.7.2 nebo novější ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="287cd-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="287cd-103">Navštivte [nuget.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3.3 nebo vyšší (2.8.6 není kompatibilní s Mono).</span><span class="sxs-lookup"><span data-stu-id="287cd-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="287cd-104">Vždy se doporučuje nejnovější verze a 4.1.0+ je nutné publikovat balíčky do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="287cd-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="287cd-105">Každé stahování `nuget.exe` je soubor přímo.</span><span class="sxs-lookup"><span data-stu-id="287cd-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="287cd-106">Nařiďte prohlížeči, aby soubor uložil do vybrané složky.</span><span class="sxs-lookup"><span data-stu-id="287cd-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="287cd-107">Soubor *není* instalačníprogram; pokud jej spustíte přímo z prohlížeče, nic neuvidíte.</span><span class="sxs-lookup"><span data-stu-id="287cd-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="287cd-108">Přidejte složku, `nuget.exe` do které jste umístili proměnnou prostředí PATH, abyste použili nástroj cli odkudkoli.</span><span class="sxs-lookup"><span data-stu-id="287cd-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="287cd-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="287cd-109">macOS/Linux</span></span>

<span data-ttu-id="287cd-110">Chování se může mírně lišit podle distribuce operačního systému.</span><span class="sxs-lookup"><span data-stu-id="287cd-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="287cd-111">Nainstalujte [Mono 4.4.2 nebo novější](https://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="287cd-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="287cd-112">Na řádku prostředí proveďte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="287cd-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="287cd-113">Vytvořte alias přidáním následujícího skriptu do příslušného `~/.bash_aliases` souboru operačního systému (obvykle nebo `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="287cd-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="287cd-114">Znovu nabijte granát.</span><span class="sxs-lookup"><span data-stu-id="287cd-114">Reload the shell.</span></span>  <span data-ttu-id="287cd-115">Otestujte instalaci `nuget` zadáním bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="287cd-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="287cd-116">NuGet CLI nápověda by se měla zobrazit.</span><span class="sxs-lookup"><span data-stu-id="287cd-116">NuGet CLI help should display.</span></span>
