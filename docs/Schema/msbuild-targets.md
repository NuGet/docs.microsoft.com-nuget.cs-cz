---
title: "NuGet pack a obnovit jako cíle MSBuild | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "NuGet pack a obnovení můžete pracovat přímo jako cíle MSBuild s NuGet 4.0 +."
keywords: "NuGet a MSBuild NuGet pack cíl, cíl obnovení NuGet"
ms.reviewer: karann-msft
ms.openlocfilehash: def01380e5bc3bf878e72dd437f52cd033641ca5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet pack a obnovení jako cíle nástroje MSBuild

*NuGet 4.0 +*

NuGet 4.0 + může spolupracovat přímo s informace v `.csproj` souboru bez nutnosti samostatné `.nuspec` nebo `project.json` souboru. Všechna metadata, která byla dříve uložená v těchto konfigurační soubory se místo toho uloží `.csproj` souboru přímo, jak je popsáno v tomto poli.

Pomocí nástroje MSBuild 15.1 + NuGet je také prvotřídní MSBuild občanem s `pack` a `restore` cílem, jak je popsáno níže. Tyto cíle umožňují pracovat s NuGet, stejně jako s jinými úlohy nástroje MSBuild nebo cíl. (Pro NuGet 3.x a starší, použijte [pack](../tools/cli-ref-pack.md) a [obnovení](../tools/cli-ref-restore.md) příkazy prostřednictvím rozhraní příkazového řádku NuGet místo.)

V tomto tématu:

- [Pořadí sestavení cílů](#target-build-order)
- [cíl Pack](#pack-target)
- [scénáře aktualizací Service Pack](#pack-scenarios)
- [Cíl obnovení](#restore-target)
- [PackageTargetFallback](#packagetargetfallback)

## <a name="target-build-order"></a>Pořadí sestavení cílů

Protože `pack` a `restore` jsou cíle MSBuild se dostanete k vylepšení vašeho pracovního postupu. Řekněme například, že chcete zkopírovat vašeho balíčku do sdílené síťové složky po balení ho. Můžete to udělat vložením následujícího textu v souboru projektu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

Podobně můžete napsat úlohy nástroje MSBuild, zápis vlastní cíl a využívat vlastnosti NuGet v úlohy nástroje MSBuild.

## <a name="pack-target"></a>cíl Pack

Při použití pack cíl, který je `msbuild /t:pack`, MSBuild nevykresluje vstupy z `.csproj` souboru místo `project.json` nebo `.nuspec` soubory. Následující tabulka popisuje vlastnosti nástroje MSBuild, které mohou být přidány do `.csproj` soubor v první `<PropertyGroup>` uzlu. Můžete provést tyto úpravy snadno v Visual Studio 2017 a později kliknutím pravým tlačítkem na projekt a výběrem **upravit {název_projektu}** v místní nabídce. Pro usnadnění práce v tabulce je seřazená podle vlastnost ekvivalentní v [ `.nuspec` soubor](../schema/nuspec.md).

Všimněte si, že `Owners` a `Summary` vlastnosti z `.nuspec` nejsou podporovány pomocí nástroje MSBuild.


| Hodnota atributu/NuSpec | Vlastnosti nástroje MSBuild | Výchozí | Poznámky |
|--------|--------|--------|--------|
| ID | ID balíčku | AssemblyName | $(AssemblyName) z nástroje MSBuild |
| Version | PackageVersion | Version | Toto je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | Nastavení PackageVersion přepíše PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) z nástroje MSBuild. Nastavení PackageVersion přepíše PackageVersionSuffix | 
| Autoři | Autoři | Uživatelské jméno aktuálního uživatele | |
| Vlastníci | Není k dispozici | Není k dispozici v NuSpec | |
| Název | Název | ID balíčku| |
| Popis | Popis | "Balíček popis" | |
| Copyright | Copyright | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| Adresa LicenseUrl | PackageLicenseUrl | empty | |
| Adrese ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Značky | PackageTags | empty | Značky jsou oddělené středníky. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| RepositoryUrl | RepositoryUrl | empty | |
| RepositoryType | RepositoryType | empty | |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Souhrn | Nepodporováno | | |


### <a name="pack-target-inputs"></a>vstupy cíl Pack

- IsPackable
- PackageVersion
- ID balíčku
- Autoři
- Popis
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
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

Jako součást změny pro [NuGet problém 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` bude nakonec změnit tak, aby `PackageIconUri` a může být relativní cesta k ikonu souboru, který bude zahrnut v kořenovém adresáři výsledné balíčku.

### <a name="output-assemblies"></a>Výstup sestavení

`nuget pack`kopie výstupní soubory s příponami `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, a `.pri`. Výstupní soubory, které jste zkopírovali závisí na MSBuild poskytuje z `BuiltOutputProjectGroup` cíl.

Existují dvě vlastnosti nástroje MSBuild, které můžete použít v souboru projektu nebo příkazového řádku na ovládací prvek kde přejděte výstup sestavení:

- `IncludeBuildOutput`: Logická hodnota, která určuje, zda by měl být sestavení výstupu sestavení součástí balíčku.
- `BuildOutputTargetFolder`: Určuje složku, ve kterém má být umístěn výstup sestavení. Výstup sestavení (a ostatní výstupní soubory) se zkopírují do jejich odpovídajících framework složky.

### <a name="package-references"></a>Odkazy na balíček

V tématu [balíček odkazy v souborech projektu](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Projekt odkazů projektu

Projekt odkazů projektu jsou považovány za ve výchozím nastavení jako odkazy na balíček nuget, například:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Pro odkaz na projekt můžete také přidat následující metadata:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Včetně obsahu v balíčku

Chcete-li zahrnout obsah, přidejte doplňující metadata do existující `<Content>` položky. Ve výchozím nastavení všechno typ, který "Obsah" získá v balíčku zahrnutý Pokud přepíšete s položkami jako následující:

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

Ve výchozím nastavení, vše, co přidá do kořenového adresáře `content` a `contentFiles\any\<target_framework>` složky v balíčku a uchovává složce relativní struktury, pokud zadáte cestu k balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenových složek bylo (místo `content` a `contentFiles` oba), můžete použít vlastnost MSBuild `ContentTargetFolders`, což výchozí nastavení "obsah; contentFiles", ale může být nastavena na žádné jiné názvy složek. Všimněte si, aby pouze určení "contentFiles" v `ContentTargetFolders` převádí soubory v `contentFiles\any\<target_framework>` nebo `contentFiles\<language>\<target_framework>` na základě `buildAction`.

`PackagePath`může být sadu cílových cest oddělený středníkem. Zadání cesty prázdný balíček by soubor přidat do kořenového adresáře balíčku. Například následující přidá `libuv.txt` k `content\myfiles`, `content\samples`a kořenového adresáře balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Je také ve vlastnosti nástroje MSBuild `$(IncludeContentInPack)`, což výchozí nastavení `true`. Pokud je nastavena v `false` na jakýkoli projekt, pak obsah z daného projektu nejsou součástí balíček nuget.

Zahrnuje další konkrétní metadata aktualizací Service pack, kterou můžete nastavit na některou z výše uvedených položek ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` které nastaví ```CopyToOutput``` a ```Flatten``` hodnoty na ```contentFiles``` položku v výstupní soubor nuspec.


> [!Note]
> Vedle položky obsahu `<Pack>` a `<PackagePath>` metadata můžete také nastavit na soubory pomocí akce sestavení kompilace, EmbeddedResource, ApplicationDefinition, stránky, prostředků, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo žádný.
>
> Pro pack připojit název souboru pro cestu k balíčku, při použití vzory expanze názvů cestu k balíčku musí končit složky oddělovací znak, jinak hodnota cestou balíčku je považován za úplnou cestu včetně názvu souboru.

### <a name="includesymbols"></a>IncludeSymbols

Při použití `MSBuild /t:pack /p:IncludeSymbols=true`, odpovídající `.pdb` spolu s další výstupní soubory kopírují soubory (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíčku symbolů.

### <a name="includesource"></a>IncludeSource

Je to stejné nastavení jako `IncludeSymbols`kromě toho, že ho zkopíruje zdrojové soubory spolu s `.pdb` i soubory. Všechny soubory typu `Compile` se překopírují na `src\<ProjectName>\` zachování struktura složek relativní cestu v výsledné balíčku. Stejné také se stane pro zdrojové soubory libovolného `ProjectReference` jehož `TreatAsPackageReference` nastavena na `false`.

Pokud soubor typu kompilovat, je mimo složku projekt, pak je právě přidali do `src\<ProjectName>\`.

### <a name="istool"></a>IsTool

Při použití `MSBuild /t:pack /p:IsTool=true`, všechny výstupní soubory, jak je uvedeno v [výstup sestavení](#output-assemblies) scénáři se zkopírují do `tools` složky místo `lib` složky. Všimněte si, že se to neliší od `DotNetCliTool` , která je určena podle nastavení `PackageType` v `.csproj` souboru.

### <a name="packing-using-a-nuspec"></a>Balení pomocí příponou .nuspec

Můžete použít `.nuspec` soubor pack projektu za předpokladu, že soubor projektu k importu `NuGet.Build.Tasks.Pack.targets` tak, aby úloha sady mohou být provedeny. Následující tři vlastnosti nástroje MSBuild jsou relevantní pro balení, použití `.nuspec`:

1. `NuspecFile`: relativní nebo absolutní cesta k `.nuspec` soubor používá pro okolních.
1. `NuspecProperties`: středníky oddělený seznam klíč = hodnota páry. Vzhledem ke způsobu MSBuild příkazového řádku analýzy funguje více vlastností se musí zadat následujícím způsobem: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Základní cesta pro `.nuspec` souboru.

Pokud používáte `dotnet.exe` pack projektu, použijte příkaz takto:

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

Pokud pomocí nástroje MSBuild pack projektu, použijte příkaz takto:

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a>Cíl obnovení

`MSBuild /t:restore`(která `nuget restore` a `dotnet restore` použít s projekty .NET Core), obnoví balíčky, kterou se odkazuje v souboru projektu následujícím způsobem:

1. Číst všechny odkazy na projekt na projekt
1. Přečtěte si vlastnosti projektu najít zprostředkující složku a cíl rozhraní
1. Předat msbuild data NuGet.Build.Tasks.dll
1. Spustit obnovení
1. Stáhnout balíčky
1. Zápis soubor prostředků, cílů a props


### <a name="restore-properties"></a>Obnovit vlastnosti

Nastavení další obnovení mohou pocházet z vlastnosti nástroje MSBuild v souboru projektu. Hodnoty můžete také nastavit z příkazového řádku pomocí `/p:` přepínače (viz následující příklady).

| Vlastnost | Popis |
|--------|--------|
| RestoreSources | Seznam oddělený středníkem zdroji balíčků. |
| RestorePackagesPath | Cesta ke složce balíčků uživatele. |
| RestoreDisableParallel | Limit stahování do jeden po druhém. |
| RestoreConfigFile | Cesta k `Nuget.Config` lze uplatnit. |
| RestoreNoCache | V případě hodnoty true nevyužívá webové mezipaměti. |
| RestoreIgnoreFailedSources | V případě hodnoty true ignoruje chybě nebo chybějící zdroje balíčků. |
| RestoreTaskAssemblyFile | Cesta k `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Seznam oddělený středníkem projekty k obnovení, který by měl obsahovat absolutní cesty. |
| RestoreOutputPath | Výstupní složky, jako výchozí bude použit `obj` složky. |

**Příklady**

Příkazový řádek:

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

Soubor projektu:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a>Obnovení výstupy

Obnovení vytvoří následující soubory v sestavení `obj` složky:

| Soubor | Popis |
|--------|--------|
| `project.assets.json` | Dříve`project.lock.json` |
| `{projectName}.projectFileExtension.nuget.g.props` | Odkazy na MSBuild props součástí balíčků |
| `{projectName}.projectFileExtension.nuget.g.targets` | Odkazy na cíle MSBuild součástí balíčků |


### <a name="packagetargetfallback"></a>PackageTargetFallback 

`PackageTargetFallback` Element umožňuje určit sadu kompatibilní cíle, který se má použít při obnovování balíčků (ekvivalent [ `imports` v `project.json` ](../schema/project-json.md#imports)). Je navržen tak, aby balíčky, které používají dotnet. [TxM](../schema/target-frameworks.md) k práci s kompatibilní balíčky, které nejsou deklarovat dotnet TxM. To znamená, pokud projektu používá dotnet TxM, pak všechny balíčky, které závisí na musí také mít dotnet TxM, pokud přidáte `<PackageTargetFallback>` do projektu, aby bylo možné povolit platformy bez dotnet. aby bylo kompatibilní s dotnet. 

Například, pokud je projekt pomocí `netstandard1.6` TxM a závislý balíček obsahuje pouze `lib/net45/a.dll` a `lib/portable-net45+win81/a.dll`, pak projektu se nepovede. Pokud chcete mají být předány se druhé knihovny DLL, pak můžete přidat `PackageTargetFallback` následujícím způsobem. Tím vyjádříte, který `portable-net45+win81` DLL je kompatibilní:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Deklarovat zálohu pro všechny cíle v projektu, nechte `Condition` atribut. Můžete také rozšířit, všechny existující `PackageTargetFallback` zahrnutím `$(PackageTargetFallback)` jak je vidět tady:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a>Nahrazení jedna knihovna z obnovení grafu

Pokud obnovení je přináší nesprávný sestavení, je možné pro vyloučení, výchozí výběr balíčků a nahraďte ji metodou dle svého výběru. První s nejvyšší úrovní `PackageReference`, vyloučit všechny prostředky:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

V dalším kroku přidejte vlastní odkaz na příslušné místní kopie knihovny DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
