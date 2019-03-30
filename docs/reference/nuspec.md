---
title: Odkaz na soubor souboru .nuspec pro NuGet
description: Souboru .nuspec soubor obsahuje metadata balíčků používat při vytváření balíčku a zadejte informace pro spotřebitele balíčku.
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 21678cc36fd9bf1ed49143bee3f35208640fc8a7
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637646"
---
# <a name="nuspec-reference"></a>odkaz na souboru .nuspec

A `.nuspec` je soubor manifestu XML, který obsahuje metadata balíčků. Tento manifest slouží k vytvoření balíčku a zadejte informace pro uživatele. Manifest je vždy součástí balíčku.

V tomto tématu:

- [Obecný tvar a schématu](#general-form-and-schema)
- [Nahrazení tokeny](#replacement-tokens) (při použití s projektu sady Visual Studio)
- [Závislosti](#dependencies)
- [Odkazy na explicitní sestavení](#explicit-assembly-references)
- [Odkazy na sestavení rozhraní](#framework-assembly-references)
- [Včetně souborů sestavení](#including-assembly-files)
- [Včetně souborů obsahu](#including-content-files)
- [Příklad souboru nuspec soubory](#example-nuspec-files)

## <a name="general-form-and-schema"></a>Obecný tvar a schématu

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

Vizuální znázornění schématu, otevřete soubor schématu v sadě Visual Studio v režimu návrhu a klikněte **Průzkumníka schémat XML** odkaz. Alternativně otevřete soubor jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **zobrazení Průzkumníka schémat XML**. V obou případech, které získáte zobrazení jako na následující (v rozbaleném většinou):

![Visual Studio Průzkumníka schémat s nuspec.xsd otevřít](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Prvky požadovaná metadata

I když tyto prvky jsou minimální požadavky pro balíček, měli byste zvážit přidání [volitelná metadata prvky](#optional-metadata-elements) zlepšit celkové prostředí mají vývojáři součástí vašeho balíčku. 

Tyto prvky musí být uvedena v rámci `<metadata>` elementu.

#### <a name="id"></a>id 
Identifikátor balíčku velká a malá písmena, která musí být jedinečný v rámci nuget.org nebo cokoli jiného balíčku se nachází v galerii. ID nemůže obsahovat mezery nebo znaky, které nejsou platné pro adresu URL a obvykle postupují podle pravidla oboru názvů .NET. Zobrazit [výběr balíčku jedinečný identifikátor](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) pokyny.
#### <a name="version"></a>verze
Verze balíčku, následující *hlavníverze.podverze.oprava* vzor. Čísla verzí může obsahovat příponu předběžné verze, jak je popsáno v [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions). 
#### <a name="description"></a>description
Dlouhý popis balíčku zobrazí v uživatelském rozhraní. 
#### <a name="authors"></a>Autoři
Čárkou oddělený seznam autorů balíčků, odpovídající názvy profilů na nuget.org. Tyto jsou zobrazeny v galerii NuGet na nuget.org a slouží k křížový odkaz balíčky stejné autory. 

### <a name="optional-metadata-elements"></a>Volitelná metadata elementy

#### <a name="title"></a>název
Lidské popisný název balíčku, obvykle používaných v uživatelském rozhraní na webech nuget.org a Správce balíčků v sadě Visual Studio. Pokud není zadán, použije se ID balíčku. 
#### <a name="owners"></a>Vlastníci
Čárkou oddělený seznam Tvůrce balíčku pomocí názvy profilů na nuget.org. To je často seznamu stejné jako v `authors`a je ignorován při nahrávání balíčku do nuget.org. Zobrazit [vlastníky Správa balíčků na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). 
#### <a name="projecturl"></a>projectUrl
Adresa URL domovské stránky balíčku, často zobrazuje v uživatelském rozhraní nuget.org. 
#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl je zastaralé. Místo toho použijte licenci.

Adresa URL licence balíčku, často zobrazuje v uživatelském rozhraní nuget.org.
#### <a name="license"></a>Licence
Výraz SPDX licence nebo cesta k souboru licencí v rámci balíčku, často zobrazuje v uživatelském rozhraní nuget.org. V případě, že licencujete balíčku v rámci běžných licence, jako je například BSD-2klauzule nebo MIT, použijte přidružený identifikátor SPDX licence.<br>Příklad: `<license type="expression">MIT</license>`

Tady je úplný seznam [SPDX licence identifikátory](https://spdx.org/licenses/). NuGet.org přijímá pouze OSI nebo licenci FSF schválení licence při použití výrazu typu.

Pokud váš balíček je licencován několik běžných licence, můžete zadat složené licencí pomocí [SPDX výraz syntaxe verze 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).<br>Příklad: `<license type="expression">BSD-2-Clause OR MIT</license>`

Pokud používáte licenci, která ještě není přiřazený identifikátor SPDX, nebo vlastní licenci, můžete zabalit do souboru (pouze `.txt` nebo `.md`) s textem licence. Příklad:
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

Ekvivalent MSBuild, podívejte se na [balení výrazu licence nebo licenční soubor](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

Syntaxe výrazů licence NuGet je popsaný dole v [ABNF](https://tools.ietf.org/html/rfc5234).
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
Adresa URL pro bitovou kopii 64 x 64 s průhlednost pozadí použít jako ikona pro balíček zobrazená v uživatelském rozhraní. Ujistěte se, obsahuje tento element *přímá adresa URL obrázku* nikoli adresa URL webové stránky, který obsahuje bitovou kopii. Například pokud chcete použít některou image z Githubu, použijte soubor raw, jako je adresa URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>. 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence balíčku před instalací balíčku.
#### <a name="developmentdependency"></a>DevelopmentDependency
*(2.8+)* Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků. S PackageReference (NuGet 4.8 +) tento příznak také znamená, že vyloučí kompilace prostředků z kompilace. Zobrazit [DevelopmentDependency podporu pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)
#### <a name="summary"></a>souhrn
Krátký popis balíčku zobrazí v uživatelském rozhraní. Pokud tento parametr vynechán, zkrácená verze `description` se používá.
#### <a name="releasenotes"></a>ReleaseNotes
*(1.5+)* Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.
#### <a name="copyright"></a>Copyright
*(1.5+)* Copyright podrobnosti balíčku.
#### <a name="language"></a>jazyk
ID národního prostředí pro balíček. Zobrazit [vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).
#### <a name="tags"></a>značky
Mezerami oddělený seznam značek a klíčových slov, které popisují balíček a podpora zjistitelnost balíčků prostřednictvím vyhledávání a filtrování. 
#### <a name="serviceable"></a>možnost změny 
*(3.3+)* Pouze pro interní NuGet použít.
#### <a name="repository"></a>úložiště
Metadata úložiště, skládající se z čtyři volitelné atributy: *typ* a *url* *(4.0 +)*, a *větev* a  *potvrzení* *(4.6 +)*. Tyto atributy umožňují namapovat .nupkg do úložiště, který sestavilo, má potenciál, chcete-li získat podrobné jako jednotlivé větev nebo potvrzení změn, které sestaven balíček. To by měl být veřejně dostupnou adresu url, který lze vyvolat přímo pomocí softwaru pro řízení verzí. Neměl by být stránku html jako ten je určený pro počítače. Pro odkazování na stránku projektu, použijte `projectUrl` pole, místo toho.

#### <a name="minclientversion"></a>minClientVersion
Určuje minimální verzi klienta NuGet, který můžete nainstalovat tento balíček, vynucuje nuget.exe a Správce balíčků sady Visual Studio. Používá se pokaždé, když se balíček závisí na konkrétních funkcí služby `.nuspec` souborů, které byly přidány v konkrétní verzi klienta NuGet. Třeba balíček pomocí `developmentDependency` atribut by měl určovat "2.8" pro `minClientVersion`. Obdobně balíček pomocí `contentFiles` – element (viz další části) by měl nastavit `minClientVersion` na "3.3". Upozorňujeme také, že klienti NuGet před 2.5 nedokáže rozpoznat tento příznak jsou *vždy* odmítnout instalace balíčku bez ohledu na to, co `minClientVersion` obsahuje.

#### <a name="collection-elements"></a>Elementy v kolekci

#### <a name="packagetypes"></a>packageTypes
*(3.5 +)*  Kolekce nula nebo více `<packageType>` elementy typu balíčku Pokud než tradiční závislost balíčku. Každý packageType má atributy *název* a *verze*. Zobrazit [nastavení typ balíčku](../create-packages/creating-a-package.md#setting-a-package-type).
#### <a name="dependencies"></a>závislosti
Kolekce nula nebo více `<dependency>` prvky určení závislostí pro balíček. Každá závislost má atributy *id*, *verze*, *zahrnují* (3.x+), a *vyloučit* (3.x+). Zobrazit [závislosti](#dependencies-element) níže.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2 +)*  Kolekce nula nebo více `<frameworkAssembly>` prvků identifikace odkazy na sestavení rozhraní .NET Framework, které vyžaduje tento balíček, které zajišťuje, že jsou přidány odkazy na projekty využívající balíček. Má každý frameworkAssembly *assemblyName* a *targetFramework* atributy. Zobrazit [zadání framework sestavení odkazuje na globální mezipaměti](#specifying-framework-assembly-references-gac) níže. |
#### <a name="references"></a>odkazy
*(1.5 +)*  Kolekce nula nebo více `<reference>` prvky názvy sestavení v balíčku `lib` složku, která jsou přidány jako odkazy na projekt. Každý odkaz má *souboru* atribut. `<references>` může také obsahovat `<group>` element s *targetFramework* atribut, pak obsahující `<reference>` elementy. Pokud tento parametr vynechán, všechny odkazy v `lib` jsou zahrnuty. Zobrazit [odkazy na sestavení explicitní určení](#specifying-explicit-assembly-references) níže.
#### <a name="contentfiles"></a>contentFiles
*(3.3 +)*  Kolekce `<files>` prvky, které identifikují soubory obsahu, které mají být zahrnuty náročné projektu. Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů. Zobrazit [určující soubory, které chcete zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.
#### <a name="files"></a>soubory  
`<package>` Uzel může obsahovat `<files>` uzel na stejné úrovni k `<metadata>`a `<contentFiles>` dítě `<metadata>`, určete, jaké soubory sestavení a obsah zahrnout do balíčku. Zobrazit [včetně souborů sestavení](#including-assembly-files) a [včetně soubory obsahu](#including-content-files) dále v tomto tématu podrobnosti.

## <a name="replacement-tokens"></a>Nahrazování tokenů

Při vytváření balíčku, [ `nuget pack` příkaz](../tools/cli-ref-pack.md) nahradí $oddělených tokenů v `.nuspec` souboru `<metadata>` uzlu s hodnotami, které pocházejí ze souboru projektu nebo `pack` příkazu `-properties`přepínat.

Na příkazovém řádku zadáte hodnoty tokenu s `nuget pack -properties <name>=<value>;<name>=<value>`. Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a zadejte hodnoty v následujícím způsobem balení čas:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Chcete-li hodnoty z projektu, zadat tokenů popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` například `AssemblyInfo.cs` nebo `AssemblyInfo.vb`).

Pokud chcete použít tyto tokeny, spusťte `nuget pack` do souboru projektu namísto pouze `.nuspec`. Například, když pomocí následujícího příkazu `$id$` a `$version$` tokeny v `.nuspec` souboru jsou nahrazeny projektu `AssemblyName` a `AssemblyVersion` hodnoty:

```ps
nuget pack MyProject.csproj
```

Obvykle, když máte projekt, vytvoříte `.nuspec` zpočátku pomocí `nuget spec MyProject.csproj` což automaticky zahrnuje některé z těchto standardních tokenů. Nicméně, pokud projekt neobsahuje hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` selže. Navíc pokud můžete změnit hodnoty projektu, je nutné znovu sestavit před vytvořením balíčku. To můžete udělat jednoduše pomocí příkazu pack `build` přepnout.

S výjimkou produktů `$configuration$`, jsou hodnoty v projektu použít preferenci pro libovolné přiřazen stejný token v příkazovém řádku.

| Podpisový | Hodnota zdroje | Hodnota
| --- | --- | ---
| **$id$** | soubor projektu | AssemblyName (název) ze souboru projektu |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion, pokud jsou k dispozici, jinak AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Sestavení knihovny DLL | Konfigurace použitý k vytvoření sestavení, jako výchozí se použije k ladění. Všimněte si, že pokud chcete vytvořit balíček pomocí konfiguraci vydané verze, vždy používáte `-properties Configuration=Release` na příkazovém řádku. |

Tokeny je také možné přeložit cesty, jakmile zahrnete [soubory sestavení](#including-assembly-files) a [obsah souborů](#including-content-files). Tokeny mají stejné názvy jako vlastnosti nástroje MSBuild, což umožňuje vyberte soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení. Například, pokud použijete následující klíčová slova v `.nuspec` souboru:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

A vytvoření sestavení jehož `AssemblyName` je `LoggingLibrary` s `Release` konfigurace v nástroji MSBuild, výsledný vstupující `.nuspec` souborů v balíčku je následujícím způsobem:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Dependencies – element

`<dependencies>` Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvky, které určují další balíčky, na kterých závisí balíček nejvyšší úrovně. Atributy pro každý `<dependency>` jsou následující:

| Atribut | Popis |
| --- | --- |
| `id` | (Povinné) Ukazuje, na stránce balíček pro ID balíčku závislosti, jako je například "EntityFramework" a "NUnit", což je název balíčku nuget.org. |
| `version` | (Povinné) Rozsah verzí přijatelné jako závislost. Zobrazit [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) přesnou syntaxi. |
| include | Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti, které mají být zahrnuty do koncového balíčku. Výchozí hodnota je `all`. |
| exclude | Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti pro vyloučení ve finálním balíčku. Výchozí hodnota je `build,analyzers` může být přepsání. Ale `content/ ContentFiles` nevylučují se také implicitně ve finálním balíčku, který nelze přepsání. Značky s `exclude` přednost zadaným `include`. Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`. |

| Zahrnutí a vyloučení značek | Ovlivněné složky cíle |
| --- | --- |
| contentFiles | Obsah |
| modul runtime | Modul runtime, prostředky a FrameworkAssemblies |
| Kompilace | lib |
| sestavení | sestavení (cíle a vlastnosti nástroje MSBuild) |
| nativní | nativní |
| žádná | Žádné složky |
| všechny | Všechny složky |

Například následující řádky signalizovat závislosti na `PackageA` verze 1.1.0 nebo vyšší, a `PackageB` verzi 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Následující řádky označují závislostí na stejné balíčky, ale zadané k vložení `contentFiles` a `build` složky `PackageA` a všechno, co ale `native` a `compile` složky `PackageB`"

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`, závislosti, které existují v tomto projektu jsou automaticky obsažené ve výsledné `.nuspec` souboru.

### <a name="dependency-groups"></a>Závislostí skupin

*Verze 2.0 +*

Jako alternativu k jednomu seznamu bez stromové struktury, se dá nastavit závislosti podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<dependencies>`.

Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<dependency>` elementy. Tyto závislosti jsou nainstalovány společně, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.

`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam závislostí. Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.

> [!Important]
> Formát skupiny nelze smíšeného s nestrukturovaného seznamu.

Následující příklad ukazuje různé varianty `<group>` element:

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

`<references>` Prvek explicitně určuje sestavení, které by měly odkazovat na cílový projekt, při použití balíčku. Pokud tento prvek je k dispozici, NuGet přidat odkazy pouze na uvedené sestavení; nepřidá odkazy pro jiná sestavení v balíčku `lib` složky.

Například následující `<references>` element dává pokyn NuGet pro přidání odkazů na pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že existují další sestavení v balíčku:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Explicitní odkazy se obvykle používají pro pouze na sestavení doby návrhu. Při použití [kontrakty kódu](/dotnet/framework/debug-trace-profile/code-contracts), například sestavení kontraktu musí být vedle sestavení modulu runtime, které se rozšiřují, aby Visual Studio můžete najít, ale kontrakt sestavení nemusí být odkazuje projekt nebo zkopírovat do projektu `bin` složky.

Podobně je možné explicitní odkazy pro rozhraní pro testování částí, jako jsou XUnit, která potřebuje jeho nástroje pro sestavení vedle sestavení modulu runtime, ale nemá potřebovat, který je zahrnutý jako odkazy na projekt.

### <a name="reference-groups"></a>Referenční skupiny

Jako alternativu k jednomu plochého seznamu lze upravit odkazy podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<references>`.

Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<reference>` elementy. Tyto odkazy jsou přidány do projektu, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.

`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznamu odkazů. Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.

> [!Important]
> Formát skupiny nelze smíšeného s nestrukturovaného seznamu.

Následující příklad ukazuje různé varianty `<group>` element:

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

## <a name="framework-assembly-references"></a>Odkazy na sestavení rozhraní

Sestavení rozhraní jsou ty, které jsou součástí rozhraní .NET framework a by už měla být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač. Určením těchto sestavení v rámci `<frameworkAssemblies>` elementu balíčku můžete zajistit, že požadované odkazy jsou přidány do projektu, v případě, že projekt již nemá tyto odkazy. Takové sestavení, samozřejmě, nejsou obsažené v balíčku přímo.

`<frameworkAssemblies>` Prvek obsahuje nula nebo více `<frameworkAssembly>` prvky, z nichž každý určuje následující atributy:

| Atribut | Popis |
| --- | --- |
| **assemblyName** | (Povinné) Plně kvalifikovaný název. |
| **targetFramework** | (Volitelné) Určuje cílovou architekturu, pro který platí tento odkaz. Pokud tento parametr vynechán, označuje, že odkaz použije pro všechny platformy. Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework. |

Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové platformy a odkaz na `System.ServiceModel` pro pouze rozhraní .NET Framework 4.0:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Včetně souborů sestavení

Pokud budete postupovat podle konvence je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md), není potřeba explicitně zadat seznam souborů v `.nuspec` souboru. `nuget pack` Příkaz automaticky převezme potřebné soubory.

> [!Important]
> Při instalaci do projektu balíček NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* ty, které jsou pojmenovány `.resources.dll` vzhledem k tomu, že se budou považovat za lokalizovaná satelitní sestavení. Z tohoto důvodu se vyhněte se použití `.resources.dll` pro soubory, které jinak obsahují základní balíček kódu.

Toto automatické chování obejít a explicitně kontrolovat soubory, které jsou obsažené v balíčku, umístěte `<files>` jako podřízený element `<package>` (a na stejné úrovni `<metadata>`), identifikuje každý soubor se samostatným `<file>` element. Příklad:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Nuget 2.x a dřívějších verzí a projekty pomocí `packages.config`, `<files>` element slouží také k neměnné obsahu soubory k zahrnutí při instalaci balíčku. S NuGet 3.3 + i na PackageReference `<contentFiles>` elementu je použita. Zobrazit [včetně soubory obsahu](#including-content-files) níže podrobnosti.

### <a name="file-element-attributes"></a>Atributy souboru

Každý `<file>` prvek určuje následující atributy:

| Atribut | Popis |
| --- | --- |
| **src** | Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut. Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu. Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky. |
| **target** | Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které musí začínat `lib`, `content`, `build`, nebo `tools`. Zobrazit [vytváření souboru .nuspec z pracovního adresáře podle úmluvy](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **Vyloučení** | Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění. Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky. |

### <a name="examples"></a>Příklady

**Jediné sestavení**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Jediné sestavení specifická pro rozhraní .NET framework**

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

**Knihovny DLL pro různá rozhraní**

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

## <a name="including-content-files"></a>Včetně souborů obsahu

Soubory obsahu jsou neměnné soubory, které je potřeba zahrnout do projektu balíček. Je neměnný, nejsou určeny k používání projektu změnit. Příklad obsahu souborů patří:

- Bitové kopie, které jsou vloženy jako prostředky
- Zdrojové soubory, které jsou již kompilován
- Skripty, které musí být součástí výstupu sestavení projektu
- Konfigurační soubory pro balíček, který mají být zahrnuti do projektu, ale není třeba žádné změny specifické pro projekt

Obsahu souborů jsou součástí balíčku pomocí `<files>` elementu, určení `content` složky `target` atribut. Ale tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který používá místo toho `<contentFiles>` elementu.

Balíček pro maximální kompatibility s využívání projektů v ideálním případě Určuje soubory obsahu v obou elementech.

### <a name="using-the-files-element-for-content-files"></a>Pomocí elementu souborů pro soubory obsahu

Pro soubory obsahu, stačí použít stejný formát jako soubory sestavení, ale zadat `content` jako základní složka v `target` atributu, jak je znázorněno v následujícím příkladu.

**Soubory základního obsahu**

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

**Soubor s obsahem specifické pro cílové prostředí**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Zkopírovat do složky s tečkou v názvu souboru obsahu**

V takovém případě se zobrazí NuGet, který rozšíření v `target` se neshoduje s příponou v `src` a proto zpracovává tuto část názvu v `target` jako složka:

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

**Soubory obsahu se hloubkové cesty a hloubkové cílem**

V takovém případě protože přípony zdrojovou a cílovou odpovídají, NuGet předpokládá, že cíl je název souboru a nikoliv složka:

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

### <a name="using-the-contentfiles-element-for-content-files"></a>Pomocí elementu contentFiles pro soubory obsahu

*NuGet 4.0 + s PackageReference*

Ve výchozím nastavení, umístí balíček obsahu `contentFiles` složky (viz níže) a `nuget pack` zahrnuty všechny soubory ve složce pomocí výchozí atributy. V tomto případě není nutné zahrnout `contentFiles` uzlu `.nuspec` vůbec.

K řízení souborů, které jsou zahrnuty `<contentFiles>` prvek určuje je kolekce `<files>` mezi prvky, které identifikují přesné soubory patří.

Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů:

| Atribut | Popis |
| --- | --- |
| **include** | (Povinné) Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut. Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu. Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky. |
| **Vyloučení** | Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění. Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky. |
| **buildAction** | Akce sestavení zařadit do obsahu položky nástroje MSBuild, jako například `Content`, `None`, `Embedded Resource`, `Compile`atd. Výchozí hodnota je `Compile`. |
| **copyToOutput** | Logická hodnota označující, jestli se má kopírovat položky obsahu pro sestavení (nebo publikovat) výstupní složka. Výchozí hodnota je false. |
| **Sloučit** | Logická hodnota označující, zda se můžete kopírovat položky obsahu na jedinou složku ve výstupu sestavení (pravda), nebo zachovat strukturu složek v balíčku (false). Tento příznak funguje pouze v případě copyToOutput příznak je nastaven na hodnotu true. Výchozí hodnota je false. |

Při instalaci balíčku NuGet platí podřízených elementů `<contentFiles>` shora dolů. Pokud se shodují na stejný soubor několik záznamů se použijí všechny položky. Položky navrchu přepíše nižší položky dojde ke konfliktu pro stejný atribut.

#### <a name="package-folder-structure"></a>Struktura složky balíčku

Projekt balíčku strukturovat obsahu pomocí následujícímu vzoru:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` může být `cs`, `vb`, `fs`, `any`, nebo malým ekvivalentem znaku danou `$(ProjectLanguage)`
- `TxM` je všechny moniker právní cílového rozhraní, která podporuje NuGet (viz [platforem](../reference/target-frameworks.md)).
- Složky libovolné struktury složek může připojen na konec této syntaxe.

Příklad:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Můžete použít prázdné složky `.` chcete vyjádřit výslovný nesouhlas poskytnutí obsahu pro určité kombinace jazyka a TxM, například:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Vzorový oddíl contentFiles

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

## <a name="example-nuspec-files"></a>Příklad souboru nuspec soubory

**Jednoduchý `.nuspec` , která neurčuje závislosti nebo souborů**

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

**A `.nuspec` se sestaveními rozhraní framework**

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

V tomto příkladu tímto se nainstalují pro konkrétní projekt cílí:

- .NET4 -> `System.Web`, `System.Net`
- . NET4 -> Client Profile `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
