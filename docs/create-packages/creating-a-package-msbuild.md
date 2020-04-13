---
title: Vytvoření balíčku NuGet pomocí msbuildu
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových rozhodovacích bodů, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231315"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Vytvoření balíčku NuGet pomocí msbuildu

Při vytváření balíčku NuGet z vašeho kódu, balíček této funkce do součásti, která může být sdílena s a používat libovolný počet jiných vývojářů. Tento článek popisuje, jak vytvořit balíček pomocí MSBuild. MSBuild je dodáván předinstalovaný s každou úlohou sady Visual Studio, která obsahuje NuGet. Dále můžete také použít MSBuild prostřednictvím dotnet CLI s [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).

Pro projekty .NET Core a .NET Standard, které používají [formát ve stylu sady SDK](../resources/check-project-format.md), a všechny ostatní projekty ve stylu sady SDK použije aplikace NuGet informace v souboru projektu přímo k vytvoření balíčku.  Pro projekt, který používá `<PackageReference>`s formátem SDK , nuget také používá soubor projektu k vytvoření balíčku.

Projekty ve stylu sady SDK mají ve výchozím nastavení k dispozici funkci balíčku. Pro projekty PackageReference ve stylu sdk je třeba přidat balíček NuGet.Build.Tasks.Pack do závislostí projektu. Podrobné informace o cílech balíčku MSBuild naleznete v [tématu NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).

Příkaz, který vytvoří `msbuild -t:pack`balíček , je `dotnet pack`funkce ekvivalentní .

> [!IMPORTANT]
> Toto téma se týká projektů [ve stylu sady SDK,](../resources/check-project-format.md) obvykle projektů .NET Core a .NET Standard, a projektů, které nepoužívají packagereference.

## <a name="set-properties"></a>Nastavení vlastností

K vytvoření balíčku jsou vyžadovány následující vlastnosti.

- `PackageId`, identifikátor balíčku, který musí být jedinečný v galerii, která je hostitelem balíčku. Pokud není zadán, výchozí `AssemblyName`hodnota je .
- `Version`, konkrétní číslo verze ve tvaru *Major.Minor.Patch[-Přípona],* kde *-Přípona* identifikuje [předběžné verze](prerelease-packages.md). Pokud není zadán, výchozí hodnota je 1.0.0.
- Název balíčku, jak by se měl objevit na hostiteli (jako nuget.org)
- `Authors`, informace o autorovi a majiteli. Pokud není zadán, výchozí `AssemblyName`hodnota je .
- `Company`, název vaší společnosti. Pokud není zadán, výchozí `AssemblyName`hodnota je .

Navíc pokud balíte projekty, které nejsou ve stylu Sady SDK a používají odkaz PackageReference, je vyžadováno následující:

- `PackageOutputPath`, výstupní složka pro balíček vygenerovaný při volání balíčku.

V sadě Visual Studio můžete tyto hodnoty nastavit ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumníku řešení, zvolte **Vlastnosti**a vyberte kartu **Balíček).** Tyto vlastnosti můžete také nastavit přímo v souborech projektu (*.csproj*).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Podejte balíček identifikátor, který je jedinečný v celé nuget.org nebo jakýkoli zdroj balíčku, který používáte.

Následující příklad ukazuje jednoduchý, kompletní soubor projektu s těmito vlastnostmi zahrnuty.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
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

## <a name="add-the-nugetbuildtaskspack-package"></a>Přidání balíčku NuGet.Build.Tasks.Pack

Pokud používáte MSBuild s projektem, který není ve stylu sady SDK, a packagereference, přidejte do projektu balíček NuGet.Build.Tasks.Pack.

1. Otevřete soubor projektu a za `<PropertyGroup>` element přidejte následující:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Otevřete příkazový řádek Vývojář (Do **vyhledávacího** pole zadejte **příkazový řádek Vývojář**).

   Obvykle chcete spustit příkazový řádek pro vývojáře pro Visual Studio z nabídky **Start,** protože bude nakonfigurován se všemi potřebnými cestami pro MSBuild.

3. Přepněte do složky obsahující soubor projektu a zadejte následující příkaz pro instalaci balíčku NuGet.Build.Tasks.Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Ujistěte se, že výstup MSBuild označuje, že sestavení bylo úspěšně dokončeno.

## <a name="run-the-msbuild--tpack-command"></a>Spustit příkaz msbuild -t:pack

Chcete-li vytvořit balíček `.nupkg` NuGet (soubor) `msbuild -t:pack` z projektu, spusťte příkaz, který také automaticky vytvoří projekt:

Do příkazového řádku Vývojář pro Visual Studio zadejte následující příkaz:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

Výstup zobrazuje cestu k `.nupkg` souboru.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Automaticky generovat balíček při sestavení

Chcete-li `msbuild -t:pack` automaticky spustit při vytváření nebo obnovení projektu, přidejte do souboru projektu následující řádek v části `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Při spuštění `msbuild -t:pack` na řešení, to zabalí všechny projekty v[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) řešení, které `true`jsou sbalitelné ( vlastnost je nastavena na ).

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

- [NuGet pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md)
- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Transformace zdrojových a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze](../create-packages/prerelease-packages.md)
- [Nastavení typu balíčku](../create-packages/set-package-type.md)
- [Vytváření balíčků pomocí meziop sestavení COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Nakonec existují další typy balíčků, které mají být vědomi:

- [Nativní balíčky](../guides/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
