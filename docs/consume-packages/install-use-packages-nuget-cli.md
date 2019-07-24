---
title: Správa balíčků NuGet pomocí rozhraní příkazového řádku NuGet. exe
description: Pokyny k použití rozhraní příkazového řádku NuGet. exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317736"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="bd479-103">Správa balíčků pomocí rozhraní příkazového řádku NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="bd479-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="bd479-104">Nástroj rozhraní příkazového řádku umožňuje snadno aktualizovat a obnovovat balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="bd479-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="bd479-105">Tento nástroj poskytuje všechny funkce NuGet ve Windows a poskytuje i většinu funkcí v systémech Mac a Linux, když běží v mono.</span><span class="sxs-lookup"><span data-stu-id="bd479-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="bd479-106">Rozhraní `nuget.exe` příkazového řádku je pro vaše .NET Framework projektů a projektů, které nejsou ve stylu sady SDK (například projekt bez sady SDK, který cílí na .NET Standard knihovny).</span><span class="sxs-lookup"><span data-stu-id="bd479-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="bd479-107">Pokud používáte projekt, který není ve stylu sady SDK, který byl migrován do `PackageReference`, `dotnet` použijte místo toho příkaz CLI.</span><span class="sxs-lookup"><span data-stu-id="bd479-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="bd479-108">Rozhraní `nuget.exe` příkazového řádku vyžaduje soubor [Packages. config](../reference/packages-config.md) pro odkazy na balíčky.</span><span class="sxs-lookup"><span data-stu-id="bd479-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="bd479-109">Ve většině scénářů doporučujeme [migrovat projekty, které nejsou ve stylu sady SDK](../reference/migrate-packages-config-to-package-reference.md) , `packages.config` které používají PackageReference, a pak můžete použít rozhraní `dotnet` příkazového řádku namísto `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="bd479-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="bd479-110">Migrace není aktuálně k dispozici C++ pro projekty a ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bd479-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="bd479-111">Tento článek popisuje základní použití pro několik nejběžnějších příkazů rozhraní `nuget.exe` příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="bd479-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="bd479-112">Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadaný soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="bd479-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="bd479-113">Úplný seznam příkazů a argumenty, které můžete použít, najdete v referenčních informacích k [NuGet. exe CLI](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="bd479-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd479-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bd479-114">Prerequisites</span></span>

- <span data-ttu-id="bd479-115">Nainstalujte rozhraní `nuget.exe` příkazového řádku stažením z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), uložte tento `.exe` soubor do vhodné složky a přidejte tuto složku do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="bd479-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="bd479-116">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="bd479-116">Install a package</span></span>

<span data-ttu-id="bd479-117">Příkaz [install](../reference/cli-reference/cli-ref-install.md) stáhne a nainstaluje balíček do projektu, přičemž použije výchozí nastavení pro aktuální složku pomocí zadaných zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="bd479-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="bd479-118">Nainstalujte nové balíčky do složky *Packages* v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="bd479-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd479-119">Příkaz neupraví soubor projektu nebo Packages *. config*; tímto způsobem je podobný `restore` jako v tom, že přidává pouze balíčky na disk, ale nemění závislosti projektu. `install`</span><span class="sxs-lookup"><span data-stu-id="bd479-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="bd479-120">Chcete-li přidat závislost, buď přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte soubor *Packages. config* a `install` potom `restore`spusťte nebo.</span><span class="sxs-lookup"><span data-stu-id="bd479-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="bd479-121">Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="bd479-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="bd479-122">K instalaci balíčku NuGet do složky Packages použijte následující příkaz  .</span><span class="sxs-lookup"><span data-stu-id="bd479-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="bd479-123">Chcete-li `Newtonsoft.json` balíček nainstalovat do  složky Packages, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="bd479-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="bd479-124">Případně můžete použít následující příkaz k instalaci balíčku NuGet pomocí existujícího `packages.config` souboru do složky *Packages* .</span><span class="sxs-lookup"><span data-stu-id="bd479-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="bd479-125">Tím se balíček nepřidá do závislostí projektu, ale nainstaluje se místně.</span><span class="sxs-lookup"><span data-stu-id="bd479-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="bd479-126">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="bd479-126">Install a specific version of a package</span></span>

<span data-ttu-id="bd479-127">Pokud při použití příkazu [install](../reference/cli-reference/cli-ref-install.md) není zadána verze, NuGet nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="bd479-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="bd479-128">Můžete také nainstalovat specifickou verzi balíčku NuGet:</span><span class="sxs-lookup"><span data-stu-id="bd479-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="bd479-129">Pokud například chcete přidat 12.0.1 `Newtonsoft.json` verze balíčku, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="bd479-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="bd479-130">Další informace o omezeních a chování `install`nástroje najdete v tématu [instalace balíčku](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="bd479-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="bd479-131">Odebrat balíček</span><span class="sxs-lookup"><span data-stu-id="bd479-131">Remove a package</span></span>

<span data-ttu-id="bd479-132">Chcete-li odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat ze  složky Packages.</span><span class="sxs-lookup"><span data-stu-id="bd479-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="bd479-133">Pokud chcete balíčky znovu nainstalovat, použijte `restore` příkaz nebo. `install`</span><span class="sxs-lookup"><span data-stu-id="bd479-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="bd479-134">Výpis balíčků</span><span class="sxs-lookup"><span data-stu-id="bd479-134">List packages</span></span>

<span data-ttu-id="bd479-135">Seznam balíčků z daného zdroje můžete zobrazit pomocí příkazu [list](../reference/cli-reference/cli-ref-list.md) .</span><span class="sxs-lookup"><span data-stu-id="bd479-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="bd479-136">K omezení vyhledávání použijte možnost.`-Source`</span><span class="sxs-lookup"><span data-stu-id="bd479-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="bd479-137">Například vypíšete balíčky ve složce *Packages* .</span><span class="sxs-lookup"><span data-stu-id="bd479-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="bd479-138">Pokud používáte hledaný termín, hledání zahrnuje názvy balíčků, značek a popisů balíčků.</span><span class="sxs-lookup"><span data-stu-id="bd479-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="bd479-139">Aktualizace jednotlivého balíčku</span><span class="sxs-lookup"><span data-stu-id="bd479-139">Update an individual package</span></span>

<span data-ttu-id="bd479-140">NuGet nainstaluje nejnovější verzi balíčku, když použijete `install` příkaz, pokud nezadáte verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="bd479-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="bd479-141">Aktualizovat všechny balíčky</span><span class="sxs-lookup"><span data-stu-id="bd479-141">Update all packages</span></span>

<span data-ttu-id="bd479-142">Pomocí příkazu [Update](../reference/cli-reference/cli-ref-update.md) aktualizujte všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="bd479-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="bd479-143">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="bd479-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="bd479-144">Doporučuje se spustit `restore` před spuštěním `update`.</span><span class="sxs-lookup"><span data-stu-id="bd479-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="bd479-145">Obnovit balíčky</span><span class="sxs-lookup"><span data-stu-id="bd479-145">Restore packages</span></span>

<span data-ttu-id="bd479-146">Použijte příkaz [Restore](../reference/cli-reference/cli-ref-restore.md) , který stáhne a nainstaluje ze složky Packages chybějící  balíčky.</span><span class="sxs-lookup"><span data-stu-id="bd479-146">Use the [restore](../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="bd479-147">`restore`přidá pouze balíčky na disk, ale nemění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="bd479-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="bd479-148">Chcete-li obnovit závislosti projektu `packages.config`, upravte a pak `restore` použijte příkaz.</span><span class="sxs-lookup"><span data-stu-id="bd479-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="bd479-149">Stejně jako u ostatních `nuget.exe` příkazů CLI otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="bd479-149">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="bd479-150">Postup obnovení balíčku pomocí `restore`:</span><span class="sxs-lookup"><span data-stu-id="bd479-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```