---
title: Vytvoření a publikování balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Návod k vytvoření a publikování balíčku NuGet pomocí .NET Core CLI, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 30a77b427fe0a33b41262c5784045e5a6b10852f
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419982"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="8022b-103">Rychlý start: Vytvoření a publikování balíčku (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="8022b-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="8022b-104">Je to jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET a jeho publikování na NuGet.org pomocí `dotnet` rozhraní příkazového řádku (CLI).</span><span class="sxs-lookup"><span data-stu-id="8022b-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8022b-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8022b-105">Prerequisites</span></span>

1. <span data-ttu-id="8022b-106">Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/), která obsahuje rozhraní `dotnet` příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="8022b-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="8022b-107">Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8022b-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="8022b-108">[Zaregistrujte si bezplatný účet na NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , pokud ho ještě nemáte.</span><span class="sxs-lookup"><span data-stu-id="8022b-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="8022b-109">Když se vytvoří nový účet, pošle se potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="8022b-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="8022b-110">Než budete moct nahrát balíček, musíte účet potvrdit.</span><span class="sxs-lookup"><span data-stu-id="8022b-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="8022b-111">Vytvořit projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="8022b-111">Create a class library project</span></span>

<span data-ttu-id="8022b-112">Můžete použít existující projekt knihovny tříd .NET pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="8022b-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="8022b-113">Vytvořte složku s názvem `AppLogger` a změňte ji na ni.</span><span class="sxs-lookup"><span data-stu-id="8022b-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="8022b-114">Vytvořte projekt pomocí `dotnet new classlib`, který používá název aktuální složky pro projekt.</span><span class="sxs-lookup"><span data-stu-id="8022b-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="8022b-115">Přidat metadata balíčku do souboru projektu</span><span class="sxs-lookup"><span data-stu-id="8022b-115">Add package metadata to the project file</span></span>

<span data-ttu-id="8022b-116">Každý balíček NuGet potřebuje manifest, který popisuje obsah balíčku a závislosti.</span><span class="sxs-lookup"><span data-stu-id="8022b-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="8022b-117">V konečném balíčku manifest je `.nuspec` soubor, který je generován z vlastností metadat NuGet, které zahrnete do souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="8022b-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="8022b-118">Otevřete soubor projektu (`.csproj`) a do existující `<PropertyGroup>` značky přidejte následující minimální vlastnosti. Změňte hodnoty podle potřeby:</span><span class="sxs-lookup"><span data-stu-id="8022b-118">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="8022b-119">Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte.</span><span class="sxs-lookup"><span data-stu-id="8022b-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="8022b-120">Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).</span><span class="sxs-lookup"><span data-stu-id="8022b-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="8022b-121">Přidejte všechny volitelné vlastnosti popsané ve [vlastnostech metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="8022b-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="8022b-122">Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.</span><span class="sxs-lookup"><span data-stu-id="8022b-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="8022b-123">Spuštění příkazu Pack</span><span class="sxs-lookup"><span data-stu-id="8022b-123">Run the pack command</span></span>

<span data-ttu-id="8022b-124">Chcete-li vytvořit balíček NuGet ( `.nupkg` soubor) z projektu, `dotnet pack` spusťte příkaz, který také automaticky vytvoří projekt:</span><span class="sxs-lookup"><span data-stu-id="8022b-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="8022b-125">Výstup zobrazuje cestu k `.nupkg` souboru:</span><span class="sxs-lookup"><span data-stu-id="8022b-125">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="8022b-126">Automaticky generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="8022b-126">Automatically generate package on build</span></span>

<span data-ttu-id="8022b-127">Chcete-li `dotnet pack` automaticky spustit při `dotnet build`spuštění, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="8022b-127">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="8022b-128">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="8022b-128">Publish the package</span></span>

<span data-ttu-id="8022b-129">Jakmile budete mít `.nupkg` soubor, publikujete ho do NuGet.org `dotnet nuget push` pomocí příkazu společně s klíčem rozhraní API získaným z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="8022b-129">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="8022b-130">Získání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="8022b-130">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="8022b-131">Publikování pomocí příkazu dotnet NuGet push</span><span class="sxs-lookup"><span data-stu-id="8022b-131">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="8022b-132">Chyby publikování</span><span class="sxs-lookup"><span data-stu-id="8022b-132">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="8022b-133">Správa publikovaného balíčku</span><span class="sxs-lookup"><span data-stu-id="8022b-133">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="8022b-134">Další kroky</span><span class="sxs-lookup"><span data-stu-id="8022b-134">Next steps</span></span>

<span data-ttu-id="8022b-135">Blahopřejeme k vytvoření prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="8022b-135">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8022b-136">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="8022b-136">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="8022b-137">Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.</span><span class="sxs-lookup"><span data-stu-id="8022b-137">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="8022b-138">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="8022b-138">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="8022b-139">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="8022b-139">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="8022b-140">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="8022b-140">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="8022b-141">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="8022b-141">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="8022b-142">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="8022b-142">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="8022b-143">Vytváření balíčků symbolů</span><span class="sxs-lookup"><span data-stu-id="8022b-143">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="8022b-144">Podepsání balíčků</span><span class="sxs-lookup"><span data-stu-id="8022b-144">Signing packages</span></span>](../create-packages/Sign-a-package.md)
