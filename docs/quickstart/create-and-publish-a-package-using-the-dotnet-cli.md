---
title: Vytvoření a publikování balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Kurz návod týkající se vytváření a publikování balíčku NuGet pomocí .NET Core CLI, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 4e96d9969c8b4570ee69501d6529986f891ea4dc
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842597"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Rychlý start: Vytvoření a publikování balíčku (rozhraní příkazového řádku dotnet)

Je jednoduchý proces vytvoření balíčku NuGet z knihovny tříd .NET a publikování na nuget.org pomocí `dotnet` rozhraní příkazového řádku (CLI).

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/), což zahrnuje `dotnet` rozhraní příkazového řádku. Spouští se v sadě Visual Studio 2017, které pomocí libovolné platformy .NET Core se automaticky nainstaluje rozhraní příkazového řádku dotnet související úlohy.

1. [Zaregistrujte si bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte. Vytvoření nového účtu se odešle e-mail s potvrzením. Účet musí ověřit dříve, než můžete nahrát balíček.

## <a name="create-a-class-library-project"></a>Vytvořte projekt knihovny tříd

Můžete použít existující projekt knihovny tříd .NET pro kód, který chcete balíček nebo vytvořit jednoduchý následujícím způsobem:

1. Vytvořte složku s názvem `AppLogger` a změňte do něj.

1. Vytvořte projekt pomocí `dotnet new classlib`, který používá název aktuální složky projektu.

## <a name="add-package-metadata-to-the-project-file"></a>Přidejte balíček metadata do souboru projektu

Každý balíček NuGet musí manifestu, který popisuje obsah balíčku a závislosti. V posledním balíčku je manifest `.nuspec` souboru, který je generován z vlastnosti metadat NuGet, které zahrnete do souboru projektu.

1. Otevřete soubor projektu (`.csproj`) a přidejte následující minimální vlastnosti uvnitř stávající `<PropertyGroup>` značky, změna hodnoty podle potřeby:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Zadejte balíček identifikátor, který je jedinečný v rámci nuget.org nebo cokoli, co můžete hostovat používáte. Pro Tento názorný postup doporučujeme, abyste pozdějším kroku publikování provádění balíček veřejně viditelné (i když nepravděpodobné, že kdo bude ve skutečnosti použít) včetně "Ukázkový" nebo "Test" v názvu.

1. Přidat všechny volitelné vlastnosti podle popisu ve [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Pro balíčky sestavené ke zveřejnění, věnujte zvláštní pozornost **PackageTags** vlastnost, protože značky pomoci ostatním najít váš balíček a pochopit jeho význam.

## <a name="run-the-pack-command"></a>Spusťte příkaz pack

K sestavení balíčku NuGet ( `.nupkg` souboru) z projektu, spusťte `dotnet pack` příkaz, který také automaticky sestaví projekt:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Výstup zobrazuje cestu k `.nupkg` souboru:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automaticky generovat balíček na sestavení

Pro automatické spouštění `dotnet pack` při spuštění `dotnet build`, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Publikování balíčku

Jakmile budete mít `.nupkg` souboru, ji publikujete do nuget.org pomocí `dotnet nuget push` příkaz spolu s klíčem rozhraní API získaných z nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získat klíč rozhraní API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí nuget dotnet nasdílení změn

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikování chyby

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Správa publikované balíčku

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../nuget-org/publish-a-package.md)
- [Balíčky v předběžné verzi](../create-packages/Prerelease-Packages.md)
- [Podpora více cílových architektur](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Vytváření balíčků symbolů](../create-packages/symbol-packages-snupkg.md)
- [Podepsání balíčků](../create-packages/Sign-a-package.md)
