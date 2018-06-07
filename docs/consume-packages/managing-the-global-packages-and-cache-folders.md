---
title: Jak spravovat globální balíčky, mezipaměť, dočasné složky v NuGet
description: Jak spravovat globální balíček instalační složku, do mezipaměti balíček a dočasné složky, které existují v počítači, které se použijí při instalaci, obnovení a aktualizaci balíčků.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 89f70c8d22f5a6409bc3db751646a253f6ad034a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817481"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="36de3-103">Správa globální balíčky, mezipaměti a dočasné složky</span><span class="sxs-lookup"><span data-stu-id="36de3-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="36de3-104">Vždy, když instalace, aktualizace nebo obnovení balíčku NuGet spravuje balíčky a informací o balíčku v několika složkách mimo strukturu projektu:</span><span class="sxs-lookup"><span data-stu-id="36de3-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="36de3-105">Název</span><span class="sxs-lookup"><span data-stu-id="36de3-105">Name</span></span> | <span data-ttu-id="36de3-106">Popis a umístění (na uživatele)</span><span class="sxs-lookup"><span data-stu-id="36de3-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="36de3-107">globální&#8209;balíčky</span><span class="sxs-lookup"><span data-stu-id="36de3-107">global&#8209;packages</span></span> | <span data-ttu-id="36de3-108">*Globální balíčky* složka je, kde NuGet nainstaluje všechny staženého balíčku.</span><span class="sxs-lookup"><span data-stu-id="36de3-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="36de3-109">Každý balíček je plně rozšířit do podsložky, která odpovídá identifikátor balíčku a číslo verze.</span><span class="sxs-lookup"><span data-stu-id="36de3-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="36de3-110">Projektů pomocí PackageReference formátu vždy balíčky pro použití přímo z této složky.</span><span class="sxs-lookup"><span data-stu-id="36de3-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="36de3-111">Při použití `packages.config`, balíčky instalují *globální balíčky* složky, poté zkopírovat do projektu `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="36de3-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="36de3-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="36de3-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="36de3-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="36de3-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="36de3-114">Přepsat pomocí proměnné prostředí NUGET_PACKAGES `globalPackagesFolder` nebo `repositoryPath` [nastavení konfigurace](../reference/nuget-config-file.md#config-section) (při použití PackageReference a `packages.config`, v uvedeném pořadí), nebo `RestorePackagesPath` nástroje MSBuild vlastnost (MSBuild pouze).</span><span class="sxs-lookup"><span data-stu-id="36de3-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="36de3-115">Proměnné prostředí mají přednost před nastavením konfigurace.</span><span class="sxs-lookup"><span data-stu-id="36de3-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="36de3-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="36de3-116">http&#8209;cache</span></span> | <span data-ttu-id="36de3-117">Správce balíčků Visual Studio (NuGet 3.x+) a `dotnet` nástroj úložiště kopie stažených balíčků do mezipaměti, (Uložit jako `.dat` soubory), jsou uspořádány do podsložek pro jednotlivé zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="36de3-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="36de3-118">Balíčky nejsou rozšířit a mezipaměť obsahuje čas vypršení platnosti 30 minut.</span><span class="sxs-lookup"><span data-stu-id="36de3-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="36de3-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="36de3-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="36de3-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="36de3-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="36de3-121">Přepište pomocí proměnné prostředí NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="36de3-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="36de3-122">dočasné</span><span class="sxs-lookup"><span data-stu-id="36de3-122">temp</span></span> | <span data-ttu-id="36de3-123">Do složky, kde NuGet ukládá dočasné soubory během jeho různé operace.</span><span class="sxs-lookup"><span data-stu-id="36de3-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="36de3-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="36de3-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="36de3-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="36de3-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="36de3-126">NuGet 3.5 a starší používá *balíčky mezipaměti* místo *http mezipaměti*, který se nachází v `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="36de3-126">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="36de3-127">Pomocí mezipaměti a *globální balíčky* složek, NuGet obecně zabraňuje stahovali balíčky, které již existují na počítači, zvýšení výkonu instalaci, aktualizaci a operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="36de3-127">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="36de3-128">Při použití PackageReference, *globální balíčky* složky také zabraňuje zachování stažené balíčky v projektu složky, kde se může nechtěně zařadí do správy zdrojového kódu a snižuje NuGet celkového vlivu na počítači úložiště.</span><span class="sxs-lookup"><span data-stu-id="36de3-128">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="36de3-129">Když se zobrazí dotaz pro načtení balíčku, NuGet nejprve hledá v *globální balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="36de3-129">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="36de3-130">Pokud není přesnou verzi balíčku, NuGet kontroluje všechny zdroje balíčků jiným protokolem než HTTP.</span><span class="sxs-lookup"><span data-stu-id="36de3-130">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="36de3-131">Pokud stále nebyl nalezen balíček, NuGet hledá balíčku *http mezipaměti* nezadáte `--no-cache` s `dotnet.exe` příkazy nebo `-NoCache` s `nuget.exe` příkazy.</span><span class="sxs-lookup"><span data-stu-id="36de3-131">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="36de3-132">Pokud balíček není v mezipaměti, nebo do mezipaměti se nepoužívá, NuGet potom načte balíček přes protokol HTTP.</span><span class="sxs-lookup"><span data-stu-id="36de3-132">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="36de3-133">Další informace najdete v tématu [co se stane, když je nainstalován balíček](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="36de3-133">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="36de3-134">Umístění složek pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="36de3-134">Viewing folder locations</span></span>

<span data-ttu-id="36de3-135">Můžete zobrazit pomocí umístění složek [příkaz místní hodnoty – nuget dotnet](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="36de3-135">You can view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="36de3-136">Typické výstup (Mac/Linux; aktuální uživatelské jméno je "uživatel1"):</span><span class="sxs-lookup"><span data-stu-id="36de3-136">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

<span data-ttu-id="36de3-137">Chcete-li zobrazit umístění jednotlivých složek, použijte `http-cache`, `global-packages`, nebo `temp` místo `all`.</span><span class="sxs-lookup"><span data-stu-id="36de3-137">To display the location of a single folder, use `http-cache`, `global-packages`, or `temp` instead of `all`.</span></span> 

<span data-ttu-id="36de3-138">Můžete také zobrazit umístění pomocí [příkaz místní hodnoty – nuget](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="36de3-138">You also view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

<span data-ttu-id="36de3-139">Typické výstup (Windows; aktuální uživatelské jméno je "uživatel1"):</span><span class="sxs-lookup"><span data-stu-id="36de3-139">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

<span data-ttu-id="36de3-140">(`package-cache` se používá v NuGet 2.x a zobrazí se s NuGet 3.5 a starší.)</span><span class="sxs-lookup"><span data-stu-id="36de3-140">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="36de3-141">Vymazání místní složky</span><span class="sxs-lookup"><span data-stu-id="36de3-141">Clearing local folders</span></span>

<span data-ttu-id="36de3-142">Pokud dojde k potížím instalace balíčku nebo jinak potřeba zajistit, že instalujete balíčky ze vzdáleného galerie, použijte `locals --clear` možnost (dotnet.exe) nebo `locals -clear` (nuget.exe), zadání složky, které chcete vymazat, nebo `all` na Zrušte zaškrtnutí políčka všechny složky:</span><span class="sxs-lookup"><span data-stu-id="36de3-142">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="36de3-143">Všechny balíčky používané projekty, které jsou právě otevřeny v sadě Visual Studio nejsou vymazána z *globální balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="36de3-143">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="36de3-144">V aplikaci Visual Studio 2017, použijte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** nabídky příkazu a pak vyberte **zrušte všechny Cache(s) NuGet**.</span><span class="sxs-lookup"><span data-stu-id="36de3-144">In Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="36de3-145">Správa mezipaměti není v současné době dostupná přes konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="36de3-145">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="36de3-146">V sadě Visual Studio 2015 pomocí rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="36de3-146">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Příkaz NuGet možnost pro vymazání mezipaměti](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="36de3-148">Řešení potíží s chybami</span><span class="sxs-lookup"><span data-stu-id="36de3-148">Troubleshooting errors</span></span>

<span data-ttu-id="36de3-149">Následující chyby může stát při použití `nuget locals` nebo `dotnet nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="36de3-149">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="36de3-150">*Chyba: Proces nemá přístup k souboru <package> vzhledem k tomu, že je stále používán jiným procesem* nebo *vymazání místních prostředků se nezdařilo: nelze odstranit jeden nebo více souborů*</span><span class="sxs-lookup"><span data-stu-id="36de3-150">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="36de3-151">Jeden nebo více souborů ve složce je používán jiným procesem; Otevřete, který odkazuje na balíčky v projektu sady Visual Studio je například *globální balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="36de3-151">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="36de3-152">Zavřete tyto procesy a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="36de3-152">Close those processes and try again.</span></span>

- <span data-ttu-id="36de3-153">*Chyba: Přístup k cestě <path> byl odepřen* nebo *adresář není prázdná*</span><span class="sxs-lookup"><span data-stu-id="36de3-153">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="36de3-154">Nemáte oprávnění k odstranění souborů v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="36de3-154">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="36de3-155">Změnit oprávnění složky, pokud je to možné a akci opakujte.</span><span class="sxs-lookup"><span data-stu-id="36de3-155">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="36de3-156">Jinak obraťte se na správce systému.</span><span class="sxs-lookup"><span data-stu-id="36de3-156">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="36de3-157">*Chyba: Zadaná cesta a název souboru jsou příliš dlouhé. Plně kvalifikovaný název souboru musí být méně než 260 znaků a název adresáře musí být méně než 248 znaků.*</span><span class="sxs-lookup"><span data-stu-id="36de3-157">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="36de3-158">Zkraťte názvy složek a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="36de3-158">Shorten the folder names and try again.</span></span>
