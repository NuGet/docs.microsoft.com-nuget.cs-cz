---
title: Odkaz na soubor. nuspec pro NuGet
description: Soubor. nuspec obsahuje metadata balíčku, která se používají při sestavování balíčku a poskytování informací pro uživatele balíčku.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 67bc95135f746c4a4685773808756df399cbf01e
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959707"
---
# <a name="nuspec-reference"></a>odkaz. nuspec

`.nuspec` Soubor je manifest XML, který obsahuje metadata balíčku. Tento manifest slouží k sestavení balíčku a k poskytování informací pro uživatele. Manifest je vždy součástí balíčku.

V tomto tématu:

- [Obecné formuláře a schéma](#general-form-and-schema)
- [Náhradní tokeny](#replacement-tokens) (při použití s projektem sady Visual Studio)
- [Závislosti](#dependencies)
- [Explicitní odkazy na sestavení](#explicit-assembly-references)
- [Odkazy na sestavení rozhraní .NET Framework](#framework-assembly-references)
- [Zahrnutí souborů sestavení](#including-assembly-files)
- [Zahrnutí souborů obsahu](#including-content-files)
- [Příklady souborů nuspec](#example-nuspec-files)

## <a name="project-type-compatibility"></a>Kompatibilita typů projektu

- Použijte `.nuspec` `packages.config`s `nuget.exe pack` pro projekty, které nejsou ve stylu sady SDK, které používají.

- Soubor není vyžadován k vytváření balíčků pro projekty ve [stylu sady SDK](../resources/check-project-format.md) (obvykle se jedná o projekty .NET Core a .NET Standard, které používají [atribut SDK](/dotnet/core/tools/csproj#additions)). `.nuspec` (Všimněte si, `.nuspec` že se generuje při vytváření balíčku.)

   Pokud `dotnet.exe pack` vytváříte balíček pomocí nebo `msbuild pack target`, doporučujeme místo toho [Zahrnout všechny](../reference/msbuild-targets.md#pack-target) `.nuspec` vlastnosti, které jsou obvykle v souboru v souboru projektu. Místo toho se ale můžete rozhodnout [použít `.nuspec` soubor k `dotnet.exe` balení pomocí `msbuild pack target`nebo ](../reference/msbuild-targets.md#packing-using-a-nuspec).

- Pro projekty migrované z `packages.config` aplikace do `.nuspec` [PackageReference](../consume-packages/package-references-in-project-files.md) není pro vytvoření balíčku vyžadován soubor. Místo toho použijte [MSBuild-t:Pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

## <a name="general-form-and-schema"></a>Obecné formuláře a schéma

Aktuální `nuspec.xsd` soubor schématu najdete v [úložišti GitHub NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

V rámci tohoto schématu `.nuspec` má soubor následující obecný tvar:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

V případě jasné vizuální reprezentace schématu otevřete soubor schématu v aplikaci Visual Studio v režimu návrhu a klikněte na odkaz **Průzkumník schémat XML** . Případně soubor otevřete jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **Zobrazit Průzkumníka schémat XML**. Jak můžete vidět následující pohled (Pokud je převážně rozbalený):

![Průzkumník schémat sady Visual Studio s otevřeným nuspec. xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Požadované prvky metadat

I když následující prvky jsou minimální požadavky na balíček, měli byste zvážit přidání [volitelných prvků metadat](#optional-metadata-elements) pro zlepšení celkového prostředí, které vývojáři mají s vaším balíčkem. 

Tyto prvky se musí objevit v `<metadata>` rámci elementu.

#### <a name="id"></a>id 
Identifikátor balíčku bez rozlišení velkých a malých písmen, který musí být jedinečný v rámci nuget.org nebo jakákoli galerie, v níž se balíček nachází. ID nesmí obsahovat mezery ani znaky, které nejsou platné pro adresu URL a obecně následují pravidla oboru názvů .NET. Pokyny najdete v tématu [Volba jedinečného identifikátoru balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .
#### <a name="version"></a>verze
Verze balíčku, podle vzoru *hlavní_verze. podverze. Oprava* . Čísla verzí můžou obsahovat příponu předběžné verze, jak je popsáno v tématu [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions). 
#### <a name="description"></a>description
Dlouhý popis balíčku pro zobrazení uživatelského rozhraní. 
#### <a name="authors"></a>Autoři
Čárkami oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazí v galerii NuGet na nuget.org a používají se pro balíčky křížového odkazu stejnými autory. 

### <a name="optional-metadata-elements"></a>Volitelné prvky metadat

#### <a name="owners"></a>vlastníka
Čárkami oddělený seznam tvůrců balíčků s použitím názvů profilů v nuget.org. Často se jedná o stejný seznam jako v `authors`a při nahrávání balíčku do NuGet.org se ignoruje. Viz [Správa vlastníků balíčků na NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). 

#### <a name="projecturl"></a>projectUrl
Adresa URL domovské stránky balíčku, která se často zobrazuje v uživatelském rozhraní, a také nuget.org. 

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl se už nepoužívá. Místo toho použijte licenci.

Adresa URL licence balíčku, která se často zobrazuje v uživatelská rozhraní jako nuget.org.

#### <a name="license"></a>průkaz
SPDX licenční výraz nebo cesta k souboru s licencí v balíčku, který se často zobrazuje v uživatelská rozhraní jako nuget.org. Pokud je balíček licencován v rámci společné licence, jako je například MIT nebo BSD-2, použijte přidružený [identifikátor licence SPDX](https://spdx.org/licenses/). Příklad:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org akceptuje pouze licenční výrazy, které jsou schváleny v rámci iniciativy Open Source nebo Free Software Foundation.

Pokud je váš balíček licencován více běžnými licencemi, můžete zadat složenou licenci pomocí [syntaxe výrazu SPDX verze 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60). Příklad:

`<license type="expression">BSD-2-Clause OR MIT</license>`

Pokud používáte vlastní licenci, která není podporovaná výrazy licence, můžete zabalit `.txt` soubor nebo `.md` soubor s textem licence. Příklad:

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

V případě ekvivalentu MSBuild si prohlédněte [balení licenčního výrazu nebo souboru s licencí](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

Přesná Syntaxe výrazů s licenčními výrazy NuGet je popsaná níže v tématu [ABNF](https://tools.ietf.org/html/rfc5234).
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl
Adresa URL 64 × 64 obrázku s pozadím průhlednosti, která se má použít jako ikona balíčku v zobrazení uživatelského rozhraní. Ujistěte se, že tento prvek obsahuje *adresu URL přímého obrázku* , a ne adresu URL webové stránky, která obsahuje obrázek. Pokud například chcete použít image z GitHubu, použijte adresu URL nezpracovaného souboru <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>jako. 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku.

#### <a name="developmentdependency"></a>developmentDependency
*(2.8+)* Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků. Pomocí PackageReference (NuGet 4,8 +) Tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace. Viz [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)

#### <a name="summary"></a>souhrn
Krátký popis balíčku pro zobrazení uživatelského rozhraní. `description` Je-li tento parametr vynechán, je použita zkrácená verze nástroje.

#### <a name="releasenotes"></a>releaseNotes
*(1.5+)* Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.

#### <a name="copyright"></a>Úprava
*(1.5+)* Copyright podrobnosti balíčku.

#### <a name="language"></a>jazyk
ID národního prostředí balíčku. Viz [vytváření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).

#### <a name="tags"></a>značky
Mezerou oddělený seznam značek a klíčových slov, které popisují balíček a pomáhají zjistit balíčky pomocí vyhledávání a filtrování. 

#### <a name="serviceable"></a>serviceable 
*(3.3+)* Pouze pro interní NuGet použít.

#### <a name="repository"></a>úložiště
Metadata úložiště sestávající ze čtyř volitelných atributů: `type` a `url` *(4.0 +)* a `branch` a `commit` *(4.6 +)* . Tyto atributy umožňují mapování `.nupkg` na úložiště, které ho vytvořilo, s potenciálem, který se má považovat za název jednotlivé větve a/nebo na potvrzení hodnoty hash SHA-1, která balíček vytvořila. Měla by to být veřejně dostupná adresa URL, kterou lze vyvolat přímo pomocí softwaru pro správu verzí. Neměla by se jednat o stránku HTML, která je určena pro daný počítač. Pro odkazování na stránku projektu použijte `projectUrl` místo toho pole.

Příklad:
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a>název
Popisný název balíčku, který se dá použít v některých zobrazeních uživatelského rozhraní. (nuget.org a správce balíčků v aplikaci Visual Studio nezobrazuje název)

#### <a name="collection-elements"></a>Prvky kolekce

#### <a name="packagetypes"></a>packageTypes
*(3.5 +)* Kolekce nula nebo více `<packageType>` prvků určující typ balíčku, pokud je jiný než tradiční balíček závislostí. Každý packageType má atributy *názvu* a *verze*. Viz [Nastavení typu balíčku](../create-packages/set-package-type.md).
#### <a name="dependencies"></a>závislosti
Kolekce nula nebo více `<dependency>` prvků, které určují závislosti pro balíček. Každá závislost má atributy *ID*, *verze*, *include* (3. x +) a *Exclude* (3. x +). Viz [závislosti](#dependencies-element) níže.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1,2 +)* Kolekce nula nebo více `<frameworkAssembly>` prvků, které identifikují .NET Framework odkazy na sestavení, které tento balíček vyžaduje, což zajistí přidání odkazů do projektů, které balíček spotřebovává. Každý frameworkAssembly má atributy *AssemblyName* a *targetFramework* . Viz [určení sestavení rozhraní odkazy v mezipaměti GAC](#specifying-framework-assembly-references-gac) níže. |
#### <a name="references"></a>odkazy
*(1,5 +)* Kolekce nula nebo více `<reference>` prvků pojmenování sestavení ve `lib` složce balíčku, které jsou přidány jako odkazy na projekt. Každý odkaz má atribut *File* . `<references>`může také obsahovat `<group>` element s atributem *targetFramework* , který pak obsahuje `<reference>` prvky. Pokud tento parametr vynecháte, `lib` jsou zahrnuty všechny odkazy v nástroji. Viz [zadání explicitních odkazů na sestavení](#specifying-explicit-assembly-references) níže.
#### <a name="contentfiles"></a>contentFiles
*(3.3 +)* Kolekce `<files>` prvků, které identifikují soubory obsahu, které mají být zahrnuty do náročného projektu. Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu. Viz [Určení souborů, které se mají zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.
#### <a name="files"></a>soubory 
`<metadata>` `<contentFiles>` Uzel může `<files>` obsahovat uzel jako uzel na `<metadata>`stejné úrovni a podřízená položka v rámci, k určení sestavení a souborů obsahu, které mají být zahrnuty do balíčku. `<package>` Podrobnosti najdete v části [zahrnutí souborů sestavení](#including-assembly-files) a [zahrnutí souborů obsahu](#including-content-files) dále v tomto tématu.

### <a name="metadata-attributes"></a>atributy metadat

#### <a name="minclientversion"></a>minClientVersion
Určuje minimální verzi klienta NuGet, která může nainstalovat tento balíček, který vynutila NuGet. exe a správce balíčků sady Visual Studio. Tato funkce se používá vždy, když balíček závisí na konkrétních funkcích `.nuspec` souboru, které byly přidány v konkrétní verzi klienta NuGet. Například balíček, který používá `developmentDependency` atribut, by měl pro `minClientVersion`použít hodnotu "2,8". Podobně balíček, který používá `contentFiles` element (viz další oddíl), by měl být nastaven `minClientVersion` na "3,3". Všimněte si také, že vzhledem k tomu, že klienti NuGet starší než 2,5 nerozpoznávají tento příznak, *vždy* zamítnou instalaci balíčku bez `minClientVersion` ohledu na to, co obsahuje.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a>Náhradní tokeny

Při vytváření balíčku `-properties` `.nuspec` `pack` `<metadata>` [ `nuget pack` nahradí příkaz](../reference/cli-reference/cli-ref-pack.md) tokeny $-s oddělovači v uzlu souboru hodnotami, které pocházejí ze souboru projektu nebo přepínače příkazu.

Na příkazovém řádku určíte hodnoty tokenu pomocí `nuget pack -properties <name>=<value>;<name>=<value>`. Například můžete použít token `$owners$` jako a `$desc$` v `.nuspec` a a zadat hodnoty v době balení následujícím způsobem:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Pokud chcete použít hodnoty z projektu, zadejte tokeny popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` `AssemblyInfo.cs` takovém případě nebo `AssemblyInfo.vb`).

Chcete-li použít tyto tokeny, spusťte `nuget pack` se souborem projektu, a ne `.nuspec`pouze. Například při použití `$id$` následujícího příkazu jsou tokeny a `$version$` v `.nuspec` souboru nahrazeny hodnotami projektu `AssemblyName` a `AssemblyVersion` :

```ps
nuget pack MyProject.csproj
```

Obvykle, když máte projekt, vytvoříte `.nuspec` `nuget spec MyProject.csproj` počáteční, který automaticky obsahuje některé z těchto standardních tokenů. Pokud však projekt nemá hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` dojde k chybě. Pokud navíc změníte hodnoty projektu, nezapomeňte před vytvořením balíčku znovu sestavit. To lze provést pohodlně pomocí `build` přepínače příkazu Pack.

S výjimkou `$configuration$`jsou hodnoty v projektu použity v předvolbách pro všechny přiřazené ke stejnému tokenu na příkazovém řádku.

| Podpisový | Zdroj hodnoty | Value
| --- | --- | ---
| **$id $** | Soubor projektu | AssemblyName (title) ze souboru projektu |
| **$version $** | AssemblyInfo | AssemblyInformationalVersion, pokud je k dispozici, jinak AssemblyVersion |
| **$author $** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description $** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Knihovna DLL sestavení | Konfigurace použitá pro sestavení sestavení, výchozí nastavení pro ladění. Všimněte si, že pokud chcete vytvořit balíček pomocí konfigurace vydané verze, vždy `-properties Configuration=Release` použijte příkaz na příkazovém řádku. |

Tokeny lze také použít k překladu cest při zahrnutí [souborů sestavení](#including-assembly-files) a [souborů obsahu](#including-content-files). Tokeny mají stejné názvy jako vlastnosti MSBuild, což umožňuje vybrat soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení. Například pokud v `.nuspec` souboru použijete následující tokeny:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

A sestavíte sestavení, `AssemblyName` jehož `LoggingLibrary` je s `Release` konfigurací `.nuspec` v nástroji MSBuild, výsledné řádky v souboru v balíčku jsou následující:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Element závislosti

Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvků, které identifikují další balíčky, na kterých závisí balíček nejvyšší úrovně. `<dependencies>` Atributy pro každý `<dependency>` z nich jsou následující:

| Atribut | Popis |
| --- | --- |
| `id` | Požadovanou ID balíčku závislosti, například "EntityFramework" a "NUnit", což je název balíčku nuget.org zobrazený na stránce balíčku. |
| `version` | Požadovanou Rozsah verzí, které jsou přijatelné jako závislost. Přesnou syntaxi najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) . Zástupné verze (plovoucí) nejsou podporovány. |
| include | Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, kterou chcete zahrnout do finálního balíčku. Výchozí hodnota je `all`. |
| exclude | Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, která se má vyloučit v konečném balíčku. Výchozí hodnota je `build,analyzers` , která může být přepsána. Ale `content/ ContentFiles` jsou také implicitně vyloučené v konečném balíčku, který nelze přepsat. Zadané značky s `exclude` prioritou mají přednost před hodnotami určenými pomocí. `include` Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`. |

| Značka include/Exclude | Ovlivněné složky v cíli |
| --- | --- |
| contentFiles | Obsah |
| modul runtime | Modul runtime, prostředky a FrameworkAssemblies |
| sestavení | Knihovna |
| sestavení | Build (MSBuild props and targets) |
| nativní | nativní |
| žádná | Žádné složky |
| všechny | Všechny složky |

Například následující řádky označují závislosti `PackageA` verze 1.1.0 nebo vyšší a `PackageB` verze 1. x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Následující řádky označují závislosti pro stejné balíčky, `contentFiles` ale určují, že se mají zahrnout složky `build` `PackageA` a a všechno, ale `native` složky `PackageB`a `compile` .

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> Při vytváření `.nuspec` z projektu pomocí nástroje `nuget spec`nejsou závislosti, které existují v tomto projektu, automaticky zahrnuty ve výsledném `.nuspec` souboru. Místo toho použijte `nuget pack myproject.csproj`a získejte soubor *. nuspec* v rámci generovaného souboru *. nupkg* . This *. nuspec* obsahuje závislosti.

### <a name="dependency-groups"></a>Skupiny závislostí

*Verze 2.0 +*

Jako alternativu k jednomu nestrukturovanému seznamu lze závislosti zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci. `<dependencies>`

Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` prvků. Tyto závislosti jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem rozhraní projektu.

`<group>` Prvek`targetFramework` bez atributu je použit jako výchozí nebo záložní seznam závislostí. Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .

> [!Important]
> Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.

Následující příklad ukazuje různé varianty `<group>` elementu:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Explicitní odkazy na sestavení

Element je používán projekty pomocí `packages.config` k explicitnímu určení sestavení, na které by měl cílový projekt odkazovat při použití balíčku. `<references>` Explicitní odkazy jsou obvykle používány pro sestavení pouze v době návrhu. Další informace naleznete na stránce věnované [výběru sestavení odkazovaných projekty](../create-packages/select-assemblies-referenced-by-projects.md) , kde najdete další informace.

Například následující `<references>` element instruuje NuGet, aby přidal odkazy pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že jsou v balíčku k dispozici další sestavení:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>Referenční skupiny

Jako alternativu k jednomu nestrukturovanému seznamu lze odkazy zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci. `<references>`

Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<reference>` prvků. Tyto odkazy jsou přidány do projektu, pokud je cílová architektura kompatibilní s profilem rozhraní projektu.

`<group>` Prvek`targetFramework` bez atributu je použit jako výchozí nebo záložní seznam odkazů. Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .

> [!Important]
> Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.

Následující příklad ukazuje různé varianty `<group>` elementu:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Odkazy na sestavení rozhraní .NET Framework

Sestavení rozhraní jsou ta, která jsou součástí rozhraní .NET Framework a měla by již být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač. Díky identifikaci těchto sestavení v rámci `<frameworkAssemblies>` elementu může balíček zajistit, aby byly do projektu přidány požadované odkazy v případě, že projekt nemá takové odkazy již. Taková sestavení samozřejmě nejsou součástí balíčku přímo.

Element obsahuje nula nebo více `<frameworkAssembly>` elementů, z nichž každý určuje následující atributy: `<frameworkAssemblies>`

| Atribut | Popis |
| --- | --- |
| **assemblyName** | Požadovanou Plně kvalifikovaný název sestavení. |
| **targetFramework** | Volitelné Určuje cílovou architekturu, na kterou se vztahuje tento odkaz. Je-li tento parametr vynechán, znamená to, že odkaz se vztahuje na všechna rozhraní. Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) . |

Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové rozhraní a odkaz na `System.ServiceModel` pro .NET Framework 4,0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Zahrnutí souborů sestavení

Pokud budete postupovat podle konvencí popsaných v [tématu Vytvoření balíčku](../create-packages/creating-a-package.md), nemusíte explicitně zadat seznam souborů v `.nuspec` souboru. `nuget pack` Příkaz automaticky vybere potřebné soubory.

> [!Important]
> Když je balíček nainstalován do projektu, NuGet automaticky přidá odkazy na sestavení do knihoven DLL balíčku, *kromě* těch, které jsou pojmenovány `.resources.dll` , protože se předpokládá, že jsou lokalizovaná satelitní sestavení. Z tohoto důvodu `.resources.dll` nepoužívejte pro soubory, které jinak obsahují základní kód balíčku.

Chcete-li obejít toto automatické chování a explicitně řídit, které soubory jsou součástí balíčku, `<files>` umístěte prvek jako `<package>` podřízený objekt `<metadata>`(a na stejné místo) a Identifikujte každý soubor samostatným `<file>` prvkem. Příklad:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

S NuGet 2. x a starším a projekty, `packages.config`které `<files>` používají, se element používá také k zahrnutí neměnných souborů obsahu při instalaci balíčku. S NuGet 3.3 + a projekty PackageReference `<contentFiles>` se místo toho použije element. Podrobnosti najdete v části [zahrnutí souborů obsahu](#including-content-files) níže.

### <a name="file-element-attributes"></a>Atributy elementu souboru

Každý `<file>` prvek určuje následující atributy:

| Atribut | Popis |
| --- | --- |
| **src** | Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem. Cesta je relativní vzhledem k `.nuspec` souboru, pokud není zadána absolutní cesta. Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky. |
| **cílové** | Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které `lib`musí začínat `build`na, `content`, nebo `tools`. Viz [vytvoření. nuspec z pracovního adresáře založeného na konvencích](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **slevy** | Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, `src` jsou odděleny středníkem. Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky. |

### <a name="examples"></a>Příklady

**Jedno sestavení**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Samostatné sestavení specifické pro cílovou architekturu**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Sada knihoven DLL pomocí zástupného znaku**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Knihovny DLL pro různé architektury**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Vyloučení souborů**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Zahrnutí souborů obsahu

Soubory obsahu jsou neměnné soubory, které musí balíček zahrnout do projektu. Neměnné, nejsou určeny pro úpravy nenáročným projektem. Mezi příklady souborů obsahu patří:

- Obrázky, které jsou vložené jako prostředky
- Zdrojové soubory, které jsou již kompilovány
- Skripty, které je potřeba zahrnout do výstupu sestavení projektu
- Konfigurační soubory balíčku, které je potřeba zahrnout do projektu, ale nevyžadují žádné změny specifické pro projekt

Soubory obsahu jsou zahrnuty v balíčku pomocí `<files>` elementu a `content` určení složky v `target` atributu. Nicméně tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který místo toho používá `<contentFiles>` element.

Pro maximální kompatibilitu s spotřebou projektů balíček v ideálním případě Určuje soubory obsahu v obou prvcích.

### <a name="using-the-files-element-for-content-files"></a>Použití elementu Files pro soubory obsahu

Pro soubory obsahu stačí použít stejný formát jako u souborů sestavení, ale určete `content` jako základní složku `target` v atributu, jak je znázorněno v následujících příkladech.

**Základní soubory obsahu**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Soubory obsahu s adresářovou strukturou**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Soubor obsahu specifický pro cílovou architekturu**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Soubor obsahu byl zkopírován do složky s tečkou v názvu**

V takovém případě NuGet zjistí, že rozšíření v `target` neodpovídá rozšíření v `src` nástroji, a proto zpracovává tuto `target` část názvu jako složku:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Soubory obsahu bez rozšíření**

Chcete-li zahrnout soubory bez přípony, použijte `*` zástupné znaky nebo `**` :

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Soubory obsahu s hlubokým umístěním a hlubokou cílovou cestou**

V tomto případě předpokládá, že vzhledem k příponám souborů ve zdrojové a cílové shodě NuGet předpokládá, že cílem je název souboru, a ne složka:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Přejmenování souboru obsahu v balíčku**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Vyloučení souborů**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Použití elementu contentFiles pro soubory obsahu

*NuGet 4.0 + s PackageReference*

Ve výchozím nastavení balíček umístí obsah do `contentFiles` složky (viz níže) a `nuget pack` zahrne všechny soubory v této složce s použitím výchozích atributů. V takovém případě není nutné zahrnout `contentFiles` uzel `.nuspec` do.

Chcete-li určit, které soubory jsou `<contentFiles>` zahrnuty, prvek určuje `<files>` kolekci prvků, které identifikují přesné soubory.

Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu:

| Atribut | Popis |
| --- | --- |
| **include** | Požadovanou Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem. Cesta je relativní ke `contentFiles` složce, pokud není zadána absolutní cesta. Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky. |
| **slevy** | Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, `src` jsou odděleny středníkem. Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky. |
| **buildAction** | Akce sestavení, která má být přiřazena položce obsahu pro `Content`MSBuild, jako například `Embedded Resource`, `None` `Compile`,, atd. Výchozí hodnota je `Compile`. |
| **copyToOutput** | Logická hodnota označující, zda se mají kopírovat položky obsahu do výstupní složky Build (nebo Publishing). Výchozí hodnota je false. |
| **Flatten** | Logická hodnota označující, zda se mají kopírovat položky obsahu do jediné složky ve výstupu sestavení (true), nebo pro zachování struktury složek v balíčku (false). Tento příznak funguje pouze v případě, že příznak copyToOutput je nastaven na hodnotu true. Výchozí hodnota je false. |

Při instalaci balíčku NuGet aplikuje podřízené prvky `<contentFiles>` od shora dolů. Pokud se stejný soubor shoduje s více položkami, uplatní se všechny položky. Pokud dojde ke konfliktu pro stejný atribut, přepíše položka nejvyšší úrovně nižší položky.

#### <a name="package-folder-structure"></a>Struktura složky balíčku

Projekt balíčku by měl strukturovat obsah pomocí následujícího vzoru:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages`může to `cs`být `vb`, `fs` ,`any`, nebo malý ekvivalent daného`$(ProjectLanguage)`
- `TxM`je libovolný moniker platného cílového rozhraní, který podporuje NuGet (viz [cílové architektury](../reference/target-frameworks.md)).
- Ke konci této syntaxe může být připojena jakákoli struktura složky.

Příklad:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Prázdné složky se můžou `.` použít k odhlášení o poskytování obsahu pro určité kombinace jazyka a TxM, například:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Příklad oddílu contentFiles

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a>Příklady souborů nuspec

**Jednoduchá `.nuspec` , která neurčuje závislosti nebo soubory**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**A `.nuspec` se závislostmi**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**A `.nuspec` se soubory**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**A `.nuspec` se sestaveními architektury**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

V tomto příkladu jsou nainstalovány následující pro konkrétní cíle projektu:

- .NET4 -> `System.Web`, `System.Net`
- . Profil klienta NET4 – >`System.Net`
- Silverlight 3 – >`System.Json`
- WindowsPhone -> `Microsoft.Devices.Sensors`
