---
title: Instalace a Správa balíčků NuGet pomocí rozhraní příkazového řádku dotnet
description: Pokyny pro použití rozhraní příkazového řádku dotnet pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: fecf14f0f04d5063f89080b2756f988739c1412c
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859262"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="cf94d-103">Instalace a Správa balíčků pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="cf94d-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="cf94d-104">Nástroj rozhraní příkazového řádku umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="cf94d-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="cf94d-105">Běží na Windows, Mac OS X a Linux.</span><span class="sxs-lookup"><span data-stu-id="cf94d-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="cf94d-106">Rozhraní příkazového řádku dotnet je pro použití ve vašem projektu .NET Core a .NET Standard (typy projektů ve stylu sady SDK) a pro všechny další projekty ve stylu sady SDK (například projekt sady SDK, který cílí na .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="cf94d-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="cf94d-107">Další informace najdete v tématu [atribut sady SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="cf94d-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="cf94d-108">Tento článek popisuje základní použití pro několik nejběžnějších příkazů příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="cf94d-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="cf94d-109">Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud soubor projektu není zadán v příkazu (soubor projektu je volitelný přepínač).</span><span class="sxs-lookup"><span data-stu-id="cf94d-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="cf94d-110">Úplný seznam příkazů a argumenty, které můžete použít, najdete v tématu [nástroje rozhraní příkazového řádku (CLI) .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="cf94d-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf94d-111">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="cf94d-111">Prerequisites</span></span>

- <span data-ttu-id="cf94d-112">[.NET Core SDK](https://www.microsoft.com/net/download/), která poskytuje `dotnet` Nástroj příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="cf94d-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="cf94d-113">Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.</span><span class="sxs-lookup"><span data-stu-id="cf94d-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="cf94d-114">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="cf94d-114">Install a package</span></span>

<span data-ttu-id="cf94d-115">[dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu a potom spustí `dotnet restore` instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="cf94d-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="cf94d-116">Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="cf94d-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="cf94d-117">K instalaci balíčku NuGet použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="cf94d-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="cf94d-118">Pokud například chcete `Newtonsoft.Json` balíček nainstalovat, použijte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="cf94d-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="cf94d-119">Po dokončení příkazu si prohlédněte soubor projektu a ujistěte se, že byl balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="cf94d-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="cf94d-120">Tento soubor můžete otevřít `.csproj` a zobrazit tak přidaný odkaz:</span><span class="sxs-lookup"><span data-stu-id="cf94d-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="cf94d-121">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="cf94d-121">Install a specific version of a package</span></span>

<span data-ttu-id="cf94d-122">Pokud není zadaná verze, NuGet nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="cf94d-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="cf94d-123">K instalaci konkrétní verze balíčku NuGet můžete použít taky příkaz [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) :</span><span class="sxs-lookup"><span data-stu-id="cf94d-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="cf94d-124">Pokud například chcete přidat 12.0.1 verze `Newtonsoft.Json` balíčku, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="cf94d-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="cf94d-125">Výpis odkazů na balíčky</span><span class="sxs-lookup"><span data-stu-id="cf94d-125">List package references</span></span>

<span data-ttu-id="cf94d-126">Odkazy na balíček pro svůj projekt můžete zobrazit pomocí příkazu pro [Výpis balíčku dotnet](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) .</span><span class="sxs-lookup"><span data-stu-id="cf94d-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="cf94d-127">Odebrat balíček</span><span class="sxs-lookup"><span data-stu-id="cf94d-127">Remove a package</span></span>

<span data-ttu-id="cf94d-128">Pomocí příkazu [dotnet Remove Package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) odeberte odkaz na balíček ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="cf94d-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="cf94d-129">Chcete-li například odebrat `Newtonsoft.Json` balíček, použijte následující příkaz</span><span class="sxs-lookup"><span data-stu-id="cf94d-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="cf94d-130">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="cf94d-130">Update a package</span></span>

<span data-ttu-id="cf94d-131">NuGet nainstaluje nejnovější verzi balíčku, když použijete `dotnet add package` příkaz, pokud nezadáte verzi balíčku ( `-v` přepínač).</span><span class="sxs-lookup"><span data-stu-id="cf94d-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="cf94d-132">Obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="cf94d-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
