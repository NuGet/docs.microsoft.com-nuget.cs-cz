---
title: Sada NuGet Pack a obnovení jako cíle MSBuild
description: Sada NuGet Pack a obnovení může pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 6a49e410617c14e22f0d4a67d8bfe280f64f5505
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510793"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Sada NuGet Pack a obnovení jako cíle MSBuild

*NuGet 4.0 +*

Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného souboru `.nuspec`.

Pomocí nástroje MSBuild 15.1 + nástroj NuGet je také první třídou občana MSBuild s cíli `pack` a `restore`, jak je popsáno níže. Tyto cíle vám umožňují pracovat s balíčky NuGet stejně jako s ostatními úlohami nebo cíli MSBuild. Pokyny k vytvoření balíčku NuGet pomocí nástroje MSBuild najdete v tématu [Vytvoření balíčku NuGet pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md). (Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového řádku NuGet.)

## <a name="target-build-order"></a>Pořadí cílového sestavení

Vzhledem k tomu, že `pack` a `restore` jsou cílem MSBuild, můžete k nim získat přístup, abyste mohli vylepšit svůj pracovní postup. Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky. To lze provést přidáním následujícího do souboru projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Podobně můžete napsat úlohu MSBuild, napsat vlastní cíl a využít vlastnosti NuGet v úloze MSBuild.

> [!NOTE]
> `$(OutputPath)` je relativní a očekává, že příkaz spouštíte z kořenového adresáře projektu.

## <a name="pack-target"></a>cíl balíčku

Pro .NET Standard projekty pomocí formátu PackageReference pomocí `msbuild -t:pack` kreslí vstupy ze souboru projektu, které se použijí při vytváření balíčku NuGet.

Následující tabulka popisuje vlastnosti nástroje MSBuild, které lze přidat do souboru projektu v prvním uzlu `<PropertyGroup>`. Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce. Pro přehlednost je tabulka uspořádaná podle ekvivalentní vlastnosti v [souboru `.nuspec`](../reference/nuspec.md).

Všimněte si, že nástroj MSBuild nepodporuje vlastnosti `Owners` a `Summary` z `.nuspec`.

| Hodnota atributu/NuSpec | Vlastnost MSBuild | Výchozí | Poznámky |
|--------|--------|--------|--------|
| Účet | PackageId | Doplňk | $ (AssemblyName) z MSBuild |
| Version | PackageVersion | Version | To je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | Nastavení PackageVersion přepsání PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $ (VersionSuffix) z MSBuild. Nastavení PackageVersion přepsání PackageVersionSuffix |
| Autoři | Autoři | Uživatelské jméno aktuálního uživatele | |
| vlastníka | Není k dispozici | Nepřítomno v NuSpec | |
| Název | Název | PackageId| |
| Popis | Popis | Popis balíčku | |
| Úprava | Úprava | empty | |
| requireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| průkaz | PackageLicenseExpression | empty | Odpovídá `<license type="expression">` |
| průkaz | PackageLicenseFile | empty | Odpovídá `<license type="file">`. Je možné, že bude nutné explicitně sbalit soubor s odkazem na licenci. |
| licenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` je zastaralá, použijte vlastnost PackageLicenseExpression nebo PackageLicenseFile. |
| projectUrl | PackageProjectUrl | empty | |
| Ikona | PackageIcon | empty | Možná budete muset explicitně sbalit soubor obrázku odkazované ikony.|
| iconUrl | PackageIconUrl | empty | `PackageIconUrl` je zastaralá, použijte vlastnost PackageIcon. |
| Značky | PackageTags | empty | Značky jsou středníky odděleny středníkem. |
| releaseNotes | PackageReleaseNotes | empty | |
| Úložiště/adresa URL | RepositoryUrl | empty | Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu. Příklad: *https://github.com/NuGet/NuGet.Client.git* |
| Úložiště/typ | RepositoryType | empty | Typ úložiště Příklady: *Git*, *TFS*. |
| Úložiště/větev | RepositoryBranch | empty | Volitelné informace o větvi úložiště Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* . Příklad: *Master* (NuGet 4.7.0 +) |
| Úložiště/potvrzení změn | RepositoryCommit | empty | Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen. Pro zahrnutí této vlastnosti je nutné zadat také *RepositoryUrl* . Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Souhrn | Není podporováno | | |

### <a name="pack-target-inputs"></a>cílové vstupy balení

- Ispackable nastavenou
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- Autoři
- Popis
- Úprava
- PackageRequireLicenseAcceptance
- developmentDependency
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
- packageTypes
- Nástroj
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

## <a name="pack-scenarios"></a>scénáře sady Pack

### <a name="suppress-dependencies"></a>Potlačit závislosti

Chcete-li potlačit závislosti balíčků z generovaného balíčku NuGet, nastavte `SuppressDependenciesWhenPacking` na `true`, což umožní přeskočí všechny závislosti ze generovaného souboru nupkg.

### <a name="packageiconurl"></a>PackageIconUrl

> [!Important]
> PackageIconUrl je zastaralá s NuGet 5.3 a + & Visual Studio 2019 verze 16.3 +. Místo toho použijte [PackageIcon](#packing-an-icon-image-file) .

### <a name="packing-an-icon-image-file"></a>Balení souboru obrázku ikony

Při balení souboru obrázku ikony musíte použít vlastnost PackageIcon a zadat cestu k balíčku relativní ke kořenu balíčku. Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku. Velikost souboru obrázku je omezená na 1 MB. Podporované formáty souborů zahrnují JPEG a PNG. Doporučujeme, abyste 64 × 64 rozlišení obrazu.

Příklad:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Ukázka ikony balíčku](https://github.com/NuGet/Samples/tree/master/PackageIconExample)

Pro ekvivalent nuspec se podívejte na [nuspec reference pro Icon](nuspec.md#icon).

### <a name="output-assemblies"></a>Výstupní sestavení

`nuget pack` kopíruje výstupní soubory s rozšířeními `.exe`, `.dll`, `.xml`, `.winmd`, `.json` a `.pri`. Výstupní soubory, které jsou zkopírovány, závisí na tom, co MSBuild poskytuje z cíle `BuiltOutputProjectGroup`.

Existují dvě vlastnosti nástroje MSBuild, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:

- `IncludeBuildOutput`: logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.
- `BuildOutputTargetFolder`: Určuje složku, do které se mají umístit výstupní sestavení. Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní.

### <a name="package-references"></a>Odkazy na balíčky

Viz [odkazy na balíčky v souborech projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Odkazy na projekt a projekt

Odkazy na projekt na projekt jsou ve výchozím nastavení považovány za odkazy na balíčky NuGet, například:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Do odkazu na projekt můžete také přidat následující metadata:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Zahrnutí obsahu do balíčku

Chcete-li zahrnout obsah, přidejte do existující položky `<Content>` další metadata. Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Ve výchozím nastavení se vše přidá do kořenové složky `content` a `contentFiles\any\<target_framework>` v rámci balíčku a zachová relativní strukturu složek, pokud nezadáte cestu k balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Pokud chcete kopírovat veškerý obsah jenom na konkrétní kořenové složky (místo `content` a `contentFiles`), můžete použít vlastnost MSBuild `ContentTargetFolders`, která má výchozí hodnotu "Content; contentFiles", ale dá se nastavit na jiné názvy složek. Všimněte si, že stačí zadat "contentFiles" ve `ContentTargetFolders` vloží soubory do `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` založené na `buildAction`.

`PackagePath` může být sada cílových cest oddělená středníky. Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku. Například následující příkaz přidá `libuv.txt` do `content\myfiles`, `content\samples` a kořen balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

K dispozici je také vlastnost MSBuild `$(IncludeContentInPack)`, která má výchozí hodnotu `true`. Pokud je tato hodnota nastavená na `false` na jakémkoli projektu, pak obsah z tohoto projektu není zahrnutý v balíčku NuGet.

Další metadata specifická pro sadu, která můžete nastavit u kterékoli z výše uvedených položek, zahrnují ```<PackageCopyToOutput>``` a ```<PackageFlatten>```, které nastaví hodnoty ```CopyToOutput``` a ```Flatten``` na položku ```contentFiles``` ve výstupním nuspec.

> [!Note]
> Kromě položek obsahu lze metadata `<Pack>` a `<PackagePath>` také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.
>
> Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.

### <a name="includesymbols"></a>IncludeSymbols

Při použití `MSBuild -t:pack -p:IncludeSymbols=true` se odpovídající soubory `.pdb` zkopírují spolu s jinými výstupními soubory (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíček symbolů.

### <a name="includesource"></a>IncludeSource

To je stejné jako `IncludeSymbols` s tím rozdílem, že kopíruje i zdrojové soubory spolu se soubory `.pdb`. Všechny soubory typu `Compile` se zkopírují do `src\<ProjectName>\`, ve kterém se zachová struktura složek relativní cesty ve výsledném balíčku. Totéž se taky stane u zdrojových souborů libovolného `ProjectReference`, který má `TreatAsPackageReference` nastavenou na `false`.

Pokud je soubor typu kompilovat mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Balení licenčního výrazu nebo licenčního souboru

Při použití licenčního výrazu by se měla použít vlastnost PackageLicenseExpression. 
[Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[Přečtěte si další informace o výrazech licencí a licencích, které jsou přijaty nástrojem NuGet.org](nuspec.md#license).

Při balení licenčního souboru musíte použít vlastnost PackageLicenseFile a zadat cestu k balíčku relativní ke kořenu balíčku. Kromě toho je nutné zajistit, aby byl soubor zahrnut do balíčku. Příklad:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

[Ukázka licenčního souboru](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>Nástroj

Při použití `MSBuild -t:pack -p:IsTool=true` jsou všechny výstupní soubory, jak je uvedeno ve scénáři [výstupní sestavení](#output-assemblies) , zkopírovány do složky `tools` namísto složky `lib`. Všimněte si, že se liší od `DotNetCliTool`, který je určen nastavením `PackageType` v souboru `.csproj`.

### <a name="packing-using-a-nuspec"></a>Balení pomocí. nuspec

I když se doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které se obvykle nacházejí v souboru `.nuspec` v souboru projektu, můžete použít soubor `.nuspec` pro sbalení projektu. Pro projekt bez sady SDK, který používá `PackageReference`, je nutné importovat `NuGet.Build.Tasks.Pack.targets`, aby bylo možné spustit úlohu balíčku. Před zabalením souboru nuspec je ještě nutné projekt obnovit. (Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)

Cílová architektura souboru projektu je nerelevantní a při balení nuspec se nepoužívá. Následující tři vlastnosti MSBuild jsou relevantní pro balení pomocí `.nuspec`:

1. `NuspecFile`: relativní nebo absolutní cesta k souboru `.nuspec`, který se používá k balení.
1. `NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota. Kvůli způsobu, jakým funguje analýza příkazového řádku nástroje MSBuild, je nutné zadat více vlastností následujícím způsobem: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: základní cesta k souboru `.nuspec`.

Pokud k sbalení projektu použijete `dotnet.exe`, použijte příkaz podobný následujícímu:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Při použití nástroje MSBuild k sbalení projektu použijte příkaz podobný následujícímu:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Všimněte si, že balení nuspec pomocí příkazu dotnet. exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení. To je možné vyhnout předáním vlastnosti ```--no-build``` do příkazu dotnet. exe, který je ekvivalentem nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu společně s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.

Příkladem souboru *. csproj* pro zabalení souboru nuspec je:

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

### <a name="advanced-extension-points-to-create-customized-package"></a>Rozšířené body rozšíření pro vytvoření přizpůsobeného balíčku

Cíl `pack` poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní. Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:

- `TargetsForTfmSpecificBuildOutput` cíl: používá se pro soubory uvnitř složky `lib` nebo ze složky zadané pomocí `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` cíl: použijte pro soubory mimo `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Napište vlastní cíl a zadejte ho jako hodnotu vlastnosti `$(TargetsForTfmSpecificBuildOutput)`. U všech souborů, které musí přejít do `BuildOutputTargetFolder` (lib ve výchozím nastavení), by měl cíl tyto soubory zapsat do skupiny položek `BuildOutputInPackage` a nastavit následující dvě hodnoty metadat:

- `FinalOutputPath`: absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.
- `TargetPath`: (volitelné) nastavte, kdy bude soubor potřebovat přejít do podsložky v rámci `lib\<TargetFramework>`, jako jsou satelitní sestavení, která se nacházejí v odpovídajících složkách kultury. Výchozí hodnota je název souboru.

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

Napište vlastní cíl a zadejte ho jako hodnotu vlastnosti `$(TargetsForTfmSpecificContentInPackage)`. U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do skupiny položek `TfmSpecificPackageFile` a nastavit následující volitelná metadata:

- `PackagePath`: cesta, kde by měl být v balíčku výstup souboru. Při přidání více než jednoho souboru do stejné cesty k balíčku vyvolá NuGet vystavení upozornění.
- `BuildAction`: akce sestavení, která se má přiřadit k souboru, se vyžaduje jenom v případě, že je cesta k balíčku ve složce `contentFiles`. Výchozí hodnota je None.

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

## <a name="restore-target"></a>cíl obnovení

`MSBuild -t:restore` (které `nuget restore` a `dotnet restore` používat s projekty .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:

1. Číst všechny odkazy z projektu na projekt
1. Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.
1. Předání dat nástroje MSBuild do NuGet. Build. Tasks. dll
1. Spustit obnovení
1. Stáhnout balíčky
1. Zápis souboru prostředků, cílů a vlastností props

Cíl `restore` funguje **pouze** pro projekty, které používají formát PackageReference. Pro projekty **, které používají** formát `packages.config`, nefunguje. místo toho použijte [obnovení NuGet](../reference/cli-reference/cli-ref-restore.md) .

### <a name="restore-properties"></a>Obnovit vlastnosti

Další nastavení obnovení může pocházet z vlastností MSBuild v souboru projektu. Hodnoty lze také nastavit z příkazového řádku pomocí přepínače `-p:` (viz příklady níže).

| Vlastnost | Popis |
|--------|--------|
| RestoreSources | Seznam zdrojů balíčků oddělených středníkem. |
| RestorePackagesPath | Cesta ke složce uživatelských balíčků |
| RestoreDisableParallel | Omezit stahování na jednu po druhé. |
| RestoreConfigFile | Cesta k souboru `Nuget.Config`, který se má použít |
| RestoreNoCache | Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků. |
| RestoreFallbackFolders | Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků. |
| RestoreAdditionalProjectSources | Další zdroje, které se mají použít při obnovení. |
| RestoreAdditionalProjectFallbackFolders | Další záložní složky, které se mají použít při obnovení |
| RestoreAdditionalProjectFallbackFoldersExcludes | Vyloučí záložní složky zadané v `RestoreAdditionalProjectFallbackFolders`. |
| RestoreTaskAssemblyFile | Cesta k `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty. |
| RestoreUseSkipNonexistentTargets  | Když jsou projekty shromažďovány pomocí nástroje MSBuild, určuje, zda jsou shromažďovány pomocí optimalizace `SkipNonexistentTargets`. Pokud není nastaveno, výchozí hodnota je `true`. Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat. |
| MSBuildProjectExtensionsPath | Výstupní složka, výchozí nastavení `BaseIntermediateOutputPath` a složka `obj`. |
| RestoreForce | V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné. Zadání tohoto příznaku se podobá odstranění souboru `project.assets.json`. To neobejde mezipaměť HTTP-cache. |
| RestorePackagesWithLockFile | Výslovný se na použití souboru zámku. |
| RestoreLockedMode | Spustit obnovení v uzamčeném režimu. To znamená, že obnovení nebude přehodnocovat závislosti. |
| NuGetLockFilePath | Vlastní umístění souboru zámku. Výchozí umístění je vedle projektu a je pojmenované `packages.lock.json`. |
| RestoreForceEvaluate | Vynutí obnovení pro přepočítání závislostí a aktualizaci souboru zámku bez upozornění. | 

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

Příkaz Restore vytvoří ve složce Build `obj` následující soubory:

| Soubor | Popis |
|--------|--------|
| `project.assets.json` | Obsahuje graf závislostí všech odkazů na balíčky. |
| `{projectName}.projectFileExtension.nuget.g.props` | Odkazy na MSBuild props obsažená v balíčcích |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odkazy na cíle nástroje MSBuild obsažené v balíčcích |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Obnovení a sestavování pomocí jednoho příkazu MSBuild

Vzhledem k tomu, že nástroj NuGet dokáže obnovit balíčky, které vycházejí z cílů a props nástroje MSBuild, jsou vyhodnocení obnovení a sestavení spouštěna s různými globálními vlastnostmi.
To znamená, že následující nastavení bude mít nepředvídatelné a často nesprávné chování.

```cli
msbuild -t:restore,build
```

 Místo doporučeného přístupu:

```cli
msbuild -t:build -restore
```

Stejná logika platí i pro jiné cíle, podobně jako `build`.

### <a name="packagetargetfallback"></a>PackageTargetFallback

Element `PackageTargetFallback` umožňuje zadat sadu kompatibilních cílů, které se mají použít při obnovování balíčků. Je navržena tak, aby povolovala balíčkům, které používají dotnet [TxM](../reference/target-frameworks.md) pro práci s kompatibilními balíčky, které nedeklarují dotnet TxM. To znamená, že pokud váš projekt používá TxM dotnet, pak všechny balíčky, na kterých je závislá, musí mít také hodnotu dotnet TxM, pokud do projektu nepřidáte `<PackageTargetFallback>`, aby bylo možné nekompatibilní platformy bez dotnet pomocí dotnet.

Například pokud projekt používá `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, projekt se nepodaří sestavit. Pokud je to, co chcete uvést, je druhá knihovna DLL, můžete přidat `PackageTargetFallback`, aby se říká, že knihovna DLL `portable-net45+win81` je kompatibilní:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Chcete-li deklarovat zálohu pro všechny cíle v projektu, ponechte atribut `Condition`. Existující `PackageTargetFallback` můžete také zvětšit tak, že zahrnete `$(PackageTargetFallback)`, jak je znázorněno zde:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Nahrazení jedné knihovny z grafu obnovení

Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou. Nejprve s nejvyšší úrovní `PackageReference` vylučte všechny prostředky:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
