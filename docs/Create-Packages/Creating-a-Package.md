---
title: Postup vytvoření balíčku NuGet
description: Podrobný průvodce do procesu návrhu a vytvoření balíčku NuGet, včetně klíče rozhodovací body, jako jsou soubory a správu verzí.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: c1e3bfd1c7e80c7deb505ef732d73c2edf3e32f7
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/27/2018
---
# <a name="creating-nuget-packages"></a>Vytváření balíčků NuGet

Bez ohledu na jaké vašeho balíčku nebo co code je obsahuje, můžete použít `nuget.exe` do balíčku, které tuto funkci do komponenty, které je možné sdílet s a používat libovolný počet dalších vývojáři. Chcete-li nainstalovat `nuget.exe`, najdete v části [nainstalovat rozhraní příkazového řádku NuGet](../install-nuget-client-tools.md#nugetexe-cli). Všimněte si, že Visual Studio automaticky nezahrnuje `nuget.exe`.

Technicky platí, že balíček NuGet je právě soubor ZIP, který byl přejmenován s `.nupkg` rozšíření, jejichž obsah odpovídají určité konvence. Toto téma popisuje podrobný proces vytvoření balíčku, který splňuje tyto konvence. Podrobný návod, najdete v části [rychlý start: vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package.md).

Balení začíná zkompilovaný kód (sestavení), symboly a další soubory, které chcete doručit jako balíček (viz [přehled a pracovní postup](overview-and-workflow.md)). Tento proces je nezávislá kompilování nebo jinak generování souborů, které patří do balíčku, i když můžete navrhnout z informací v souboru projektu pro synchronizaci kompilované sestavení a balíčky.

> [!Note]
> Toto téma se vztahuje na typy projektů než projektů .NET Core pomocí Visual Studio 2017 a NuGet 4.0 +. V těchto projektech .NET Core NuGet používá informace v souboru projektu přímo. Podrobnosti najdete v tématu [vytvořit .NET standardní balíčky s Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) a [NuGet pack a obnovit jako cíle MSBuild](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Rozhodnutí, která sestavení do balíčku

Většina pro obecné účely balíčky obsahují jeden nebo více sestavení, které ostatní vývojáři mohou použít ve svých vlastních projektů.

- Obecně platí je nejlepší mít jedno sestavení na balíček NuGet předpokladu, že každé sestavení je nezávisle užitečné. Pokud máte například `Utilities.dll` , závisí na `Parser.dll`, a `Parser.dll` je užitečné sama o sobě, a pak vytvořte jeden balíček pro každý. Díky tomu mohou vývojáři použít `Parser.dll` nezávisle na `Utilities.dll`.

- Pokud vaše knihovna se skládá z více sestavení, které nejsou nezávisle užitečné, je vhodná pro jejich zkombinovat do jednoho balíčku. Použijeme předchozí příklad, pokud `Parser.dll` obsahuje kód, který se používá pouze systémem `Utilities.dll`, pak je v pořádku zachovat `Parser.dll` ve stejném balíčku.

- Podobně pokud `Utilities.dll` závisí na `Utilities.resources.dll`, je-li znovu tento není užitečné sama o sobě, pak přesuňte i ve stejném balíčku.

Prostředky jsou ve skutečnosti ve speciálním případě. Při instalaci balíčku do projektu NuGet automaticky přidá odkazy na sestavení pro knihovny DLL balíčku, *s výjimkou* ty, které jsou s názvem `.resources.dll` vzhledem k tomu, že se předpokládá, že lokalizované satelitní sestavení (viz [ Vytvoření lokalizovaných balíčků](creating-localized-packages.md)). Z tohoto důvodu vyhýbat se používání `.resources.dll` pro soubory, které jinak obsahují nezbytné balíček kódu.

Pokud vaše knihovna obsahuje sestavení zprostředkovatele komunikace s objekty COM, postupujte podle dalších pokynů v [vytváření balíčků s sestavení vzájemné spolupráce COM](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Role a struktura souboru s příponou .nuspec

Jakmile již víte, jaké soubory, které chcete balíček a dalším krokem je vytvoření manifestu balíčku v `.nuspec` souboru XML.

V manifestu:

1. Popisuje obsah balíčku a je sám součástí balíčku.
1. Jednotky vytvoření balíčku a dá pokyn NuGet k instalaci balíčku do projektu. Například manifest identifikuje další závislosti balíčků tak, aby NuGet můžete také nainstalovat těchto závislostí při instalaci hlavní balíčku.
1. Požadované a volitelné vlastnosti obsahuje, jak je popsáno níže. Přesné podrobnosti, včetně dalších vlastností, zde nejsou uvedeny najdete v tématu [příponou .nuspec odkaz](../reference/nuspec.md).

Požadované vlastnosti:

- Identifikátor balíčku, který musí být jedinečný v rámci galerie, který je hostitelem balíčku.
- Konkrétní verzi číslo ve tvaru *Major.Minor.Patch [-přípona]* kde *-přípona* identifikuje [předprodejní verze](prerelease-packages.md)
- Název balíčku, jako by měl se v hostitelském (např. nuget.org)
- Informace o vytváření a vlastníka.
- Dlouhý popis balíčku.

Běžné volitelné vlastnosti:

- Zpráva k vydání verze
- Informace o autorských právech
- Krátký popis [uživatelského rozhraní Správce balíčků v sadě Visual Studio](../tools/package-manager-ui.md)
- ID národního prostředí
- Domovská stránka a adresy URL licence
- Adresu URL ikony
- Seznam závislosti a odkazy
- Značky, které pomáhají při hledání Galerie

Toto je typické (ale fiktivní) `.nuspec` soubor s komentáři popisující vlastnosti:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Podrobnosti o deklarace závislosti a zadání čísla verzí, naleznete v části [Správa verzí balíčku](../reference/package-versioning.md). Je také možné do prostor prostředky z závislosti přímo v balíčku pomocí `include` a `exclude` atributy na `dependency` elementu. V tématu [příponou .nuspec odkaz - závislosti](../reference/nuspec.md#dependencies).

Manifest je zahrnutý v balíčku vytvořit z něj, proto vyhledejte libovolný počet Další příklady tak, že prověří existující balíčky. Je dobré zdroj *globální balíčky* složky v počítači, umístění, které vrátí následující příkaz:

```cli
nuget locals -list global-packages
```

Přejděte do jakéhokoli *package\version* složce, kopie `.nupkg` do souboru `.zip` souboru a pak otevřete, `.zip` soubor a zkontrolujte `.nuspec` v něm.

> [!Note]
> Při vytváření `.nuspec` z projektu sady Visual Studio manifest obsahuje tokenů, které jsou nahrazeny informace z projektu, když je balíček vytvořen. V tématu [vytváření příponou .nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>Vytvoření souboru s příponou .nuspec

Vytváření dokončení manifestu obvykle začíná základní `.nuspec` souboru vygenerovaného prostřednictvím jednoho z následujících metod:

- [Založené na konvenci pracovní adresář](#from-a-convention-based-working-directory)
- [Sestavení knihovny DLL](#from-an-assembly-dll)
- [Projekt sady Visual Studio](#from-a-visual-studio-project)    
- [Nový soubor s výchozími hodnotami](#new-file-with-default-values)

Pak upravíte soubor ručně tak, aby popisuje přesný obsah, který chcete v posledním balíčku.

> [!Important]
> Generované `.nuspec` soubory obsahují zástupné symboly, které je třeba upravit před vytvořením balíčku s `nuget pack` příkaz. Příkaz selže, pokud `.nuspec` obsahuje zástupné symboly.

### <a name="from-a-convention-based-working-directory"></a>Z založené na konvenci pracovní adresář

Protože balíčku NuGet je právě soubor ZIP, který byl přejmenován s `.nupkg` rozšíření, jeho často nejjednodušší vytvořit strukturu složek, které chcete v systému souborů, pak vytvořte `.nuspec` soubor přímo z této struktury. `nuget pack` Příkaz automaticky přidá všechny soubory v této struktuře složek (s výjimkou všechny složky, které začínají `.`, umožňuje zachovat soubory soukromých ve stejné struktuře).

Výhoda tohoto přístupu je, že nemusíte v manifestu zadejte soubory, které chcete zahrnout do balíčku (jak je popsáno dále v tomto tématu). Jednoduše může mít vaše procesu sestavení vytvořit strukturu přesnou složku, která přejde do balíčku a snadno můžete zahrnout další soubory, které nemusí být součástí projektu jinak:

- Obsah a zdrojový kód, který by měl být vloženy do cílový projekt.
- Skripty prostředí PowerShell (balíčky použité v NuGet 2.x může zahrnovat taky skriptů instalace, což není podporováno v NuGet 3.x a novější).
- Transformace na existující konfiguraci a zdrojové soubory kódu v projektu.

Konvence složky jsou následující:

| Folder | Popis | Akce při instalaci balíčku |
| --- | --- | --- |
| (uživatel root) | Umístění souboru readme.txt | Při instalaci balíčku Visual Studio zobrazí souboru readme.txt v kořenu balíčku. |
| lib / {tfm} | Sestavení (`.dll`), dokumentace (`.xml`) a symbol (`.pdb`) soubory pro danou cílový Framework Přezdívka (TFM) | Sestavení jsou přidány jako odkazy; `.xml` a `.pdb` zkopírovány do složky projektu. V tématu [podpora více cílové rozhraní](supporting-multiple-target-frameworks.md) pro vytvoření framework specifické pro cílové podsložky. |
| Moduly runtime | Architektura konkrétní sestavení (`.dll`), symbol (`.pdb`) a nativní prostředků (`.pri`) souborů | Sestavení jsou přidány jako odkazy; ostatní soubory se zkopírují do složky projektu. V tématu [podpora více cílové rozhraní](supporting-multiple-target-frameworks.md). |
| obsah | Různé soubory | Obsah je zkopírován do kořenového adresáře projektu. Představte si, že **obsah** složky jako kořen cílová aplikace, který nakonec využívá balíčku. Do mají balíček přidat bitovou kopii do aplikace */image* složku, umístěte ji do balíčku *obsah nebo obrázky* složky. |
| sestavení | MSBuild `.targets` a `.props` soubory | Automaticky vloží do souboru projektu nebo `project.lock.json` (NuGet 3.x+). |
| nástroje | Skripty prostředí PowerShell a programy, které jsou přístupné z konzoly Správce balíčků | `tools` Se přidá složka `PATH` proměnnou prostředí pro konzolu Správce balíčků (konkrétně *není* k `PATH` jako sada pro MSBuild při sestavování projektu). |

Protože struktury složky může obsahovat libovolný počet sestavení pro libovolný počet cílové rozhraní, tato metoda je nutné při vytváření balíčků, které podporují více rozhraní 

V každém případě až budete mít struktuře požadované složky na místě, spusťte následující příkaz v této složce vytvořit `.nuspec` souboru:

```cli
nuget spec
```

Znovu vygenerovaný `.nuspec` neobsahuje žádné explicitní odkazy na soubory v této struktuře. NuGet automaticky zahrne všechny soubory, když je balíček vytvořen. Stále je třeba upravit zástupné hodnoty v dalších částech tohoto manifest, ale.

### <a name="from-an-assembly-dll"></a>Ze sestavení knihoven DLL

V případě jednoduchého vytváření balíčku ze sestavení může generovat `.nuspec` souboru z metadat v sestavení pomocí následujícího příkazu:

```cli
nuget spec <assembly-name>.dll
```

Pomocí tohoto formuláře nahradí konkrétní hodnoty od sestavení, několik zástupné symboly v manifestu. Například `<id>` je nastavena na název sestavení a `<version>` je nastaven na verzi sestavení. Ostatní vlastnosti v manifestu, ale nemáte mít odpovídající hodnoty v sestavení a stále proto obsahují zástupné symboly.

### <a name="from-a-visual-studio-project"></a>Z projektu sady Visual Studio

Vytváření `.nuspec` z `.csproj` nebo `.vbproj` souboru je vhodné, protože jiné balíčky, které byly nainstalovány do těchto projektu se automaticky odkazuje jako závislosti. Ve stejné složce jako soubor projektu jednoduše použijte následující příkaz:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Výsledná `<project-name>.nuspec` soubor obsahuje *tokeny* , se nahrazují během balení hodnoty z projektu, včetně odkazů na další balíčky, které již jsou nainstalovány.

Token je oddělená `$` symboly na obou stranách vlastnosti projektu. Například `<id>` hodnota v manifestu vygenerované v tomto způsobem obvykle vypadat takto:

```xml
<id>$id$</id>
```

Tento token nahrazen `AssemblyName` hodnotu ze souboru projektu v balení čas. Pro přesné mapování projektu hodnot na `.nuspec` tokeny, najdete v článku [odkazovat nahrazení tokeny](../reference/nuspec.md#replacement-tokens).

Tokeny můžete snížit z museli klíčové hodnoty jako číslo verze v aktualizovat `.nuspec` jako aktualizace projektu. (Můžete vždy nahradit tokeny literálových hodnot v případě potřeby). 

Všimněte si, že existuje několik další balení možností při práci z projektu sady Visual Studio, jak je popsáno v [systémem nuget aktualizací Service pack ke generování souboru .nupkg v podadresáři](#running-nuget-pack-to-generate-the-nupkg-file) později.

#### <a name="solution-level-packages"></a>Balíčky úrovni řešení

*NuGet pouze 2.x. Není k dispozici v NuGet 3.0 +.*

NuGet 2.x podporované představu o úrovni řešení balíček, který nainstaluje nástroje nebo další příkazy pro konzolu Správce balíčků (obsah `tools` složky), ale nemá přidejte odkazy na obsah, nebo vytvořit vlastní nastavení na všechny projekty v řešení. Tyto balíčky obsahovat žádné soubory v jeho přímo `lib`, `content`, nebo `build` složek a jeden z jejich závislých mít soubory v jejich odpovídajících `lib`, `content`, nebo `build` složek.

Sleduje NuGet nainstalované balíky úrovni řešení v `packages.config` v soubor `.nuget` složky, nikoli projektu `packages.config` souboru.

### <a name="new-file-with-default-values"></a>Nový soubor s výchozími hodnotami

Následující příkaz vytvoří výchozí manifest se zástupnými symboly, což zajistí, že začínáte s strukturu správný soubor:

```cli
nuget spec [<package-name>]
```

Pokud vynecháte \<název balíčku\>, bude výsledný soubor je `Package.nuspec`. Pokud je třeba zadat název `Contoso.Utility.UsefulStuff`, je soubor `Contoso.Utility.UsefulStuff.nuspec`.

Výsledná `.nuspec` obsahuje zástupné symboly pro hodnot, jako `projectUrl`. Nezapomeňte upravit soubor než jej použijete k vytvoření konečné `.nupkg` souboru.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Výběr balíčku jedinečný identifikátor a nastavení číslo verze

Identifikátor balíčku (`<id>` element) a číslo verze (`<version>` element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je součástí balíčku.

**Osvědčené postupy pro identifikátor balíčku:**

- **Jedinečnost**: identifikátor musí být jedinečný v rámci nuget.org nebo jakoukoli Galerie hostitelem balíčku. Než se rozhodnete, že na identifikátor, vyhledejte galerii použít ke kontrole, pokud název je již používán. Aby nedocházelo ke konfliktům, dobrým způsobem je použít název vaší společnosti jako první část identifikátor, jako například `Contoso.`.
- **Namespace jako názvy**: postupujte podle vzor podobná obory názvů v rozhraní .NET, pomocí zápisu s tečkou místo pomlčky. Například použít `Contoso.Utility.UsefulStuff` místo `Contoso-Utility-UsefulStuff` nebo `Contoso_Utility_UsefulStuff`. Příjemci knihovny také užitečné, když se identifikátor balíčku shoduje s obory názvů používá v kódu.
- **Ukázkové balíčky**: Pokud vytvořit balíček ukázkový kód, který ukazuje, jak chcete použít jiný balíček, připojit `.Sample` jako příponu k identifikátoru, jako v `Contoso.Utility.UsefulStuff.Sample`. (Balíček ukázkové by samozřejmě jsou závislé na jiný balíček.) Při vytváření balíčku ukázka, použijte založené na konvenci pracovní adresář metody popsané výše. V `content` složce uspořádat ukázkový kód ve složce s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Osvědčené postupy pro verze balíčku:**

- Obecně platí nastavte verze balíčku tak, aby odpovídaly knihovny, i když to není nezbytně nutné. Toto je představuje jednoduché při omezit balíčku do jednoho sestavení, jak je popsáno výše v [rozhodnutí, která sestavení balíčku](#deciding-which-assemblies-to-package). Celkově platí nezapomeňte, že NuGet samotné se zabývá verze balíčku při rozpoznávání závislostem není verzí sestavení.
- Při použití nestandardní verzi schématu, nezapomeňte pravidla verzí NuGet zvažte, jak je popsáno v [Správa verzí balíčku](../reference/package-versioning.md).

> Následující řadu příspěvcích na blogu stručný jsou také užitečné rozumět Správa verzí:
>
> - [Část 1: Pořízení na knihoven DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: Algoritmus jádra](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Část 3: Sjednocení prostřednictvím přesměrování vazby](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Balíček typ nastavení

U balíčku NuGet 3.5 +, může být označen balíčky konkrétní *typ balíčku* indikující její zamýšlené použití. Balíčky s typem, včetně všech balíčky vytvořené pomocí dřívějších verzích systému NuGet, nebyl označen jako výchozí `Dependency` typu.

- `Dependency` Typ balíčky sestavení nebo běhu prostředky přidat do knihovny a aplikace a lze nainstalovat do libovolného typu projektu (za předpokladu, že jsou kompatibilní).

- `DotnetCliTool` Typ balíčky jsou rozšíření [rozhraní příkazového řádku .NET](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku. Tyto balíčky lze nainstalovat pouze v projektech .NET Core a mít žádný vliv na operace obnovení. Další podrobnosti o těchto – projekt rozšíření jsou k dispozici v [rozšiřitelnost .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentaci.

- Vlastní typ balíčků, použijte identifikátor libovolný typ, který vyhovuje pravidlům stejný formát jako ID balíčku. Jakýkoli typ jinými než `Dependency` a `DotnetCliTool`, ale nejsou rozpoznány pomocí Správce balíčků NuGet v sadě Visual Studio.

Typy balíčků jsou nastavené `.nuspec` souboru. Je nejvhodnější pro zpětnou kompatibilitu pro *není* explicitně nastaven `Dependency` zadejte a místo toho spoléhají na NuGet za předpokladu, že tento typ, pokud žádný typ zadaný.

- `.nuspec`: Označuje typ balíčku v rámci `packageTypes\packageType` pod uzlem `<metadata>` element:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>Přidání soubor readme a další soubory

Pokud chcete přímo zadat soubory, které chcete zahrnout do balíčku, použijte `<files>` uzel v `.nuspec` souboru, který *následuje* `<metadata>` značky:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Při použití přístup založené na konvenci pracovní adresář, můžete umístit souboru readme.txt kořenového adresáře balíčku a další obsah `content` složky. Ne `<file>` prvky jsou nezbytné v manifestu.

Pokud zahrnete soubor s názvem `readme.txt` v kořenu balíčku sady Visual Studio zobrazí obsah tohoto souboru jako prostý text okamžitě po instalaci balíčku přímo. (Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti). Můžete zde je ukázka, jak se zobrazí v souboru readme pro balíček HtmlAgilityPack:

![Zobrazení soubor readme pro balíček NuGet po instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> Pokud zahrnete prázdnou `<files>` uzel v `.nuspec` souboru NuGet neobsahuje žádný jiný obsah v balíčku než co je v `lib` složky.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>Včetně MSBuild props a cíle v balíčku

V některých případech můžete chtít přidat vlastní sestavovací cíle nebo vlastnosti v projektech, které využívají vašeho balíčku, jako je například spuštění vlastního nástroje nebo procesu během vytváření sestavení. To uděláte tak, že soubory ve formátu `<package_id>.targets` nebo `<package_id>.props` (například `Contoso.Utility.UsefulStuff.targets`) v rámci `\build` složce projektu.

Soubory v kořenovém `\build` složky jsou považovány za vhodné pro všechny cílové architektury. Pokud chcete zadat konkrétní rozhraní soubory, nejprve umístíte těch v rámci příslušných podsložek, například následující:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Potom v `.nuspec` souboru, ujistěte se, který bude odkazovat na těchto souborů v `<files>` uzlu:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

Včetně MSBuild props a cíle v balíčku byla [zavedené NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto se doporučuje přidat `minClientVersion="2.5"` atribut `metadata` element udávajících minimální verzi klienta NuGet potřeba využívat balíčku.

Když NuGet nainstaluje balíček s `\build` soubory, přidá MSBuild `<Import>` elementy v souboru projektu odkazující na `.targets` a `.props` soubory. (`.props` se přidá na začátek souboru projektu; `.targets` se přidá na dolní.) Samostatné podmíněného MSBuild `<Import>` prvek přidán pro každé cílové rozhraní.

MSBuild `.props` a `.targets` souborům pro cílení na mezi framework mohou být umístěny v `\buildCrossTargeting` složky. Během instalace balíčku NuGet přidá k odpovídající položce `<Import>` elementy k souboru projektu s podmínku, která cílovém Frameworku, který není nastavena (vlastnosti MSBuild `$(TargetFramework)` musí být prázdný).

U balíčku NuGet 3.x, cíle nejsou přidány do projektu, ale místo toho jsou k dispozici prostřednictvím `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>Vytváření balíčků s sestavení vzájemné spolupráce COM

Balíčky, které obsahují sestavení vzájemné spolupráce COM musí obsahovat odpovídající [cíle souboru](#including-msbuild-props-and-targets-in-a-package) tak, aby správný `EmbedInteropTypes` metadata jsou přidány do projektů pomocí formátu PackageReference. Ve výchozím nastavení `EmbedInteropTypes` metadata je vždy hodnotu false pro všechna sestavení při PackageReference se používá, takže soubor cíle přidá tato metadata explicitně. Aby nedocházelo ke konfliktům, musí být cílový název jedinečné; v ideálním případě použít kombinaci váš název balíčku a sestavení se embedded, ve které nahradíte `{InteropAssemblyName}` v níže uvedeném příkladu s danou hodnotou. (Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) příklad.)

```xml
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Všimněte si, že při použití `packages.config` formátu správy přidávání odkazů na sestavení z balíčků způsobí, že NuGet a sady Visual Studio pro kontrolu sestavení vzájemné spolupráce COM a nastavit `EmbedInteropTypes` na hodnotu true v souboru projektu. V tomto případě jsou cíle elementem.

Kromě toho ve výchozím nastavení [toku prostředky sestavení není přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Balíčky vytvořené podle postupu popsaného tady pracovní jinak po jejich vyjmutí jako přenositelné závislost z odkaz na projekt na projekt. Příjemce balíček můžete jim toku změnou výchozí hodnota PrivateAssets tak, aby neobsahoval sestavení povolit.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>S aktualizací Service pack nuget ke generování souboru .nupkg v podadresáři

Pokud používáte sestavení nebo pracovní adresář založené na konvenci, vytvořit balíček spuštěním `nuget pack` s vaší `.nuspec` souboru, nahraďte `<manifest-name>` s vaší konkrétní název souboru:

```cli
nuget pack <project-name>.nuspec
```

Při použití projektu sady Visual Studio, spusťte `nuget pack` s soubor projektu, který automaticky načte projektu `.nuspec` souboru a nahradí všechny tokeny v něm pomocí hodnot v souboru projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Přímo pomocí souboru projektu je nezbytné pro token nahrazení, protože projekt je zdrojem hodnoty tokenu. Nahrazení tokenu není dojít, pokud používáte `nuget pack` s `.nuspec` souboru.

Ve všech případech `nuget pack` vyloučí složek, které začínají s dobou, jako například `.git` nebo `.hg`.

NuGet označuje, pokud jsou všechny chyby `.nuspec` soubor, který vyžadují opravu, jako je například, že zapomenete změnit zástupné hodnoty v manifestu.

Jednou `nuget pack` úspěšné, máte `.nupkg` souborů, které můžete publikovat do Galerie vhodný, jak je popsáno v [publikování balíčku](../create-packages/publish-a-package.md).

> [!Tip]
> Užitečné způsob, jak zkontrolovat balíček po vytvoření ho otevřít v [balíček Průzkumníka](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) nástroj. To vám dává grafické zobrazení obsah balíčku a jeho manifestu. Můžete také přejmenovat, výsledná `.nupkg` do souboru `.zip` souboru a seznamte se s jeho obsahem přímo.

### <a name="additional-options"></a>Další možnosti

Můžete použít různé přepínače příkazového řádku s `nuget pack` vyloučit soubory, přepsat číslo verze v manifestu a změnit do výstupní složky mezi dalších funkcí. Úplný seznam najdete v článku [pack reference k příkazům](../tools/cli-ref-pack.md).

Pár jsou běžné u projektů sady Visual Studio jsou následující možnosti:

- **Odkazovaný projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty jako součást balíčku, nebo jako závislosti, s použitím `-IncludeReferencedProjects` možnost:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Tento proces zahrnutí je rekurzivní, takže když `MyProject.csproj` odkazy na projekty B a C a tyto projekty odkazovat D, E a F a potom soubory z B, C, D, E a F jsou součástí balíčku.

    Pokud obsahuje odkazovaný projektu `.nuspec` souboru svůj vlastní, pak NuGet přidá tento Odkazovaný projekt jako závislost místo.  Budete muset balíčku a publikování tohoto projektu v samostatně.

- **Konfigurace sestavení**: ve výchozím nastavení používá NuGet je konfigurace sestavení výchozí nastavená v souboru projektu, obvykle *ladění*. K pack soubory z různých sestavení konfigurace, jako například *verze*, použijte `-properties` možnost s konfigurací:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symboly**: Chcete-li například symboly, které umožňují příjemcům krokovat kód balíčku v ladicím programu, použijte `-Symbols` možnost:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Testování instalace balíčku

Před publikováním balíček, chcete obvykle testovat proces instalace balíčku do projektu. Testy, zkontrolujte, zda nutně soubory všechny skončili na jejich správné místech v projektu.

Můžete otestovat instalace ručně v sadě Visual Studio nebo na příkazovém řádku pomocí normální [balíček kroky instalace](../consume-packages/ways-to-install-a-package.md).

Pro automatizované testování základní proces je následující:

1. Kopírování `.nupkg` soubor do místní složky.
1. Přidat složku do vaší zdroje balíčku pomocí `nuget sources add -name <name> -source <path>` příkazu (najdete v části [zdroje nuget](../tools/cli-ref-sources.md)). Všimněte si, že budete potřebovat pouze jednou nastavit tento místní zdroj libovolného daného počítače.
1. Nainstalujte balíček z tohoto zdroje pomocí `nuget install <packageID> -source <name>` kde `<name>` odpovídá názvu zdrojového přidělený `nuget sources`. Zadání zdrojové zajistí, že balíček je nainstalovat z tohoto zdroje samostatně.
1. Zkontrolujte a zkontrolujte, zda jsou soubory správně nainstalovány v systému souborů.

## <a name="next-steps"></a>Další kroky

Po vytvoření balíčku, který je `.nupkg` souboru, můžete ji publikujete do Galerie zvoleného jak je popsáno na [publikování balíčku](../create-packages/publish-a-package.md).

Můžete také chtít rozšiřují možnosti vašeho balíčku nebo jinak podporovala jiné scénáře, jak je popsáno v následujících tématech:

- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více cílových verzí rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformace zdroje a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze](../create-packages/prerelease-packages.md)

Nakonec existují další balíčky typy zajímat:

- [Nativní balíčky](../create-packages/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
