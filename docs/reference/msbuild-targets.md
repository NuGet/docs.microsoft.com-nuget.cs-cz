---
title: Balíček NuGet a obnovení jako cílů MSBuild
description: Balíček NuGet a obnovení můžete pracovat přímo jako cílů MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 878fb582a31667c84f3ae306b554718de72eca7a
ms.sourcegitcommit: 5c5f0f0e1f79098e27d9566dd98371f6ee16f8b5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645669"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Balíček NuGet a obnovení jako cílů MSBuild

*NuGet 4.0 +*

S formátem PackageReference NuGet 4.0 + můžete ukládat všechny manifestu metadata přímo v rámci souboru projektu namísto spouštění samostatné `.nuspec` souboru.

Pomocí nástroje MSBuild 15.1 +, Správce balíčků NuGet je také prvotřídní občany MSBuild s `pack` a `restore` cílí, jak je popsáno níže. Tyto cíle umožňují pracovat s NuGet, stejně jako u jakékoli úlohy nástroje MSBuild nebo cíl. (Pro NuGet 3.x a dříve, použít [pack](../tools/cli-ref-pack.md) a [obnovení](../tools/cli-ref-restore.md) příkazy přes rozhraní příkazového řádku NuGet místo.)

## <a name="target-build-order"></a>Pořadí sestavení cílů

Protože `pack` a `restore` jsou cíle nástroje MSBuild, dostanete je k vylepšení pracovního postupu. Řekněme například, že chcete zkopírovat balíček do sdílené síťové složky po zabalení ho. Můžete to udělat přidáním následujícího kódu v souboru projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Podobně můžete napsat úlohu nástroje MSBuild, psát vlastní cílové a využívat NuGet vlastnosti v úkolu MSBuild.

## <a name="pack-target"></a>cíl balíčku

Pro projekty .NET Standard ve formátu PackageReference, pomocí `msbuild -t:pack` nakreslí vstupů ze souboru projektu k použití při vytváření balíčku NuGet.

Následující tabulka popisuje vlastnosti nástroje MSBuild, které mohou být přidány do souboru projektu v rámci první `<PropertyGroup>` uzlu. Můžete provádět tyto úpravy snadno v sadě Visual Studio 2017 a novější kliknutím pravým tlačítkem myši projekt a výběrem **upravit {project_name}** v místní nabídce. Pro usnadnění práce je uspořádaný v tabulce rovnocenné vlastností v [ `.nuspec` souboru](../reference/nuspec.md).

Všimněte si, že `Owners` a `Summary` vlastnosti z `.nuspec` nejsou podporovány nástrojem MSBuild.

| Hodnota atributu/NuSpec | Vlastnosti nástroje MSBuild | Výchozí | Poznámky |
|--------|--------|--------|--------|
| ID | ID balíčku | AssemblyName | $(AssemblyName) MSBuild |
| Version | PackageVersion | Version | Toto je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | Nastavení PackageVersion přepíše PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) MSBuild. Nastavení PackageVersion přepíše PackageVersionSuffix |
| Autoři | Autoři | Uživatelské jméno aktuálního uživatele | |
| Vlastníci | Není k dispozici | Není k dispozici v souboru NuSpec | |
| Název | Název | ID balíčku| |
| Popis | Popis | "Balíček popis" | |
| Copyright | Copyright | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| Licence | PackageLicenseExpression | empty | Odpovídá `<license type="expression">` |
| Licence | PackageLicenseFile | empty | Odpovídá `<license type="file">`. Budete muset explicitně pack odkazovaná licenční soubor. |
| LicenseUrl | PackageLicenseUrl | empty | `licenseUrl` je zastaralé, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile |
| ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Značky | PackageTags | empty | Značky jsou oddělené středníky. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| Adresa Url úložiště / | RepositoryUrl | empty | Adresa URL úložiště klonování nebo získat zdrojový kód. Příklad: *https://github.com/NuGet/NuGet.Client.git* |
| Úložiště/typu | RepositoryType | empty | Typ úložiště. Příklady: *git*, *tfs*. |
| Úložiště a větve | RepositoryBranch | empty | Informace o volitelných úložišti větev *RepositoryUrl* musí být také zadána pro tuto vlastnost, která mají být zahrnuty. Příklad: *hlavní* (NuGet 4.7.0+) |
| Úložiště na potvrzení | RepositoryCommit | empty | Volitelné úložiště potvrzení změn nebo sadu změn k označení, které zdroje balíčku byla vytvořena. *RepositoryUrl* musí být také zadána pro tuto vlastnost, která mají být zahrnuty. Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Souhrn | Nepodporováno | | |

### <a name="pack-target-inputs"></a>vstupy cíl balíčku

- IsPackable
- PackageVersion
- ID balíčku
- Autoři
- Popis
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>scénáře aktualizací Service Pack

### <a name="packageiconurl"></a>PackageIconUrl

Jako součást změn pro [NuGet problém 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` se nakonec změní na `PackageIconUri` a může být relativní cesta k souboru ikony, který bude zahrnut v kořenovém adresáři výsledný balíček.

### <a name="output-assemblies"></a>Výstup sestavení

`nuget pack` kopíruje výstupní soubory s příponami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, a `.pri`. Výstupní soubory, které jsou zkopírovány závisí na MSBuild poskytuje od `BuiltOutputProjectGroup` cíl.

Existují dvě vlastnosti nástroje MSBuild, které můžete použít v souboru projektu nebo příkazového řádku do ovládacího prvku kam se obrátit výstupní sestavení:

- `IncludeBuildOutput`: Logická hodnota, která určuje, zda sestavení výstupu sestavení by měl být součástí balíčku.
- `BuildOutputTargetFolder`: Určuje složku, ve kterém by měl být umístěn výstup sestavení. Výstup sestavení (a ostatních výstupních souborů) jsou zkopírovány do složky jejich příslušných rozhraní framework.

### <a name="package-references"></a>Odkazy na balíček

Zobrazit [balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Projekt do odkazů projektu

Projekt tak, aby projekt odkazy jsou považovány za ve výchozím nastavení jako odkazy na balíčky nuget, třeba:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Můžete také přidat následující metadata pro odkaz na projekt:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Včetně obsahu v balíčku

Zahrnout obsah, přidat ke stávající navíc metadat `<Content>` položky. Ve výchozím nastavení vše, co typu "Obsah" získá součástí balíčku nepřepíšete s položkami, jako je následující:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Ve výchozím nastavení, všechno, co přidá do kořenového adresáře `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachová relativní složka struktury, pokud zadáte cestu k balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost MSBuild `ContentTargetFolders`, která má výchozí hodnotu "obsah; contentFiles", ale může být nastaven na jiné názvy složek. Poznámka: aby pouze zadáním "contentFiles" v `ContentTargetFolders` umístí soubory s pod `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` na základě `buildAction`.

`PackagePath` může být sadu cílových cest oddělený středníkem. Zadání cesty ke prázdný balíček by přidejte soubor do kořenového adresáře balíčku. Například následující přidá `libuv.txt` k `content\myfiles`, `content\samples`a kořenový adresář balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

K dispozici je také vlastnost MSBuild `$(IncludeContentInPack)`, která má výchozí hodnotu `true`. Pokud je nastavené na `false` pro žádný projekt, pak obsah z tohoto projektu nejsou součástí balíčku nuget.

Zahrnuje další konkrétní metadata aktualizací Service pack, kterou můžete nastavit na některou z výše uvedených položek ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` který nastaví ```CopyToOutput``` a ```Flatten``` hodnoty na ```contentFiles``` záznam v souboru nuspec výstup.

> [!Note]
> Kromě obsahu položky `<Pack>` a `<PackagePath>` metadat lze nastavit také pro soubory s akcí sestavení kompilace, EmbeddedResource, označení třídy ApplicationDefinition, stránky, prostředek, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource nebo žádný.
>
> U balíčku k názvu souboru připojit k vaše cesta k balíčku, při použití vzorů podpory zástupných znaků cesta balíčku musí končit složky oddělovací znak, jinak cesta k balíčku je považován za úplnou cestu včetně názvu souboru.

### <a name="includesymbols"></a>IncludeSymbols

Při použití `MSBuild -t:pack -p:IncludeSymbols=true`, odpovídající `.pdb` soubory se zkopírují spolu s ostatních výstupních souborů (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Poznámka: Toto nastavení `IncludeSymbols=true` vytvoří regulárních balíček *a* balíček symbolů.

### <a name="includesource"></a>IncludeSource

To je stejný jako `IncludeSymbols`, s tím rozdílem, že zkopíruje zdrojové soubory společně s `.pdb` i soubory. Všechny soubory typu `Compile` se překopírují `src\<ProjectName>\` zachovává strukturu složek relativní cesta výsledný balíček. Stejné dojde také pro zdrojové soubory žádné `ProjectReference` obsahující `TreatAsPackageReference` nastavena na `false`.

Pokud kompilovat soubor typu je mimo složku projektu, pak je právě přidali do `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Balení výrazu licence nebo licenční soubor

Při použití výrazu licence, PackageLicenseExpression vlastnost použít. 
[Ukázka výrazu licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

Při balení licenční soubor, budete muset použít vlastnost PackageLicenseFile zadat cesta k balíčku, vzhledem ke kořenové složce balíčku. Kromě toho budete muset Ujistěte se, že je soubor součástí balíčku. Příklad:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
[Ukázkový soubor licence](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>IsTool

Při použití `MSBuild -t:pack -p:IsTool=true`, všechny výstupní soubory, jak je uvedeno v [výstupní sestavení](#output-assemblies) scénáři se zkopírují do `tools` složky namísto `lib` složky. Všimněte si, že se liší od `DotNetCliTool` který je určený nastavením `PackageType` v `.csproj` souboru.

### <a name="packing-using-a-nuspec"></a>Použití souboru .nuspec balení

Můžete použít `.nuspec` souboru se zabalit váš projekt, za předpokladu, že soubor projektu sadu SDK k importu `NuGet.Build.Tasks.Pack.targets` tak, aby úloha sady mohou být provedeny. Je stále potřeba obnovit projekt předtím, než můžete sbalit soubor nuspec. Cílové rozhraní projektu souboru je bezvýznamná a nepoužívá se při balení souboru nuspec. Následující tři vlastnosti nástroje MSBuild jsou relevantní pro balení, použití `.nuspec`:

1. `NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru se používají pro balení.
1. `NuspecProperties`: středníkem oddělený seznam klíč = dvojice hodnot. Kvůli způsobu, jakým MSBuild příkazového řádku analýzy funguje, musí být více vlastností zadán následujícím způsobem: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Základní cesta pro `.nuspec` souboru.

Pokud používáte `dotnet.exe` se zabalit váš projekt, použijte příkaz podobný tomuto:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Pokud se váš projekt zabalit pomocí nástroje MSBuild, použijte příkaz podobný tomuto:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Mějte prosím na paměti, že balení nuspec pomocí dotnet.exe nebo msbuild také vede k sestavení projektu ve výchozím nastavení. To se můžete vyhnout tím, že předáte ```--no-build``` vlastnost dotnet.exe, což je ekvivalentní nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu se nastavení ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu

Příklad souboru csproj se zabalit soubor nuspec je:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Pokročilé Rozšiřovací body vytvořit přizpůsobený balíček

`pack` Cílové poskytuje dva Rozšiřovací body, které běží v vnitřní, cílové rozhraní framework konkrétního sestavení. Rozšiřovací body podporují včetně obsahu konkrétní cílové rozhraní framework a sestavení do balíčku:

- `TargetsForTfmSpecificBuildOutput` Cíl: Použití pro soubory `lib` složka nebo složka zadaná pomocí `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` Cíl: Použití souborů mimo `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Napsat vlastní cíl a určit ji jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` vlastnost. Pro všechny soubory, které je potřeba, abyste přešli do `BuildOutputTargetFolder` (lib ve výchozím nastavení), cíl by měl zápisu těchto souborů do element ItemGroup `BuildOutputInPackage` a nastavte následující dvě hodnoty metadat:

- `FinalOutputPath`: Absolutní cestu k souboru; Pokud se nezadá, identita se používá k vyhodnocení cestu ke zdroji.
- `TargetPath`:  (Volitelné) Nastavit, pokud je třeba soubor přejděte do podsložky v rámci `lib\<TargetFramework>` , jako jsou satelitní sestavení tohoto go ve složkách, jejich příslušné jazykové verze. Výchozí hodnota je název souboru.

Příklad:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Napsat vlastní cíl a určit ji jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` vlastnost. Pro všechny soubory, které chcete zahrnout do balíčku, cíl zápisu těchto souborů do element ItemGroup `TfmSpecificPackageFile` a nastavte následující volitelná metadata:

- `PackagePath`: Cesta kde soubor by měl být výstup v balíčku. NuGet vydá upozornění, pokud více než jeden soubor je přidaný do stejného umístění balíčku.
- `BuildAction`: Akce sestavení, která má přiřadit k souboru, požadováno, pouze pokud cesta k balíčku v `contentFiles` složky. Výchozí hodnota je "None".

Příklad:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Cíl obnovení

`MSBuild -t:restore` (což `nuget restore` a `dotnet restore` použití s projekty .NET Core), obnoví balíčky, které jsou popsána v souboru projektu následujícím způsobem:

1. Číst všechny odkazy typu projekt na projekt
1. Přečtěte si vlastnosti projektu k vyhledání zprostředkující složky a cílové architektury
1. Předání dat msbuild NuGet.Build.Tasks.dll
1. Spustit obnovení
1. Stáhnout balíčky
1. Zápis souboru prostředků, cíle a vlastnosti

`restore` Cílit funguje **pouze** pro projekty používající formát PackageReference. Provádí **není** pro projekty pomocí fungují `packages.config` formát; použijte [obnovení nuget](../tools/cli-ref-restore.md) místo.

### <a name="restore-properties"></a>Obnovit vlastnosti

Nastavení další obnovení mohou pocházet z vlastnosti nástroje MSBuild v souboru projektu. Hodnoty lze také nastavit pomocí příkazového řádku `-p:` přepnout (Další příklady naleznete níže).

| Vlastnost | Popis |
|--------|--------|
| RestoreSources | Středníkem oddělený seznam zdroje balíčků. |
| RestorePackagesPath | Cesta ke složce balíčků uživatele. |
| RestoreDisableParallel | Limit se stáhne do postupně po jednom. |
| RestoreConfigFile | Cesta k `Nuget.Config` souboru a aplikovat. |
| RestoreNoCache | Při hodnotě true se vyhnete použitím balíčky v mezipaměti. Zobrazit [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Při hodnotě true se ignoruje neúspěšné nebo chybějící zdroje balíčků. |
| RestoreTaskAssemblyFile | Cesta k `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Středníkem oddělený seznam projekty k obnovení, který by měl obsahovat absolutní cesty. |
| RestoreOutputPath | Výstupní složky, jako výchozí se použije `obj` složky. |

#### <a name="examples"></a>Příklady

Příkazový řádek:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

Soubor projektu:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Obnovit výstupy

Obnovení vytvoří následující soubory v sestavení `obj` složky:

| Soubor | Popis |
|--------|--------|
| `project.assets.json` | Obsahuje všechny odkazy na balíčky v grafu závislostí. |
| `{projectName}.projectFileExtension.nuget.g.props` | Odkazy na vlastnosti MSBuild součástí balíčků |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odkazy na obsažených v balíčcích cíle nástroje MSBuild |

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` Element slouží k určení sady cílů kompatibilní se použije při obnovování balíčků. Je navržen tak, aby balíčky, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilní balíčky, které není deklarovat dotnet TxM. To znamená, pokud váš projekt používá dotnet TxM, pak všechny balíčky, které závisí na musí také mít dotnet TxM, pokud přidáte `<PackageTargetFallback>` do vašeho projektu, aby bylo možné povolit bez dotnet platformy se kvůli kompatibilitě s dotnet.

Například, pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, pak se nepodaří sestavit projekt. Pokud chcete přenést druhém knihovny DLL, pak můžete přidat `PackageTargetFallback` následujícím způsobem, aby říct, že `portable-net45+win81` je kompatibilní knihovny DLL:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Chcete-li deklarovat jako základní pro všechny cíle ve vašem projektu, vynechat `Condition` atribut. Můžete taky rozšířit, všechny existující `PackageTargetFallback` zahrnutím `$(PackageTargetFallback)` jak je znázorněno zde:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Nahrazení jedna knihovna z grafu obnovení

Pokud obnovení přináší na špatné sestavení, je možné, že výchozí volba balíčky a nahraďte ho vlastní možnost vyloučit. První s nejvyšší úrovní `PackageReference`, vyloučit všechny prostředky:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

V dalším kroku přidejte vlastní odkaz na příslušné místní kopie knihovny DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
