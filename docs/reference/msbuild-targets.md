---
title: Sada NuGet Pack a obnovení jako cíle MSBuild
description: Sada NuGet Pack a obnovení může pracovat přímo jako cíle MSBuild s NuGet 4.0 +.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777718"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>Sada NuGet Pack a obnovení jako cíle MSBuild

*NuGet 4.0 +*

Ve formátu [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + může ukládat všechna metadata manifestu přímo do souboru projektu místo použití samostatného `.nuspec` souboru.

Pomocí nástroje MSBuild 15.1 + nástroj NuGet je také první třídou občana MSBuild s `pack` `restore` cíli a, jak je popsáno níže. Tyto cíle vám umožňují pracovat s balíčky NuGet stejně jako s ostatními úlohami nebo cíli MSBuild. Pokyny k vytvoření balíčku NuGet pomocí nástroje MSBuild najdete v tématu [Vytvoření balíčku NuGet pomocí nástroje MSBuild](../create-packages/creating-a-package-msbuild.md). (Pro NuGet 3. x a starší použijte místo toho příkazy [Pack](../reference/cli-reference/cli-ref-pack.md) a [obnovení](../reference/cli-reference/cli-ref-restore.md) prostřednictvím rozhraní příkazového řádku NuGet.)

## <a name="target-build-order"></a>Pořadí sestavení cílů

Vzhledem `pack` k tomu, že a `restore` jsou cíle nástroje MSBuild, můžete k nim přistupovat, abyste mohli vylepšit pracovní postup. Řekněme například, že chcete po sbalení balíčku zkopírovat do sdílené síťové složky. To lze provést přidáním následujícího do souboru projektu:

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
> `$(OutputPath)` je relativní a očekává, že spouštíte příkaz z kořenového adresáře projektu.

## <a name="pack-target"></a>cíl balíčku

Pro projekty .NET, které používají `PackageReference` formát, pomocí `msbuild -t:pack` kreslí vstupy ze souboru projektu, které se mají použít při vytváření balíčku NuGet.

Následující tabulka popisuje vlastnosti MSBuild, které lze přidat do souboru projektu v rámci prvního `<PropertyGroup>` uzlu. Tyto úpravy můžete snadno upravit v aplikaci Visual Studio 2017 a novějším kliknutím pravým tlačítkem myši na projekt a výběrem možnosti **Upravit {PROJECT_NAME}** v místní nabídce. Pro usnadnění práce je tabulka uspořádána podle odpovídající vlastnosti v [ `.nuspec` souboru](../reference/nuspec.md).

Všimněte si, že nástroj `Owners` `Summary` `.nuspec` MSBuild nepodporuje vlastnosti a.

| Hodnota atributu/NuSpec | Vlastnost MSBuild | Výchozí | Poznámky |
|--------|--------|--------|--------|
| Id | PackageId | Doplňk | $ (AssemblyName) z MSBuild |
| Verze | PackageVersion | Verze | To je semver kompatibilní, například "1.0.0", "1.0.0-beta" nebo "1.0.0-beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | Nastavení PackageVersion přepsání PackageVersionPrefix |
| VersionSuffix | PackageVersionSuffix | empty | $ (VersionSuffix) z MSBuild. Nastavení PackageVersion přepsání PackageVersionSuffix |
| Autoři | Autoři | Uživatelské jméno aktuálního uživatele | Středníkem oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazí v galerii NuGet na nuget.org a používají se pro balíčky křížového odkazu stejnými autory. |
| Vlastníci | – | Nepřítomno v NuSpec | |
| Nadpis | Nadpis | PackageId| Popisný název balíčku, který se obvykle používá v uživatelském rozhraní, se zobrazuje jako v nuget.org a správce balíčků v aplikaci Visual Studio. |
| Popis | Popis | Popis balíčku | Dlouhý popis pro sestavení. Pokud `PackageDescription` parametr není zadán, tato vlastnost se používá také jako Popis balíčku. |
| Copyright | Copyright | empty | Podrobnosti o autorských právech pro balíček. |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false (nepravda) | Logická hodnota, která určuje, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku. |
| license | PackageLicenseExpression | empty | Odpovídá `<license type="expression">` . Viz [balení licenčního výrazu nebo licenčního souboru](#packing-a-license-expression-or-a-license-file). |
| license | PackageLicenseFile | empty | Cesta k souboru s licencí v rámci balíčku, pokud používáte vlastní licenci nebo licenci, ke které se nepřiřadil identifikátor SPDX Musíte explicitně sbalit soubor s odkazem na licenci. Odpovídá `<license type="file">` . Viz [balení licenčního výrazu nebo licenčního souboru](#packing-a-license-expression-or-a-license-file). |
| LicenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` je zastaralá. Použijte `PackageLicenseExpression` nebo `PackageLicenseFile` místo toho. |
| ProjectUrl | PackageProjectUrl | empty | |
| Ikona | PackageIcon | empty | Cesta k obrázku v balíčku, který se má použít jako ikona balíčku Musíte explicitně sbalit soubor obrázku odkazované ikony. Další informace najdete v tématu [sbalení souboru obrázku ikony](#packing-an-icon-image-file) a [ `icon` metadat](/nuget/reference/nuspec#icon). |
| IconUrl | PackageIconUrl | empty | `PackageIconUrl` je zastaralé namísto `PackageIcon` . Pro dosažení nejlepšího prostředí pro starší verze byste však měli zadat `PackageIconUrl` kromě `PackageIcon` . |
| Značky | PackageTags | empty | Seznam značek oddělených středníkem, který určuje balíček. |
| ReleaseNotes | PackageReleaseNotes | empty | Poznámky k verzi balíčku |
| Úložiště/adresa URL | RepositoryUrl | empty | Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu. Příklad: *https://github.com/NuGet/NuGet.Client.git* . |
| Úložiště/typ | RepositoryType | empty | Typ úložiště Příklady: `git` (výchozí), `tfs` . |
| Úložiště/větev | RepositoryBranch | empty | Volitelné informace o větvi úložiště `RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti. Příklad: *Master* (NuGet 4.7.0 +). |
| Úložiště/potvrzení změn | RepositoryCommit | empty | Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen. `RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti. Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Souhrn | Nepodporováno | | |

### <a name="pack-target-inputs"></a>cílové vstupy balení

| Vlastnost | Popis |
| - | - |
| Ispackable nastavenou | Logická hodnota, která určuje, zda lze projekt zabalit. Výchozí hodnota je `true`. |
| SuppressDependenciesWhenPacking | Nastavte na `true` , aby se potlačily závislosti balíčků z vygenerovaného balíčku NuGet. |
| PackageVersion | Určuje verzi, kterou výsledný balíček bude mít. Akceptuje všechny formy řetězce verze NuGet. Výchozí hodnota je hodnota `$(Version)` , to znamená vlastnost `Version` v projektu. |
| PackageId | Určuje název výsledného balíčku. Pokud tento parametr nezadáte, použije se ve `pack` výchozím nastavení `AssemblyName` jako název balíčku název adresáře nebo. |
| PackageDescription | Dlouhý popis balíčku pro zobrazení uživatelského rozhraní. |
| Autoři | Středníkem oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazí v galerii NuGet na nuget.org a používají se pro balíčky křížového odkazu stejnými autory. |
| Popis | Dlouhý popis pro sestavení. Pokud `PackageDescription` parametr není zadán, tato vlastnost se používá také jako Popis balíčku. |
| Copyright | Podrobnosti o autorských právech pro balíček. |
| PackageRequireLicenseAcceptance | Logická hodnota, která určuje, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku. Výchozí formát je `false`. |
| DevelopmentDependency | Logická hodnota, která určuje, zda je balíček označen jako jen pro vývoj, což zabrání zahrnutí balíčku jako závislosti v jiných balíčcích. V `PackageReference` případě (NuGet 4,8 +) Tento příznak také znamená, že prostředky při kompilaci jsou vyloučeny z kompilace. Další informace najdete v tématu [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| PackageLicenseExpression | Identifikátor nebo výraz [licence SPDX](https://spdx.org/licenses/) , například `Apache-2.0` . Další informace najdete v tématu [balení licenčního výrazu nebo licenčního souboru](#packing-a-license-expression-or-a-license-file). |
| PackageLicenseFile | Cesta k souboru s licencí v rámci balíčku, pokud používáte vlastní licenci nebo licenci, ke které se nepřiřadil identifikátor SPDX |
| PackageLicenseUrl | `PackageLicenseUrl` je zastaralá. Použijte `PackageLicenseExpression` nebo `PackageLicenseFile` místo toho. |
| PackageProjectUrl | |
| PackageIcon | Určuje cestu ikony balíčku vzhledem k kořenu balíčku. Další informace najdete v tématu [sbalení souboru obrázku ikony](#packing-an-icon-image-file). |
| PackageReleaseNotes| Poznámky k verzi balíčku |
| PackageTags | Seznam značek oddělených středníkem, který určuje balíček. |
| PackageOutputPath | Určuje výstupní cestu, do které bude zahozen zabalený balíček. Výchozí je `$(OutputPath)`. |
| IncludeSymbols | Tato logická hodnota označuje, zda má balíček při zabalení projektu vytvořit další balíček symbolů. Formát balíčku symbolů je řízen `SymbolPackageFormat` vlastností. Další informace najdete v tématu [IncludeSymbols](#includesymbols). |
| IncludeSource | Tato logická hodnota označuje, zda by měl proces balíčku vytvořit zdrojový balíček. Zdrojový balíček obsahuje zdrojový kód knihovny i soubory PDB. Zdrojové soubory jsou umístěny do `src/ProjectName` adresáře ve výsledném souboru balíčku. Další informace najdete v tématu [IncludeSource](#includesource). |
| PackageTypes
| Nástroj | Určuje, zda jsou všechny výstupní soubory zkopírovány do složky *Tools* namísto složky *lib* . Další informace najdete v tématu [Nástroj](#istool). |
| RepositoryUrl | Adresa URL úložiště, která se používá k klonování nebo načtení zdrojového kódu. Příklad: *https://github.com/NuGet/NuGet.Client.git* . |
| RepositoryType | Typ úložiště Příklady: `git` (výchozí), `tfs` . |
| RepositoryBranch | Volitelné informace o větvi úložiště `RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti. Příklad: *Master* (NuGet 4.7.0 +). |
| RepositoryCommit | Volitelné potvrzení změn úložiště nebo sada změn, které označují, na který zdroj byl balíček vytvořen. `RepositoryUrl` musí být také zadáno pro zahrnutí této vlastnosti. Příklad: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| SymbolPackageFormat | Určuje formát balíčku symbolů. Pokud se "Symbols. nupkg", vytvoří se balíček starších symbolů s příponou *. Symbols. nupkg* obsahující soubory PDB, knihovny DLL a další výstupní soubory. Pokud je "snupkg", vytvoří se balíček symbolů snupkg obsahující přenosné soubory PDB. Výchozí hodnota je "Symbols. nupkg". |
| NoPackageAnalysis | Určuje, že `pack` po sestavení balíčku by neměl spustit analýzu balíčku. |
| MinClientVersion | Určuje minimální verzi klienta NuGet, která může nainstalovat tento balíček vynutila nuget.exe a správcem balíčků sady Visual Studio. |
| IncludeBuildOutput | Tato logická hodnota určuje, zda mají být výstupní sestavení sestavení zabalena do souboru *. nupkg* nebo ne. |
| IncludeContentInPack | Tato logická hodnota určuje, zda jsou všechny položky, které mají typ, `Content` zahrnuty ve výsledném balíčku automaticky. Výchozí formát je `true`. |
| BuildOutputTargetFolder | Určuje složku, kam se mají umístit výstupní sestavení. Výstupní sestavení (a další výstupní soubory) se zkopírují do příslušných složek rozhraní. Další informace naleznete v tématu [výstupní sestavení](#output-assemblies). |
| ContentTargetFolders | Určuje výchozí umístění, kde se mají všechny soubory obsahu nacházet, pokud `PackagePath` nejsou pro ně zadány. Výchozí hodnota je Content; contentFiles. Další informace najdete v tématu [zahrnutí obsahu do balíčku](#including-content-in-a-package). |
| NuspecFile | Relativní nebo absolutní cesta k souboru *. nuspec* , který se používá pro balení. Je-li tento parametr zadán, použije se **výhradně** pro informace o balení a žádné informace v projektech se nepoužijí. Další informace naleznete v tématu [balení pomocí. nuspec](#packing-using-a-nuspec). |
| NuspecBasePath | Základní cesta pro soubor *. nuspec* Další informace naleznete v tématu [balení pomocí. nuspec](#packing-using-a-nuspec). |
| NuspecProperties | Seznam párů klíč = hodnota oddělený středníkem. Další informace naleznete v tématu [balení pomocí. nuspec](#packing-using-a-nuspec). |

## <a name="pack-scenarios"></a>scénáře sady Pack

### <a name="suppress-dependencies"></a>Potlačit závislosti

Chcete-li potlačit závislosti balíčků z vygenerovaného balíčku NuGet, nastavte na to, `SuppressDependenciesWhenPacking` `true` které umožní přeskočí všechny závislosti ze generovaného souboru nupkg.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` je zastaralá ve prospěch [`PackageIcon`](#packageicon) Vlastnosti. Od verze NuGet 5,3 a sady Visual Studio 2019 verze 16,3 `pack` vyvolá upozornění [NU5048](./errors-and-warnings/nu5048.md) , pokud je určeno pouze metadata balíčku `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Aby se zachovala zpětná kompatibilita se klienty a zdroji, které ještě nepodporují `PackageIcon` , zadejte obojí `PackageIcon` i `PackageIconUrl` . Visual Studio podporuje `PackageIcon` pro balíčky pocházející ze zdroje založeného na složkách.

#### <a name="packing-an-icon-image-file"></a>Balení souboru obrázku ikony

Při balení souboru obrázku ikony použijte `PackageIcon` vlastnost k určení cesty k souboru ikony vzhledem k kořenu balíčku. Navíc se ujistěte, že je soubor součástí balíčku. Velikost souboru obrázku je omezená na 1 MB. Podporované formáty souborů zahrnují JPEG a PNG. Doporučujeme, abyste 128 × 128 rozlišení obrazu.

Například:

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

`nuget pack` zkopíruje výstupní soubory s příponami,,,, `.exe` `.dll` `.xml` `.winmd` `.json` a `.pri` . Výstupní soubory, které jsou zkopírovány, závisí na tom, co nástroj MSBuild poskytuje z `BuiltOutputProjectGroup` cíle.

Existují dvě vlastnosti nástroje MSBuild, které lze použít v souboru projektu nebo na příkazovém řádku pro řízení, kde výstupní sestavení jdou:

- `IncludeBuildOutput`: Logická hodnota, která určuje, zda mají být do balíčku zahrnuty výstupní sestavení sestavení.
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

Chcete-li zahrnout obsah, přidejte do existující položky metadata navíc `<Content>` . Ve výchozím nastavení jsou všechny položky typu "obsah" zahrnuty do balíčku, Pokud nepřepíšete záznamy podobné následujícímu:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Ve výchozím nastavení je vše přidáno do kořenu `content` a `contentFiles\any\<target_framework>` složky v rámci balíčku a zachovává strukturu relativních složek, pokud nezadáte cestu k balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Pokud chcete kopírovat veškerý obsah pouze na konkrétní kořenové složky (místo `content` a `contentFiles` obojí), můžete použít vlastnost MSBuild `ContentTargetFolders` , která má výchozí hodnotu Content; contentFiles, ale lze ji nastavit na jiné názvy složek. Všimněte si, že pouze zadání "contentFiles" v `ContentTargetFolders` souboru vloží soubory do `contentFiles\any\<target_framework>` nebo na `contentFiles\<language>\<target_framework>` základě `buildAction` .

`PackagePath` může se jednat o sadu cílových cest oddělených středníky. Zadáním prázdné cesty k balíčku by se soubor přidal do kořenového adresáře balíčku. Například následující příkaz přidá `libuv.txt` do `content\myfiles` , `content\samples` a kořenovou složku balíčku:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

K dispozici je také vlastnost MSBuild `$(IncludeContentInPack)` , která má výchozí hodnotu `true` . Pokud je nastavená na `false` libovolný projekt, pak obsah z tohoto projektu není zahrnutý v balíčku NuGet.

Další metadata specifická pro sadu, která můžete nastavit na kterékoli z výše uvedených položek, zahrnují ```<PackageCopyToOutput>``` a ```<PackageFlatten>``` které sady ```CopyToOutput``` a ```Flatten``` hodnoty pro ```contentFiles``` položku ve výstupních nuspec.

> [!Note]
> Kromě položek obsahu `<Pack>` `<PackagePath>` lze metadata a také nastavit na soubory s akcí sestavení kompilovat, EmbeddedResource, ApplicationDefinition, Page, Resource, třídy SplashScreen, vazbě designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource nebo None.
>
> Pokud má balíček při použití vzorů expanze názvů připojit název souboru k cestě k balíčku, musí cesta k balíčku končit znakem oddělovače složky. v opačném případě se cesta k balíčku považuje za úplnou cestu včetně názvu souboru.

### <a name="includesymbols"></a>IncludeSymbols

Při použití se `MSBuild -t:pack -p:IncludeSymbols=true` `.pdb` zkopírují odpovídající soubory spolu s jinými výstupními soubory ( `.dll` , `.exe` , `.winmd` , `.xml` , `.json` , `.pri` ). Všimněte si, že nastavení `IncludeSymbols=true` vytvoří regulární balíček *a* balíček symbolů.

### <a name="includesource"></a>IncludeSource

To je stejné jako `IncludeSymbols` s tím rozdílem, že kopíruje také zdrojové soubory spolu se `.pdb` soubory. Všechny soubory typu `Compile` jsou zkopírovány za účelem `src\<ProjectName>\` zachování struktury složek relativní cesty ve výsledném balíčku. Totéž se také stane u zdrojových souborů, `ProjectReference` které mají `TreatAsPackageReference` nastavené na `false` .

Pokud je soubor typu Compile mimo složku projektu, pak je pouze přidán do `src\<ProjectName>\` .

### <a name="packing-a-license-expression-or-a-license-file"></a>Balení licenčního výrazu nebo licenčního souboru

Při použití licenčního výrazu použijte `PackageLicenseExpression` vlastnost. Ukázku najdete v tématu [Ukázka licenčního výrazu](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Další informace o výrazech licencí a licencích, které jsou přijímány službou NuGet.org, najdete v tématu [metadata licencí](nuspec.md#license).

Při balení licenčního souboru použijte `PackageLicenseFile` vlastnost k určení cesty k balíčku relativní ke kořenu balíčku. Navíc se ujistěte, že je soubor součástí balíčku. Například:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Ukázku najdete v části [Ukázka souboru s licencí](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

> [!NOTE]
> `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` V jednom okamžiku může být určena pouze jedna z, a.

### <a name="packing-a-file-without-an-extension"></a>Balení souboru bez přípony

V některých scénářích, jako je například balení souboru s licencí, může být vhodné zahrnout soubor bez přípony.
Z historických důvodů nástroj NuGet & MSBuild považuje cesty bez přípony jako adresáře.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Soubor bez ukázkového rozšíření](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).
### <a name="istool"></a>Nástroj

Při použití `MSBuild -t:pack -p:IsTool=true` aplikace jsou všechny výstupní soubory, jak je uvedeno ve scénáři [výstup sestavení](#output-assemblies) , zkopírovány do `tools` složky namísto `lib` složky. Všimněte si, že se liší od a, `DotNetCliTool` který je určen nastavením `PackageType` v `.csproj` souboru.

### <a name="packing-using-a-nuspec"></a>Balení pomocí. nuspec

I když se místo toho doporučuje [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` souboru v souboru projektu, můžete zvolit použití `.nuspec` souboru k balení projektu. Pro projekt bez sady SDK, který používá, je `PackageReference` nutné importovat, `NuGet.Build.Tasks.Pack.targets` aby bylo možné spustit úlohu balíčku. Před zabalením souboru nuspec je ještě nutné projekt obnovit. (Projekt ve stylu sady SDK obsahuje cíle balíčku ve výchozím nastavení.)

Cílová architektura souboru projektu je nerelevantní a při balení nuspec se nepoužívá. Následující tři vlastnosti MSBuild jsou relevantní pro balení pomocí `.nuspec` :

1. `NuspecFile`: relativní nebo absolutní cesta k `.nuspec` souboru, který se používá k balení.
1. `NuspecProperties`: středníkem oddělený seznam dvojic klíč = hodnota. Kvůli způsobu, jakým funguje analýza příkazového řádku nástroje MSBuild, je nutné zadat více vlastností následujícím způsobem: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: Základní cesta k `.nuspec` souboru.

Pokud používáte `dotnet.exe` k balení projektu, použijte příkaz podobný následujícímu:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Při použití nástroje MSBuild k sbalení projektu použijte příkaz podobný následujícímu:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Všimněte si prosím, že balení nuspec pomocí dotnet.exe nebo MSBuild také vede k sestavení projektu ve výchozím nastavení. K tomu je možné se vyhnout předáním ```--no-build``` vlastnosti do dotnet.exe, což je ekvivalent nastavení ```<NoBuild>true</NoBuild> ``` v souboru projektu spolu s nastavením ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` v souboru projektu.

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

`pack`Cíl poskytuje dva Rozšiřovací body, které jsou spuštěny v sestavení specifickém pro vnitřní, cílové rozhraní. Rozšiřující body podporují obsah a sestavení konkrétního cílového rozhraní do balíčku:

- `TargetsForTfmSpecificBuildOutput` cíl: použijte pro soubory uvnitř `lib` složky nebo složky zadané pomocí `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` cíl: použijte pro soubory mimo `BuildOutputTargetFolder` .

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificBuildOutput)` Vlastnosti. Pro všechny soubory, které potřebují přejít do nástroje `BuildOutputTargetFolder` (ve výchozím nastavení lib), by měl cíl zapisovat tyto soubory do skupiny Item `BuildOutputInPackage` a nastavit následující dvě hodnoty metadat:

- `FinalOutputPath`: Absolutní cesta k souboru; Pokud není zadaný, použije se identita k vyhodnocení zdrojové cesty.
- `TargetPath`: (Volitelné) nastavte, kdy bude soubor potřebovat přejít do podsložky v rámci `lib\<TargetFramework>` , jako jsou satelitní sestavení, která se nacházejí v odpovídajících složkách kultury. Výchozí hodnota je název souboru.

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

Napište vlastní cíl a zadejte ho jako hodnotu `$(TargetsForTfmSpecificContentInPackage)` Vlastnosti. U všech souborů, které se mají zahrnout do balíčku, by měl cíl tyto soubory zapsat do `TfmSpecificPackageFile` skupiny položek a nastavit následující volitelná metadata:

- `PackagePath`: Cesta, kde by měl být v balíčku výstup souboru. Při přidání více než jednoho souboru do stejné cesty k balíčku vyvolá NuGet vystavení upozornění.
- `BuildAction`: Akce sestavení, která se má souboru přiřadit, se vyžaduje jenom v případě, že je cesta k balíčku ve `contentFiles` složce. Výchozí hodnota je None.

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

`MSBuild -t:restore` (které `nuget restore` a `dotnet restore` používají se v projektech .NET Core), obnoví balíčky, na které se odkazuje v souboru projektu, takto:

1. Číst všechny odkazy z projektu na projekt
1. Přečtěte si vlastnosti projektu a najděte mezilehlé složky a cílová rozhraní.
1. Předání dat nástroje MSBuild do NuGet.Build.Tasks.dll
1. Spustit obnovení
1. Stáhnout balíčky
1. Zápis souboru prostředků, cílů a vlastností props

`restore`Cíl funguje pro projekty, které používají formát PackageReference.
`MSBuild 16.5+` má také [podporu](#restoring-packagereference-and-packagesconfig-with-msbuild) pro `packages.config` formát.

> [!NOTE]
> `restore`Cíl [by neměl být spuštěn](#restoring-and-building-with-one-msbuild-command) v kombinaci s `build` cílem.

### <a name="restore-properties"></a>Obnovit vlastnosti

Další nastavení obnovení může pocházet z vlastností MSBuild v souboru projektu. Hodnoty lze také nastavit z příkazového řádku pomocí `-p:` přepínače (viz příklady níže).

| Vlastnost | Popis |
|--------|--------|
| RestoreSources | Seznam zdrojů balíčků oddělených středníkem. |
| RestorePackagesPath | Cesta ke složce uživatelských balíčků |
| RestoreDisableParallel | Omezit stahování na jednu po druhé. |
| RestoreConfigFile | Cesta k `Nuget.Config` souboru, který se má použít |
| RestoreNoCache | Je-li nastavena hodnota true, nepoužívejte balíčky uložené v mezipaměti. Viz [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Pokud má hodnotu true, ignoruje neúspěšné nebo chybějící zdroje balíčků. |
| RestoreFallbackFolders | Záložní složky používané ve stejném způsobu, jakým se používá složka uživatelských balíčků. |
| RestoreAdditionalProjectSources | Další zdroje, které se mají použít při obnovení. |
| RestoreAdditionalProjectFallbackFolders | Další záložní složky, které se mají použít při obnovení |
| RestoreAdditionalProjectFallbackFoldersExcludes | Vyloučí záložní složky zadané v `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Cesta k `NuGet.Build.Tasks.dll` . |
| RestoreGraphProjectInput | Středníkem oddělený seznam projektů, které mají být obnoveny, které by měly obsahovat absolutní cesty. |
| RestoreUseSkipNonexistentTargets  | Když jsou projekty shromažďovány pomocí nástroje MSBuild, určuje, zda jsou shromažďovány pomocí `SkipNonexistentTargets` optimalizace. Pokud není nastaveno, výchozí hodnota je `true` . Příčinou je rychlé chování při selhání, když cíle projektu nelze importovat. |
| MSBuildProjectExtensionsPath | Výstupní složka, výchozí nastavení `BaseIntermediateOutputPath` a `obj` Složka. |
| RestoreForce | V projektech založených na PackageReference vynutí vyřešení všech závislostí i v případě, že bylo poslední obnovení úspěšné. Zadání tohoto příznaku se podobá odstranění `project.assets.json` souboru. To neobejde mezipaměť HTTP-cache. |
| RestorePackagesWithLockFile | Výslovný se na použití souboru zámku. |
| RestoreLockedMode | Spustit obnovení v uzamčeném režimu. To znamená, že obnovení nebude přehodnocovat závislosti. |
| NuGetLockFilePath | Vlastní umístění souboru zámku. Výchozí umístění je vedle projektu a je pojmenováno `packages.lock.json` . |
| RestoreForceEvaluate | Vynutí obnovení pro přepočítání závislostí a aktualizaci souboru zámku bez upozornění. |
| RestorePackagesConfig | Přepínač pro výslovný souhlas, který obnovuje projekty pomocí packages.config. Podpora pouze s nástrojem `MSBuild -t:restore` . |
| RestoreUseStaticGraphEvaluation | Přepínač výslovného souhlasu pro použití statického vyhodnocení grafu MSBuild namísto standardního vyhodnocení. Statické vyhodnocení grafu je experimentální funkce, která je výrazně rychlejší pro velké úložiště a řešení. |

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

Obnovení vytvoří ve složce buildu následující soubory `obj` :

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

Stejná logika platí pro jiné cíle podobné `build` .

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a>Obnovení PackageReference a packages.config pomocí nástroje MSBuild

Pomocí nástroje MSBuild 16.5 + packages.config jsou také podporovány pro `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` obnovení je k dispozici pouze pro `MSBuild 16.5+` , a nikoli s `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Obnovení pomocí vyhodnocení statického grafu MSBuild

> [!NOTE]
> Pomocí nástroje MSBuild 16.6 + nástroj NuGet přidal experimentální funkci pro použití statického vyhodnocení grafu z příkazového řádku, který významně vylepšuje čas obnovení pro velká úložiště.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Případně ho můžete povolit nastavením vlastnosti v adresáři. Build. props.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Od sady Visual Studio 2019. x a NuGet 5. x se tato funkce považuje za experimentální a výslovný souhlas. Podrobnosti o tom, kdy bude tato funkce ve výchozím nastavení povolená, najdete v [balíčku NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) .

Statické obnovení grafu mění část obnovení MSBuild, projekt čte a vyhodnocuje, ale nikoli algoritmus obnovení. Algoritmus obnovení je stejný u všech nástrojů NuGet (NuGet.exe, MSBuild.exe, dotnet.exe a Visual Studio).

Ve velmi málo scénářích se statické obnovení grafu může chovat odlišně od aktuálního obnovení a některé deklarované PackageReferences nebo ProjectReferences mohou chybět.

Pokud chcete při migraci na statický graf obnovit svůj názor, zvažte spuštění:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet by *neměl* hlásit žádné změny. Pokud se zobrazí nesoulad, uveďte problém na [stránce NuGet/Home](https://github.com/nuget/home/issues/new).

### <a name="replacing-one-library-from-a-restore-graph"></a>Nahrazení jedné knihovny z grafu obnovení

Pokud obnovení předává nesprávné sestavení, je možné vyřadit výchozí volbu balíčků a nahradit ji vlastní volbou. Nejprve s nejvyšší úrovní `PackageReference` , vylučte všechny prostředky:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Dále přidejte vlastní odkaz na příslušnou místní kopii knihovny DLL:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
