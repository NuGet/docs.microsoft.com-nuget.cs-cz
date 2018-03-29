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
# <a name="create-and-publish-a-package"></a>Vytvoření a publikování balíčku

Je jednoduchý proces vytvoření balíčku NuGet z knihovny tříd rozhraní .NET a publikujete ho pomocí nuget.org `dotnet` rozhraní příkazového řádku (CLI).

## <a name="prerequisites"></a>Požadavky

1. Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/), což zahrnuje `dotnet` rozhraní příkazového řádku.

1. [Zaregistrovat bezplatný účet na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Pokud již nemáte. Vytvoření nového účtu odešle e-mail s potvrzením. Účet je potřeba zkontrolovat, než můžete nahrát balíček.

## <a name="create-a-class-library-project"></a>Vytvoření projektu knihovny tříd

Můžete použít existující projekt knihovna tříd rozhraní .NET pro kód, který chcete balíček nebo vytvořit jednoduchý takto:

1. Vytvořte složku s názvem `AppLogger` a změňte do ní.

1. Vytvoření projektu pomocí `dotnet new classlib`, který používá název aktuální složce pro projekt.

## <a name="add-package-metadata-to-the-project-file"></a>Přidat balíček metadata do souboru projektu

Každý balíček NuGet musí manifestu, který popisuje obsah balíčku a závislosti. V posledním balíčku, manifest je `.nuspec` soubor, který se vygeneruje z vlastností metadat NuGet, které zahrnují v souboru projektu.

1. Otevřete soubor projektu (`.csproj`) a přidejte následující minimální vlastnosti uvnitř ukončení `<PropertyGroup>` značky, změna hodnoty podle potřeby:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Zadejte balíček identifikátor, který je jedinečný v rámci nuget.org nebo ať hostitele je používáte. Pro účely tohoto postupu doporučujeme včetně "Ukázkové" nebo "Test" v názvu publikování později zviditelnit balíček veřejně (i když nepravděpodobné, že každý, kdo bude skutečně používáte).

1. Přidejte volitelné vlastnosti popisu ve [NuGet metadata vlastnosti](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost **PackageTags** vlastnosti, jako jsou značky ostatní najít váš balíček a co provádí.

## <a name="run-the-pack-command"></a>Spusťte příkaz pack

K vytvoření balíčku NuGet ( `.nupkg` souboru) z projektu, spusťte `dotnet pack` příkaz, který také automaticky sestavení projektu:

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

Pokud chcete automaticky spustit `dotnet pack` při spuštění `dotnet build`, přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Umožňuje publikovat balíček

Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `dotnet nuget push` příkaz spolu s klíčem rozhraní API získali z nuget.org.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Získat klíč rozhraní API

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Publikování pomocí nabízených nuget dotnet.

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Publikování chyby

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Spravovat zveřejněný balíček

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Související témata

- [Vytvoření balíčku](../create-packages/creating-a-package.md)
- [Publikování balíčku](../create-packages/publish-a-package.md)
- [Podpora více cílové rozhraní](../create-packages/supporting-multiple-target-frameworks.md)
- [Správa verzí balíčků](../reference/package-versioning.md)
- [Vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md)
- [Podepsání balíčků](../create-packages/Sign-a-package.md)
