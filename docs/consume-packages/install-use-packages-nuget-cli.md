---
title: Spravovat balíčky NuGet pomocí rozhraní příkazového řádku nuget.exe
description: Pokyny k používání rozhraní příkazového řádku nuget.exe pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: e60bca8fe2f80b044e466db2a100d6c6d167edb7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427629"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="fffe3-103">Správa balíčků s využitím rozhraní příkazového řádku nuget.exe</span><span class="sxs-lookup"><span data-stu-id="fffe3-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="fffe3-104">Nástroj příkazového řádku můžete snadno aktualizovat a obnovení balíčků NuGet do projektů a řešení.</span><span class="sxs-lookup"><span data-stu-id="fffe3-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="fffe3-105">Tento nástroj poskytuje všechny funkce NuGet pro Windows a také poskytuje většinu funkcí na Mac a Linux, když je spuštěno mono.</span><span class="sxs-lookup"><span data-stu-id="fffe3-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="fffe3-106">Rozhraní příkazového řádku nuget.exe je pro projekty SDK styl, (například jeden, který cílí na knihovny .NET Standard) a rozhraní .NET Framework projektu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-106">The nuget.exe CLI is for your .NET Framework project and non-SDK-style projects (for example, one that targets .NET Standard libraries).</span></span> <span data-ttu-id="fffe3-107">Pokud používáte sadu SDK styl projektu, který se migroval na `PackageReference`, místo toho použijte rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="fffe3-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the dotnet CLI instead.</span></span> <span data-ttu-id="fffe3-108">Vyžaduje se rozhraní příkazového řádku NuGet [souboru packages.config](../reference/packages-config.md) soubor pro odkazy na balíček.</span><span class="sxs-lookup"><span data-stu-id="fffe3-108">The NuGet CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="fffe3-109">Ve většině scénářů doporučujeme [migraci projektů SDK styl](../reference/migrate-packages-config-to-package-reference.md) , které používají `packages.config` na PackageReference, a pak můžete použít rozhraní příkazového řádku dotnet místo `nuget.exe` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="fffe3-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the dotnet CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="fffe3-110">Migrace není aktuálně k dispozici pro projekty jazyka C++ a technologií ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="fffe3-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="fffe3-111">Tento článek popisuje základní informace o využití pro některé z nejčastěji používané příkazy rozhraní příkazového řádku nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="fffe3-111">This article shows you basic usage for a few of the most common nuget.exe CLI commands.</span></span> <span data-ttu-id="fffe3-112">Pro většinu těchto příkazů nástroje rozhraní příkazového řádku hledá soubor projektu do aktuálního adresáře, pokud soubor projektu je zadané v příkazu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="fffe3-113">Úplný seznam příkazů a argumenty, které můžete použít, najdete v článku [referenční informace o rozhraní příkazového řádku nuget.exe](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="fffe3-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fffe3-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="fffe3-114">Prerequisites</span></span>

- <span data-ttu-id="fffe3-115">Nainstalujte `nuget.exe` rozhraní příkazového řádku, stáhněte si ji z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), ukládání, který `.exe` soubor vhodný složky a přidání složky do proměnné prostředí PATH.</span><span class="sxs-lookup"><span data-stu-id="fffe3-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="fffe3-116">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="fffe3-116">Install a package</span></span>

<span data-ttu-id="fffe3-117">[Nainstalovat](../tools/cli-ref-install.md) příkaz stáhne a nainstaluje balíček do projektu, jako výchozí se použije aktuální složku, pomocí zadaného balíčku zdroje.</span><span class="sxs-lookup"><span data-stu-id="fffe3-117">The [install](../tools/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="fffe3-118">Nainstalovat nové balíčky do *balíčky* složku v kořenovém adresáři projektu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fffe3-119">`install`Příkaz neprovede žádné změny souboru projektu nebo *souboru packages.config*; tímto způsobem je podobný `restore` , pouze na disk přidá balíčky ale nedojde ke změně závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="fffe3-120">Můžete přidat závislost, přidejte balíček přes uživatelské rozhraní Správce balíčků nebo konzoly v sadě Visual Studio, nebo upravte *souboru packages.config* a spustit některý `install` nebo `restore`.</span><span class="sxs-lookup"><span data-stu-id="fffe3-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="fffe3-121">Otevřete příkazový řádek a přejděte do adresáře, který obsahuje váš soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="fffe3-122">Použijte následující příkaz k instalaci balíčku NuGet *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="fffe3-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="fffe3-123">K instalaci `Newtonsoft.json` balíček do *balíčky* složky, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="fffe3-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="fffe3-124">Alternativně slouží následující příkaz k instalaci balíčku NuGet pomocí existující `packages.config` do souboru *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="fffe3-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="fffe3-125">Nedojde k přidání balíčku do závislostí vašeho projektu, ale nainstaluje místně.</span><span class="sxs-lookup"><span data-stu-id="fffe3-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="fffe3-126">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="fffe3-126">Install a specific version of a package</span></span>

<span data-ttu-id="fffe3-127">Pokud neurčíte verzi, při použití [nainstalovat](../tools/cli-ref-install.md) příkaz nainstaluje nejnovější verzi balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="fffe3-127">If the version is not specified when you use the [install](../tools/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="fffe3-128">Můžete také nainstalovat určitou verzi balíčku Nuget:</span><span class="sxs-lookup"><span data-stu-id="fffe3-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="fffe3-129">Chcete-li například přidat verzi 12.0.1 `Newtonsoft.json` balíček, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="fffe3-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="fffe3-130">Další informace o omezeních a chování `install`, naleznete v tématu [nainstalovat balíček](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="fffe3-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="fffe3-131">Odebrat balíček</span><span class="sxs-lookup"><span data-stu-id="fffe3-131">Remove a package</span></span>

<span data-ttu-id="fffe3-132">Pokud chcete odstranit jeden nebo více balíčků, odstraňte balíčky, které chcete odebrat z *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="fffe3-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="fffe3-133">Pokud chcete znovu nainstaluje balíčky, použijte `restore` nebo `install` příkazu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="fffe3-134">Seznam balíčků</span><span class="sxs-lookup"><span data-stu-id="fffe3-134">List packages</span></span>

<span data-ttu-id="fffe3-135">Můžete zobrazit seznam balíčků z daného zdroje pomocí [seznamu](../tools/cli-ref-list.md) příkazu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-135">You can display a list of packages from a given source using the [list](../tools/cli-ref-list.md) command.</span></span> <span data-ttu-id="fffe3-136">Použití `-Source` pro omezení hledání.</span><span class="sxs-lookup"><span data-stu-id="fffe3-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="fffe3-137">Například balíčků v seznamu *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="fffe3-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="fffe3-138">Pokud používáte hledaný termín, hledání zahrnuje názvy balíčků, značky a Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="fffe3-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="fffe3-139">Jednotlivé aktualizace</span><span class="sxs-lookup"><span data-stu-id="fffe3-139">Update an individual package</span></span>

<span data-ttu-id="fffe3-140">NuGet nainstaluje nejnovější verzi balíčku, při použití `install` příkazu, pokud neurčíte verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="fffe3-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="fffe3-141">Aktualizovat všechny balíčky</span><span class="sxs-lookup"><span data-stu-id="fffe3-141">Update all packages</span></span>

<span data-ttu-id="fffe3-142">Použití [aktualizovat](../tools/cli-ref-update.md) příkaz k aktualizaci všech balíčků.</span><span class="sxs-lookup"><span data-stu-id="fffe3-142">Use the [update](../tools/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="fffe3-143">Aktualizuje všechny balíčky v projektu (pomocí `packages.config`) jejich nejnovější dostupné verze.</span><span class="sxs-lookup"><span data-stu-id="fffe3-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="fffe3-144">Doporučuje se spouštět `restore` dřív, než spustíte `update`.</span><span class="sxs-lookup"><span data-stu-id="fffe3-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="fffe3-145">Obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="fffe3-145">Restore packages</span></span>

<span data-ttu-id="fffe3-146">Použití [obnovení](../tools/cli-ref-restore.md) příkaz, který se stáhne a nainstaluje všechny balíčky, které chybí *balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="fffe3-146">Use the [restore](../tools/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="fffe3-147">`restore` pouze balíčky přidá na disk, ale nedojde ke změně závislosti projektu.</span><span class="sxs-lookup"><span data-stu-id="fffe3-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="fffe3-148">Chcete-li obnovit závislosti projektu, upravte `packages.config`, pak použít `restore` příkaz.</span><span class="sxs-lookup"><span data-stu-id="fffe3-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="fffe3-149">Chcete-li obnovit balíček pomocí `restore`:</span><span class="sxs-lookup"><span data-stu-id="fffe3-149">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```