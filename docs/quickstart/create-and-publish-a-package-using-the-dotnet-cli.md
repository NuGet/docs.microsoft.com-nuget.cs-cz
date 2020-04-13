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
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Úvodní příručka: Vytvoření a publikování balíčku (dotnet CLI)

Je to jednoduchý proces k vytvoření balíčku NuGet z knihovny tříd .NET a publikovat jej nuget.org pomocí rozhraní `dotnet` příkazového řádku (CLI).

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte sadu [.NET Core SDK](https://www.microsoft.com/net/download/), která obsahuje `dotnet` rozhraní se kli. Počínaje Visual Studio 2017, dotnet CLI se automaticky nainstaluje s všechny úlohy související s jádrem .NET.

1. [Zaregistrujte se zdarma účet na nuget.org,](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) pokud nemáte ještě jeden. Vytvoření nového účtu odešle potvrzovací e-mail. Před nahráním balíčku musíte účet potvrdit.

## <a name="create-a-class-library-project"></a>Vytvoření projektu knihovny tříd

Můžete použít existující projekt knihovny tříd .NET pro kód, který chcete zabalit, nebo vytvořit jednoduchý takto:

1. Vytvořte složku `AppLogger`s názvem .

1. Otevřete příkazový řádek `AppLogger` a přepněte do složky.

1. Typ `dotnet new classlib`, který používá název aktuální složky projektu.

   Tím se vytvoří nový projekt.

## <a name="add-package-metadata-to-the-project-file"></a>Přidání metadat balíčku do souboru projektu

Každý balíček NuGet potřebuje manifest, který popisuje obsah balíčku a závislosti. V konečném balíčku manifest je `.nuspec` soubor, který je generován z vlastností metadat NuGet, které zahrnete do souboru projektu.

1. Otevřete soubor`.csproj`projektu ( ) a přidejte `<PropertyGroup>` následující minimální vlastnosti uvnitř existující značky a podle potřeby změníte hodnoty:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Poskytněte balíčku identifikátor, který je jedinečný v nuget.org nebo libovolném hostiteli, který používáte. Pro tento návod doporučujeme zahrnout "Ukázka" nebo "Test" v názvu jako pozdější krok publikování dělá balíček veřejně viditelné (i když je nepravděpodobné, že někdo bude skutečně používat).

1. Přidejte všechny volitelné vlastnosti popsané ve [vlastnostech metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags,** protože značky pomáhají ostatním najít váš balíček a pochopit, co dělá.

## <a name="run-the-pack-command"></a>Spuštění příkazu pack

Chcete-li vytvořit balíček `.nupkg` NuGet (soubor) `dotnet pack` z projektu, spusťte příkaz, který také automaticky vytvoří projekt:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

Výstup ukazuje cestu k `.nupkg` souboru:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automaticky generovat balíček při sestavení

Chcete-li `dotnet pack` se `dotnet build`při spuštění automaticky spustit , `<PropertyGroup>`přidejte do souboru projektu následující řádek v části :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile máte `.nupkg` soubor, publikujete jej `dotnet nuget push` nuget.org pomocí příkazu spolu s klíčem rozhraní API získaným z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získání klíče rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikovat pomocí dotnet nuget push

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Chyby publikování

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikovaného balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a>Související video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

Další videa NuGet najdete na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) a [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="next-steps"></a>Další kroky

Gratulujeme k vytvoření prvního balíčku NuGet!

> [!div class="nextstepaction"]
> [Vytvoření balíčku](../create-packages/creating-a-package-dotnet-cli.md)

Chcete-li prozkoumat další, které NuGet nabízí, vyberte níže uvedené odkazy.

- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Předběžné verze balíčků](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Vytváření balíčků symbolů](../create-packages/symbol-packages-snupkg.md)
- [Podepsání balíčků](../create-packages/Sign-a-package.md)
