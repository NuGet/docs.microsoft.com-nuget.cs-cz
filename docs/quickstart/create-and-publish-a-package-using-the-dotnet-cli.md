---
title: Vytvoření a publikování balíčku NuGet pomocí rozhraní se konstatování dotnet
description: Návod k vytvoření a publikování balíčku NuGet pomocí rozhraní .NET Core CLI, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231302"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="3c717-103">Úvodní příručka: Vytvoření a publikování balíčku (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="3c717-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="3c717-104">Je to jednoduchý proces k vytvoření balíčku NuGet z knihovny tříd .NET a publikovat jej nuget.org pomocí rozhraní `dotnet` příkazového řádku (CLI).</span><span class="sxs-lookup"><span data-stu-id="3c717-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c717-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="3c717-105">Prerequisites</span></span>

1. <span data-ttu-id="3c717-106">Nainstalujte sadu [.NET Core SDK](https://www.microsoft.com/net/download/), která obsahuje `dotnet` rozhraní se kli.</span><span class="sxs-lookup"><span data-stu-id="3c717-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="3c717-107">Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s všechny úlohy související s jádrem .NET.</span><span class="sxs-lookup"><span data-stu-id="3c717-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="3c717-108">[Zaregistrujte se zdarma účet na nuget.org,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) pokud nemáte ještě jeden.</span><span class="sxs-lookup"><span data-stu-id="3c717-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="3c717-109">Vytvoření nového účtu odešle potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="3c717-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="3c717-110">Před nahráním balíčku musíte účet potvrdit.</span><span class="sxs-lookup"><span data-stu-id="3c717-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="3c717-111">Vytvoření projektu knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="3c717-111">Create a class library project</span></span>

<span data-ttu-id="3c717-112">Můžete použít existující projekt knihovny tříd .NET pro kód, který chcete zabalit, nebo vytvořit jednoduchý takto:</span><span class="sxs-lookup"><span data-stu-id="3c717-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="3c717-113">Vytvořte složku `AppLogger`s názvem .</span><span class="sxs-lookup"><span data-stu-id="3c717-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="3c717-114">Otevřete příkazový řádek `AppLogger` a přepněte do složky.</span><span class="sxs-lookup"><span data-stu-id="3c717-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="3c717-115">Typ `dotnet new classlib`, který používá název aktuální složky projektu.</span><span class="sxs-lookup"><span data-stu-id="3c717-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="3c717-116">Tím se vytvoří nový projekt.</span><span class="sxs-lookup"><span data-stu-id="3c717-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="3c717-117">Přidání metadat balíčku do souboru projektu</span><span class="sxs-lookup"><span data-stu-id="3c717-117">Add package metadata to the project file</span></span>

<span data-ttu-id="3c717-118">Každý balíček NuGet potřebuje manifest, který popisuje obsah balíčku a závislosti.</span><span class="sxs-lookup"><span data-stu-id="3c717-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="3c717-119">V konečném balíčku manifest je `.nuspec` soubor, který je generován z vlastností metadat NuGet, které zahrnete do souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="3c717-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="3c717-120">Otevřete soubor`.csproj`projektu ( ) a přidejte `<PropertyGroup>` následující minimální vlastnosti uvnitř existující značky a podle potřeby změníte hodnoty:</span><span class="sxs-lookup"><span data-stu-id="3c717-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="3c717-121">Poskytněte balíčku identifikátor, který je jedinečný v nuget.org nebo libovolném hostiteli, který používáte.</span><span class="sxs-lookup"><span data-stu-id="3c717-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="3c717-122">Pro tento návod doporučujeme zahrnout "Ukázka" nebo "Test" v názvu jako pozdější krok publikování dělá balíček veřejně viditelné (i když je nepravděpodobné, že někdo bude skutečně používat).</span><span class="sxs-lookup"><span data-stu-id="3c717-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="3c717-123">Přidejte všechny volitelné vlastnosti popsané ve [vlastnostech metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="3c717-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="3c717-124">U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags,** protože značky pomáhají ostatním najít váš balíček a pochopit, co dělá.</span><span class="sxs-lookup"><span data-stu-id="3c717-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="3c717-125">Spuštění příkazu pack</span><span class="sxs-lookup"><span data-stu-id="3c717-125">Run the pack command</span></span>

<span data-ttu-id="3c717-126">Chcete-li vytvořit balíček `.nupkg` NuGet (soubor) `dotnet pack` z projektu, spusťte příkaz, který také automaticky vytvoří projekt:</span><span class="sxs-lookup"><span data-stu-id="3c717-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="3c717-127">Výstup ukazuje cestu k `.nupkg` souboru:</span><span class="sxs-lookup"><span data-stu-id="3c717-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="3c717-128">Automaticky generovat balíček při sestavení</span><span class="sxs-lookup"><span data-stu-id="3c717-128">Automatically generate package on build</span></span>

<span data-ttu-id="3c717-129">Chcete-li `dotnet pack` se `dotnet build`při spuštění automaticky spustit , `<PropertyGroup>`přidejte do souboru projektu následující řádek v části :</span><span class="sxs-lookup"><span data-stu-id="3c717-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="3c717-130">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="3c717-130">Publish the package</span></span>

<span data-ttu-id="3c717-131">Jakmile máte `.nupkg` soubor, publikujete jej `dotnet nuget push` nuget.org pomocí příkazu spolu s klíčem rozhraní API získaným z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3c717-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="3c717-132">Získání klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="3c717-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="3c717-133">Publikovat pomocí dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="3c717-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="3c717-134">Chyby publikování</span><span class="sxs-lookup"><span data-stu-id="3c717-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="3c717-135">Správa publikovaného balíčku</span><span class="sxs-lookup"><span data-stu-id="3c717-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="3c717-136">Související video</span><span class="sxs-lookup"><span data-stu-id="3c717-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="3c717-137">Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="3c717-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c717-138">Další kroky</span><span class="sxs-lookup"><span data-stu-id="3c717-138">Next steps</span></span>

<span data-ttu-id="3c717-139">Gratulujeme k vytvoření prvního balíčku NuGet!</span><span class="sxs-lookup"><span data-stu-id="3c717-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c717-140">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="3c717-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="3c717-141">Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.</span><span class="sxs-lookup"><span data-stu-id="3c717-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="3c717-142">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="3c717-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="3c717-143">Předběžné verze balíčků</span><span class="sxs-lookup"><span data-stu-id="3c717-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="3c717-144">Podpora více cílových architektur</span><span class="sxs-lookup"><span data-stu-id="3c717-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="3c717-145">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="3c717-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="3c717-146">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="3c717-146">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="3c717-147">Vytváření balíčků symbolů</span><span class="sxs-lookup"><span data-stu-id="3c717-147">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="3c717-148">Podepsání balíčků</span><span class="sxs-lookup"><span data-stu-id="3c717-148">Signing packages</span></span>](../create-packages/Sign-a-package.md)
