---
title: Vytvoření balíčku NuGet pomocí cli nuget.exe
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových rozhodovacích bodů, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b3e6f0efc9e2e12de186ffd4ce29d496d07d5fc4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428945"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>Vytvoření balíčku pomocí cli nuget.exe

Bez ohledu na to, co váš balíček dělá nebo jaký `nuget.exe` kód `dotnet.exe`obsahuje, použijete jeden z nástrojů rozhraní rozhraní rozhraní cli, nebo , k balení této funkce do součásti, která může být sdílena s libovolným počtem jiných vývojářů. Informace o instalaci nástrojů ClI nuget, naleznete [v tématu Instalace klientských nástrojů NuGet](../install-nuget-client-tools.md). Všimněte si, že Visual Studio neobsahuje automaticky nástroj cli.

- U projektů, které nejsou ve stylu sady SDK, obvykle projekty rozhraní .NET Framework, vytvořte balíček podle kroků popsaných v tomto článku. Podrobné pokyny pomocí sady Visual Studio `nuget.exe` a rozhraní příkazového příkazu naleznete v [tématu Vytvoření a publikování balíčku rozhraní .NET Framework](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).

- Pro projekty .NET Core a .NET Standard, které používají [formát ve stylu sady SDK,](../resources/check-project-format.md)a všechny ostatní projekty ve stylu sady SDK naleznete v [tématu Vytvoření balíčku NuGet pomocí rozhraní příkazového příkazu dotnet .](creating-a-package-dotnet-cli.md)

- Pro projekty `packages.config` migrované z [PackageReference](../consume-packages/package-references-in-project-files.md)použijte [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

Technicky vzato, balíček NuGet je pouze soubor ZIP, `.nupkg` který byl přejmenován s příponou a jehož obsah odpovídá určitým konvencím. Toto téma popisuje podrobný proces vytváření balíčku, který splňuje tyto konvence.

Balení začíná kompilovaným kódem (sestaveními), symboly a/nebo jinými soubory, které chcete doručit jako balíček (viz [Přehled a pracovní postup).](overview-and-workflow.md) Tento proces je nezávislý na kompilaci nebo jiné generování souborů, které přejdou do balíčku, i když můžete čerpat z informací v souboru projektu, aby zkompilovaná sestavení a balíčky v synchronizaci.

> [!Important]
> Toto téma se týká projektů, které nejsou ve stylu sady SDK, obvykle projekty než .NET Core a .NET Standard projekty pomocí Visual Studio 2017 a vyšší verze a NuGet 4.0 +.

## <a name="decide-which-assemblies-to-package"></a>Rozhodněte se, která sestavení mají být zabalena

Většina balíčků pro obecné účely obsahuje jedno nebo více sestavení, které mohou ostatní vývojáři použít ve svých vlastních projektech.

- Obecně je nejlepší mít jedno sestavení na balíček NuGet, za předpokladu, že každé sestavení je nezávisle užitečné. Například pokud máte, `Utilities.dll` který `Parser.dll`závisí `Parser.dll` na , a je užitečné samostatně, pak vytvořte jeden balíček pro každý. To umožňuje vývojářům `Parser.dll` používat `Utilities.dll`nezávisle na .

- Pokud se vaše knihovna skládá z více sestavení, která nejsou nezávisle užitečná, je v pořádku je kombinovat do jednoho balíčku. Použití předchozího příkladu, pokud `Parser.dll` obsahuje kód, který se používá pouze `Utilities.dll`v , pak je v pořádku zachovat `Parser.dll` ve stejném balíčku.

- Podobně, pokud `Utilities.dll` závisí `Utilities.resources.dll`na , kde opět není užitečné samo o sobě, pak dát oba ve stejném balíčku.

Zdroje jsou ve skutečnosti zvláštní případ. Při instalaci balíčku do projektu NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* těch, které jsou pojmenovány, `.resources.dll` protože jsou považovány za lokalizované satelitní sestavení (viz [Vytváření lokalizovaných balíčků](creating-localized-packages.md)). Z tohoto důvodu `.resources.dll` se vyhněte použití pro soubory, které jinak obsahují základní kód balíčku.

Pokud vaše knihovna obsahuje sestavení interop com, postupujte podle dalších pokynů v [části Vytvořit balíčky s meziop sestaveními com](author-packages-with-com-interop-assemblies.md).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Role a struktura souboru .nuspec

Jakmile budete vědět, jaké soubory chcete zabalit, dalším krokem `.nuspec` je vytvoření manifestu balíčku v souboru XML.

Manifest:

1. Popisuje obsah balíčku a je sám součástí balíčku.
1. Řídí vytvoření balíčku a instruuje NuGet o tom, jak nainstalovat balíček do projektu. Například manifest identifikuje jiné závislosti balíčků tak, aby NuGet můžete také nainstalovat tyto závislosti při instalaci hlavního balíčku.
1. Obsahuje požadované i volitelné vlastnosti, jak je popsáno níže. Přesné podrobnosti, včetně dalších vlastností, které zde nejsou uvedeny, naleznete v [odkazu .nuspec](../reference/nuspec.md).

Požadované vlastnosti:

- Identifikátor balíčku, který musí být jedinečný v celé galerii, která je hostitelem balíčku.
- Konkrétní číslo verze ve formuláři *Major.Minor.Patch[-Přípona],* kde *přípona* identifikuje [předběžné verze](prerelease-packages.md)
- Název balíčku, jak by se měl objevit na hostiteli (jako nuget.org)
- Informace o autorovi a majiteli.
- Dlouhý popis balíčku.

Běžné volitelné vlastnosti:

- Poznámky k verzi
- Informace o autorských právech
- Stručný popis [ui Správce balíčků v sadě Visual Studio](../consume-packages/install-use-packages-visual-studio.md)
- ID národního prostředí
- Adresa URL projektu
- Licence jako výraz nebo`licenseUrl` soubor ( je zastaralá, použijte [ `license` prvek metadat nuspec](../reference/nuspec.md#license))
- Adresa URL ikony
- Seznamy závislostí a odkazů
- Značky, které pomáhají při vyhledávání v galerii

Následuje typický (ale fiktivní) `.nuspec` soubor s komentáři popisujícími vlastnosti:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

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

Podrobnosti o deklarování závislostí a určení čísel verzí naleznete v tématech [packages.config](../reference/packages-config.md) a [Package versioning](../concepts/package-versioning.md). Je také možné povrchové prostředky ze závislostí přímo `include` `exclude` v balíčku `dependency` pomocí atributy a na prvek. Viz [odkaz .nuspec - závislosti](../reference/nuspec.md#dependencies).

Vzhledem k tomu, že manifest je součástí balíčku vytvořeného z něj, můžete najít libovolný počet dalších příkladů zkoumáním existující balíčky. Dobrým zdrojem je složka *globálních balíčků* v počítači, jejíž umístění je vráceno následujícím příkazem:

```cli
nuget locals -list global-packages
```

Přejděte do libovolné složky `.nupkg` *package\version,* zkopírujte `.zip` soubor do `.nuspec` souboru, `.zip` otevřete jej a zkontrolujte v něm.

> [!Note]
> Při vytváření `.nuspec` z projektu sady Visual Studio manifest obsahuje tokeny, které jsou nahrazeny informacemi z projektu při sestavení balíčku. Viz [Vytvoření .nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).

## <a name="create-the-nuspec-file"></a>Vytvoření souboru Nuspec

Vytvoření úplného manifestu obvykle začíná `.nuspec` základním souborem generovaným jednou z následujících metod:

- [Pracovní adresář založený na konvencích](#from-a-convention-based-working-directory)
- [DLL sestavy](#from-an-assembly-dll)
- [Projekt sady Visual Studio](#from-a-visual-studio-project)    
- [Nový soubor s výchozími hodnotami](#new-file-with-default-values)

Potom upravit soubor ručně tak, aby popis přesně obsah, který chcete v konečném balíčku.

> [!Important]
> Generované `.nuspec` soubory obsahují zástupné symboly, které musí `nuget pack` být změněny před vytvořením balíčku pomocí příkazu. Tento příkaz se `.nuspec` nezdaří, pokud obsahuje všechny zástupné symboly.

### <a name="from-a-convention-based-working-directory"></a>Z pracovního adresáře založeného na konvencích

Vzhledem k tomu, že balíček NuGet je `.nupkg` pouze soubor ZIP, který byl přejmenován s příponou, je často `.nuspec` nejjednodušší vytvořit strukturu složek, kterou chcete v místním systému souborů, a pak soubor vytvořit přímo z této struktury. Příkaz `nuget pack` pak automaticky přidá všechny soubory ve struktuře složek (s výjimkou všech složek, které začínají `.`, což umožňuje zachovat soukromé soubory ve stejné struktuře).

Výhodou tohoto přístupu je, že není nutné zadat v manifestu, které soubory chcete zahrnout do balíčku (jak je vysvětleno dále v tomto tématu). Můžete jednoduše mít proces sestavení vytvořit přesnou strukturu složek, která jde do balíčku a můžete snadno zahrnout další soubory, které nemusí být součástí projektu jinak:

- Obsah a zdrojový kód, který by měl být vložen do cílového projektu.
- Skripty prostředí PowerShell
- Transformace na existující konfigurace a soubory zdrojového kódu v projektu.

Konvence složek jsou následující:

| Složka | Popis | Akce při instalaci balíčku |
| --- | --- | --- |
| (kořen) | Umístění souboru readme.txt | Visual Studio zobrazí soubor readme.txt v kořenovém adresáři balíčku při instalaci balíčku. |
| lib/{tfm} | Assembly`.dll`( ),`.xml`dokumentace (`.pdb`) a symbol ( ) soubory pro daný cílový rámec moniker (TFM) | Sestavení jsou přidány jako odkazy pro kompilování i runtime; `.xml` a `.pdb` zkopírovány do složek projektu. Viz [Podpora více cílových rozhraní](supporting-multiple-target-frameworks.md) pro vytváření podsložek specifických pro cíl rámce. |
| ref/{tfm} | Assembly`.dll`( )`.pdb`a symbol ( ) soubory pro daný cílový rámec zástupný název (TFM) | Sestavení jsou přidány jako odkazy pouze pro čas kompilace; Takže nic nebude zkopírováno do složky přihrádky projektu. |
| Runtime | Sestavení specifické pro`.dll`architekturu`.pdb`( ),`.pri`symbol ( ) a nativní soubory prostředků ( ) | Sestavení jsou přidány jako odkazy pouze pro běh. ostatní soubory jsou zkopírovány do složek projektu. Ve `/ref/{tfm}` složce by mělo být `AnyCPU` vždy odpovídající sestavení specifické pro (TFM), které poskytuje odpovídající sestavení času kompilace. Viz [Podpora více cílových architektur](supporting-multiple-target-frameworks.md). |
| content | Libovolné soubory | Obsah se zkopíruje do kořenového adresáře projektu. Představte si složku **obsahu** jako kořen cílové aplikace, která nakonec spotřebovává balíček. Chcete-li, aby balíček přidal obrázek do složky */images* aplikace, umístěte jej do složky *obsahu/obrázků* balíčku. |
| sestavení | *(3.x+)* MSBuild `.targets` `.props` a soubory | Automaticky vložendo projektu. |
| buildMultiTargeting | *(4.0+)* MSBuild `.targets` `.props` a soubory pro cílení napříč rámci | Automaticky vložendo projektu. |
| buildTransitive | *(5.0+)* MSBuild `.targets` `.props` a soubory, které toku přechodně na všechny náročné projektu. Podívejte se na stránku [funkcí.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) | Automaticky vložendo projektu. |
| nástroje | Skripty a programy prostředí Powershell přístupné z konzoly Správce balíčků | Složka `tools` je přidána `PATH` do proměnné prostředí pouze pro konzolu `PATH` Správce balíčků (konkrétně *ne* na sadu msbuild při vytváření projektu). |

Vzhledem k tomu, že struktura složek může obsahovat libovolný počet sestavení pro libovolný počet cílových architektur, je tato metoda nezbytná při vytváření balíčků, které podporují více architektur.

V každém případě, jakmile budete mít požadovanou strukturu složek na místě, spusťte následující příkaz v této složce k vytvoření souboru: `.nuspec`

```cli
nuget spec
```

Znovu `.nuspec` generované neobsahuje žádné explicitní odkazy na soubory ve struktuře složek. NuGet automaticky zahrnuje všechny soubory při vytvoření balíčku. Stále je však nutné upravit zástupné hodnoty v jiných částech manifestu.

### <a name="from-an-assembly-dll"></a>Z dll sestavy

V jednoduchém případě vytvoření balíčku z sestavení můžete `.nuspec` vygenerovat soubor z metadat v sestavení pomocí následujícího příkazu:

```cli
nuget spec <assembly-name>.dll
```

Pomocí tohoto formuláře nahradí několik zástupných symbolů v manifestu se specifickými hodnotami ze sestavy. Například `<id>` vlastnost je nastavena na název `<version>` sestavení a je nastavena na verzi sestavení. Ostatní vlastnosti v manifestu však nemají odpovídající hodnoty v sestavení a proto stále obsahují zástupné symboly.

### <a name="from-a-visual-studio-project"></a>Z projektu sady Visual Studio

Vytvoření `.nuspec` ze `.csproj` souboru nebo `.vbproj` je vhodné, protože ostatní balíčky, které byly nainstalovány do tohoto projektu jsou automaticky odkazovány jako závislosti. Jednoduše použijte následující příkaz ve stejné složce jako soubor projektu:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Výsledný `<project-name>.nuspec` soubor obsahuje *tokeny,* které jsou nahrazeny v době balení s hodnotami z projektu, včetně odkazů na všechny ostatní balíčky, které již byly nainstalovány.

Pokud máte balíčky závislostí zahrnout do *.nuspec*, místo toho použít `nuget pack`a získat soubor *.nuspec* z v rámci generovaného souboru *.nupkg.* Použijte například následující příkaz.

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

Token je oddělen `$` symboly na obou stranách vlastnosti projektu. Například `<id>` hodnota v manifestu generované tímto způsobem se obvykle zobrazí takto:

```xml
<id>$id$</id>
```

Tento token je nahrazen `AssemblyName` hodnotou ze souboru projektu v době balení. Přesné mapování hodnot projektu `.nuspec` na tokeny naleznete v [odkazu na tokeny nahrazení tokenů](../reference/nuspec.md#replacement-tokens).

Tokeny vás zbaví nutnosti aktualizovat klíčové hodnoty, `.nuspec` jako je číslo verze při aktualizaci projektu. (Tokeny můžete vždy v případě potřeby nahradit literálovými hodnotami). 

Všimněte si, že existuje několik dalších možností balení k dispozici při práci z projektu sady Visual Studio, jak je popsáno v [spuštění nuget pack pro generování souboru .nupkg](#run-nuget-pack-to-generate-the-nupkg-file) později.

#### <a name="solution-level-packages"></a>Balíčky na úrovni řešení

*Pouze NuGet 2.x. Není k dispozici v NuGet 3.0+.*

NuGet 2.x podporuje pojem balíček na úrovni řešení, který nainstaluje nástroje nebo `tools` další příkazy pro konzolu Správce balíčků (obsah složky), ale nepřidává odkazy, obsah nebo sestavení vlastního nastavení pro všechny projekty v řešení. Tyto balíčky neobsahují `lib`žádné `content`soubory `build` v jeho přímé , nebo složky `lib` `content`a `build` žádný z jeho závislostí mají soubory v jejich příslušné , , nebo složky.

NuGet sleduje nainstalované balíčky `packages.config` na `.nuget` úrovni řešení v souboru `packages.config` ve složce, nikoli soubor projektu.

### <a name="new-file-with-default-values"></a>Nový soubor s výchozími hodnotami

Následující příkaz vytvoří výchozí manifest se zástupnými symboly, který zajistí, že začnete se správnou strukturou souboru:

```cli
nuget spec [<package-name>]
```

Pokud vyneche \<\>název balíčku , `Package.nuspec`výsledný soubor je . Pokud zadáte název, `Contoso.Utility.UsefulStuff`například , `Contoso.Utility.UsefulStuff.nuspec`soubor je .

Výsledek `.nuspec` obsahuje zástupné symboly `projectUrl`pro hodnoty, jako je . Nezapomeňte soubor upravit, než soubor použijete `.nupkg` k vytvoření konečného souboru.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Zvolte jedinečný identifikátor balíčku a nastavení čísla verze

Identifikátor balíčku`<id>` (element) a číslo`<version>` verze ( element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je obsažen v balíčku.

**Doporučené postupy pro identifikátor balíčku:**

- **Jedinečnost**: Identifikátor musí být jedinečný v celé nuget.org nebo v jakékoli galerii, která balíček hostuje. Než se rozhodnete pro identifikátor, vyhledejte v příslušné galerii, zda je název již používán. Chcete-li se vyhnout konfliktům, je dobrým vzorem použití názvu společnosti `Contoso.`jako první části identifikátoru, například .
- **Názvy podobné oboru názvů**: Postupujte podle vzoru podobného oborům názvů v rozhraní .NET pomocí tečkového zápisu místo spojovníků. Například použijte `Contoso.Utility.UsefulStuff` spíše `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`než nebo . Spotřebitelé také najít užitečné, když identifikátor balíčku odpovídá obory názvů používané v kódu.
- **Ukázkové balíčky**: Pokud vytvoříte balíček ukázkový kód, `.Sample` který ukazuje, jak používat jiný `Contoso.Utility.UsefulStuff.Sample`balíček, připojte jako příponu k identifikátoru, jako v . (Ukázkový balíček by samozřejmě měl závislost na druhém balíčku.) Při vytváření ukázkového balíčku použijte metodu pracovního adresáře založenou na konvencích, která byla popsána výše. Ve `content` složce uspořádejte ukázkový `\Samples\<identifier>` kód `\Samples\Contoso.Utility.UsefulStuff.Sample`do složky volané jako v .

**Doporučené postupy pro verzi balíčku:**

- Obecně platí, že nastavte verzi balíčku tak, aby odpovídala knihovně, i když to není nezbytně nutné. Toto je jednoduchá záležitost, když omezíte balíček na jedno sestavení, jak je popsáno výše v [rozhodnutí, která sestavení balíček](#decide-which-assemblies-to-package). Celkově nezapomeňte, že NuGet sám se zabývá verze balíčků při řešení závislostí, nikoli verze sestavení.
- Při použití nestandardní verze schématu, nezapomeňte zvážit NuGet pravidla správy verzí, jak je vysvětleno v [package versioning](../concepts/package-versioning.md).

> Následující série krátkých blogových příspěvků je také užitečná pro pochopení správy verzí:
>
> - [Část 1: Převzetí DLL Hell](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: Základní algoritmus](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Část 3: Sjednocení prostřednictvím závazných přesměrování](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>Přidání souboru readme a dalších souborů

Chcete-li přímo určit soubory, které `<files>` mají být `.nuspec` zahrnuty do `<metadata>` balíčku, použijte uzel v souboru, který následuje *za* značkou:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> Při použití přístupu pracovního adresáře založeného na konvencích můžete soubor readme.txt umístit do kořenového adresáře balíčku a dalšího obsahu ve `content` složce. V `<file>` manifestu nejsou nutné žádné prvky.

Když zahrnete `readme.txt` soubor pojmenovaný do kořenového adresáře balíčku, Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo. (Soubory Readme se nezobrazují pro balíčky nainstalované jako závislosti). Například zde je návod, jak se zobrazí readme pro balíček HtmlAgilityPack:

![Zobrazení souboru readme pro balíček NuGet při instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> Pokud do `<files>` `.nuspec` souboru zahrnete prázdný uzel, NuGet nezahrne do balíčku žádný `lib` jiný obsah než co je ve složce.

## <a name="include-msbuild-props-and-targets-in-a-package"></a>Zahrnout rekvizity a cíle MSBuild do balíčku

V některých případech můžete chtít přidat vlastní cíle sestavení nebo vlastnosti v projektech, které spotřebovávají váš balíček, jako je například spuštění vlastního nástroje nebo procesu během sestavení. To provést umístěním souborů `<package_id>.targets` ve `<package_id>.props` formuláři `Contoso.Utility.UsefulStuff.targets`nebo `\build` (například ) do složky projektu.

Soubory v `\build` kořenové složce jsou považovány za vhodné pro všechny cílové architektury. Chcete-li poskytnout soubory specifické pro architekturu, umístěte je nejprve do příslušných podsložek, například následující:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Pak v `.nuspec` souboru, ujistěte se, `<files>` že odkazovat na tyto soubory v uzlu:

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

Včetně MSBuild rekvizity a cíle v balíčku byla [zavedena s NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto se doporučuje přidat `minClientVersion="2.5"` atribut do `metadata` prvku, k označení minimální verze klienta NuGet potřebné ke spotřebě balíčku.

Když NuGet nainstaluje `\build` balíček se soubory, `<Import>` přidá prvky MSBuild v souboru projektu směřující na soubory `.targets` a. `.props` (`.props` je přidán v horní části souboru projektu; `.targets` je přidán v dolní části.) Pro každý cílový `<Import>` rámec je přidán samostatný podmíněný prvek MSBuild.

MSBuild `.props` `.targets` a soubory pro cílení mezi rámci `\buildMultiTargeting` lze umístit do složky. Během instalace balíčku NuGet `<Import>` přidá odpovídající prvky do souboru projektu s podmínkou, že `$(TargetFramework)` cílová architektura není nastavena (MSBuild vlastnost musí být prázdný).

S NuGet 3.x cíle nejsou přidány do projektu, `{projectName}.nuget.g.targets` ale `{projectName}.nuget.g.props`jsou k dispozici prostřednictvím a .

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>Spuštěním balíčku nuget pro generování souboru .nupkg

Při použití sestavení nebo pracovního adresáře založeného `nuget pack` na `.nuspec` konventu `<project-name>` vytvořte balíček spuštěním se souborem a nahrazením určitým názvem souboru:

```cli
nuget pack <project-name>.nuspec
```

Při použití projektu sady `nuget pack` Visual Studio spusťte s souborem `.nuspec` projektu, který automaticky načte soubor projektu a nahradí všechny tokeny v něm pomocí hodnot v souboru projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Použití souboru projektu přímo je nezbytné pro nahrazení tokenu, protože projekt je zdrojem hodnot tokenu. Nahrazení tokenu se nestane, pokud používáte `nuget pack` se souborem. `.nuspec`

Ve všech `nuget pack` případech nezahrnuje složky začínající tečkou, například `.git` nebo `.hg`.

NuGet označuje, pokud jsou `.nuspec` nějaké chyby v souboru, které je třeba opravit, například zapomínání změnit zástupné hodnoty v manifestu.

Jakmile `nuget pack` uspějete, máte `.nupkg` soubor, který můžete publikovat do vhodné galerie, jak je popsáno v publikování [balíčku](../nuget-org/publish-a-package.md).

> [!Tip]
> Užitečným způsobem, jak zkontrolovat balíček po jeho vytvoření, je otevřít jej v nástroji [Průzkumník balíčků.](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) To vám dává grafické zobrazení obsahu balíčku a jeho manifestu. Výsledný `.nupkg` soubor můžete také přejmenovat `.zip` na soubor a přímo prozkoumat jeho obsah.

### <a name="additional-options"></a>Další možnosti

Můžete použít různé přepínače `nuget pack` příkazového řádku s vyloučit soubory, přepsat číslo verze v manifestu a změnit výstupní složku, mimo jiné funkce. Úplný seznam naleznete v [odkazu na příkaz balení](../reference/cli-reference/cli-ref-pack.md).

Následující možnosti jsou některé, které jsou společné s projekty sady Visual Studio:

- **Odkazované projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty jako `-IncludeReferencedProjects` součást balíčku nebo jako závislosti pomocí možnosti:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Tento proces zahrnutí je rekurzivní, takže pokud `MyProject.csproj` odkazuje na projekty B a C a tyto projekty odkazují na D, E a F, pak jsou do balíčku zahrnuty soubory z B, C, D, E a F.

    Pokud odkazovaný projekt `.nuspec` obsahuje vlastní soubor, pak NuGet přidá tento odkazovaný projekt jako závislost místo.  Je třeba balíček a publikovat tento projekt samostatně.

- **Konfigurace sestavení**: Ve výchozím nastavení používá nuget výchozí konfigurační sadu sestavení v souboru projektu, obvykle *ladění*. Chcete-li zabalit soubory z jiné konfigurace `-properties` sestavení, jako je *například release*, použijte tuto možnost s konfigurací:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symboly**: chcete-li zahrnout symboly, které umožňují spotřebitelům `-Symbols` krokovat kód balíčku v ladicím programu, použijte možnost:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Instalace testovacího balíčku

Před publikováním balíčku obvykle chcete otestovat proces instalace balíčku do projektu. Testy ujistěte se, že nutně soubory všechny skončí na jejich správných místech v projektu.

Instalace můžete testovat ručně v sadě Visual Studio nebo na příkazovém řádku pomocí běžných [kroků instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

Pro automatizované testování je základní proces následující:

1. Zkopírujte `.nupkg` soubor do místní složky.
1. Přidejte složku do zdrojů `nuget sources add -name <name> -source <path>` balíčku pomocí příkazu (viz [nuget zdroje](../reference/cli-reference/cli-ref-sources.md)). Všimněte si, že stačí nastavit tento místní zdroj pouze jednou v daném počítači.
1. Nainstalujte balíček z `nuget install <packageID> -source <name>` `<name>` tohoto zdroje pomocí místa, `nuget sources`kde odpovídá názvu zdroje, jak je uvedeno na . Zadání zdroje zajišťuje, že balíček je nainstalován z tohoto zdroje sám.
1. Zkontrolujte systém souborů a zkontrolujte, zda jsou soubory nainstalovány správně.

## <a name="next-steps"></a>Další kroky

Po vytvoření balíčku, což je `.nupkg` soubor, můžete jej publikovat do galerie podle vašeho výběru, jak je popsáno na [publikování balíčku](../nuget-org/publish-a-package.md).

Můžete také rozšířit možnosti balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:

- [Správa verzí balíčku](../concepts/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformace zdrojových a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze](../create-packages/prerelease-packages.md)
- [Nastavení typu balíčku](../create-packages/set-package-type.md)
- [Vytváření balíčků pomocí meziop sestavení COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Nakonec existují další typy balíčků, které mají být vědomi:

- [Nativní balíčky](../guides/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages-snupkg.md)
