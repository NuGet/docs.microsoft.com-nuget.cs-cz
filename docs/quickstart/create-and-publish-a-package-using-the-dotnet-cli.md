---
title: Vytvoření a publikování balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Kurz návod týkající se vytváření a publikování balíčku NuGet pomocí .NET Core CLI, dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: 02aa7bb9d27352bbecfc718ef5bd6ee33501018d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548426"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="819b2-103">Rychlý start: Vytvoření a publikování balíčku (rozhraní příkazového řádku dotnet)</span><span class="sxs-lookup"><span data-stu-id="819b2-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="819b2-104">Je jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET a publikování na nuget.org pomocí `dotnet` rozhraní příkazového řádku (CLI).</span><span class="sxs-lookup"><span data-stu-id="819b2-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="819b2-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="819b2-105">Prerequisites</span></span>

1. <span data-ttu-id="819b2-106">Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/), což zahrnuje `dotnet` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="819b2-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="819b2-107">[Zaregistrujte si bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte.</span><span class="sxs-lookup"><span data-stu-id="819b2-107">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="819b2-108">Vytvoření nového účtu se odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="819b2-108">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="819b2-109">Účet musí ověřit dříve, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="819b2-109">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="819b2-110">Vytvořte projekt knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="819b2-110">Create a class library project</span></span>

<span data-ttu-id="819b2-111">Můžete použít existující projekt knihovny tříd .NET pro kód, který chcete balíček nebo vytvořit jednoduchý následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="819b2-111">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="819b2-112">Vytvořte složku s názvem `AppLogger` a změňte do něj.</span><span class="sxs-lookup"><span data-stu-id="819b2-112">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="819b2-113">Vytvořte projekt pomocí `dotnet new classlib`, který používá název aktuální složky projektu.</span><span class="sxs-lookup"><span data-stu-id="819b2-113">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="819b2-114">Přidejte balíček metadata do souboru projektu</span><span class="sxs-lookup"><span data-stu-id="819b2-114">Add package metadata to the project file</span></span>

<span data-ttu-id="819b2-115">Každý balíček NuGet musí manifestu, který popisuje obsah balíčku a závislosti.</span><span class="sxs-lookup"><span data-stu-id="819b2-115">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="819b2-116">V posledním balíčku je manifest `.nuspec` souboru, který je generován z vlastnosti metadat NuGet, které zahrnete do souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="819b2-116">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="819b2-117">Otevřete soubor projektu (`.csproj`) a přidejte následující minimální vlastnosti uvnitř stávající `<PropertyGroup>` značky, změna hodnoty podle potřeby:</span><span class="sxs-lookup"><span data-stu-id="819b2-117">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="819b2-118">Zadejte balíček identifikátor, který je jedinečný v rámci nuget.org nebo cokoli, co můžete hostovat používáte.</span><span class="sxs-lookup"><span data-stu-id="819b2-118">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="819b2-119">Pro Tento názorný postup doporučujeme, abyste pozdějším kroku publikování provádění balíček veřejně viditelné (i když nepravděpodobné, že kdo bude ve skutečnosti použít) včetně "Ukázkový" nebo "Test" v názvu.</span><span class="sxs-lookup"><span data-stu-id="819b2-119">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="819b2-120">Přidat všechny volitelné vlastnosti podle popisu ve [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="819b2-120">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="819b2-121">Pro balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost **PackageTags** vlastnost, protože značky pomoci ostatním najít váš balíček a pochopit jeho význam.</span><span class="sxs-lookup"><span data-stu-id="819b2-121">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="819b2-122">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="819b2-122">Run the pack command</span></span>

<span data-ttu-id="819b2-123">K sestavení balíčku NuGet ( `.nupkg` souboru) z projektu, spusťte `dotnet pack` příkaz, který také automaticky sestaví projekt:</span><span class="sxs-lookup"><span data-stu-id="819b2-123">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="819b2-124">Výstup zobrazuje cestu k `.nupkg` souboru:</span><span class="sxs-lookup"><span data-stu-id="819b2-124">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="819b2-125">Automaticky generovat balíček na sestavení</span><span class="sxs-lookup"><span data-stu-id="819b2-125">Automatically generate package on build</span></span>

<span data-ttu-id="819b2-126">Pro automatické spouštění `dotnet pack` při spuštění `dotnet build`, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="819b2-126">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="819b2-127">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="819b2-127">Publish the package</span></span>

<span data-ttu-id="819b2-128">Jakmile budete mít `.nupkg` souboru, ji publikujete do nuget.org pomocí `dotnet nuget push` příkaz spolu s klíčem rozhraní API získaných z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="819b2-128">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="819b2-129">Získat klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="819b2-129">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="819b2-130">Publikování pomocí nuget dotnet nasdílení změn</span><span class="sxs-lookup"><span data-stu-id="819b2-130">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="819b2-131">Publikování chyby</span><span class="sxs-lookup"><span data-stu-id="819b2-131">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="819b2-132">Správa publikované balíčku</span><span class="sxs-lookup"><span data-stu-id="819b2-132">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="819b2-133">Související témata</span><span class="sxs-lookup"><span data-stu-id="819b2-133">Related topics</span></span>

- [<span data-ttu-id="819b2-134">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="819b2-134">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="819b2-135">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="819b2-135">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="819b2-136">Balíčky v předběžné verzi</span><span class="sxs-lookup"><span data-stu-id="819b2-136">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="819b2-137">Podpora více cílových platforem</span><span class="sxs-lookup"><span data-stu-id="819b2-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="819b2-138">Správa verzí balíčků</span><span class="sxs-lookup"><span data-stu-id="819b2-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="819b2-139">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="819b2-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="819b2-140">Podepsání balíčků</span><span class="sxs-lookup"><span data-stu-id="819b2-140">Signing packages</span></span>](../create-packages/Sign-a-package.md)
