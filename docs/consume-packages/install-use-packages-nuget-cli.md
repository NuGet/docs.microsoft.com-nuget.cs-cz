---
title: Správa balíčků NuGet pomocí rozhraní příkazového řádku NuGet. exe
description: Pokyny k použití rozhraní příkazového řádku NuGet. exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428686"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="47f48-103">Správa balíčků pomocí rozhraní příkazového řádku NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="47f48-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="47f48-104">Nástroj rozhraní příkazového řádku umožňuje snadno aktualizovat a obnovovat balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="47f48-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="47f48-105">Tento nástroj poskytuje všechny funkce NuGet ve Windows a poskytuje i většinu funkcí v systémech Mac a Linux, když běží v mono.</span><span class="sxs-lookup"><span data-stu-id="47f48-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="47f48-106">Rozhraní příkazového řádku `nuget.exe` je pro projekt .NET Framework a projekty, které nejsou ve stylu sady SDK (například projekt bez sady SDK, který cílí na .NET Standard knihovny).</span><span class="sxs-lookup"><span data-stu-id="47f48-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="47f48-107">Pokud používáte projekt, který není ve stylu sady SDK, který byl migrován do `PackageReference`, použijte místo toho `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="47f48-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="47f48-108">`nuget.exe` CLI vyžaduje soubor [Packages. config](../reference/packages-config.md) pro odkazy na balíčky.</span><span class="sxs-lookup"><span data-stu-id="47f48-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="47f48-109">Ve většině scénářů doporučujeme [migrovat projekty, které nejsou ve stylu sady SDK](../consume-packages/migrate-packages-config-to-package-reference.md) , které používají `packages.config` PackageReference, a pak můžete použít `dotnet` cli místo `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="47f48-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="47f48-110">Migrace není aktuálně k dispozici C++ pro projekty a ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="47f48-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="47f48-111">Tento článek popisuje základní použití pro několik nejběžnějších příkazů `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="47f48-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="47f48-112">Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadaný soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="47f48-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="47f48-113">Úplný seznam příkazů a argumenty, které můžete použít, najdete v [referenčních informacích k NuGet. exe CLI](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="47f48-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47f48-114">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="47f48-114">Prerequisites</span></span>

- <span data-ttu-id="47f48-115">Nainstalujte `nuget.exe` CLI tak, že ho stáhnete z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), uložíte tento `.exe` soubor do vhodné složky a přidáte tuto složku do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="47f48-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="47f48-116">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="47f48-116">Install a package</span></span>

<span data-ttu-id="47f48-117">Příkaz [install](../reference/cli-reference/cli-ref-install.md) stáhne a nainstaluje balíček do projektu, přičemž použije výchozí nastavení pro aktuální složku pomocí zadaných zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="47f48-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="47f48-118">Nainstalujte nové balíčky do složky *Packages* v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="47f48-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47f48-119">Příkaz `install`neupraví soubor projektu nebo *Packages. config*; tímto způsobem je podobný `restore` v tom, že přidává jenom balíčky na disk, ale nemění závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="47f48-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="47f48-120">Chcete-li přidat závislost, buď přidejte balíček prostřednictvím uživatelského rozhraní nebo konzoly Správce balíčků v aplikaci Visual Studio, nebo upravte soubor *Packages. config* a pak spusťte `install` nebo `restore`.</span><span class="sxs-lookup"><span data-stu-id="47f48-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="47f48-121">Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="47f48-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="47f48-122">K instalaci balíčku NuGet do složky *Packages* použijte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="47f48-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="47f48-123">Chcete-li nainstalovat balíček `Newtonsoft.json` do složky *Packages* , použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="47f48-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="47f48-124">Případně můžete použít následující příkaz k instalaci balíčku NuGet pomocí stávajícího `packages.config` souboru do složky *Packages* .</span><span class="sxs-lookup"><span data-stu-id="47f48-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="47f48-125">Tím se balíček nepřidá do závislostí projektu, ale nainstaluje se místně.</span><span class="sxs-lookup"><span data-stu-id="47f48-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="47f48-126">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="47f48-126">Install a specific version of a package</span></span>

<span data-ttu-id="47f48-127">Pokud při použití příkazu [install](../reference/cli-reference/cli-ref-install.md) není zadána verze, NuGet nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="47f48-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="47f48-128">Můžete také nainstalovat specifickou verzi balíčku NuGet:</span><span class="sxs-lookup"><span data-stu-id="47f48-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="47f48-129">Pokud například chcete přidat 12.0.1 verze balíčku `Newtonsoft.json`, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="47f48-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="47f48-130">Další informace o omezeních a chování `install`najdete v tématu [instalace balíčku](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="47f48-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="47f48-131">Odebrat balíček</span><span class="sxs-lookup"><span data-stu-id="47f48-131">Remove a package</span></span>

<span data-ttu-id="47f48-132">Chcete-li odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat ze složky *Packages* .</span><span class="sxs-lookup"><span data-stu-id="47f48-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="47f48-133">Pokud chcete balíčky znovu nainstalovat, použijte příkaz `restore` nebo `install`.</span><span class="sxs-lookup"><span data-stu-id="47f48-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="47f48-134">Výpis balíčků</span><span class="sxs-lookup"><span data-stu-id="47f48-134">List packages</span></span>

<span data-ttu-id="47f48-135">Seznam balíčků z daného zdroje můžete zobrazit pomocí příkazu [list](../reference/cli-reference/cli-ref-list.md) .</span><span class="sxs-lookup"><span data-stu-id="47f48-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="47f48-136">K omezení vyhledávání použijte možnost `-Source`.</span><span class="sxs-lookup"><span data-stu-id="47f48-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="47f48-137">Například vypíšete balíčky ve složce *Packages* .</span><span class="sxs-lookup"><span data-stu-id="47f48-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="47f48-138">Pokud používáte hledaný termín, hledání zahrnuje názvy balíčků, značek a popisů balíčků.</span><span class="sxs-lookup"><span data-stu-id="47f48-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="47f48-139">Aktualizace jednotlivého balíčku</span><span class="sxs-lookup"><span data-stu-id="47f48-139">Update an individual package</span></span>

<span data-ttu-id="47f48-140">NuGet nainstaluje nejnovější verzi balíčku, když použijete příkaz `install`, pokud nezadáte verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="47f48-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="47f48-141">Aktualizovat všechny balíčky</span><span class="sxs-lookup"><span data-stu-id="47f48-141">Update all packages</span></span>

<span data-ttu-id="47f48-142">Pomocí příkazu [Update](../reference/cli-reference/cli-ref-update.md) aktualizujte všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="47f48-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="47f48-143">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) na nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="47f48-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="47f48-144">Před spuštěním `update`se doporučuje spustit `restore`.</span><span class="sxs-lookup"><span data-stu-id="47f48-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="47f48-145">Obnovit balíčky</span><span class="sxs-lookup"><span data-stu-id="47f48-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="47f48-146">Získat verzi rozhraní příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="47f48-146">Get the CLI version</span></span>

<span data-ttu-id="47f48-147">Použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="47f48-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="47f48-148">První řádek ve výstupu pro Help zobrazuje verzi.</span><span class="sxs-lookup"><span data-stu-id="47f48-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="47f48-149">Abyste se vyhnuli posouvání, použijte místo toho `nuget help | more`.</span><span class="sxs-lookup"><span data-stu-id="47f48-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>