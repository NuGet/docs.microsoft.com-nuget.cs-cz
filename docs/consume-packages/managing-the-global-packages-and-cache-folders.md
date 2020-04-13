---
title: Jak spravovat globální balíčky, cache, dočasné složky v NuGet
description: Jak spravovat globální instalační složku balíčku, mezipaměť balíčků a dočasné složky, které existují v počítači a které se používají při instalaci, obnovení a aktualizaci balíčků.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428966"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="bd207-103">Správa globálních balíčků, mezipaměti a dočasných složek</span><span class="sxs-lookup"><span data-stu-id="bd207-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="bd207-104">Kdykoli nainstalujete, aktualizujete nebo obnovíte balíček, nuget spravuje balíčky a informace o balíčku v několika složkách mimo strukturu projektu:</span><span class="sxs-lookup"><span data-stu-id="bd207-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="bd207-105">Name (Název)</span><span class="sxs-lookup"><span data-stu-id="bd207-105">Name</span></span> | <span data-ttu-id="bd207-106">Popis a umístění (na uživatele)</span><span class="sxs-lookup"><span data-stu-id="bd207-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="bd207-107">globální&#8209;balíčky</span><span class="sxs-lookup"><span data-stu-id="bd207-107">global&#8209;packages</span></span> | <span data-ttu-id="bd207-108">Složka *globální balíčky* je místo, kde NuGet nainstaluje všechny stažené balíček.</span><span class="sxs-lookup"><span data-stu-id="bd207-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="bd207-109">Každý balíček je plně rozbalen do podsložky, která odpovídá identifikátoru balíčku a číslo verze.</span><span class="sxs-lookup"><span data-stu-id="bd207-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="bd207-110">Projekty používající formát [PackageReference](package-references-in-project-files.md) vždy používají balíčky přímo z této složky.</span><span class="sxs-lookup"><span data-stu-id="bd207-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="bd207-111">Při použití [souboru packages.config](../reference/packages-config.md)jsou balíčky nainstalovány do složky *globálních balíčků* a poté zkopírovány do `packages` složky projektu.</span><span class="sxs-lookup"><span data-stu-id="bd207-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="bd207-112">Windows:`%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="bd207-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="bd207-113">Mac/Linux:`~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="bd207-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="bd207-114">Přepsat `globalPackagesFolder` pomocí proměnné NUGET_PACKAGES prostředí, `repositoryPath` nastavení nebo [konfigurace](../reference/nuget-config-file.md#config-section) (při použití PackageReference a `packages.config`, příslušně) nebo `RestorePackagesPath` MSBuild vlastnost (Pouze MSBuild).</span><span class="sxs-lookup"><span data-stu-id="bd207-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="bd207-115">Proměnná prostředí má přednost před nastavením konfigurace.</span><span class="sxs-lookup"><span data-stu-id="bd207-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="bd207-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="bd207-116">http&#8209;cache</span></span> | <span data-ttu-id="bd207-117">Visual Studio Package Manager (NuGet 3.x+) a `dotnet` nástroj ukládat kopie stažených balíčků v této mezipaměti (uložené jako `.dat` soubory), uspořádané do podsložek pro každý zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="bd207-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="bd207-118">Balíčky nejsou rozbaleny a mezipaměť má dobu vypršení platnosti 30 minut.</span><span class="sxs-lookup"><span data-stu-id="bd207-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="bd207-119">Windows:`%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="bd207-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="bd207-120">Mac/Linux:`~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="bd207-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="bd207-121">Přepsat pomocí proměnné prostředí NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="bd207-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="bd207-122">Temp</span><span class="sxs-lookup"><span data-stu-id="bd207-122">temp</span></span> | <span data-ttu-id="bd207-123">Složka, kde NuGet ukládá dočasné soubory během různých operací.</span><span class="sxs-lookup"><span data-stu-id="bd207-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="bd207-124">Windows:`%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="bd207-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="bd207-125">Mac/Linux:`/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="bd207-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="bd207-126">pluginy-cache **4,8+**</span><span class="sxs-lookup"><span data-stu-id="bd207-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="bd207-127">Složka, kde NuGet ukládá výsledky z požadavku deklarace identity operace.</span><span class="sxs-lookup"><span data-stu-id="bd207-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="bd207-128">Windows:`%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="bd207-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="bd207-129">Mac/Linux:`~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="bd207-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="bd207-130">Přepsat pomocí proměnné NUGET_PLUGINS_CACHE_PATH prostředí.</span><span class="sxs-lookup"><span data-stu-id="bd207-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="bd207-131">NuGet 3.5 a starší používá *balíčky cache* namísto *http-cache*, který je umístěn v `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="bd207-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="bd207-132">Pomocí mezipaměti a *globální balíčky* složky NuGet obecně vyhýbá stahování balíčků, které již existují v počítači, zlepšení výkonu instalace, aktualizace a obnovení operací.</span><span class="sxs-lookup"><span data-stu-id="bd207-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="bd207-133">Při použití PackageReference, *globální balíčky* složky také zabraňuje udržování stažené balíčky uvnitř složky projektu, kde mohou být neúmyslně přidány do správy zdrojového kódu a snižuje Celkový dopad NuGet na úložiště počítače.</span><span class="sxs-lookup"><span data-stu-id="bd207-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="bd207-134">Když budete vyzváni k načtení balíčku, NuGet nejprve vyhledá ve složce *globální balíčky.*</span><span class="sxs-lookup"><span data-stu-id="bd207-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="bd207-135">Pokud přesná verze balíčku není k dispozici, pak NuGet zkontroluje všechny zdroje balíčku bez HTTP.</span><span class="sxs-lookup"><span data-stu-id="bd207-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="bd207-136">Pokud balíček stále nebyl nalezen, NuGet hledá balíček v `--no-cache` *http-cache,* `nuget.exe` pokud zadáte pomocí `dotnet.exe` příkazů nebo `-NoCache` s příkazy.</span><span class="sxs-lookup"><span data-stu-id="bd207-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="bd207-137">Pokud balíček není v mezipaměti nebo mezipaměti není použit, NuGet pak načte balíček přes HTTP .</span><span class="sxs-lookup"><span data-stu-id="bd207-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="bd207-138">Další informace naleznete v [tématu Co se stane, když je balíček nainstalován?](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="bd207-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="bd207-139">Zobrazení umístění složek</span><span class="sxs-lookup"><span data-stu-id="bd207-139">Viewing folder locations</span></span>

<span data-ttu-id="bd207-140">Umístění můžete zobrazit pomocí [příkazu nuget locals](../reference/cli-reference/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="bd207-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="bd207-141">Typický výstup (Windows; "user1" je aktuální uživatelské jméno):</span><span class="sxs-lookup"><span data-stu-id="bd207-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="bd207-142">(`package-cache` se používá v NuGet 2.x a zobrazí se s NuGet 3.5 a starší.)</span><span class="sxs-lookup"><span data-stu-id="bd207-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="bd207-143">Umístění složek můžete také zobrazit pomocí [příkazu dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="bd207-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="bd207-144">Typický výstup (Mac/Linux; "user1" je aktuální uživatelské jméno):</span><span class="sxs-lookup"><span data-stu-id="bd207-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="bd207-145">Chcete-li zobrazit umístění jedné `http-cache`složky, `plugins-cache` použijte `all`místo aplikace použití `global-packages`, `temp`, nebo .</span><span class="sxs-lookup"><span data-stu-id="bd207-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="bd207-146">Vymazání místních složek</span><span class="sxs-lookup"><span data-stu-id="bd207-146">Clearing local folders</span></span>

<span data-ttu-id="bd207-147">Pokud narazíte na problémy s instalací balíčku nebo chcete jinak zajistit, `locals --clear` že instalujete balíčky ze vzdálené galerie, použijte možnost (dotnet.exe) nebo `locals -clear` (nuget.exe) a určete složku, kterou chcete vymazat, nebo `all` vymazat všechny složky:</span><span class="sxs-lookup"><span data-stu-id="bd207-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="bd207-148">Všechny balíčky používané projekty, které jsou aktuálně otevřené v sadě Visual Studio nejsou vymazány ze složky *globální balíčky.*</span><span class="sxs-lookup"><span data-stu-id="bd207-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="bd207-149">Počínaje Visual Studio 2017, použijte **nástroje > NuGet Správce balíčků > nastavení správce balíčků,** pak vyberte **Vymazat všechny NuGet Cache (y)**.</span><span class="sxs-lookup"><span data-stu-id="bd207-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="bd207-150">Správa mezipaměti není v současné době k dispozici prostřednictvím konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="bd207-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="bd207-151">V sadě Visual Studio 2015 použijte příkazy příkazového příkazu.</span><span class="sxs-lookup"><span data-stu-id="bd207-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Příkaz možnosti NuGet pro vymazání mezipamětí](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="bd207-153">Řešení chyb</span><span class="sxs-lookup"><span data-stu-id="bd207-153">Troubleshooting errors</span></span>

<span data-ttu-id="bd207-154">Při použití `nuget locals` nebo `dotnet nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="bd207-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="bd207-155">*Chyba: Proces nemá přístup <package> k souboru, protože je používán jiným procesem* nebo *vymazáním místních prostředků se nezdařilo: Nelze odstranit jeden nebo více souborů.*</span><span class="sxs-lookup"><span data-stu-id="bd207-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="bd207-156">Jeden nebo více souborů ve složce jsou používány jiným procesem; Například je otevřený projekt sady Visual Studio, který odkazuje na balíčky ve složce *globální balíčky.*</span><span class="sxs-lookup"><span data-stu-id="bd207-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="bd207-157">Zavřete tyto procesy a akci opakujte.</span><span class="sxs-lookup"><span data-stu-id="bd207-157">Close those processes and try again.</span></span>

- <span data-ttu-id="bd207-158">*Chyba: Přístup k <path> cestě je odepřen* nebo *adresář není prázdný.*</span><span class="sxs-lookup"><span data-stu-id="bd207-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="bd207-159">Nemáte oprávnění k odstranění souborů v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="bd207-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="bd207-160">Pokud je to možné, změňte oprávnění ke složce a akci opakujte.</span><span class="sxs-lookup"><span data-stu-id="bd207-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="bd207-161">V opačném případě se obraťte na správce systému.</span><span class="sxs-lookup"><span data-stu-id="bd207-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="bd207-162">*Chyba: Zadaná cesta, název souboru nebo obojí jsou příliš dlouhé. Úplný název souboru musí být menší než 260 znaků a název adresáře musí být menší než 248 znaků.*</span><span class="sxs-lookup"><span data-stu-id="bd207-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="bd207-163">Zkraťte názvy složek a akci opakujte.</span><span class="sxs-lookup"><span data-stu-id="bd207-163">Shorten the folder names and try again.</span></span>
