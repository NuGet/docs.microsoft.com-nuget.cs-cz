---
title: Vytvoření balíčku NuGet pomocí rozhraní se kontinua dotnet CLI
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových rozhodovacích bodů, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230574"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>Vytvoření balíčku NuGet pomocí rozhraní se kontinua dotnet CLI

Bez ohledu na to, co váš balíček dělá nebo jaký `nuget.exe` kód `dotnet.exe`obsahuje, použijete jeden z nástrojů rozhraní rozhraní rozhraní cli, nebo , k balení této funkce do součásti, která může být sdílena s libovolným počtem jiných vývojářů. Tento článek popisuje, jak vytvořit balíček pomocí rozhraní SE kontinu dotnet CLI. Informace o `dotnet` instalaci nařízení o nastavení systému řízení o elIt naleznete v [tématu Instalace klientských nástrojů NuGet](../install-nuget-client-tools.md). Počínaje Visual Studio 2017, dotnet CLI je součástí úloh .NET Core.

Pro projekty .NET Core a .NET Standard, které používají [formát ve stylu sady SDK](../resources/check-project-format.md), a všechny ostatní projekty ve stylu sady SDK použije aplikace NuGet informace v souboru projektu přímo k vytvoření balíčku. Podrobné kurzy naleznete v tématu [Vytvoření standardních balíčků .NET pomocí rozhraní SE kontinu pro dotnet NEBO](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) [Vytvoření standardních balíčků .NET pomocí sady Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack`je funkce ekvivalentní `dotnet pack`. Pokud chcete stavět pomocí MSBuild, [přečtěte si informace o vytvoření balíčku NuGet pomocí služby MSBuild](creating-a-package-msbuild.md).

> [!IMPORTANT]
> Toto téma se týká projektů [ve stylu sady SDK,](../resources/check-project-format.md) obvykle projektů .NET Core a .NET Standard.

## <a name="set-properties"></a>Nastavení vlastností

K vytvoření balíčku jsou vyžadovány následující vlastnosti.

- `PackageId`, identifikátor balíčku, který musí být jedinečný v galerii, která je hostitelem balíčku. Pokud není zadán, výchozí `AssemblyName`hodnota je .
- `Version`, konkrétní číslo verze ve tvaru *Major.Minor.Patch[-Přípona],* kde *-Přípona* identifikuje [předběžné verze](prerelease-packages.md). Pokud není zadán, výchozí hodnota je 1.0.0.
- Název balíčku, jak by se měl objevit na hostiteli (jako nuget.org)
- `Authors`, informace o autorovi a majiteli. Pokud není zadán, výchozí `AssemblyName`hodnota je .
- `Company`, název vaší společnosti. Pokud není zadán, výchozí `AssemblyName`hodnota je .

V sadě Visual Studio můžete tyto hodnoty nastavit ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení, zvolte **Vlastnosti**a vyberte kartu **Balíček).** Tyto vlastnosti můžete také nastavit přímo`.csproj`v souborech projektu ( ).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Podejte balíček identifikátor, který je jedinečný v celé nuget.org nebo jakýkoli zdroj balíčku, který používáte.

Následující příklad ukazuje jednoduchý, kompletní soubor projektu s těmito vlastnostmi zahrnuty. (Pomocí `dotnet new classlib` příkazu můžete vytvořit nový výchozí projekt.)

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

Můžete `Title`také nastavit volitelné vlastnosti, `PackageDescription`například , `PackageTags`a , jak je popsáno v [cílech balíčku MSBuild](../reference/msbuild-targets.md#pack-target), [Řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> U balíčků vytvořených pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags,** protože značky pomáhají ostatním najít váš balíček a pochopit, co dělá.

Podrobnosti o deklarování závislostí a určení čísel verzí naleznete [v tématu Odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md) a [správa verzí balíčků](../concepts/package-versioning.md). Je také možné povrchové prostředky ze závislostí přímo `<IncludeAssets>` `<ExcludeAssets>` v balíčku pomocí atributy a. Další informace naleznete v tématu [Controlling závislost assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Přidání volitelného pole popisu

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Zvolte jedinečný identifikátor balíčku a nastavte číslo verze.

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Spuštění příkazu pack

Chcete-li vytvořit balíček `.nupkg` NuGet (soubor) `dotnet pack` z projektu, spusťte příkaz, který také automaticky vytvoří projekt:

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

Chcete-li `dotnet pack` se `dotnet build`při spuštění automaticky spustit , `<PropertyGroup>`přidejte do souboru projektu následující řádek v části :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Při spuštění `dotnet pack` na řešení, to zabalí všechny projekty v[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) řešení, které `true`jsou sbalitelné ( vlastnost je nastavena na ).

> [!NOTE]
> Při automatickém generování balíčku čas balení zvyšuje dobu sestavení pro váš projekt.

### <a name="test-package-installation"></a>Instalace testovacího balíčku

Před publikováním balíčku obvykle chcete otestovat proces instalace balíčku do projektu. Testy ujistěte se, že nutně soubory všechny skončí na jejich správných místech v projektu.

Instalace můžete testovat ručně v sadě Visual Studio nebo na příkazovém řádku pomocí běžných [kroků instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Balíčky jsou neměnné. Pokud problém opravíte, změňte obsah balíčku a zabalte znovu, když znovu otestujete, budete stále používat starou verzi balíčku, dokud [nevymažete složku globálních balíčků.](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) To je zvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předběžné verze v každém sestavení.

## <a name="next-steps"></a>Další kroky

Po vytvoření balíčku, což je `.nupkg` soubor, můžete jej publikovat do galerie podle vašeho výběru, jak je popsáno na [publikování balíčku](../nuget-org/publish-a-package.md).

Můžete také rozšířit možnosti balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:

- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Přidat ikonu balíčku](../reference/nuspec.md#icon)
- [Transformace zdrojových a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze](../create-packages/prerelease-packages.md)
- [Nastavení typu balíčku](../create-packages/set-package-type.md)
- [Vytváření balíčků pomocí meziop sestavení COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Nakonec existují další typy balíčků, které mají být vědomi:

- [Nativní balíčky](../guides/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
