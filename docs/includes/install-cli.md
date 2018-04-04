#### <a name="windows"></a><span data-ttu-id="0980d-101">Windows</span><span class="sxs-lookup"><span data-stu-id="0980d-101">Windows</span></span>
1. <span data-ttu-id="0980d-102">Navštivte [nuget.org/downloads](https://nuget.org/downloads) a vyberte NuGet 3.3 nebo vyšší (2.8.6 přílohy není kompatibilní s Mono).</span><span class="sxs-lookup"><span data-stu-id="0980d-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="0980d-103">Vždy doporučujeme nejnovější verzi a 4.1.0+ je potřeba publikovat balíčky do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0980d-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="0980d-104">Každého stažení je `nuget.exe` souboru přímo.</span><span class="sxs-lookup"><span data-stu-id="0980d-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="0980d-105">Určit, aby váš prohlížeč k uložení souboru do složky podle svého výběru.</span><span class="sxs-lookup"><span data-stu-id="0980d-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="0980d-106">Soubor je *není* na instalační program; nic nebude zobrazeno, pokud ho spustit přímo z prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="0980d-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="0980d-107">Přidat složku, kam jste umístili `nuget.exe` do vaší proměnné prostředí PATH použít nástroj příkazového řádku z libovolného místa.</span><span class="sxs-lookup"><span data-stu-id="0980d-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="0980d-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="0980d-108">macOS/Linux</span></span>
<span data-ttu-id="0980d-109">Chování se může mírně liší podle operačního systému distribučního.</span><span class="sxs-lookup"><span data-stu-id="0980d-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="0980d-110">Nainstalujte [Mono 4.4.2 nebo novější](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="0980d-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="0980d-111">Spuštěním následujících příkazů v řádku prostředí:</span><span class="sxs-lookup"><span data-stu-id="0980d-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="0980d-112">Vytvořte alias přidáním následující skript k příslušnému souboru pro váš operační systém (obvykle `~/.bash_aliases` nebo `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="0980d-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="0980d-113">Znovu načte prostředí.</span><span class="sxs-lookup"><span data-stu-id="0980d-113">Reload the shell.</span></span>  <span data-ttu-id="0980d-114">Testování instalace zadáním `nuget` bez parametrů.</span><span class="sxs-lookup"><span data-stu-id="0980d-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="0980d-115">Rozhraní příkazového řádku NuGet nápovědy má zobrazit.</span><span class="sxs-lookup"><span data-stu-id="0980d-115">NuGet CLI help should display.</span></span>