---
title: Správa balíčků NuGet pomocí cli nuget.exe
description: Pokyny pro použití cli nuget.exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428686"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="cbdc7-103">Správa balíčků pomocí cli nuget.exe</span><span class="sxs-lookup"><span data-stu-id="cbdc7-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="cbdc7-104">Nástroj CLI umožňuje snadno aktualizovat a obnovit balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="cbdc7-105">Tento nástroj poskytuje všechny funkce NuGet v systému Windows a také poskytuje většinu funkcí na Mac a Linux při spuštění pod Mono.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="cbdc7-106">Rozhraní `nuget.exe` se konstatování je pro projekty rozhraní .NET Framework a projekty, které nejsou ve stylu sady SDK (například projekt bez sdk stylu, který cílí na knihovny .NET Standard).</span><span class="sxs-lookup"><span data-stu-id="cbdc7-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="cbdc7-107">Pokud používáte projekt, který nebyl ve stylu sady SDK, který byl migrován , `PackageReference`použijte místo toho `dotnet` cli.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="cbdc7-108">ClI `nuget.exe` vyžaduje [soubor packages.config](../reference/packages-config.md) pro odkazy na balíčky.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="cbdc7-109">Ve většině scénářů doporučujeme [migrovat projekty,](../consume-packages/migrate-packages-config-to-package-reference.md) které `packages.config` se nepoužívají ve stylu `dotnet` sady SDK, a pak můžete místo `nuget.exe` cli použít zapínací úsečkové číslo.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="cbdc7-110">Migrace není v současné době k dispozici pro projekty jazyka C++ a ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="cbdc7-111">Tento článek ukazuje základní použití pro několik `nuget.exe` nejběžnějších příkazů příkazového příkazu.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="cbdc7-112">U většiny těchto příkazů nástroj příkazcli hledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadán soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="cbdc7-113">Úplný seznam příkazů a argumentů, které můžete použít, naleznete v [odkazu cli nuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="cbdc7-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbdc7-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cbdc7-114">Prerequisites</span></span>

- <span data-ttu-id="cbdc7-115">Nainstalujte `nuget.exe` rozhraní se konstatování pomocí `.exe` nuget.org [,](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)uložíte jej do vhodné složky a přidáte tuto složku do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="cbdc7-116">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="cbdc7-116">Install a package</span></span>

<span data-ttu-id="cbdc7-117">Příkaz [install](../reference/cli-reference/cli-ref-install.md) stáhne a nainstaluje balíček do projektu, který je výchozí pro aktuální složku pomocí určených zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="cbdc7-118">Nainstalujte nové balíčky do složky *balíčky* v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbdc7-119">Příkaz `install`nezmění soubor projektu nebo *soubor packages.config*; tímto způsobem je podobný `restore` v tom, že pouze přidává balíčky na disk, ale nemění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="cbdc7-120">Chcete-li přidat závislost, přidejte balíček prostřednictvím uzly Správce balíčků nebo konzoly v `install` `restore`sadě Visual Studio nebo upravte *soubor packages.config* a spusťte buď nebo .</span><span class="sxs-lookup"><span data-stu-id="cbdc7-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="cbdc7-121">Otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="cbdc7-122">Pomocí následujícího příkazu nainstalujte balíček NuGet do složky *packages.*</span><span class="sxs-lookup"><span data-stu-id="cbdc7-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="cbdc7-123">Chcete-li `Newtonsoft.json` balíček nainstalovat do složky *balíčky,* použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="cbdc7-124">Alternativně můžete použít následující příkaz k instalaci balíčku NuGet pomocí existujícího `packages.config` souboru do složky *balíčky.*</span><span class="sxs-lookup"><span data-stu-id="cbdc7-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="cbdc7-125">To nepřidá balíček do závislostí projektu, ale nainstaluje místně.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="cbdc7-126">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="cbdc7-126">Install a specific version of a package</span></span>

<span data-ttu-id="cbdc7-127">Pokud verze není zadána při použití příkazu [install,](../reference/cli-reference/cli-ref-install.md) NuGet nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="cbdc7-128">Můžete také nainstalovat konkrétní verzi balíčku Nuget:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="cbdc7-129">Chcete-li například přidat verzi `Newtonsoft.json` balíčku 12.0.1, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="cbdc7-130">Další informace o omezeních a `install`chování aplikace naleznete v [tématu Instalace balíčku](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="cbdc7-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="cbdc7-131">Odebrání balíčku</span><span class="sxs-lookup"><span data-stu-id="cbdc7-131">Remove a package</span></span>

<span data-ttu-id="cbdc7-132">Chcete-li odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat ze složky *balíčky.*</span><span class="sxs-lookup"><span data-stu-id="cbdc7-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="cbdc7-133">Pokud chcete přeinstalovat balíčky, `restore` `install` použijte příkaz nebo.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="cbdc7-134">Seznam balíčků</span><span class="sxs-lookup"><span data-stu-id="cbdc7-134">List packages</span></span>

<span data-ttu-id="cbdc7-135">Seznam balíčků z daného zdroje můžete zobrazit pomocí příkazu [seznam.](../reference/cli-reference/cli-ref-list.md)</span><span class="sxs-lookup"><span data-stu-id="cbdc7-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="cbdc7-136">Pomocí `-Source` možnosti můžete hledání omezit.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="cbdc7-137">Například seznam balíčků ve složce *balíčky.*</span><span class="sxs-lookup"><span data-stu-id="cbdc7-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="cbdc7-138">Pokud používáte hledaný výraz, hledání obsahuje názvy balíčků, značek a popisů balíčků.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="cbdc7-139">Aktualizace jednotlivého balíčku</span><span class="sxs-lookup"><span data-stu-id="cbdc7-139">Update an individual package</span></span>

<span data-ttu-id="cbdc7-140">NuGet nainstaluje nejnovější verzi balíčku při `install` použití příkazu, pokud zadáte verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="cbdc7-141">Aktualizovat všechny balíčky</span><span class="sxs-lookup"><span data-stu-id="cbdc7-141">Update all packages</span></span>

<span data-ttu-id="cbdc7-142">Pomocí příkazu [update](../reference/cli-reference/cli-ref-update.md) aktualizujte všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="cbdc7-143">Aktualizuje všechny balíčky v `packages.config`projektu (pomocí) na jejich nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="cbdc7-144">Před spuštěním `update` `restore` se doporučuje spustit .</span><span class="sxs-lookup"><span data-stu-id="cbdc7-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="cbdc7-145">Obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="cbdc7-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="cbdc7-146">Získání verze CLI</span><span class="sxs-lookup"><span data-stu-id="cbdc7-146">Get the CLI version</span></span>

<span data-ttu-id="cbdc7-147">Pomocí tohoto příkazu:</span><span class="sxs-lookup"><span data-stu-id="cbdc7-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="cbdc7-148">První řádek ve výstupu nápovědy zobrazuje verzi.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="cbdc7-149">Chcete-li se vyhnout `nuget help | more` posouvání nahoru, použijte místo toho.</span><span class="sxs-lookup"><span data-stu-id="cbdc7-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>