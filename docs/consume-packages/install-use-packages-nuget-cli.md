---
title: Spravovat balíčky NuGet pomocí rozhraní příkazového řádku nuget.exe
description: Pokyny k používání rozhraní příkazového řádku nuget.exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a7177b956930835693921163e634321548c22462
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842373"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="18f0f-103">Správa balíčků s využitím rozhraní příkazového řádku nuget.exe</span><span class="sxs-lookup"><span data-stu-id="18f0f-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="18f0f-104">Nástroj příkazového řádku můžete snadno aktualizovat a obnovení balíčků NuGet do projektů a řešení.</span><span class="sxs-lookup"><span data-stu-id="18f0f-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="18f0f-105">Tento nástroj poskytuje všechny funkce NuGet pro Windows a také poskytuje většinu funkcí na Mac a Linux, když je spuštěno mono.</span><span class="sxs-lookup"><span data-stu-id="18f0f-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="18f0f-106">Rozhraní příkazového řádku nuget.exe je pro projekty SDK stylu (například-sady SDK styl projekt, který cílí na knihovny .NET Standard) a rozhraní .NET Framework projektu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-106">The nuget.exe CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="18f0f-107">Pokud používáte sadu SDK styl projektu, který se migroval na `PackageReference`, místo toho použijte rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="18f0f-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the dotnet CLI instead.</span></span> <span data-ttu-id="18f0f-108">Vyžaduje se rozhraní příkazového řádku NuGet [souboru packages.config](../reference/packages-config.md) soubor pro odkazy na balíček.</span><span class="sxs-lookup"><span data-stu-id="18f0f-108">The NuGet CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="18f0f-109">Ve většině scénářů doporučujeme [migraci projektů SDK styl](../reference/migrate-packages-config-to-package-reference.md) , které používají `packages.config` na PackageReference, a pak můžete použít rozhraní příkazového řádku dotnet místo `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="18f0f-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the dotnet CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="18f0f-110">Migrace není aktuálně k dispozici pro projekty jazyka C++ a technologií ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="18f0f-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="18f0f-111">Tento článek popisuje základní informace o využití pro některé z nejčastěji používané příkazy rozhraní příkazového řádku nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="18f0f-111">This article shows you basic usage for a few of the most common nuget.exe CLI commands.</span></span> <span data-ttu-id="18f0f-112">Pro většinu těchto příkazů nástroje rozhraní příkazového řádku hledá soubor projektu do aktuálního adresáře, pokud soubor projektu je zadané v příkazu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="18f0f-113">Úplný seznam příkazů a argumenty, které můžete použít, najdete v článku [referenční informace o rozhraní příkazového řádku nuget.exe](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="18f0f-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18f0f-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="18f0f-114">Prerequisites</span></span>

- <span data-ttu-id="18f0f-115">Nainstalujte `nuget.exe` rozhraní příkazového řádku, stáhněte si ji z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, který `.exe` soubor vhodný složky a přidání složky do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="18f0f-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="18f0f-116">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="18f0f-116">Install a package</span></span>

<span data-ttu-id="18f0f-117">[Nainstalovat](../tools/cli-ref-install.md) příkaz stáhne a nainstaluje balíček do projektu, jako výchozí se použije aktuální složku, pomocí zadaného balíčku zdroje.</span><span class="sxs-lookup"><span data-stu-id="18f0f-117">The [install](../tools/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="18f0f-118">Nainstalovat nové balíčky do *balíčky* složku v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18f0f-119">`install`Příkaz neprovede žádné změny souboru projektu nebo *souboru packages.config*; tímto způsobem je podobný `restore` , pouze na disk přidá balíčky ale nedojde ke změně závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="18f0f-120">Můžete přidat závislost, přidejte balíček přes uživatelské rozhraní Správce balíčků nebo konzoly v sadě Visual Studio, nebo upravte *souboru packages.config* a spustit některý `install` nebo `restore`.</span><span class="sxs-lookup"><span data-stu-id="18f0f-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="18f0f-121">Otevřete příkazový řádek a přejděte do adresáře, který obsahuje váš soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="18f0f-122">Použijte následující příkaz k instalaci balíčku NuGet *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="18f0f-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="18f0f-123">K instalaci `Newtonsoft.json` balíček do *balíčky* složky, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="18f0f-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="18f0f-124">Alternativně slouží následující příkaz k instalaci balíčku NuGet pomocí existující `packages.config` do souboru *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="18f0f-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="18f0f-125">Nedojde k přidání balíčku do závislostí vašeho projektu, ale nainstaluje místně.</span><span class="sxs-lookup"><span data-stu-id="18f0f-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="18f0f-126">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="18f0f-126">Install a specific version of a package</span></span>

<span data-ttu-id="18f0f-127">Pokud neurčíte verzi, při použití [nainstalovat](../tools/cli-ref-install.md) příkaz nainstaluje nejnovější verzi balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="18f0f-127">If the version is not specified when you use the [install](../tools/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="18f0f-128">Můžete také nainstalovat určitou verzi balíčku Nuget:</span><span class="sxs-lookup"><span data-stu-id="18f0f-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="18f0f-129">Chcete-li například přidat verzi 12.0.1 `Newtonsoft.json` balíček, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="18f0f-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="18f0f-130">Další informace o omezeních a chování `install`, naleznete v tématu [nainstalovat balíček](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="18f0f-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="18f0f-131">Odebrat balíček</span><span class="sxs-lookup"><span data-stu-id="18f0f-131">Remove a package</span></span>

<span data-ttu-id="18f0f-132">Pokud chcete odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat z *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="18f0f-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="18f0f-133">Pokud chcete znovu nainstaluje balíčky, použijte `restore` nebo `install` příkazu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="18f0f-134">Seznam balíčků</span><span class="sxs-lookup"><span data-stu-id="18f0f-134">List packages</span></span>

<span data-ttu-id="18f0f-135">Můžete zobrazit seznam balíčků z daného zdroje pomocí [seznamu](../tools/cli-ref-list.md) příkazu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-135">You can display a list of packages from a given source using the [list](../tools/cli-ref-list.md) command.</span></span> <span data-ttu-id="18f0f-136">Použití `-Source` pro omezení hledání.</span><span class="sxs-lookup"><span data-stu-id="18f0f-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="18f0f-137">Například balíčků v seznamu *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="18f0f-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="18f0f-138">Pokud používáte hledaný termín, hledání zahrnuje názvy balíčků, značky a Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="18f0f-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="18f0f-139">Jednotlivé aktualizace</span><span class="sxs-lookup"><span data-stu-id="18f0f-139">Update an individual package</span></span>

<span data-ttu-id="18f0f-140">NuGet nainstaluje nejnovější verzi balíčku, při použití `install` příkazu, pokud neurčíte verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="18f0f-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="18f0f-141">Aktualizovat všechny balíčky</span><span class="sxs-lookup"><span data-stu-id="18f0f-141">Update all packages</span></span>

<span data-ttu-id="18f0f-142">Použití [aktualizovat](../tools/cli-ref-update.md) příkaz k aktualizaci všech balíčků.</span><span class="sxs-lookup"><span data-stu-id="18f0f-142">Use the [update](../tools/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="18f0f-143">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) jejich nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="18f0f-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="18f0f-144">Doporučuje se spouštět `restore` dřív, než spustíte `update`.</span><span class="sxs-lookup"><span data-stu-id="18f0f-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="18f0f-145">Obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="18f0f-145">Restore packages</span></span>

<span data-ttu-id="18f0f-146">Použití [obnovení](../tools/cli-ref-restore.md) příkaz, který se stáhne a nainstaluje všechny balíčky, které chybí *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="18f0f-146">Use the [restore](../tools/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="18f0f-147">`restore` pouze balíčky přidá na disk, ale nedojde ke změně závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="18f0f-148">Chcete-li obnovit závislosti projektu, upravte `packages.config`, pak použít `restore` příkaz.</span><span class="sxs-lookup"><span data-stu-id="18f0f-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="18f0f-149">Stejně jako u druhé `dotnet` příkazy rozhraní příkazového řádku, nejprve otevřete příkazový řádek a přejděte do adresáře, který obsahuje váš soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="18f0f-149">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="18f0f-150">Chcete-li obnovit balíček pomocí `restore`:</span><span class="sxs-lookup"><span data-stu-id="18f0f-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```