---
title: Vytvoření a publikování balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Návod k vytvoření a publikování balíčku NuGet pomocí .NET Core CLI, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 55f9c760ae05f060b748e6fbb82d8e9bd77c4e37
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825317"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Rychlý Start: vytvoření a publikování balíčku (dotnet CLI)

Je to jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET a jeho publikování na nuget.org pomocí rozhraní příkazového řádku (CLI) `dotnet`.

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/), která zahrnuje `dotnet` CLI. Počínaje sadou Visual Studio 2017 se rozhraní příkazového řádku dotnet automaticky nainstaluje se všemi úlohami souvisejícími s .NET Core.

1. [Zaregistrujte si bezplatný účet na NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , pokud ho ještě nemáte. Když se vytvoří nový účet, pošle se potvrzovací e-mail. Než budete moct nahrát balíček, musíte účet potvrdit.

## <a name="create-a-class-library-project"></a>Vytvořit projekt knihovny tříd

Můžete použít existující projekt knihovny tříd .NET pro kód, který chcete zabalit, nebo vytvořit jednoduchý, a to následujícím způsobem:

1. Vytvořte složku s názvem `AppLogger`.

1. Otevřete příkazový řádek a přepněte do složky `AppLogger`.

1. Zadejte `dotnet new classlib`, který používá název aktuální složky pro projekt.

   Tím se vytvoří nový projekt.

## <a name="add-package-metadata-to-the-project-file"></a>Přidat metadata balíčku do souboru projektu

Každý balíček NuGet potřebuje manifest, který popisuje obsah balíčku a závislosti. V konečném balíčku je manifest `.nuspec` soubor, který je vygenerován z vlastností metadat NuGet, které zahrnete do souboru projektu.

1. Otevřete soubor projektu (`.csproj`) a do existující značky `<PropertyGroup>` přidejte následující minimální vlastnosti, podle potřeby změňte hodnoty:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo libovolného hostitele, který používáte. Pro tento návod doporučujeme, abyste v názvu jako pozdější krok publikování použili "Sample" nebo "test", aby byl balíček veřejně viditelný (i když je to nepravděpodobné, že ho kdokoli bude používat).

1. Přidejte všechny volitelné vlastnosti popsané ve [vlastnostech metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.

## <a name="run-the-pack-command"></a>Spuštění příkazu Pack

Chcete-li vytvořit balíček NuGet (`.nupkg` soubor) z projektu, spusťte příkaz `dotnet pack`, který také automaticky vytvoří projekt:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

Výstup zobrazuje cestu k souboru `.nupkg`:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automaticky generovat balíček při sestavení

Chcete-li automaticky spouštět `dotnet pack` při spuštění `dotnet build`, přidejte do souboru projektu v rámci `<PropertyGroup>`následující řádek:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile budete mít soubor `.nupkg`, publikujete ho na nuget.org pomocí příkazu `dotnet nuget push` společně s klíčem rozhraní API získaným z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí příkazu dotnet NuGet push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Chyby publikování

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikovaného balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Další kroky

Blahopřejeme k vytvoření prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Vytvoření balíčku](../create-packages/creating-a-package-dotnet-cli.md)

Pokud chcete prozkoumat další možnosti, které NuGet nabízí, vyberte odkazy níže.

- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Předběžné verze balíčků](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Vytváření balíčků symbolů](../create-packages/symbol-packages-snupkg.md)
- [Podepsání balíčků](../create-packages/Sign-a-package.md)
