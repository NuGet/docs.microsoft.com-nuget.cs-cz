---
title: "Odkaz na soubor příponou .nuspec pro NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d4a4db9b-5c2d-46aa-9107-d2b01733df7c
description: "Soubor s příponou .nuspec obsahuje metadata balíčků použít při vytváření balíčku a poskytnout informace k příjemce balíčku."
keywords: "odkaz na soubor nuspec, metadata balíčků NuGet, manifest balíčku NuGet, nuspec schématu"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: b8c286b9a5705526e2e8fcf259c6503d48e5d181
ms.sourcegitcommit: d576d84fb4b6a178eb2ac11f55deb08ac771ba1c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2018
---
# <a name="nuspec-reference"></a>referenční dokumentace příponou .nuspec

A `.nuspec` je soubor manifestu XML, který obsahuje metadata balíčků. Tento manifest se používá k vytvoření balíčku a zadejte informace k příjemce. Manifest je vždy součástí balíčku.

V tomto tématu:

- [Obecné formuláře a schématu](#general-form-and-schema)
- [Nahrazení tokeny](#replacement-tokens) (při použití s projekt sady Visual Studio)
- [Závislosti](#dependencies)
- [Odkazy na explicitní sestavení](#explicit-assembly-references)
- [Odkazy na sestavení Framework](#framework-assembly-references)
- [Včetně souborů sestavení](#including-assembly-files)
- [Včetně souborů obsahu](#including-content-files)
- [Příklady](#examples)

## <a name="general-form-and-schema"></a>Obecné formuláře a schématu

Aktuální `nuspec.xsd` soubor schématu najdete v [úložiště NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

V tomto schématu `.nuspec` soubor má následující Obecné formuláře:

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

Pro zřetelné vizuální reprezentace schématu, otevřete soubor schématu v sadě Visual Studio v režimu návrhu a klikněte na **Explorer schématu XML** odkaz. Můžete také otevřít soubor jako kód, klikněte pravým tlačítkem myši v editoru a vyberte **zobrazit Explorer schématu XML**. V obou případech, které získáte zobrazení stejný, jako je pod (většinou rozšířit):

![Schéma Průzkumníka Visual Studio s nuspec.xsd otevřít](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>Atributy metadat

`<metadata>` Element podporuje atributy popsané v následující tabulce.

| Atribut | Požadováno | Popis |
| --- | --- | --- | 
| **minClientVersion** | Ne | *(2.5 +)*  Určuje minimální verzi klienta NuGet, který můžete nainstalovat tento balíček vynucováno nuget.exe a Správce balíčků Visual Studio. Používá se vždy, když balíček závisí na specifické funkce `.nuspec` souborů, které byly přidány v konkrétní verzi klienta NuGet. Například balíčku pomocí `developmentDependency` atribut by měl určovat "2.8" pro `minClientVersion`. Podobně balíčku pomocí `contentFiles` (viz další část) musí nastavit element `minClientVersion` k "3.3". Poznámka: protože klienty NuGet před 2.5 nerozpoznávají tento příznak, budou *vždy* odmítnout k instalaci balíčku bez ohledu na to, co `minClientVersion` obsahuje. |

### <a name="required-metadata-elements"></a>Požadovaná metadata elementy

I když tyto prvky jsou minimální požadavky pro balíček, měli byste zvážit přidání [volitelná metadata elementy](#optional-metadata-elements) celkové lepší vývojáři mají spolu s balíčkem.

Tyto prvky musí být v rámci `<metadata>` elementu.

| Prvek | Popis |
| --- | --- |
| **id** | Identifikátor balíčku velká a malá písmena, která musí být jedinečný v rámci nuget.org nebo jiná balíčku se nachází v galerii. ID nesmí obsahovat mezery nebo znaky, které nejsou platné pro adresu URL a obecně podle oboru názvů pravidla technologie .NET. V tématu [výběr balíčku jedinečný identifikátor](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) pokyny. |
| **verze** | Verze balíčku, následující *major.minor.patch* vzor. Čísla verzí může zahrnovat příponu předběžné verze, jak je popsáno v [Správa verzí balíčku](../reference/package-versioning.md#pre-release-versions). |
| **Popis** | Dlouhý popis balíčku pro zobrazení uživatelského rozhraní. |
| **Autoři** | Seznam balíčků autoři, odpovídající profil názvy v nuget.org oddělených čárkami. Tyto jsou zobrazeny v galerii NuGet v nuget.org a jsou používané pro křížovou balíčky autory stejné. |

### <a name="optional-metadata-elements"></a>Volitelná metadata elementy

Může se zobrazit tyto prvky v rámci `<metadata>` elementu.

#### <a name="single-elements"></a>Jednotlivé prvky

| Prvek | Popis |
| --- | --- |
| **title** | Lidské popisný název balíčku, obvykle používaných v zobrazení uživatelského rozhraní na nuget.org a Správce balíčků v sadě Visual Studio. Pokud není zadaný, použije se ID balíčku. |
| **Vlastníci** | Seznam creators balíček pomocí profilu názvy v nuget.org oddělených čárkami. Tento problém je často seznamu stejné jako v `authors`a při odesílání balíčku pro nuget.org ignorováno. V tématu [Správa vlastníků balíčku na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). |
| **projectUrl** | Zobrazí adresu URL pro domovskou stránku balíčku, často se zobrazí v uživatelském rozhraní a také nuget.org. |
| **licenseUrl** | Adresa URL pro balíčku licenci, často se zobrazí v zobrazení uživatelského rozhraní, jakož i nuget.org. |
| **iconUrl** | Adresu URL pro bitovou kopii 64 x 64 s průhlednost pozadí chcete použít jako ikonu balíčku v zobrazení uživatelského rozhraní. Ujistěte se, obsahuje tento element *přímá adresa URL obrázku* nikoli adresa URL webové stránky, který obsahuje bitovou kopii. Například pokud chcete použít bitovou kopii z Githubu, použijte soubor raw, jako adresa URL `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`. |
| **requireLicenseAcceptance** | Logická hodnota určující, jestli klient musí zobrazovat výzvu k příjemce tak, aby přijímal licenční balíček před instalací balíčku. |
| **developmentDependency** | *(2.8 +)*  A logickou hodnotu určující, zda tento balíček je označit jako vývoj jen závislost, která zabraňuje balíček zahrnutí v závislosti na dalších balíčků. |
| **summary** | Stručný popis balíčku pro zobrazení uživatelského rozhraní. Pokud tento parametr vynechán, zkrácený verzi `description` se používá. |
| **releaseNotes** | *(1.5 +)*  Popis změn provedených v této verzi balíčku, často se používá v uživatelském rozhraní, jako **aktualizace** karta nástroje Visual Studio Správce balíčků místo Popis balíčku. |
| **copyright** | *(1.5 +)*  Copyright podrobnosti balíčku. |
| **jazyk** | ID národního prostředí pro daný balíček. V tématu [vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md). |
| **značky** | Mezerami oddělený seznam značek a klíčová slova, která popisují možnosti rozpoznání balíčku a podpory balíčků prostřednictvím vyhledávání a filtrování. |
| **možnost změny** | *(3.3 +)*  Pouze pro interní NuGet použít. |

#### <a name="collection-elements"></a>Elementy v kolekci

| Prvek | Popis |
| --- | --- |
**packageTypes** | *(3.5 +)*  Kolekce nula nebo více `<packageType>` elementy určení typu balíčku Pokud než tradiční závislost balíčku. Každý packageType má atributy *název* a *verze*. V tématu [nastavení typ balíčku](../create-packages/creating-a-package.md#setting-a-package-type). |
| **závislosti** | Kolekce nula nebo více `<dependency>` elementy určení závislostí pro balíček. Každá závislost má atributy *id*, *verze*, *zahrnují* (3.x+), a *vyloučit* (3.x+). V tématu [závislosti](#dependencies) níže. |
| **frameworkAssemblies** | *(1.2 +)*  Kolekce nula nebo více `<frameworkAssembly>` elementy identifikace odkazy na sestavení rozhraní .NET Framework, které tento balíček vyžaduje, což zajistí, že odkazy jsou přidány do projekty využívající balíčku. Má každý frameworkAssembly *assemblyName* a *targetFramework* atributy. V tématu [zadání sestavení rozhraní odkazuje GAC](#specifying-framework-assembly-references-gac) níže. |
| **odkazy** | *(1.5 +)*  Kolekce nula nebo více `<reference>` elementy pojmenování sestavení v balíčku `lib` složky, které jsou přidány jako odkazy na projekt. Má každý odkaz *souboru* atribut. `<references>`může také obsahovat `<group>` element s *targetFramework* atribut, který pak obsahuje `<reference>` elementy. Pokud tento parametr vynechán, všechny odkazy v `lib` jsou zahrnuty. V tématu [zadání odkazy na sestavení explicitní](#specifying-explicit-assembly-references) níže. |
| **contentFiles** | *(3.3 +)*  Kolekce `<files>` prvky, které identifikují soubory obsahu pro zahrnutí do projektu náročná. Tyto soubory jsou určeny sadu atributů, které popisují, jak mají být použity v rámci systému projektu. V tématu [určující soubory, které chcete zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže. |

### <a name="files-element"></a>Files – element

`<package>` Uzel může obsahovat `<files>` uzlu na stejnou úroveň jako `<metadata>`a nebo `<contentFiles>` dítěte mladšího `<metadata>`, určete, které soubory sestavení a obsah balíčku. V tématu [včetně souborů sestavení](#including-assembly-files) a [včetně soubory obsahu](#including-content-files) dál v tomto tématu podrobnosti.

## <a name="replacement-tokens"></a>Nahrazení tokenů

Při vytváření balíčku, [ `nuget pack` příkaz](../tools/cli-ref-pack.md) nahrazuje oddělený $ tokeny v `.nuspec` souboru `<metadata>` uzlu s hodnotami, které pocházejí z buď soubor projektu nebo `pack` příkazu `-properties`přepínače.

Na příkazovém řádku, zadejte hodnoty tokenu s `nuget pack -properties <name>=<value>;<name>=<value>`. Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a zadejte hodnoty v balení čas následujícím způsobem:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Chcete-li použít hodnoty z projektu, zadejte tokeny popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` například `AssemblyInfo.cs` nebo `AssemblyInfo.vb`).

Pokud chcete použít tyto tokeny, spusťte `nuget pack` do souboru projektu spíše než jenom `.nuspec`. Například když pomocí následujícího příkazu `$id$` a `$version$` tokeny v `.nuspec` soubor se nahradí projektu `AssemblyName` a `AssemblyVersion` hodnoty:

```ps
nuget pack MyProject.csproj
```

Obvykle, když máte projekt, můžete vytvořit `.nuspec` původně pomocí `nuget spec MyProject.csproj` který automaticky zahrnuje některé tyto standardní tokeny. Ale pokud projektu chybí hodnoty pro požadované `.nuspec` elementy, pak `nuget pack` selže. Kromě toho pokud změníte projektu hodnoty, je nutné znovu vytvořit před vytvořením balíčku. To lze provést pohodlně pomocí příkazu pack `build` přepínače.

S výjimkou produktů `$configuration$`, jsou všechny přiřazen stejný token na příkazovém řádku použít hodnoty v projektu.

| Token | Hodnota zdroje | Hodnota
| --- | --- | ---
| **$id$** | soubor projektu | AssemblyName ze souboru projektu |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion, pokud existuje, jinak hodnota AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Sestavení knihovny DLL | Konfigurace použitá k vytvoření sestavení, jako výchozí bude použit k ladění. Upozorňujeme, že pokud chcete vytvořit balíček pomocí konfigurace verze, můžete vždy použít `-properties Configuration=Release` na příkazovém řádku. |

Tokeny lze také vyřešit cesty, jakmile zahrnete [soubory sestavení](#including-assembly-files) a [obsahu souborů](#including-content-files). Tokeny mají stejné názvy jako vlastnosti nástroje MSBuild, což umožňuje vyberte soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení. Například, pokud používáte následující klíčová slova v `.nuspec` souboru:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

A vytváření sestavení jejichž `AssemblyName` je `LoggingLibrary` s `Release` konfigurace v nástroji MSBuild, výsledná řádků v `.nuspec` souboru v balíčku je následující:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>Závislosti

`<dependencies>` v rámci `<metadata>` obsahuje libovolný počet `<dependency>` elementy, které identifikují další balíčky, na kterých závisí balíček nejvyšší úrovně. Atributy pro každou `<dependency>` jsou následující:

| Atribut | Popis |
| --- | --- |
| `id` | (Povinné) ID balíčku závislosti, jako je například "EntityFramework" a "NUnit", což je název nuget.org balíčku se zobrazí na stránce balíček. |
| `version` | (Povinné) Rozsah verze přijatelné jako závislost. V tématu [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards) pro přesná syntaxe. |
| include | Čárkami oddělený seznam zahrnutí a vyloučení značky (viz níže), která určuje závislosti, které chcete zahrnout do konečné balíčku. Výchozí hodnota je `none`. |
| exclude | Čárkami oddělený seznam zahrnutí a vyloučení značky (viz níže), která určuje závislosti k vyloučení z poslední balíček. Výchozí hodnota je `all`. Značky s `exclude` mají přednost před uvedenými s `include`. Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`. |

| Zahrnutí a vyloučení značky | Ovlivněné složky cíle |
| --- | --- |
| contentFiles | Obsah  |
| modul runtime | Modul runtime, prostředky a FrameworkAssemblies  |
| compile | lib |
| sestavení | sestavení (MSBuild props a cíle) |
| nativní | nativní |
| žádná | Žádné složky |
| všechny | Všechny složky |

Například následující řádky označovat závislosti na `PackageA` verze 1.1.0 nebo vyšší, a `PackageB` verze 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Následující řádky znamenat závislostí na stejné balíčky, ale zadat zahrnout `contentFiles` a `build` složky `PackageA` a všechno ale `native` a `compile` složky `PackageB`"

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`, závislosti, které existují v tomto projektu jsou automaticky součástí výsledná `.nuspec` souboru.

### <a name="dependency-groups"></a>Závislost skupiny

*Verze 2.0 +*

Jako alternativu k jediný plochý seznam závislosti lze podle profil framework cílový projekt pomocí `<group>` elementů v rámci `<dependencies>`.

Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` elementy. Tyto závislosti jsou nainstalovány společně při cílovém Frameworku, který je kompatibilní s profilem framework projektu.

`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam závislosti. V tématu [cílové rozhraní](../schema/target-frameworks.md) pro identifikátory přesný framework.

> [!Important]
> Formát skupiny nelze smíšeného s jako plochý seznam.

Následující příklad ukazuje různých variant `<group>` element:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Odkazy na explicitní sestavení

`<references>` Element explicitně určuje ta sestavení, které cílový projekt by měl odkazovat při použití balíčku. Když se nachází tento element, NuGet přidáte odkazy na sestavení pouze uvedené; nepřidá odkazy pro všechny ostatní sestavení v balíčku `lib` složky.

Například následující `<references>` element dá pokyn NuGet, čímž přidáte odkazy na pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že existují další sestavení v balíčku:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Explicitní odkazy jsou obvykle používány pro návrh jen sestavení. Při použití [kontrakty kódu](/dotnet/framework/debug-trace-profile/code-contracts), například sestavení smlouvy musí být vedle sestavení modulu runtime, která budou posílení, aby Visual Studio můžete najít, ale sestavení kontrakt nemusí být odkazuje projektu nebo zkopírovat do projektu `bin` složky.

Podobně explicitní odkazy lze systémů testů jednotek, jako je například XUnit, který se musí jeho nástroje pro sestavení vedle sestavení za běhu, ale nemá potřebovat, je zahrnuta jako odkazy na projekt.

### <a name="reference-groups"></a>Odkazové skupiny

*Verze 2.5 +*

Jako alternativu k jediný plochý seznam odkazů na lze podle profil framework cílový projekt pomocí `<group>` elementů v rámci `<references>`.

Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nula nebo více `<reference>` elementy. Tyto odkazy se přidají do projektu, když cílovém Frameworku, který je kompatibilní s profilem framework projektu.

`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam odkazů. V tématu [cílové rozhraní](../schema/target-frameworks.md) pro identifikátory přesný framework.

> [!Important]
> Formát skupiny nelze smíšeného s jako plochý seznam.

Následující příklad ukazuje různých variant `<group>` element:

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

## <a name="framework-assembly-references"></a>Odkazy na sestavení Framework

Sestavení architektury jsou ty, které jsou součástí rozhraní .NET framework a by už měla být v globální mezipaměti sestavení (GAC) pro všechny daný počítač. Určením těchto sestavení v rámci `<frameworkAssemblies>` elementu balíček můžete zajistit, že požadované odkazy jsou přidány do projektu, v případě, že projekt již nemá tyto odkazy. Takové sestavení samozřejmě nejsou zahrnuty v balíčku přímo.

`<frameworkAssemblies>` Element obsahuje nula nebo více `<frameworkAssembly>` prvky, z nichž každý určuje následující atributy:

| Atribut | Popis |
| --- | --- |
| **assemblyName** | (Povinné) Plně kvalifikovaný název. |
| **targetFramework** | (Volitelné) Určuje cílový framework, pro kterou platí tento odkaz. Pokud tento parametr vynechán, označuje, že odkaz na použije pro všechna rozhraní. V tématu [cílové rozhraní](../schema/target-frameworks.md) pro identifikátory přesný framework. |

Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové architektury a odkaz na `System.ServiceModel` pro pouze rozhraní .NET Framework 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Včetně souborů sestavení

Pokud budete postupovat podle konvence popsané v [vytváření balíčku](../create-packages/creating-a-package.md), není nutné explicitně zadat seznam souborů v `.nuspec` souboru. `nuget pack` Příkaz automaticky převezme potřebné soubory.

> [!Important]
> Při instalaci balíčku do projektu NuGet automaticky přidá odkazy na sestavení pro knihovny DLL balíčku, *s výjimkou* ty, které jsou s názvem `.resources.dll` vzhledem k tomu, že se předpokládá, že lokalizované satelitní sestavení. Z tohoto důvodu vyhýbat se používání `.resources.dll` pro soubory, které jinak obsahují nezbytné balíček kódu.

Nepoužívat toto automatické chování a explicitně řídit soubory, které jsou součástí balíčku, umístit `<files>` jako podřízený element `<package>` (a na stejné úrovni jako `<metadata>`), identifikace každý soubor s samostatné `<file>` element. Příklad:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

U balíčku NuGet 2.x a starší a projektů pomocí `packages.config`, `<files>` element se používá i k zahrnují neměnné soubory obsahu při instalaci balíčku. S NuGet 3.3 + a projektů pomocí `project.json` pr PackageReference, `<contentFiles>` element se používá místo. V tématu [včetně soubory obsahu](#including-content-files) níže podrobnosti.

### <a name="file-element-attributes"></a>Element atributy souboru

Každý `<file>` element určuje následující atributy:

| Atribut | Popis |
| --- | --- |
| **src** | Umístění souboru nebo soubory, které chcete zahrnout, podstoupí vyloučení určeného `exclude` atribut. Cesta je vzhledem k `.nuspec` souboru uvedeno absolutní cesta. Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání. |
| **target** | Relativní cesta ke složce v rámci balíčku umístění zdrojových souborů, které musí začínat `lib`, `content`, `build`, nebo `tools`. V tématu [vytváření příponou .nuspec z pracovního adresáře založené na konvenci](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory). |
| **exclude** | Seznam oddělený středníkem souborů nebo vzorů souborů, které chcete vyloučit z `src` umístění. Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání. |

### <a name="examples"></a>Příklady

**Jednoho sestavení**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Jediné sestavení, které jsou specifické pro cílové prostředí**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Sada knihovny DLL pomocí zástupného znaku**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Knihovny DLL pro různé rozhraní**

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
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Včetně souborů obsahu

Soubory obsahu jsou neměnné soubory, které je potřeba zahrnout do projektu balíček. Se nedá změnit, nejsou určeny k využívání projektu upravit. Soubory obsahu příklad patří:

- Bitové kopie, které jsou vloženy jako prostředky
- Zdrojové soubory, které jsou již kompilovat
- Skripty, které musí být součástí výstupu sestavení projektu
- Konfigurační soubory pro balíček, který mají být zahrnuti v projektu, ale nemusí změny specifické pro projekt

Obsahu souborů jsou součástí balíčku pomocí `<files>` elementu, určení `content` složky v `target` atribut. Ale tyto soubory jsou při instalaci balíčku do projektu pomocí ignorovány `project.json` systém NuGet 3.3 + nebo PackageReference v NuGet 4 +, která místo toho používá `<contentFiles>` elementu.

Pro maximální kompatibility s využívání projekty balíček v ideálním případě Určuje soubory obsahu v obou elementů.

### <a name="using-the-files-element-for-content-files"></a>Pomocí elementu soubory souborů obsahu

Pro soubory obsahu, stačí použít stejný formát jako soubory sestavení, ale zadat `content` jako základní složka v `target` atribut podle následujících příkladů.

**Základní soubory obsahu**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Soubory obsahu s adresářovou strukturu**

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

**Obsah souboru, které jsou specifické pro cílové prostředí**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Zkopírován do složky s tečkou v názvu souboru obsahu**

V takovém případě který NuGet uvidí rozšíření v `target` se neshoduje s příponou v `src` a proto považuje část názvu v `target` jako složku:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Soubory obsahu bez přípony**

Chcete-li zahrnout soubory bez přípony, použijte `*` nebo `**` zástupné znaky:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Soubory obsahu s hloubkovým cestou a hloubkového cíl**

V takovém případě protože přípony souborů zdrojové a cílové shodují, NuGet předpokládá, že cíl je název souboru a nikoliv složka:

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

### <a name="using-the-contentfiles-element-for-content-files"></a>Pomocí elementu contentFiles souborů obsahu

*Verze 3.3 + s project.json a 4.0 + s PackageReference*

Výchozí umístění obsahu v balíčku `contentFiles` složky (viz níže) a `nuget pack` zahrnuty všechny soubory v této složce pomocí výchozí atributy. V takovém případě není nutné zahrnovat `contentFiles` uzlu `.nuspec` vůbec.

K řízení, které soubory jsou zahrnuty `<contentFiles>` element určuje je kolekce `<files>` prvky, které identifikují přesný soubory patří.

Tyto soubory jsou určeny sadu atributů, které popisují, jak mají být použity v rámci systému projektu:

| Atribut | Popis |
| --- | --- |
| **Zahrnout** | (Povinné) Umístění souboru nebo soubory, které chcete zahrnout, podstoupí vyloučení určeného `exclude` atribut. Cesta je vzhledem k `.nuspec` souboru uvedeno absolutní cesta. Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání. |
| **exclude** | Seznam oddělený středníkem souborů nebo vzorů souborů, které chcete vyloučit z `src` umístění. Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání. |
| **buildAction** | Akce sestavení přiřadit položku obsahu pro MSBuild, jako například `Content`, `None`, `Embedded Resource`, `Compile`atd. Výchozí hodnota je `Compile`. |
| **copyToOutput** | Logická hodnota, která určuje, zda zkopírovat položky obsahu do výstupní složky sestavení. Výchozí hodnota je false. |
| **flatten** | Logická hodnota, která určuje, jestli kopírování obsahu položky do jediné složky ve výstupu sestavení (true) nebo chcete zachovat struktura složek v balíčku (false). Tento příznak pouze funguje, když je příznak copyToOutput nastaven na hodnotu true. Výchozí hodnota je false. |

Při instalaci balíčku, NuGet platí podřízených elementů `<contentFiles>` shora dolů. Pokud stejný soubor shodovat s více položek se použijí všechny položky. Položka nejvyšší přepíše nižší položky, pokud dojde ke konfliktu pro stejný atribut.

#### <a name="package-folder-structure"></a>Struktura složek balíčku

Balíček projekt by měl struktury obsah pomocí následujícího vzorce:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages`může být `cs`, `vb`, `fs`, `any`, nebo malá ekvivalent danou`$(ProjectLanguage)`
- `TxM`je všechny Přezdívka právní cílový framework, který NuGet podporuje (viz [cílové rozhraní](../schema/target-frameworks.md)).
- Libovolné struktury složek může připojen na konec této syntaxe.

Příklad:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Můžete použít prázdné složky `.` pro vyjádření výslovného nesouhlasu poskytování obsahu pro určité kombinace jazyka a TxM, například:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Příklad contentFiles části

```xml
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
```

## <a name="example-nuspec-files"></a>Příklad příponou .nuspec soubory

**Jednoduchý `.nuspec` která neurčuje závislosti nebo soubory**

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
    <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
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

**A `.nuspec` s framework sestavení**

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

V tomto příkladu následující se nainstalují pro konkrétní projekt cíle:

- .NET4 -> `System.Web`, `System.Net`
- . NET4 -> Client Profile`System.Net`
- -> Silverlight 3`System.Json`
- Silverlight 4 ->`System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
