---
title: Správa globálních balíčků, mezipaměť, dočasné složky ve Správci NuGet
description: Jak spravovat globální balíčku Instalační složka mezipaměti balíčku a dočasné složky, které existují na počítači, které se použijí při instalaci, obnovení a aktualizace balíčků.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 545e658d26b557f27d6534bf677f467e65a315b4
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793615"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="b4fc7-103">Správa globálních balíčků, mezipaměť a dočasné složky</span><span class="sxs-lookup"><span data-stu-id="b4fc7-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="b4fc7-104">Pokaždé, když se nainstalovat, aktualizovat nebo obnovit balíček NuGet spravuje balíčky a informace o balíčku v mimo strukturu projektu několik složek:</span><span class="sxs-lookup"><span data-stu-id="b4fc7-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="b4fc7-105">Název</span><span class="sxs-lookup"><span data-stu-id="b4fc7-105">Name</span></span> | <span data-ttu-id="b4fc7-106">Popis a umístění (na jednoho uživatele)</span><span class="sxs-lookup"><span data-stu-id="b4fc7-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="b4fc7-107">globální&#8209;balíčky</span><span class="sxs-lookup"><span data-stu-id="b4fc7-107">global&#8209;packages</span></span> | <span data-ttu-id="b4fc7-108">*Global-packages* kde NuGet nainstaluje všechny staženého balíčku je složka.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="b4fc7-109">Každý balíček je úplně rozbalen do podsložky, která odpovídá identifikátor balíčku a číslo verze.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="b4fc7-110">Projekty pomocí PackageReference formátu vždy balíčky pro použití přímo z této složky.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="b4fc7-111">Při použití `packages.config`, balíčky se nainstalují do *global-packages* složku, pak zkopíruje do projektu `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="b4fc7-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="b4fc7-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="b4fc7-114">Přepsat pomocí proměnné prostředí NUGET_PACKAGES `globalPackagesFolder` nebo `repositoryPath` [nastavení konfigurace](../reference/nuget-config-file.md#config-section) (při použití PackageReference a `packages.config`v uvedeném pořadí), nebo `RestorePackagesPath` MSBuild vlastnosti (pouze nástroj MSBuild).</span><span class="sxs-lookup"><span data-stu-id="b4fc7-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="b4fc7-115">Proměnná prostředí má přednost před nastavením konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="b4fc7-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="b4fc7-116">http&#8209;cache</span></span> | <span data-ttu-id="b4fc7-117">Balíček správce sady Visual Studio (NuGet 3.x+) a `dotnet` nástroj úložiště kopie v mezipaměti stažených balíčků (Uložit jako `.dat` soubory) uspořádaných do podsložky pro jednotlivé zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="b4fc7-118">Balíčky nejsou rozbalen a mezipaměti má čas vypršení platnosti 30 minut.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="b4fc7-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="b4fc7-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="b4fc7-121">Přepište NUGET_HTTP_CACHE_PATH proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="b4fc7-122">temp</span><span class="sxs-lookup"><span data-stu-id="b4fc7-122">temp</span></span> | <span data-ttu-id="b4fc7-123">Složka, ve kterém NuGet ukládá dočasné soubory během jeho různé operace.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="b4fc7-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="b4fc7-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="b4fc7-126">moduly plug-in mezipaměti **4.8 +**</span><span class="sxs-lookup"><span data-stu-id="b4fc7-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="b4fc7-127">Složky, kde NuGet uchovává výsledky z deklarací identity požadavek operation.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="b4fc7-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="b4fc7-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="b4fc7-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="b4fc7-130">Přepište NUGET_PLUGINS_CACHE_PATH proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="b4fc7-131">NuGet 3.5 a starších používá *mezipaměť balíčků* místo *http-cache*, který se nachází v `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="b4fc7-132">Mezipaměť a *global-packages* složek, NuGet obecně se vyhnete stahovali balíčky, které již existují na počítači, vylepšení výkonu instalovat, aktualizovat a operace obnovení.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="b4fc7-133">Při použití PackageReference, *global-packages* složku také zabraňuje uchování stáhnout balíčky uvnitř složky projektu, kde se může nechtěně přidat do správy zdrojového kódu a snižuje celkový dopad NuGet na počítači úložiště.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="b4fc7-134">Když se zobrazí výzva k načtení balíčku, nejprve hledá NuGet v *global-packages* složky.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="b4fc7-135">Pokud není přesné verze balíčku, NuGet kontroluje všechny zdroje balíčků jiným protokolem než HTTP.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="b4fc7-136">Pokud balíček není stále nalezen, NuGet hledá v balíčku *http-cache* neurčíte `--no-cache` s `dotnet.exe` příkazy nebo `-NoCache` s `nuget.exe` příkazy.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="b4fc7-137">Pokud balíček není v mezipaměti, nebo do mezipaměti se nepoužívá, NuGet pak načte balíček přes protokol HTTP.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="b4fc7-138">Další informace najdete v tématu [co se stane, když je nainstalován balíček](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="b4fc7-138">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="b4fc7-139">Zobrazení umístění složek</span><span class="sxs-lookup"><span data-stu-id="b4fc7-139">Viewing folder locations</span></span>

<span data-ttu-id="b4fc7-140">Zobrazí se umístění s využitím [příkaz nuget locals](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="b4fc7-140">You can view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="b4fc7-141">Příklad typického výstupu (Windows; aktuální uživatelské jméno je "uživatel1"):</span><span class="sxs-lookup"><span data-stu-id="b4fc7-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="b4fc7-142">(`package-cache` používá NuGet 2.x a zobrazí se u NuGet 3.5 a starší.)</span><span class="sxs-lookup"><span data-stu-id="b4fc7-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="b4fc7-143">Umístění složky s využitím můžete zobrazit také [příkaz dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="b4fc7-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="b4fc7-144">Příklad typického výstupu (Mac/Linux; aktuální uživatelské jméno je "uživatel1"):</span><span class="sxs-lookup"><span data-stu-id="b4fc7-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="b4fc7-145">Chcete-li zobrazit umístění jednotlivých složek, použijte `http-cache`, `global-packages`, `temp`, nebo `plugins-cache` místo `all`.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="b4fc7-146">Vymazává se místní složky</span><span class="sxs-lookup"><span data-stu-id="b4fc7-146">Clearing local folders</span></span>

<span data-ttu-id="b4fc7-147">Pokud docházet k problémům při instalaci balíčku nebo jinak chcete zajistit, že instalujete balíčky ze vzdáleného galerii, použijte `locals --clear` možnost (dotnet.exe) nebo `locals -clear` (nuget.exe) určující složku, kterou chcete vymazat, nebo `all` do Vymažte všechny složky:</span><span class="sxs-lookup"><span data-stu-id="b4fc7-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

<span data-ttu-id="b4fc7-148">Všechny balíčky, které používají projekty, které jsou právě otevřeny v sadě Visual Studio se vymazat z *global-packages* složky.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="b4fc7-149">V sadě Visual Studio 2017, použijte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** nabídce příkaz a pak vyberte **vymazat všechny mezipaměti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-149">In Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="b4fc7-150">Správa mezipaměti není v současné době dostupná přes konzolu Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="b4fc7-151">V sadě Visual Studio 2015 pomocí příkazů rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Příkaz NuGet možnost pro vymazání mezipaměti](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="b4fc7-153">Řešení potíží s chybami</span><span class="sxs-lookup"><span data-stu-id="b4fc7-153">Troubleshooting errors</span></span>

<span data-ttu-id="b4fc7-154">Těmto chybám může dojít při použití `nuget locals` nebo `dotnet nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="b4fc7-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="b4fc7-155">*Chyba: Proces nemá přístup k souboru <package> protože ho používá jiný proces* nebo *vymazat místní prostředky se nezdařilo: nelze odstranit jeden nebo více souborů*</span><span class="sxs-lookup"><span data-stu-id="b4fc7-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="b4fc7-156">Jeden nebo více souborů ve složce se používají v jiném procesu; otevřít, který odkazuje na balíčky v projektu sady Visual Studio je třeba *global-packages* složky.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="b4fc7-157">Zavřít tyto procesy a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-157">Close those processes and try again.</span></span>

- <span data-ttu-id="b4fc7-158">*Chyba: Přístup k cestě <path> odepřen* nebo *adresář není prázdný*</span><span class="sxs-lookup"><span data-stu-id="b4fc7-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="b4fc7-159">Nemáte oprávnění k odstranění souborů v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="b4fc7-160">Změnit oprávnění, pokud je to možné a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="b4fc7-161">Jinak obraťte se na správce systému.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="b4fc7-162">*Chyba: Zadaná cesta, název souboru nebo obojí jsou příliš dlouhé. Plně kvalifikovaný název musí být kratší než 260 znaků a název adresáře musí být kratší než 248 znaků.*</span><span class="sxs-lookup"><span data-stu-id="b4fc7-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="b4fc7-163">Zkraťte název složky a zkuste to znovu.</span><span class="sxs-lookup"><span data-stu-id="b4fc7-163">Shorten the folder names and try again.</span></span>
