---
title: Vytváření a publikování balíčku NuGet pomocí rozhraní příkazového řádku dotnet.
description: Návod kurz týkající se vytváření a publikování balíčku NuGet pomocí rozhraní .NET Core příkazového řádku, dotnet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: c50c92f966cd68477cd3f29ab99857911299b7ea
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818448"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="b3b72-103">Rychlý úvod: Vytvoření a publikování balíčku (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="b3b72-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="b3b72-104">Je jednoduchý proces vytvoření balíčku NuGet z knihovny tříd rozhraní .NET a publikujete ho pomocí nuget.org `dotnet` rozhraní příkazového řádku (CLI).</span><span class="sxs-lookup"><span data-stu-id="b3b72-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3b72-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b3b72-105">Prerequisites</span></span>

1. <span data-ttu-id="b3b72-106">Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/), což zahrnuje `dotnet` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="b3b72-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="b3b72-107">[Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="b3b72-107">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="b3b72-108">Vytvoření nového účtu odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="b3b72-108">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="b3b72-109">Účet je potřeba zkontrolovat, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="b3b72-109">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="b3b72-110">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="b3b72-110">Create a class library project</span></span>

<span data-ttu-id="b3b72-111">Můžete použít existující projekt knihovna tříd rozhraní .NET pro kód, který chcete balíček nebo vytvořit jednoduchý takto:</span><span class="sxs-lookup"><span data-stu-id="b3b72-111">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="b3b72-112">Vytvořte složku s názvem `AppLogger` a změňte do ní.</span><span class="sxs-lookup"><span data-stu-id="b3b72-112">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="b3b72-113">Vytvoření projektu pomocí `dotnet new classlib`, který používá název aktuální složce pro projekt.</span><span class="sxs-lookup"><span data-stu-id="b3b72-113">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="b3b72-114">Přidat balíček metadata do souboru projektu</span><span class="sxs-lookup"><span data-stu-id="b3b72-114">Add package metadata to the project file</span></span>

<span data-ttu-id="b3b72-115">Každý balíček NuGet musí manifestu, který popisuje obsah balíčku a závislosti.</span><span class="sxs-lookup"><span data-stu-id="b3b72-115">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="b3b72-116">V posledním balíčku, manifest je `.nuspec` soubor, který se vygeneruje z vlastností metadat NuGet, které zahrnují v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="b3b72-116">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="b3b72-117">Otevřete soubor projektu (`.csproj`) a přidejte následující minimální vlastnosti uvnitř ukončení `<PropertyGroup>` značky, změna hodnoty podle potřeby:</span><span class="sxs-lookup"><span data-stu-id="b3b72-117">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="b3b72-118">Zadejte balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte.</span><span class="sxs-lookup"><span data-stu-id="b3b72-118">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="b3b72-119">Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).</span><span class="sxs-lookup"><span data-stu-id="b3b72-119">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="b3b72-120">Přidejte volitelné vlastnosti popisu ve [NuGet metadata vlastnosti](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="b3b72-120">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="b3b72-121">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **PackageTags** vlastnosti, jako jsou značky ostatní najít váš balíček a co provádí.</span><span class="sxs-lookup"><span data-stu-id="b3b72-121">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="b3b72-122">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="b3b72-122">Run the pack command</span></span>

<span data-ttu-id="b3b72-123">K vytvoření balíčku NuGet ( `.nupkg` souboru) z projektu, spusťte `dotnet pack` příkaz, který také automaticky sestavení projektu:</span><span class="sxs-lookup"><span data-stu-id="b3b72-123">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="b3b72-124">Výstup zobrazuje cestu k `.nupkg` souboru:</span><span class="sxs-lookup"><span data-stu-id="b3b72-124">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="b3b72-125">Automaticky generovat balíček na sestavení</span><span class="sxs-lookup"><span data-stu-id="b3b72-125">Automatically generate package on build</span></span>

<span data-ttu-id="b3b72-126">Pokud chcete automaticky spustit `dotnet pack` při spuštění `dotnet build`, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="b3b72-126">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="b3b72-127">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="b3b72-127">Publish the package</span></span>

<span data-ttu-id="b3b72-128">Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `dotnet nuget push` příkaz spolu s klíčem rozhraní API získali z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b3b72-128">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="b3b72-129">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="b3b72-129">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="b3b72-130">Publikování pomocí nabízených nuget dotnet.</span><span class="sxs-lookup"><span data-stu-id="b3b72-130">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="b3b72-131">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="b3b72-131">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="b3b72-132">Spravovat zveřejněný balíček</span><span class="sxs-lookup"><span data-stu-id="b3b72-132">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="b3b72-133">Související témata</span><span class="sxs-lookup"><span data-stu-id="b3b72-133">Related topics</span></span>

- [<span data-ttu-id="b3b72-134">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="b3b72-134">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="b3b72-135">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="b3b72-135">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="b3b72-136">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="b3b72-136">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="b3b72-137">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="b3b72-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="b3b72-138">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="b3b72-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b3b72-139">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="b3b72-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b3b72-140">Podepsání balíčků</span><span class="sxs-lookup"><span data-stu-id="b3b72-140">Signing packages</span></span>](../create-packages/Sign-a-package.md)
