---
title: Vytvoření balíčku NuGet pomocí NuGet. exe CLI
description: Podrobný průvodce procesem navrhování a vytváření balíčku NuGet, včetně klíčových bodů rozhodování, jako jsou soubory a správa verzí.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: f33624cf50248d8a137216ed0d725ed88c0defd2
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833375"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>Vytvoření balíčku pomocí rozhraní příkazového řádku NuGet. exe

Bez ohledu na to, co váš balíček používá, nebo jaký kód obsahuje, můžete použít jeden z nástrojů rozhraní `nuget.exe` příkazového řádku (nebo `dotnet.exe`) k zabalení této funkce do komponenty, kterou lze sdílet a používat v jakémkoli počtu jiných vývojářů. Pokud chcete nainstalovat nástroje NuGet CLI, přečtěte si téma [Instalace nástrojů klienta NuGet](../install-nuget-client-tools.md). Všimněte si, že Visual Studio nezahrnuje automaticky nástroj CLI.

- Pro projekty, které nejsou ve stylu sady SDK, obvykle .NET Framework projekty, postupujte podle kroků popsaných v tomto článku a vytvořte balíček. Podrobné pokyny k používání sady Visual Studio a rozhraní `nuget.exe` příkazového řádku najdete v tématu [Vytvoření a publikování .NET Framework balíčku](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).

- Pro projekty .NET Core a .NET Standard, které používají [Formát ve stylu sady SDK](../resources/check-project-format.md), a všechny další projekty ve stylu sady SDK, přečtěte si téma [Vytvoření balíčku NuGet pomocí rozhraní příkazového řádku dotnet](creating-a-package-dotnet-cli.md).

- Pro projekty migrované z `packages.config` aplikace do [PackageReference](../consume-packages/package-references-in-project-files.md)použijte [MSBuild-t:Pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

Technicky řečeno, balíček NuGet je jenom soubor zip, který se přejmenoval s `.nupkg` příponou a jehož obsah se shoduje s některými úmluvami. Toto téma popisuje podrobný proces vytváření balíčku, který splňuje tyto konvence.

Balení začíná kompilovaným kódem (sestavení), symboly a/nebo dalšími soubory, které chcete doručit jako balíček (viz [Přehled a pracovní postup](overview-and-workflow.md)). Tento proces je nezávislý na kompilování nebo jinak generují soubory, které se nacházejí v balíčku, i když můžete kreslit z informací v souboru projektu, aby se zkompilované sestavení a balíčky udržovaly synchronizované.

> [!Important]
> Toto téma se vztahuje na projekty nevyužívající sadu SDK, obvykle v jiných projektech než .NET Core a .NET Standard projekty pomocí sady Visual Studio 2017 a novějších verzí a NuGet 4.0 +.

## <a name="decide-which-assemblies-to-package"></a>Rozhodněte, která sestavení se mají zabalit

Většina balíčků pro obecné účely obsahuje jedno nebo více sestavení, která mohou používat jiní vývojáři ve svých vlastních projektech.

- Obecně je vhodné mít jedno sestavení pro každý balíček NuGet za předpokladu, že každé sestavení je nezávisle užitečné. Například pokud máte `Utilities.dll` a, který závisí na `Parser.dll`a `Parser.dll` je vhodný pro vlastní, vytvořte pro každou z nich jeden balíček. To umožňuje vývojářům používat `Parser.dll` `Utilities.dll`nezávisle na.

- Pokud se knihovna skládá z více sestavení, která nejsou nezávislá na sobě, je vhodné je kombinovat do jednoho balíčku. Pokud použijete předchozí příklad, `Parser.dll` Pokud obsahuje kód, který používá `Utilities.dll`pouze, pak je vše v jednom balíčku `Parser.dll` zachováno.

- Podobně, pokud `Utilities.dll` závisí na `Utilities.resources.dll`, kde je znovu neužitečné, a pak do stejného balíčku vložte obojí.

Prostředky jsou ve skutečnosti zvláštním případem. Když je balíček nainstalován do projektu, NuGet automaticky přidá odkazy na sestavení do knihoven DLL balíčku, *kromě* těch, které jsou pojmenovány `.resources.dll` , protože se předpokládá, že jsou lokalizovaná satelitní sestavení (viz téma [vytváření lokalizovaných balíčky](creating-localized-packages.md)). Z tohoto důvodu `.resources.dll` nepoužívejte pro soubory, které jinak obsahují základní kód balíčku.

Pokud vaše knihovna obsahuje sestavení zprostředkovatele komunikace s objekty COM, postupujte podle dalších pokynů v části [Vytvoření balíčků se sestaveními zprostředkovatele komunikace s objekty COM](author-packages-with-com-interop-assemblies.md).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Role a struktura souboru. nuspec

Jakmile víte, které soubory chcete zabalit, další krok vytvoří manifest balíčku v `.nuspec` souboru XML.

Manifest:

1. Popisuje obsah balíčku a je sám součástí balíčku.
1. Vydělí jak vytvoření balíčku, tak instruuje nástroj NuGet o tom, jak balíček nainstalovat do projektu. Například manifest identifikuje jiné závislosti balíčků, takže může NuGet nainstalovat i tyto závislosti při instalaci hlavního balíčku.
1. Obsahuje požadované i volitelné vlastnosti, jak je popsáno níže. Přesné podrobnosti, včetně dalších vlastností, které zde nejsou uvedeny, naleznete v tématu [. nuspec reference](../reference/nuspec.md).

Požadované vlastnosti:

- Identifikátor balíčku, který musí být jedinečný v rámci Galerie, která hostuje balíček.
- Konkrétní číslo verze ve formátu *hlavní. podverze. Oprava [-přípona]* , kde *-přípona* identifikuje [předběžné verze verzí](prerelease-packages.md)
- Název balíčku, jak by měl být zobrazen na hostiteli (například nuget.org)
- Informace o autorovi a vlastníka.
- Dlouhý popis balíčku.

Běžné volitelné vlastnosti:

- Zpráva k vydání verze
- Informace o autorských právech
- Krátký popis [uživatelského rozhraní Správce balíčků v aplikaci Visual Studio](../consume-packages/install-use-packages-visual-studio.md)
- ID národního prostředí
- Adresa URL projektu
- Licence jako výraz nebo soubor (`licenseUrl` je zastaralá, [ `license` použijte element metadat nuspec](../reference/nuspec.md#license))
- Adresa URL ikony
- Seznam závislostí a odkazů
- Značky, které pomáhají při hledání v galerii

Následuje typický (ale fiktivní) `.nuspec` soubor s komentáři popisujícím vlastnosti:

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

Podrobnosti o deklarování závislostí a zadání čísel verzí najdete v tématu [Packages. config](../reference/packages-config.md) a [Správa verzí balíčků](../reference/package-versioning.md). Je také možné Surface prostředků ze závislostí přímo v balíčku pomocí `include` atributů `dependency` a `exclude` elementu. Viz [referenční závislosti. nuspec](../reference/nuspec.md#dependencies).

Vzhledem k tomu, že je manifest součástí balíčku, který byl vytvořen z něj, můžete najít libovolný počet dalších příkladů zkoumáním existujících balíčků. Dobrým zdrojem je složka *globálního balíčku* v počítači, umístění, které je vráceno následujícím příkazem:

```cli
nuget locals -list global-packages
```

Přejít do libovolné *složky package\version* `.nupkg` , zkopírovat soubor do `.zip` souboru, otevřít tento `.zip` soubor a prošetřit `.nuspec` ho.

> [!Note]
> Při vytváření `.nuspec` z projektu sady Visual Studio obsahuje manifest tokeny, které jsou nahrazeny informacemi z projektu při sestavení balíčku. Viz [vytvoření. nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).

## <a name="create-the-nuspec-file"></a>Vytvoření souboru. nuspec

Vytvoření kompletního manifestu obvykle začíná základním `.nuspec` souborem generovaným pomocí jedné z následujících metod:

- [Pracovní adresář na základě konvence](#from-a-convention-based-working-directory)
- [Knihovna DLL sestavení](#from-an-assembly-dll)
- [Projekt sady Visual Studio](#from-a-visual-studio-project)    
- [Nový soubor s výchozími hodnotami](#new-file-with-default-values)

Soubor pak upravíte ručně, aby pomohly v konečném balíčku popsaný přesný obsah.

> [!Important]
> Vygenerované `.nuspec` soubory obsahují zástupné symboly, které je třeba upravit před vytvořením balíčku `nuget pack` pomocí příkazu. Tento příkaz se `.nuspec` nezdařil, pokud obsahuje všechny zástupné symboly.

### <a name="from-a-convention-based-working-directory"></a>Z pracovního adresáře založeného na konvencích

Vzhledem k tomu, že balíček NuGet je jenom soubor zip, který se přejmenoval s `.nupkg` příponou, často je nejjednodušší vytvořit v místním systému souborů strukturu složek, kterou chcete, a pak `.nuspec` vytvořit soubor přímo z této struktury. Příkaz pak automaticky přidá všechny soubory v této struktuře složek (kromě všech složek, které `.`začínají, což vám umožní zachovat soukromé soubory ve stejné struktuře). `nuget pack`

Výhodou tohoto přístupu je, že nemusíte určovat v manifestu, které soubory chcete zahrnout do balíčku (jak je popsáno dále v tomto tématu). Proces sestavení může jednoduše vytvořit přesnou strukturu složky, která je součástí balíčku, a můžete snadno zahrnout další soubory, které nemusí být součástí projektu, jinak:

- Obsah a zdrojový kód, které by měly být vloženy do cílového projektu.
- PowerShellové skripty
- Transformace na existující soubory konfigurace a zdrojového kódu v projektu.

Konvence složek jsou následující:

| Folder | Popis | Akce při instalaci balíčku |
| --- | --- | --- |
| zobrazuje | Umístění souboru Readme. txt | Sada Visual Studio při instalaci balíčku zobrazí v kořenovém adresáři balíčku soubor Readme. txt. |
| lib/{tfm} | Assembly (`.dll`), dokumentace (`.xml`) a soubory symbolů (`.pdb`) pro daný moniker cílového rozhraní (TFM) | Sestavení jsou přidána jako reference pro kompilaci a také za běhu; `.xml` a`.pdb` zkopírovány do složek projektu. Viz [Podpora více cílových rozhraní](supporting-multiple-target-frameworks.md) pro vytváření podadresářů specifických pro cíl rozhraní. |
| ref/{TFM} | Sestavení (`.dll`) a symboly (`.pdb`) souborů pro daný moniker cílového rozhraní (TFM) | Sestavení jsou přidána jako odkazy pouze pro dobu kompilace; Takže se nic nezkopíruje do složky Bin projektu. |
| moduly runtime | Soubory sestavení (`.dll`), symbolů (`.pdb`) a nativních prostředků (`.pri`) specifických pro architekturu | Sestavení jsou přidána jako odkazy pouze pro modul runtime; jiné soubory jsou zkopírovány do složek projektu. V rámci `AnyCPU` `/ref/{tfm}` složky by mělo být vždy odpovídající (TFM) specifické sestavení, které poskytuje odpovídající sestavení doby kompilace. Viz [Podpora více cílových rozhraní](supporting-multiple-target-frameworks.md). |
| obsah | Libovolné soubory | Obsah je zkopírován do kořenového adresáře projektu. Složku **obsahu** si můžete představit jako kořen cílové aplikace, která nakonec balíček spotřebovává. Pokud chcete, aby balíček přidal obrázek do složky */images* aplikace, umístěte ho do složky *obsah/image* balíčku. |
| sestavení | MSBuild `.targets` a `.props` soubory | Automaticky vložen do souboru projektu nebo `project.lock.json` (NuGet 3. x +). |
| nástroje | Skripty a programy PowerShellu dostupné z konzoly Správce balíčků | Složka je přidána `PATH` do proměnné prostředí pouze pro konzolu Správce balíčků ( `PATH` konkrétně při sestavování sady MSBuild při sestavování projektu). `tools` |

Vzhledem k tomu, že struktura složky může obsahovat libovolný počet sestavení pro libovolný počet cílových rozhraní, tato metoda je nezbytná při vytváření balíčků, které podporují více rozhraní.

V každém případě, když máte zavedenou strukturu složky, spusťte v této složce následující příkaz pro vytvoření `.nuspec` souboru:

```cli
nuget spec
```

Vygenerovaná `.nuspec` aplikace znovu neobsahuje žádné explicitní odkazy na soubory ve struktuře složek. NuGet automaticky zahrnuje všechny soubory při vytvoření balíčku. Je však stále nutné upravovat zástupné hodnoty v jiných částech manifestu.

### <a name="from-an-assembly-dll"></a>Z knihovny DLL sestavení

V jednoduchém případě vytvoření balíčku ze sestavení můžete vygenerovat `.nuspec` soubor z metadat v sestavení pomocí následujícího příkazu:

```cli
nuget spec <assembly-name>.dll
```

Použití tohoto formuláře nahrazuje několik zástupných symbolů v manifestu s konkrétními hodnotami ze sestavení. Například `<id>` vlastnost je nastavena na název sestavení a `<version>` je nastavena na verzi sestavení. Jiné vlastnosti v manifestu však nemají v sestavení shodné hodnoty, takže stále obsahují zástupné symboly.

### <a name="from-a-visual-studio-project"></a>Z projektu sady Visual Studio

Vytváření souborů `.nuspec` `.vbproj` ze souboru nebo je vhodné, protože další balíčky, které byly do těchto projektů nainstalovány, jsou automaticky odkazovány jako závislosti. `.csproj` Jednoduše použijte následující příkaz ve stejné složce jako soubor projektu:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Výsledný `<project-name>.nuspec` soubor obsahuje *tokeny* , které jsou nahrazeny v době balení s hodnotami z projektu, včetně odkazů na všechny ostatní balíčky, které již byly nainstalovány.

Token je oddělen `$` symbolem na obou stranách vlastnosti projektu. Například `<id>` hodnota v manifestu generované tímto způsobem obvykle vypadá takto:

```xml
<id>$id$</id>
```

Tento token je nahrazen `AssemblyName` hodnotou ze souboru projektu v době balení. Přesné mapování hodnot projektu na `.nuspec` tokeny najdete v referenčních informacích k náhradním [tokenům](../reference/nuspec.md#replacement-tokens).

Tokeny vám zbavují nutnost aktualizace důležitých hodnot, jako je číslo verze v `.nuspec` při aktualizaci projektu. (V případě potřeby můžete tokeny vždy nahradit hodnotami literálů). 

Všimněte si, že při práci z projektu sady Visual Studio je k dispozici několik dalších možností balení, jak je popsáno v tématu [spuštění sady NuGet Pack pro vygenerování souboru. nupkg](#run-nuget-pack-to-generate-the-nupkg-file) později.

#### <a name="solution-level-packages"></a>Balíčky na úrovni řešení

*Pouze NuGet 2. x. Není k dispozici v NuGet 3.0 + +.*

NuGet 2. x podporoval pojem balíčku na úrovni řešení, který nainstaluje nástroje nebo další příkazy pro konzolu Správce balíčků (obsah `tools` složky), ale nepřidá odkazy, obsah ani přizpůsobení sestavení pro žádné projekty v. řešení. Takové balíčky neobsahují žádné soubory v `lib`přímých `content`, nebo `build` složkách a žádná z jejích závislostí nemá soubory v příslušných `lib`složkách, `content`nebo `build` .

NuGet sleduje nainstalované balíčky na úrovni řešení v `packages.config` souboru `.nuget` ve složce, `packages.config` nikoli v souboru projektu.

### <a name="new-file-with-default-values"></a>Nový soubor s výchozími hodnotami

Následující příkaz vytvoří výchozí manifest se zástupnými symboly, který vám zajistí začátek správné struktury souborů:

```cli
nuget spec [<package-name>]
```

Vynecháte \<-li název\>balíčku `Package.nuspec`, bude výsledný soubor. Pokud zadáte název `Contoso.Utility.UsefulStuff`, například, soubor je `Contoso.Utility.UsefulStuff.nuspec`.

Výsledek `.nuspec` obsahuje zástupné symboly pro hodnoty, `projectUrl`jako je. Nezapomeňte soubor před jeho použitím upravit a vytvořit tak konečný `.nupkg` soubor.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Vyberte jedinečný identifikátor balíčku a nastavte číslo verze.

Identifikátor balíčku (`<id>` element) a číslo verze (`<version>` element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je obsažen v balíčku.

**Osvědčené postupy pro identifikátor balíčku:**

- **Jedinečnost**: Identifikátor musí být jedinečný v rámci nuget.org nebo bez ohledu na to, jakou galerii hostují balíček. Než se rozhodnete pro identifikátor, vyhledejte příslušnou galerii a ověřte, jestli se tento název už používá. Aby nedocházelo ke konfliktům, dobrým vzorem je použít název vaší společnosti jako první část identifikátoru, například `Contoso.`.
- **Názvy podobných oborům názvů**: Sledujte vzor podobný oborům názvů v rozhraní .NET pomocí notace tečky namísto spojovníků. Použijte `Contoso.Utility.UsefulStuff` například `Contoso-Utility-UsefulStuff` místo nebo`Contoso_Utility_UsefulStuff`. Příjemci také naleznou užitečné, pokud se identifikátor balíčku shoduje s obory názvů použitými v kódu.
- **Ukázkové balíčky**: Pokud vytváříte balíček ukázkového kódu, který ukazuje, jak použít jiný balíček, připojte `.Sample` se jako přípona k identifikátoru, jako `Contoso.Utility.UsefulStuff.Sample`v. (Vzorový balíček samozřejmě má závislost na druhém balíčku.) Při vytváření ukázkového balíčku použijte metodu pracovní adresáře založenou na konvenci, která je popsaná výše. Ve složce uspořádejte vzorový kód do složky s názvem `\Samples\<identifier>` jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`. `content`

**Osvědčené postupy pro verzi balíčku:**

- Obecně platí, že nastavte verzi balíčku tak, aby odpovídala knihovně, i když to není nezbytně nutné. Toto je jednoduchá skutečnost při omezení balíčku na jedno sestavení, jak je popsáno výše v tématu [určení sestavení, která chcete](#decide-which-assemblies-to-package)zabalit. Celkově mějte na paměti, že aplikace NuGet pracuje s verzemi balíčku při řešení závislostí, nikoli ve verzích sestavení.
- Při použití nestandardního schématu verzí nezapomeňte zvážit pravidla správy verzí NuGet, jak je vysvětleno v tématu [Správa verzí balíčků](../reference/package-versioning.md).

> Následující řada stručných příspěvků na blogu je také užitečná pro pochopení správy verzí:
>
> - [Část 1: Přijetí na Hell knihovny DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: Základní algoritmus](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Část 3: Sjednocení pomocí přesměrování vazeb](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>Přidání souboru Readme a dalších souborů

Chcete-li přímo určit soubory, které mají být zahrnuty do `<files>` balíčku, použijte `.nuspec` uzel v `<metadata>` souboru, který *následuje* Značka:

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
> Pokud používáte přístup k pracovnímu adresáři založenému na konvenci, můžete soubor Readme. txt umístit do kořenového adresáře balíčku a `content` dalšího obsahu ve složce. V `<file>` manifestu nejsou potřebné žádné prvky.

Pokud zahrnete soubor s názvem `readme.txt` v kořenovém adresáři balíčku, sada Visual Studio zobrazí obsah tohoto souboru jako prostý text ihned po instalaci balíčku přímo. (Soubory Readme se nezobrazí pro balíčky nainstalované jako závislosti). Tady je příklad, jak se zobrazí soubor Readme pro balíček HtmlAgilityPack:

![Zobrazení souboru Readme pro balíček NuGet při instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> Pokud zahrnete `.nuspec` do souboru `<files>` prázdný uzel, NuGet neobsahuje žádný další obsah v balíčku, `lib` než co je ve složce.

## <a name="include-msbuild-props-and-targets-in-a-package"></a>Zahrnutí vlastností MSBuild a cílů do balíčku

V některých případech můžete chtít přidat vlastní cíle sestavení nebo vlastnosti v projektech, které používají váš balíček, jako je například spuštění vlastního nástroje nebo procesu během sestavování. To provedete tak, že umístíte soubory `<package_id>.targets` ve `<package_id>.props` formuláři nebo ( `Contoso.Utility.UsefulStuff.targets` `\build` například) do složky projektu.

Soubory v kořenové `\build` složce jsou považovány za vhodné pro všechny cílové platformy. Chcete-li poskytnout soubory specifické pro rozhraní, umístěte je nejprve do příslušných podsložek, například následující:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Pak v `.nuspec` souboru nezapomeňte odkazovat na tyto soubory `<files>` v uzlu:

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

Zahrnutí a cíle nástroje MSBuild do balíčku bylo zavedeno [s NuGet 2,5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto je vhodné přidat `minClientVersion="2.5"` atribut k `metadata` elementu, aby označovala minimální verzi klienta NuGet nutnou ke spotřebování balíčku.

Když NuGet nainstaluje `\build` balíček se soubory, přidá do souboru `.targets` projektu `<Import>` prvky MSBuild, které odkazují na soubory a `.props` . (`.props` je přidáno v horní části souboru projektu; `.targets` je přidáno v dolní části.) Pro každé cílové rozhraní `<Import>` se přidá samostatný podmíněný element MSBuild.

Nástroj `.props` `.targets` MSBuild a soubory pro cílení na různé architektury lze umístit do složky. `\buildMultiTargeting` V průběhu instalace balíčku NuGet přidá odpovídající `<Import>` prvky do souboru projektu s podmínkou, že cílové rozhraní není nastavené (vlastnost `$(TargetFramework)` MSBuild musí být prázdná).

S NuGet 3. x nejsou cíle do projektu přidány, ale jsou místo toho k dispozici prostřednictvím `project.lock.json`.

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>Spustit balíček NuGet pro vygenerování souboru. nupkg

Při použití sestavení nebo pracovního adresáře založeného na konvenci vytvořte balíček spuštěním `nuget pack` souboru s vaším `.nuspec` souborem, který nahradíte `<project-name>` konkrétním názvem souboru:

```cli
nuget pack <project-name>.nuspec
```

Při použití projektu sady Visual Studio spusťte `nuget pack` se souborem projektu, který automaticky načte `.nuspec` soubor projektu a nahradí všechny tokeny v rámci něj pomocí hodnot v souboru projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Použití souboru projektu přímo je nezbytné pro nahrazení tokenu, protože projekt je zdrojem hodnot tokenu. Nahrazení tokenu se nestane, pokud `nuget pack` použijete `.nuspec` se souborem.

Ve všech případech `nuget pack` vyloučí složky, které začínají tečkou, `.git` například nebo `.hg`.

NuGet indikuje, jestli v `.nuspec` souboru nejsou nějaké chyby, které vyžadují opravení, například forgetting, aby se změnily zástupné hodnoty v manifestu.

Po `nuget pack` úspěšném dokončení budete `.nupkg` mít soubor, který můžete publikovat do vhodné galerie, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

> [!Tip]
> Užitečný způsob, jak prostudovat balíček po jeho vytvoření, je otevřít v nástroji [Průzkumník balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) . Získáte tak grafické zobrazení obsahu balíčku a jeho manifestu. Výsledný `.nupkg` soubor můžete také přejmenovat `.zip` na soubor a prozkoumat jeho obsah přímo.

### <a name="additional-options"></a>Další možnosti

Můžete použít různé přepínače příkazového řádku s nástrojem `nuget pack` k vyloučení souborů, přepište číslo verze v manifestu a změnit výstupní složku, a to mimo jiné funkce. Úplný seznam najdete v referenčních informacích k [příkazu Pack](../reference/cli-reference/cli-ref-pack.md).

Následující možnosti jsou běžné v projektech sady Visual Studio:

- **Odkazované projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty jako součást balíčku nebo jako závislosti pomocí `-IncludeReferencedProjects` možnosti:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Tento proces zahrnutí je rekurzivní, takže pokud `MyProject.csproj` odkazy na projekty b a C a tyto projekty odkazují D, E a f, jsou do balíčku zahrnuty soubory z B, C, D, E a f.

    Pokud odkazovaný projekt obsahuje `.nuspec` vlastní soubor, pak NuGet místo toho přidá tento odkazovaný projekt jako závislost.  Tento projekt je nutné zabalit a publikovat samostatně.

- **Konfigurace sestavení**: Ve výchozím nastavení používá NuGet výchozí konfigurační sadu sestavení v souboru projektu, obvykle *ladění*. Chcete-li zabalit soubory z jiné konfigurace sestavení, jako je například `-properties` verze, použijte možnost s konfigurací:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symboly**: Pokud chcete zahrnout symboly, které uživatelům umožňují procházet kód balíčku v ladicím programu, použijte `-Symbols` možnost:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Instalace testovacího balíčku

Před publikováním balíčku obvykle budete chtít otestovat proces instalace balíčku do projektu. Testy zajistí, že všechny soubory v projektu budou mít všechny na správném místě.

Instalaci můžete v aplikaci Visual Studio nebo na příkazovém řádku otestovat ručně pomocí [kroků normální instalace balíčku](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).

Pro automatizované testování je základní proces následující:

1. `.nupkg` Zkopírujte soubor do místní složky.
1. Přidejte složku do zdrojů balíčku pomocí `nuget sources add -name <name> -source <path>` příkazu (viz [zdroje NuGet](../reference/cli-reference/cli-ref-sources.md)). Všimněte si, že tento místní zdroj je potřeba nastavit jenom jednou na daném počítači.
1. Nainstalujte balíček z tohoto zdroje pomocí `nuget install <packageID> -source <name>` , kde `<name>` se shoduje s názvem `nuget sources`vašeho zdroje, jak je uvedeno v. Zadání zdroje zajistí, že se balíček nainstaluje jenom z tohoto zdroje.
1. Kontrolou systému souborů ověřte, zda jsou soubory správně nainstalovány.

## <a name="next-steps"></a>Další kroky

Po vytvoření balíčku, který je `.nupkg` soubor, můžete ho publikovat do Galerie podle svého výběru, jak je popsáno v tématu [publikování balíčku](../nuget-org/publish-a-package.md).

Můžete také chtít zvětšit možnosti vašeho balíčku nebo jinak podporovat jiné scénáře, jak je popsáno v následujících tématech:

- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformace zdrojových a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze verzí](../create-packages/prerelease-packages.md)
- [Nastavení typu balíčku](../create-packages/set-package-type.md)
- [Vytváření balíčků pomocí sestavení zprostředkovatele komunikace s objekty COM](../create-packages/author-packages-with-COM-interop-assemblies.md)

Nakonec existují další typy balíčků, o kterých byste měli vědět:

- [Nativní balíčky](../create-packages/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
