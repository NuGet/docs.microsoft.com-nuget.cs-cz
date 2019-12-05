---
title: Instalace a Správa balíčků NuGet pomocí rozhraní příkazového řádku dotnet
description: Pokyny pro použití rozhraní příkazového řádku dotnet pro práci s balíčky NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825154"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="183ee-103">Instalace a Správa balíčků pomocí rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="183ee-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="183ee-104">Nástroj rozhraní příkazového řádku umožňuje snadno nainstalovat, odinstalovat a aktualizovat balíčky NuGet v projektech a řešeních.</span><span class="sxs-lookup"><span data-stu-id="183ee-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="183ee-105">Běží na Windows, Mac OS X a Linux.</span><span class="sxs-lookup"><span data-stu-id="183ee-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="183ee-106">Rozhraní příkazového řádku dotnet je pro použití ve vašem projektu .NET Core a .NET Standard (typy projektů ve stylu sady SDK) a pro všechny další projekty ve stylu sady SDK (například projekt sady SDK, který cílí na .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="183ee-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="183ee-107">Další informace najdete v tématu [atribut sady SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="183ee-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="183ee-108">Tento článek popisuje základní použití pro několik nejběžnějších příkazů příkazového řádku dotnet.</span><span class="sxs-lookup"><span data-stu-id="183ee-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="183ee-109">Pro většinu těchto příkazů nástroj CLI vyhledá soubor projektu v aktuálním adresáři, pokud soubor projektu není zadán v příkazu (soubor projektu je volitelný přepínač).</span><span class="sxs-lookup"><span data-stu-id="183ee-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="183ee-110">Úplný seznam příkazů a argumenty, které můžete použít, najdete v tématu [nástroje rozhraní příkazového řádku (CLI) .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="183ee-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="183ee-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="183ee-111">Prerequisites</span></span>

- <span data-ttu-id="183ee-112">[.NET Core SDK](https://www.microsoft.com/net/download/), který poskytuje nástroj příkazového řádku `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="183ee-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="183ee-113">Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.</span><span class="sxs-lookup"><span data-stu-id="183ee-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="183ee-114">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="183ee-114">Install a package</span></span>

<span data-ttu-id="183ee-115">[dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) přidá odkaz na balíček do souboru projektu a potom spustí `dotnet restore` pro instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="183ee-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="183ee-116">Otevřete příkazový řádek a přejděte do adresáře, který obsahuje soubor projektu.</span><span class="sxs-lookup"><span data-stu-id="183ee-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="183ee-117">K instalaci balíčku NuGet použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="183ee-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="183ee-118">Například pro instalaci balíčku `Newtonsoft.Json` použijte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="183ee-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="183ee-119">Po dokončení příkazu si prohlédněte soubor projektu a ujistěte se, že byl balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="183ee-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="183ee-120">Pokud chcete zobrazit přidaný odkaz, můžete otevřít soubor `.csproj`:</span><span class="sxs-lookup"><span data-stu-id="183ee-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="183ee-121">Instalace konkrétní verze balíčku</span><span class="sxs-lookup"><span data-stu-id="183ee-121">Install a specific version of a package</span></span>

<span data-ttu-id="183ee-122">Pokud není zadaná verze, NuGet nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="183ee-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="183ee-123">K instalaci konkrétní verze balíčku NuGet můžete použít taky příkaz [dotnet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) :</span><span class="sxs-lookup"><span data-stu-id="183ee-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="183ee-124">Pokud například chcete přidat 12.0.1 verze balíčku `Newtonsoft.Json`, použijte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="183ee-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="183ee-125">Výpis odkazů na balíčky</span><span class="sxs-lookup"><span data-stu-id="183ee-125">List package references</span></span>

<span data-ttu-id="183ee-126">Odkazy na balíček pro svůj projekt můžete zobrazit pomocí příkazu pro [Výpis balíčku dotnet](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) .</span><span class="sxs-lookup"><span data-stu-id="183ee-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="183ee-127">Odebrat balíček</span><span class="sxs-lookup"><span data-stu-id="183ee-127">Remove a package</span></span>

<span data-ttu-id="183ee-128">Pomocí příkazu [dotnet Remove Package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) odeberte odkaz na balíček ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="183ee-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="183ee-129">Chcete-li například odebrat balíček `Newtonsoft.Json`, použijte následující příkaz</span><span class="sxs-lookup"><span data-stu-id="183ee-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="183ee-130">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="183ee-130">Update a package</span></span>

<span data-ttu-id="183ee-131">Pokud nezadáte verzi balíčku (`-v` přepínač), nainstaluje balíček NuGet nejnovější verzi balíčku, když použijete příkaz `dotnet add package`.</span><span class="sxs-lookup"><span data-stu-id="183ee-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="183ee-132">Obnovit balíčky</span><span class="sxs-lookup"><span data-stu-id="183ee-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
