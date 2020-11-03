---
title: Vytvoření balíčku NuGet pomocí nástroje MSBuild
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 47a20c5566affec1cdc7772c86d8101dab162d85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237968"
---
# <a name="create-a-nuget-package-using-msbuild"></a>Vytvoření balíčku NuGet pomocí nástroje MSBuild

Když vytvoříte balíček NuGet z kódu, zabalíte tuto funkci do komponenty, kterou můžete sdílet s a používat v jakémkoli počtu jiných vývojářů. Tento článek popisuje, jak vytvořit balíček pomocí nástroje MSBuild. Nástroj MSBuild přináší předinstalované všechny úlohy sady Visual Studio, které obsahují NuGet. Kromě toho můžete také použít MSBuild prostřednictvím rozhraní příkazového řádku dotnet s nástrojem [dotnet MSBuild](/dotnet/core/tools/dotnet-msbuild).

Pro projekty .NET Core a .NET Standard, které používají [Formát styly sady SDK](../resources/check-project-format.md)a všechny další projekty ve stylu sady SDK, nástroj NuGet používá informace v souboru projektu přímo k vytvoření balíčku.  Pro nepoužitý projekt ve stylu sady SDK, který používá `<PackageReference>` , nástroj NuGet používá k vytvoření balíčku také soubor projektu.

Projekty ve stylu sady SDK mají ve výchozím nastavení dostupné funkce balíčku. Pro projekty PackageReference bez sady SDK je nutné přidat balíček NuGet. Build. Tasks. Pack do závislostí projektu. Podrobné informace o cílech sady MSBuild Pack naleznete v tématu [sada NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md).

Příkaz, který vytváří balíček, `msbuild -t:pack` , je funkce, která je ekvivalentní `dotnet pack` .

> [!IMPORTANT]
> Toto téma se vztahuje na projekty ve [stylu sady SDK](../resources/check-project-format.md) , obvykle v projektech .NET Core a .NET Standard a na projekty ve stylu jiné než SDK, které používají PackageReference.

## <a name="set-properties"></a>Nastavení vlastností

Pro vytvoření balíčku jsou vyžadovány následující vlastnosti.

- `PackageId`, identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček. Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .
- `Version`, konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md). Pokud není zadaný, použije se výchozí hodnota 1.0.0.
- Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)
- `Authors`, informace o autorovi a vlastníka. Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .
- `Company`, název vaší společnosti. Pokud není zadaný, použije se výchozí hodnota `AssemblyName` .

Kromě toho, pokud jste balíte projekty, které nejsou ve stylu sady SDK, které používají PackageReference, je třeba zadat následující:

- `PackageOutputPath`, výstupní složka balíčku vygenerovaného při volání Pack.

V sadě Visual Studio můžete nastavit tyto hodnoty ve vlastnostech projektu (klikněte pravým tlačítkem myši na projekt v Průzkumník řešení, zvolte **vlastnosti** a vyberte kartu **balíček** ). Tyto vlastnosti lze také nastavit přímo v souborech projektu ( *. csproj* ).

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Poskytněte balíčku identifikátor, který je jedinečný v rámci nuget.org nebo jakýkoli ze zdrojů balíčku, který používáte.

Následující příklad ukazuje jednoduchý a kompletní soubor projektu s těmito vlastnostmi, které jsou k dispozici.

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

Můžete také nastavit volitelné vlastnosti, například, `Title` `PackageDescription` a `PackageTags` , jak je popsáno v tématu [cíle sady MSBuild](../reference/msbuild-targets.md#pack-target), [řízení prostředků závislosti](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)a [vlastnosti metadat NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).

> [!NOTE]
> Pro balíčky sestavené pro veřejnou spotřebu věnujte zvláštní pozornost vlastnosti **PackageTags** , protože značky můžou ostatním uživatelům najít váš balíček a pochopit, co to dělá.

Podrobnosti o deklarování závislostí a zadání čísel verzí naleznete v tématu [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md) a [Správa verzí balíčků](../concepts/package-versioning.md). Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí `<IncludeAssets>` `<ExcludeAssets>` atributů a. Další informace najdete v Seee [řízení prostředků závislostí](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

## <a name="add-an-optional-description-field"></a>Přidat volitelné pole popisu

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>Přidat balíček NuGet. Build. Tasks. Pack

Pokud používáte nástroj MSBuild s projektem a PackageReference, který není typu SDK, přidejte do projektu balíček NuGet. Build. Tasks. Pack.

1. Otevřete soubor projektu a přidejte následující za `<PropertyGroup>` element:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Otevřete příkazový řádek pro vývojáře (do **vyhledávacího** pole zadejte **příkaz Developer Command Prompt** ).

   Obvykle chcete spustit Developer Command Prompt pro Visual Studio z nabídky **Start** , jak bude nakonfigurován se všemi nezbytnými cestami pro MSBuild.

3. Přepněte do složky obsahující soubor projektu a zadejte následující příkaz pro instalaci balíčku NuGet. Build. Tasks. Pack.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   Ujistěte se, že výstup nástroje MSBuild označuje, že sestavení bylo úspěšně dokončeno.

## <a name="run-the-msbuild--tpack-command"></a>Spuštění příkazu MSBuild-t:Pack

Chcete-li vytvořit balíček NuGet ( `.nupkg` soubor) z projektu, spusťte `msbuild -t:pack` příkaz, který také automaticky vytvoří projekt:

Do příkazového řádku pro vývojáře pro Visual Studio zadejte následující příkaz:

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

Chcete-li automaticky spustit `msbuild -t:pack` při sestavování nebo obnovování projektu, přidejte následující řádek do souboru projektu v `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Při spuštění `msbuild -t:pack` v řešení jsou všechny projekty v řešení, které lze zabalit ( [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) vlastnost nastavena na hodnotu `true` ).

> [!NOTE]
> Když balíček automaticky vygenerujete, čas k zabalení zvýší čas sestavení pro váš projekt.

### <a name="test-package-installation"></a>Instalace testovacího balíčku

Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu. Testy zajistí, že všechny soubory v projektu budou mít všechny na správném místě.

Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

> [!IMPORTANT]
> Balíčky jsou neměnné. Pokud problém opravíte, znovu ho změňte a znovu spusťte. při opětovném testování bude stále použita stará verze balíčku, dokud [nevymažete složku globálních balíčků](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) . To je obzvláště důležité při testování balíčků, které nepoužívají jedinečný popisek předprodejní verze pro každé sestavení.

## <a name="next-steps"></a>Další kroky

Po vytvoření balíčku, který je `.nupkg` soubor, můžete ho publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:

- [Sada NuGet Pack a obnovení jako cíle MSBuild](../reference/msbuild-targets.md)
- [Správa verzí balíčků](../concepts/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/multiple-target-frameworks-project-file.md)
- [Transformace zdrojových a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze verzí](../create-packages/prerelease-packages.md)
- [Nastavení typu balíčku](../create-packages/set-package-type.md)
- [Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Nakonec existují další typy balíčků, o kterých byste měli vědět:

- [Nativní balíčky](../guides/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)