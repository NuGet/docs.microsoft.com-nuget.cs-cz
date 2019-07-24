---
title: Správa globálních balíčků, mezipaměti, dočasných složek v NuGetu
description: Jak spravovat instalační složku globálního balíčku, mezipaměť balíčků a dočasné složky, které existují na počítači, které se používají při instalaci, obnovení a aktualizaci balíčků.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: f5d418fd5b6b9bb88958d6b7e9e3034f40485a7d
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419957"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="08875-103">Správa globálních balíčků, mezipaměti a dočasných složek</span><span class="sxs-lookup"><span data-stu-id="08875-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="08875-104">Kdykoli nainstalujete, aktualizujete nebo obnovíte balíček, aplikace NuGet spravuje balíčky a informace o balíčcích v několika složkách mimo vaši strukturu projektu:</span><span class="sxs-lookup"><span data-stu-id="08875-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="08875-105">Name</span><span class="sxs-lookup"><span data-stu-id="08875-105">Name</span></span> | <span data-ttu-id="08875-106">Popis a umístění (na uživatele)</span><span class="sxs-lookup"><span data-stu-id="08875-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="08875-107">globální&#8209;balíčky</span><span class="sxs-lookup"><span data-stu-id="08875-107">global&#8209;packages</span></span> | <span data-ttu-id="08875-108">Složka *Global-Packages* je místo, kde NuGet nainstaluje libovolný stažený balíček.</span><span class="sxs-lookup"><span data-stu-id="08875-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="08875-109">Každý balíček je plně rozbalen do podsložky, která odpovídá identifikátoru a číslu verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="08875-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="08875-110">Projekty, které používají formát [PackageReference](package-references-in-project-files.md) , vždy používají balíčky přímo z této složky.</span><span class="sxs-lookup"><span data-stu-id="08875-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="08875-111">Při použití [souboru Packages. config](../reference/packages-config.md)jsou balíčky nainstalovány do složky *Global-Packages* a následně zkopírovány do `packages` složky projektu.</span><span class="sxs-lookup"><span data-stu-id="08875-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="08875-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="08875-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="08875-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="08875-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="08875-114">Popište pomocí proměnné prostředí `globalPackagesFolder` NUGET_PACKAGES, [nastavení konfigurace](../reference/nuget-config-file.md#config-section) `packages.config`nebo `repositoryPath` (při použití PackageReference `RestorePackagesPath` a, v uvedeném pořadí) nebo pomocí vlastnosti MSBuild (jenom MSBuild).</span><span class="sxs-lookup"><span data-stu-id="08875-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="08875-115">Proměnná prostředí má přednost před nastavením konfigurace.</span><span class="sxs-lookup"><span data-stu-id="08875-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="08875-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="08875-116">http&#8209;cache</span></span> | <span data-ttu-id="08875-117">Správce balíčků sady Visual Studio (NuGet 3. x +) a `dotnet` nástroj ukládá kopie stažených balíčků v této mezipaměti (uložené jako `.dat` soubory), které jsou uspořádány do podsložek pro každý zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="08875-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="08875-118">Balíčky nejsou rozbalené a mezipaměť má čas vypršení platnosti 30 minut.</span><span class="sxs-lookup"><span data-stu-id="08875-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="08875-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="08875-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="08875-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="08875-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="08875-121">Popište pomocí proměnné prostředí NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="08875-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="08875-122">názvem</span><span class="sxs-lookup"><span data-stu-id="08875-122">temp</span></span> | <span data-ttu-id="08875-123">Složka, ve které NuGet ukládá dočasné soubory během různých operací.</span><span class="sxs-lookup"><span data-stu-id="08875-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="08875-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="08875-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="08875-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="08875-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="08875-126">moduly plug-in – mezipaměť **4,8 +**</span><span class="sxs-lookup"><span data-stu-id="08875-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="08875-127">Složka, ve které NuGet ukládá výsledky z požadavku na Operations identity</span><span class="sxs-lookup"><span data-stu-id="08875-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="08875-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="08875-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="08875-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="08875-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="08875-130">Popište pomocí proměnné prostředí NUGET_PLUGINS_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="08875-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="08875-131">NuGet 3,5 a starší používá *mezipaměť balíčků* místo *HTTP-cache*, která je umístěna v `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="08875-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="08875-132">Pomocí složek cache a *Global-Packages* NuGet se obecně vyhne stahování balíčků, které již v počítači existují, což zlepšuje výkon operací instalace, aktualizace a obnovení.</span><span class="sxs-lookup"><span data-stu-id="08875-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="08875-133">Při použití PackageReference se složka *Global-Packages* také vyhne zachovávání stažených balíčků ve složkách projektu, kde by mohly být neúmyslně přidány do správy zdrojových kódů, a snižuje celkový dopad na úložiště počítače.</span><span class="sxs-lookup"><span data-stu-id="08875-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="08875-134">Když se zobrazí výzva k načtení balíčku, NuGet nejprve vyhledá složku *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="08875-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="08875-135">Pokud není k dispozici přesná verze balíčku, vyhledá NuGet všechny zdroje balíčků bez HTTP.</span><span class="sxs-lookup"><span data-stu-id="08875-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="08875-136">Pokud se balíček ještě nenašel, NuGet vyhledá balíček v *mezipaměti HTTP-cache* , pokud `--no-cache` nezadáte příkazy s `dotnet.exe` příkazy nebo `-NoCache` s `nuget.exe` příkazy.</span><span class="sxs-lookup"><span data-stu-id="08875-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="08875-137">Pokud balíček není v mezipaměti, nebo se mezipaměť nepoužívá, NuGet ho načte pomocí protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="08875-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="08875-138">Další informace najdete v tématu [co se stane, když se balíček nainstaluje?](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="08875-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="08875-139">Zobrazení umístění složek</span><span class="sxs-lookup"><span data-stu-id="08875-139">Viewing folder locations</span></span>

<span data-ttu-id="08875-140">Umístění můžete zobrazit pomocí [příkazu NuGet Locals](../reference/cli-reference/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="08875-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="08875-141">Typický výstup (Windows; "Uživatel1" je aktuální uživatelské jméno:</span><span class="sxs-lookup"><span data-stu-id="08875-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="08875-142">(`package-cache` používá se v NuGet 2. x a zobrazí se NuGet 3,5 a starším.)</span><span class="sxs-lookup"><span data-stu-id="08875-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="08875-143">Umístění složek můžete zobrazit také pomocí [příkazu dotnet NuGet Locals](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="08875-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="08875-144">Typický výstup (Mac/Linux; "Uživatel1" je aktuální uživatelské jméno:</span><span class="sxs-lookup"><span data-stu-id="08875-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="08875-145">Chcete-li zobrazit umístění jedné složky, použijte `http-cache` `temp`, `global-packages`, nebo `plugins-cache` místo `all`.</span><span class="sxs-lookup"><span data-stu-id="08875-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="08875-146">Mazání místních složek</span><span class="sxs-lookup"><span data-stu-id="08875-146">Clearing local folders</span></span>

<span data-ttu-id="08875-147">Pokud narazíte na problémy s instalací balíčku nebo pokud chcete, aby se balíčky instalovaly ze vzdálené galerie, použijte `locals --clear` možnost (dotnet. exe) nebo `locals -clear` (NuGet. exe), určete složku, která se má vymazat `all` , nebo na vymazat všechny složky:</span><span class="sxs-lookup"><span data-stu-id="08875-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

<span data-ttu-id="08875-148">Všechny balíčky používané projekty, které jsou aktuálně otevřeny v aplikaci Visual Studio, nejsou vymazány ze složky *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="08875-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="08875-149">V aplikaci Visual Studio 2017 použijte **Správce balíčků NuGet nástroje > > příkaz Správce balíčků** a pak vyberte **Vymazat všechny mezipaměti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="08875-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="08875-150">Správa mezipaměti není v současnosti k dispozici prostřednictvím konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="08875-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="08875-151">V aplikaci Visual Studio 2015 použijte místo toho příkazy rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="08875-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Příkaz NuGet pro mazání mezipamětí](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="08875-153">Řešení chyb</span><span class="sxs-lookup"><span data-stu-id="08875-153">Troubleshooting errors</span></span>

<span data-ttu-id="08875-154">Při použití `nuget locals` nebo `dotnet nuget locals`se můžou objevit tyto chyby:</span><span class="sxs-lookup"><span data-stu-id="08875-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="08875-155">*Chyba: Proces nemůže získat přístup k souboru <package> , protože ho používá jiný proces* nebo *došlo k chybě při mazání místních prostředků: Nepovedlo se odstranit jeden nebo víc souborů.*</span><span class="sxs-lookup"><span data-stu-id="08875-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="08875-156">Jeden nebo více souborů ve složce používá jiný proces. například projekt sady Visual Studio je otevřen, který odkazuje na balíčky ve složce *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="08875-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="08875-157">Zavřete tyto procesy a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="08875-157">Close those processes and try again.</span></span>

- <span data-ttu-id="08875-158">*Chyba: Přístup k cestě <path> byl odepřen* nebo adresář není *prázdný* .</span><span class="sxs-lookup"><span data-stu-id="08875-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="08875-159">Nemáte oprávnění k odstranění souborů v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="08875-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="08875-160">Pokud je to možné, změňte oprávnění složky a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="08875-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="08875-161">V opačném případě se obraťte na správce systému.</span><span class="sxs-lookup"><span data-stu-id="08875-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="08875-162">*Chyba: Zadaná cesta, název souboru nebo obojí jsou příliš dlouhé. Plně kvalifikovaný název souboru musí být kratší než 260 znaků a název adresáře musí být kratší než 248 znaků.*</span><span class="sxs-lookup"><span data-stu-id="08875-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="08875-163">Zkraťte název složky a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="08875-163">Shorten the folder names and try again.</span></span>
