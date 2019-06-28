---
title: Nainstalovat a spravovat balíčky NuGet pomocí rozhraní příkazového řádku dotnet
description: Pokyny k používání rozhraní příkazového řádku dotnet pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a8fd525f2446f9468664f1d80ef8808127a24be7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427641"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="c099e-103">Instalace a Správa balíčků s využitím rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="c099e-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="c099e-104">Nástroj příkazového řádku umožňuje snadno nainstalování, odinstalování a aktualizace balíčků NuGet do projektů a řešení.</span><span class="sxs-lookup"><span data-stu-id="c099e-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="c099e-105">Běží na Windows, Mac OS X a Linux.</span><span class="sxs-lookup"><span data-stu-id="c099e-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="c099e-106">Rozhraní příkazového řádku dotnet je pro použití v projektu .NET Core a .NET Standard (typy SDK – vizuální styl projektu) a pro jakékoli jiné sady SDK – vizuální styl projekty (například SDK – vizuální styl projektu aplikace, které cílí na .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="c099e-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="c099e-107">Další informace najdete v tématu [SDK atribut](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="c099e-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="c099e-108">Tento článek popisuje základní informace o využití pro některé z nejčastěji používané příkazy rozhraní příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="c099e-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="c099e-109">Pro většinu těchto příkazů nástroje rozhraní příkazového řádku hledá soubor projektu do aktuálního adresáře, pokud soubor projektu je zadané v příkazu (soubor projektu je volitelný přepínač).</span><span class="sxs-lookup"><span data-stu-id="c099e-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="c099e-110">Úplný seznam příkazů a argumenty, které můžete použít, najdete v článku [nástroje rozhraní příkazového řádku (CLI) pro .NET Core](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="c099e-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../tools/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c099e-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c099e-111">Prerequisites</span></span>

- <span data-ttu-id="c099e-112">[.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="c099e-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="c099e-113">Spouští se v sadě Visual Studio 2017, které pomocí libovolné platformy .NET Core se automaticky nainstaluje rozhraní příkazového řádku dotnet související úlohy.</span><span class="sxs-lookup"><span data-stu-id="c099e-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="c099e-114">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="c099e-114">Install a package</span></span>

<span data-ttu-id="c099e-115">[příkaz DotNet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu a pak spustí `dotnet restore` k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="c099e-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="c099e-116">Otevřete příkazový řádek a přejděte do adresáře, který obsahuje váš soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="c099e-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="c099e-117">Použijte následující příkaz k instalaci balíčku Nuget:</span><span class="sxs-lookup"><span data-stu-id="c099e-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="c099e-118">Například, chcete-li nainstalovat `Newtonsoft.Json` balíček, použijte následující příkaz</span><span class="sxs-lookup"><span data-stu-id="c099e-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="c099e-119">Po dokončení příkazu, podívejte se na soubor projektu a ujistěte se, že byl nainstalován balíček.</span><span class="sxs-lookup"><span data-stu-id="c099e-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="c099e-120">Můžete otevřít `.csproj` soubor přidaný odkaz:</span><span class="sxs-lookup"><span data-stu-id="c099e-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="c099e-121">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="c099e-121">Install a specific version of a package</span></span>

<span data-ttu-id="c099e-122">Pokud není zadána verze, NuGet nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="c099e-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="c099e-123">Můžete také použít [se příkaz dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) příkaz k instalaci na konkrétní verzi balíčku Nuget:</span><span class="sxs-lookup"><span data-stu-id="c099e-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="c099e-124">Chcete-li například přidat verzi 12.0.1 `Newtonsoft.Json` balíček, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="c099e-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="c099e-125">Odkazy na balíček seznamu</span><span class="sxs-lookup"><span data-stu-id="c099e-125">List package references</span></span>

<span data-ttu-id="c099e-126">Můžete zobrazit seznam odkazy na balíček pro váš projekt používá [uvedení balíčku dotnet](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) příkazu.</span><span class="sxs-lookup"><span data-stu-id="c099e-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="c099e-127">Odebrat balíček</span><span class="sxs-lookup"><span data-stu-id="c099e-127">Remove a package</span></span>

<span data-ttu-id="c099e-128">Použití [dotnet odebrat balíček](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) příkazu odeberte odkaz na balíček ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="c099e-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="c099e-129">Například, chcete-li odebrat `Newtonsoft.Json` balíček, použijte následující příkaz</span><span class="sxs-lookup"><span data-stu-id="c099e-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="c099e-130">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="c099e-130">Update a package</span></span>

<span data-ttu-id="c099e-131">NuGet nainstaluje nejnovější verzi balíčku, při použití `dotnet add package` příkazu, pokud neurčíte verzi balíčku (`-v` přepínače).</span><span class="sxs-lookup"><span data-stu-id="c099e-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="c099e-132">Obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="c099e-132">Restore packages</span></span>

<span data-ttu-id="c099e-133">Použití [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) příkaz, který obnoví balíčky uvedené v souboru projektu (viz [PackageReference](../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="c099e-133">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="c099e-134">S .NET Core 2.0 nebo novější, obnovení se provádí automaticky pomocí `dotnet build` a `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="c099e-134">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="c099e-135">Od verze NuGet 4.0, toto řešení běží stejný kód jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="c099e-135">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="c099e-136">Chcete-li obnovit balíček pomocí `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="c099e-136">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```
