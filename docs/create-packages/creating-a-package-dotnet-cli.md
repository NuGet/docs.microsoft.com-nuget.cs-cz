---
title: Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 2fcba9dd6bbc7ff4e9b5b8b57250c399f59a1c5e
ms.sourcegitcommit: e02482e15c0cef63153086ed50d14f5b2a38f598
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473841"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet

Bez ohledu na to, co váš balíček používá, nebo jaký kód obsahuje, můžete použít jeden z nástrojů rozhraní příkazového řádku ( `nuget.exe` nebo) `dotnet.exe` k zabalení této funkce do komponenty, kterou lze sdílet a používat v jakémkoli počtu jiných vývojářů. Tento článek popisuje, jak vytvořit balíček pomocí rozhraní příkazového řádku dotnet. Informace o instalaci rozhraní `dotnet` příkazového řádku najdete v tématu [Instalace nástrojů klienta NuGet](../install-nuget-client-tools.md). Počínaje sadou Visual Studio 2017 je rozhraní příkazového řádku dotnet součástí úloh .NET Core.

Pro projekty .NET Core a .NET Standard, které používají [Formát styly sady SDK](../resources/check-project-format.md)a všechny další projekty ve stylu sady SDK, nástroj NuGet používá informace v souboru projektu přímo k vytvoření balíčku. Podrobné kurzy najdete v tématech [vytváření .NET Standard balíčků pomocí příkazu DOTNET CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) nebo [vytváření balíčků .NET Standard pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack`je obdobou funkcí `dotnet pack` . Pro sestavení pomocí nástroje MSBuild si přečtěte téma [Vytvoření balíčku NuGet pomocí MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Toto téma se vztahuje na projekty ve [stylu sady SDK](../resources/check-project-format.md) , obvykle v projektech .NET Core a .NET Standard.

## <a name="set-properties"></a>Nastavení vlastností

Pro vytvoření balíčku jsou vyžadovány následující vlastnosti.

- `PackageId`, identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček. Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .
- `Version`, konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md). Pokud není zadaný, použije se výchozí hodnota 1.0.0.
- Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)
- `Authors`, informace o autorovi a vlastníka. Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .
- `Company`, název vaší společnosti. Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .

V sadě Visual Studio můžete nastavit tyto hodnoty ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, zvolte **vlastnosti**a vyberte kartu **balíček** ). Tyto vlastnosti lze také nastavit přímo v souborech projektu ( `.csproj` ).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo jakýkoli ze zdrojů balíčku, který používáte.

Následující příklad ukazuje jednoduchý a kompletní soubor projektu s těmito vlastnostmi, které jsou k dispozici. (Pomocí příkazu můžete vytvořit nový výchozí projekt `dotnet new classlib` .)

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

Můžete také nastavit volitelné vlastnosti, například, `Title` `PackageDescription` a `PackageTags` , jak je popsáno v tématu [cíle sady MSBuild](../reference/msbuild-targets.md#pack-target), [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.

Podrobnosti o deklarování závislostí a zadání čísel verzí naleznete v tématu [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md) a [Správa verzí balíčků](../concepts/package-versioning.md). Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí `<IncludeAssets>` `<ExcludeAssets>` atributů a. Další informace najdete v Seee [řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Přidat volitelné pole popisu

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Spuštění příkazu Pack

Chcete-li vytvořit balíček NuGet ( `.nupkg` soubor) z projektu, spusťte `dotnet pack` příkaz, který také automaticky vytvoří projekt:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

Výstup zobrazuje cestu k `.nupkg` souboru.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automaticky generovat balíček při sestavení

Chcete-li automaticky spustit `dotnet pack` při spuštění `dotnet build` , přidejte následující řádek do souboru projektu v rámci `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Při spuštění `dotnet pack` v řešení jsou všechny projekty v řešení, které lze zabalit ( [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) vlastnost nastavena na hodnotu `true` ).

> [!NOTE]
> Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.

### <a name="test-package-installation"></a>Instalace testovacího balíčku

Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu. Testy zajistěte, aby všechny potřebné soubory byly všechny na správném místě v projektu.

Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Balíčky jsou neměnné. Pokud problém opravíte, znovu ho změňte a znovu spusťte. při opětovném testování bude stále použita stará verze balíčku, dokud [nevymažete složku globálních balíčků](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) . To je obzvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předprodejní verze pro každé sestavení.

## <a name="next-steps"></a>Další kroky

Po vytvoření balíčku, který je `.nupkg` soubor, můžete ho publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:

- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Přidat ikonu balíčku](../reference/nuspec.md#icon)
- [Transformace zdrojových a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze verzí](../create-packages/prerelease-packages.md)
- [Nastavení typu balíčku](../create-packages/set-package-type.md)
- [Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Nakonec existují další typy balíčků, o kterých byste měli vědět:

- [Nativní balíčky](../guides/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
