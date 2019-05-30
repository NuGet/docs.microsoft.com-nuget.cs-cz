---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271499"
---
#### <a name="windows"></a><span data-ttu-id="e2474-101">Windows</span><span class="sxs-lookup"><span data-stu-id="e2474-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="e2474-102">NuGet.exe 5.0 nebo novější vyžaduje rozhraní .NET Framework 4.7.2 nebo později ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="e2474-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="e2474-103">Navštivte [nuget.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3.3 nebo novější (2.8.6 přílohy není kompatibilní s Mono).</span><span class="sxs-lookup"><span data-stu-id="e2474-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="e2474-104">Doporučujeme vždy na nejnovější verzi a 4.1.0+ je potřeba publikovat balíčky nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e2474-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="e2474-105">Každý soubor ke stažení je `nuget.exe` přímo soubor.</span><span class="sxs-lookup"><span data-stu-id="e2474-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="e2474-106">Dáte pokyn, aby prohlížeč k uložení souboru do složky podle vašeho výběru.</span><span class="sxs-lookup"><span data-stu-id="e2474-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="e2474-107">Soubor je *není* příslušný instalační program; vám nic neuvidí, je-li spustit přímo z prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="e2474-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="e2474-108">Přidat složku, kam jste umístili `nuget.exe` do proměnné prostředí PATH použít nástroj příkazového řádku z libovolného místa.</span><span class="sxs-lookup"><span data-stu-id="e2474-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="e2474-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="e2474-109">macOS/Linux</span></span>

<span data-ttu-id="e2474-110">Chování se může mírně lišit podle distribuce operačního systému.</span><span class="sxs-lookup"><span data-stu-id="e2474-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="e2474-111">Nainstalujte [Mono 4.4.2 nebo novější](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="e2474-111">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="e2474-112">Spuštěním následujícího příkazu v příkazovém řádku shell:</span><span class="sxs-lookup"><span data-stu-id="e2474-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="e2474-113">Vytvořit alias, přidejte následující skript k příslušnému souboru pro váš operační systém (obvykle `~/.bash_aliases` nebo `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="e2474-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="e2474-114">Znovu načte prostředí.</span><span class="sxs-lookup"><span data-stu-id="e2474-114">Reload the shell.</span></span>  <span data-ttu-id="e2474-115">Otestujte instalaci tak, že zadáte `nuget` bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="e2474-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="e2474-116">Zobrazit nápovědu příkazového řádku NuGet.</span><span class="sxs-lookup"><span data-stu-id="e2474-116">NuGet CLI help should display.</span></span>
