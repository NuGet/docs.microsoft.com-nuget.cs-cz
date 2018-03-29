---
title: Vytváření a publikování balíčku NuGet pomocí rozhraní příkazového řádku dotnet. | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Návod kurz týkající se vytváření a publikování balíčku NuGet pomocí rozhraní .NET Core příkazového řádku, dotnet.
keywords: Balíček NuGet vytvoření, publikování balíčku NuGet, NuGet kurzu balíček NuGet publikovat dotnet.
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 536e39ae64649ca1c11afa95c20872515e9e4c83
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="0fc2f-104">Vytvoření a publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="0fc2f-104">Create and publish a package</span></span>

<span data-ttu-id="0fc2f-105">Je jednoduchý proces vytvoření balíčku NuGet z knihovny tříd rozhraní .NET a publikujete ho pomocí nuget.org `dotnet` rozhraní příkazového řádku (CLI).</span><span class="sxs-lookup"><span data-stu-id="0fc2f-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fc2f-106">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0fc2f-106">Prerequisites</span></span>

1. <span data-ttu-id="0fc2f-107">Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/), což zahrnuje `dotnet` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-107">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="0fc2f-108">[Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="0fc2f-109">Vytvoření nového účtu odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="0fc2f-110">Účet je potřeba zkontrolovat, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="0fc2f-111">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="0fc2f-111">Create a class library project</span></span>

<span data-ttu-id="0fc2f-112">Můžete použít existující projekt knihovna tříd rozhraní .NET pro kód, který chcete balíček nebo vytvořit jednoduchý takto:</span><span class="sxs-lookup"><span data-stu-id="0fc2f-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="0fc2f-113">Vytvořte složku s názvem `AppLogger` a změňte do ní.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="0fc2f-114">Vytvoření projektu pomocí `dotnet new classlib`, který používá název aktuální složce pro projekt.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="0fc2f-115">Přidat balíček metadata do souboru projektu</span><span class="sxs-lookup"><span data-stu-id="0fc2f-115">Add package metadata to the project file</span></span>

<span data-ttu-id="0fc2f-116">Každý balíček NuGet musí manifestu, který popisuje obsah balíčku a závislosti.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="0fc2f-117">V posledním balíčku, manifest je `.nuspec` soubor, který se vygeneruje z vlastností metadat NuGet, které zahrnují v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="0fc2f-118">Otevřete soubor projektu (`.csproj`) a přidejte následující minimální vlastnosti uvnitř ukončení `<PropertyGroup>` značky, změna hodnoty podle potřeby:</span><span class="sxs-lookup"><span data-stu-id="0fc2f-118">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="0fc2f-119">Zadejte balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="0fc2f-120">Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).</span><span class="sxs-lookup"><span data-stu-id="0fc2f-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="0fc2f-121">Přidejte volitelné vlastnosti popisu ve [NuGet metadata vlastnosti](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="0fc2f-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="0fc2f-122">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **PackageTags** vlastnosti, jako jsou značky ostatní najít váš balíček a co provádí.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="0fc2f-123">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="0fc2f-123">Run the pack command</span></span>

<span data-ttu-id="0fc2f-124">K vytvoření balíčku NuGet ( `.nupkg` souboru) z projektu, spusťte `dotnet pack` příkaz, který také automaticky sestavení projektu:</span><span class="sxs-lookup"><span data-stu-id="0fc2f-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="0fc2f-125">Výstup zobrazuje cestu k `.nupkg` souboru:</span><span class="sxs-lookup"><span data-stu-id="0fc2f-125">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="0fc2f-126">Automaticky generovat balíček na sestavení</span><span class="sxs-lookup"><span data-stu-id="0fc2f-126">Automatically generate package on build</span></span>

<span data-ttu-id="0fc2f-127">Pokud chcete automaticky spustit `dotnet pack` při spuštění `dotnet build`, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="0fc2f-127">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="0fc2f-128">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="0fc2f-128">Publish the package</span></span>

<span data-ttu-id="0fc2f-129">Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `dotnet nuget push` příkaz spolu s klíčem rozhraní API získali z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-129">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="0fc2f-130">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="0fc2f-130">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="0fc2f-131">Publikování pomocí nabízených nuget dotnet.</span><span class="sxs-lookup"><span data-stu-id="0fc2f-131">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="0fc2f-132">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="0fc2f-132">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="0fc2f-133">Spravovat zveřejněný balíček</span><span class="sxs-lookup"><span data-stu-id="0fc2f-133">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="0fc2f-134">Související témata</span><span class="sxs-lookup"><span data-stu-id="0fc2f-134">Related topics</span></span>

- [<span data-ttu-id="0fc2f-135">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="0fc2f-135">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="0fc2f-136">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="0fc2f-136">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="0fc2f-137">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="0fc2f-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="0fc2f-138">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="0fc2f-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="0fc2f-139">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="0fc2f-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="0fc2f-140">Podepsání balíčků</span><span class="sxs-lookup"><span data-stu-id="0fc2f-140">Signing packages</span></span>](../create-packages/Sign-a-package.md)
