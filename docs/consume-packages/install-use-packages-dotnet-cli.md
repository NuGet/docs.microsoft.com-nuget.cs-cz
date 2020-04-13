---
title: Instalace a správa balíčků NuGet pomocí rozhraní SE konstatování dotnet
description: Pokyny pro použití dotnet CLI pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825154"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="586d3-103">Instalace a správa balíčků pomocí rozhraní SE kontinua dotnet</span><span class="sxs-lookup"><span data-stu-id="586d3-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="586d3-104">Nástroj CLI umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="586d3-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="586d3-105">Běží na Windows, Mac OS X a Linux.</span><span class="sxs-lookup"><span data-stu-id="586d3-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="586d3-106">Rozhraní SE konstatování dotnet cli je pro použití v projektu .NET Core a .NET Standard (typy projektů ve stylu sady SDK) a pro všechny ostatní projekty ve stylu sady SDK (například projekt ve stylu sady SDK, který cílí na rozhraní .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="586d3-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="586d3-107">Další informace naleznete v [atributu SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="586d3-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="586d3-108">Tento článek ukazuje základní použití pro několik nejběžnějších příkazů příkazového příkazu příkazu příkazu příkazu příkazu příkazu dotnet.</span><span class="sxs-lookup"><span data-stu-id="586d3-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="586d3-109">U většiny těchto příkazů nástroj příkazcli hledá soubor projektu v aktuálním adresáři, pokud není v příkazu zadán soubor projektu (soubor projektu je volitelný přepínač).</span><span class="sxs-lookup"><span data-stu-id="586d3-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="586d3-110">Úplný seznam příkazů a argumentů, které můžete použít, naleznete v [nástrojích rozhraní CLI (.NET Core) rozhraní příkazového řádku (CLI).](../reference/dotnet-commands.md)</span><span class="sxs-lookup"><span data-stu-id="586d3-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="586d3-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="586d3-111">Prerequisites</span></span>

- <span data-ttu-id="586d3-112">Sada [.NET Core SDK](https://www.microsoft.com/net/download/) `dotnet` , která poskytuje nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="586d3-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="586d3-113">Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s všechny úlohy související s jádrem .NET.</span><span class="sxs-lookup"><span data-stu-id="586d3-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="586d3-114">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="586d3-114">Install a package</span></span>

<span data-ttu-id="586d3-115">[dotnet přidat balíček](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu, pak spustí `dotnet restore` k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="586d3-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="586d3-116">Otevřete příkazový řádek a přepněte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="586d3-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="586d3-117">K instalaci balíčku Nuget použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="586d3-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="586d3-118">Chcete-li například `Newtonsoft.Json` nainstalovat balíček, použijte následující příkaz</span><span class="sxs-lookup"><span data-stu-id="586d3-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="586d3-119">Po dokončení příkazu se podívejte na soubor projektu a ujistěte se, že byl balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="586d3-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="586d3-120">Soubor můžete `.csproj` otevřít a zobrazit tak přidanou referenci:</span><span class="sxs-lookup"><span data-stu-id="586d3-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="586d3-121">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="586d3-121">Install a specific version of a package</span></span>

<span data-ttu-id="586d3-122">Pokud není zadána verze, NuGet nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="586d3-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="586d3-123">Příkaz [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) můžete také použít k instalaci konkrétní verze balíčku Nuget:</span><span class="sxs-lookup"><span data-stu-id="586d3-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="586d3-124">Chcete-li například přidat verzi `Newtonsoft.Json` balíčku 12.0.1, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="586d3-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="586d3-125">Seznam odkazů na balíčky</span><span class="sxs-lookup"><span data-stu-id="586d3-125">List package references</span></span>

<span data-ttu-id="586d3-126">Můžete seznam odkazů na balíček pro váš projekt pomocí příkazu [balíček seznamu dotnet.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)</span><span class="sxs-lookup"><span data-stu-id="586d3-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="586d3-127">Odebrání balíčku</span><span class="sxs-lookup"><span data-stu-id="586d3-127">Remove a package</span></span>

<span data-ttu-id="586d3-128">Pomocí příkazu [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) odeberte odkaz na balíček ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="586d3-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="586d3-129">Chcete-li například `Newtonsoft.Json` balíček odebrat, použijte následující příkaz</span><span class="sxs-lookup"><span data-stu-id="586d3-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="586d3-130">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="586d3-130">Update a package</span></span>

<span data-ttu-id="586d3-131">NuGet nainstaluje nejnovější verzi balíčku při `dotnet add package` použití příkazu, pokud`-v` nezadáte verzi balíčku (přepínač).</span><span class="sxs-lookup"><span data-stu-id="586d3-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="586d3-132">Obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="586d3-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
