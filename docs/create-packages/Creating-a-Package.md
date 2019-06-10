---
title: Jak vytvořit balíček NuGet
description: Podrobné pokyny k procesu návrhu a vytvoření balíčku NuGet, včetně klíčových rozhodovací body, jako jsou soubory a správy verzí.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 5e362673acfab4b31c8a2e02a521afd8b19d2754
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812916"
---
# <a name="creating-nuget-packages"></a>Vytváření balíčků NuGet

Bez ohledu na to co dělá váš balíček nebo co kódu obsahuje, použít jednu z nástroje rozhraní příkazového řádku, buď `nuget.exe` nebo `dotnet.exe`, do balíčku, které tuto funkci do komponenty, které můžete sdílet s a používat libovolný počet dalších vývojářů. Chcete-li instalovat nástroje rozhraní příkazového řádku NuGet, naleznete v tématu [klientských nástrojů Nugetu nainstalovat](../install-nuget-client-tools.md). Všimněte si, že Visual Studio automaticky nezahrnuje nástroj rozhraní příkazového řádku.

- Pro projekty .NET Core a .NET Standard, které používají formát SDK – vizuální styl ([SDK atribut](/dotnet/core/tools/csproj#additions)), a všechny ostatní sady SDK – vizuální styl projekty, NuGet přímo k vytvoření balíčku používá informace v souboru projektu. Podrobnosti najdete v tématu [vytvořit standardní balíčky .NET se sadou Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) a [NuGet aktualizací Service pack a obnovení jako cílů MSBuild](../reference/msbuild-targets.md).

- Projekty sady SDK styl postupujte podle kroků popsaných v tomto článku vytvořte balíček.

- Pro projekty migrované z `packages.config` k [PackageReference](../consume-packages/package-references-in-project-files.md), použijte [msbuild - t: pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

Technicky vzato balíček NuGet je jenom soubor ZIP, který je byl přejmenován s `.nupkg` rozšíření a jehož obsah odpovídat určité konvence. Toto téma popisuje podrobný postup vytvoření balíčku, který splňuje tyto konvence. Podrobný návod najdete v tématu [rychlý start: vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package.md).

Balení začíná zkompilovaného kódu (sestavení), symboly a/nebo jiné soubory, které má být dodána jako balíček (viz [přehled a pracovní postup](overview-and-workflow.md)). Tento proces je nezávislý na kompilace nebo jinak generování souborů, které patří do balíčku, i když můžete nakreslit z informací v souboru projektu pro synchronizaci kompilované sestavení a balíčky.

> [!Note]
> Toto téma platí pro projekty SDK styl, obvykle projekty jiné než .NET Core a .NET Standard projektů pomocí Visual Studio 2017 a NuGet 4.0 +.

## <a name="deciding-which-assemblies-to-package"></a>Rozhodování o tom, která sestavení do balíčku

Většina pro obecné účely balíčky obsahují jeden nebo více sestavení, které ostatní vývojáři mohou použít ve své vlastní projekty.

- Obecně je vhodné mít jedno sestavení na balíček NuGet, za předpokladu, že každé sestavení je nezávisle na sobě užitečné. Například, pokud máte `Utilities.dll` , který závisí na `Parser.dll`, a `Parser.dll` je užitečné sama o sobě a pak vytvořte jeden balíček pro každého. To umožňuje vývojářům využít `Parser.dll` nezávisle na `Utilities.dll`.

- Pokud vaše knihovna se skládá z více sestavení, které nejsou nezávisle na sobě užitečné, pak je v pořádku je zkombinovat do jednoho balíčku. Použijeme předchozí příklad, pokud `Parser.dll` obsahuje kód, který je používán pouze `Utilities.dll`, pak můžete zachovat `Parser.dll` ve stejném balíku.

- Podobně pokud `Utilities.dll` závisí na `Utilities.resources.dll`, je-li znovu odkazující aktivita není užitečná sama o sobě, potom se spojí i ve stejném balíku.

Prostředky ve skutečnosti představují zvláštní případ. Při instalaci do projektu balíček NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* ty, které jsou pojmenovány `.resources.dll` vzhledem k tomu, že se budou považovat za lokalizovaná satelitní sestavení (viz [ Vytvoření lokalizovaných balíčků](creating-localized-packages.md)). Z tohoto důvodu se vyhněte se použití `.resources.dll` pro soubory, které jinak obsahují základní balíček kódu.

Pokud vaše knihovna obsahuje sestavení vzájemné spolupráce COM, postupujte podle dalších pokynů v [vytváření balíčků pomocí sestavení vzájemné spolupráce COM](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Role a struktura souboru .nuspec souboru

Když víte, jaké soubory, které chcete balíček, dalším krokem je vytvoření manifestu balíčku v `.nuspec` souboru XML.

Manifest:

1. Popisuje obsah balíčku a je součástí balíčku.
1. Vytvoření balíčku a nastaví na tom, jak nainstalovat do projektu balíček NuGet. Například manifest identifikuje další závislosti balíčků tak, aby NuGet můžete nainstalovat také těchto závislostí při instalaci hlavního balíčku.
1. Obsahuje vlastnosti požadované a volitelné, jak je popsáno níže. Naleznete v části najdete přesné informace, včetně dalších vlastností, zde nejsou uvedeny [souboru .nuspec odkaz](../reference/nuspec.md).

Požadované vlastnosti:

- Identifikátor balíčku musí být jedinečný ve galerii, který je hostitelem balíčku.
- Konkrétní verzi číslo ve tvaru *Hlavníverze.podverze.oprava [-přípona]* kde *– přípona* identifikuje [předběžných verzí](prerelease-packages.md)
- Název balíčku jak by se měla objevit na hostiteli (jako je nuget.org)
- Informace o Autor a vlastník.
- Dlouhý popis balíčku.

Společné vlastnosti volitelné:

- Zpráva k vydání verze
- Informace o autorských právech
- Krátký popis [uživatelského rozhraní Správce balíčků v sadě Visual Studio](../tools/package-manager-ui.md)
- ID národního prostředí
- Adresa URL projektu
- Licence jako výraz nebo souboru (`licenseUrl` je zastaralé, použijte [ `license` prvek metadat souboru nuspec](../reference/nuspec.md#license))
- Adresa URL ikony
- Seznam závislosti a odkazy
- Značky, které pomáhají při hledání v galerii

Tady je typické (ale fiktivní) `.nuspec` soubor s komentáři popisující vlastnosti:

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

Podrobnosti o deklarace závislostí a zadání čísla verzí, naleznete v tématu [Správa verzí balíčků](../reference/package-versioning.md). Je také možné na povrchu prostředky od závislostí přímo v balíčku pomocí `include` a `exclude` atributy na `dependency` elementu. Zobrazit [souboru .nuspec Reference - závislosti](../reference/nuspec.md#dependencies).

Protože manifest je součástí balíčku vytvořených z ní, najdete prozkoumáním existující balíčky libovolný počet dalších příkladů. Dobrým zdrojem je *global-packages* složky v počítači, umístění se vrátí následující příkaz:

```cli
nuget locals -list global-packages
```

Přejděte do libovolného *package\version* složka, Kopírovat `.nupkg` do souboru `.zip` souboru a pak otevřete, který `.zip` souboru a zkoumat `.nuspec` v něm.

> [!Note]
> Při vytváření `.nuspec` z projektu sady Visual Studio obsahuje manifest tokeny, které jsou nahrazeny informacemi z projektu při vytváření balíčku. Zobrazit [vytváření souboru .nuspec z projektu sady Visual Studio](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>Vytvoření souboru .nuspec souboru

Vytvoření kompletní manifestu obvykle začíná základní `.nuspec` soubor generovaný prostřednictvím jednoho z následujících metod:

- [Podle úmluvy pracovní adresář](#from-a-convention-based-working-directory)
- [Sestavení knihovny DLL](#from-an-assembly-dll)
- [A Visual Studio project](#from-a-visual-studio-project)    
- [Nový soubor s výchozími hodnotami.](#new-file-with-default-values)

Pak upravíte soubor ručně tak, aby popisuje přesný obsah, který chcete ve finálním balíčku.

> [!Important]
> Vygeneruje `.nuspec` soubory obsahují zástupné symboly, které musí být upravena před vytvořením balíčku s `nuget pack` příkazu. Příkaz selže, pokud `.nuspec` obsahuje zástupné symboly.

### <a name="from-a-convention-based-working-directory"></a>Z pracovního adresáře podle úmluvy

Vzhledem k tomu, že balíček NuGet je jenom soubor ZIP, který je byl přejmenován s `.nupkg` rozšíření, často je nejjednodušší vytvořit strukturu složky na vašem místním systému souborů a pak se vytvořit `.nuspec` souboru přímo z této struktury. `nuget pack` Příkaz automaticky přidá všechny soubory v danou strukturu složek (s výjimkou některou ze složek, které začínají `.`, díky tomu můžete zachovat soukromé soubory ve stejné struktuře).

Výhodou tohoto přístupu je, že nemusíte určit v manifestu soubory, které chcete zahrnout do balíčku (jak je popsáno dále v tomto tématu). Můžete jednoduše použít proces sestavení vytvořit strukturu přesně složka, která přejdou do balíčku a snadno můžete zahrnout další soubory, které nemusí být součástí projektu jinak:

- Obsah a zdrojový kód, který by měl být vloženy do cílový projekt.
- Skripty prostředí PowerShell
- Transformací do existující konfigurace a soubory zdrojového kódu v projektu.

Vytváření složky jsou následující:

| Folder | Popis | Akce při instalaci balíčku |
| --- | --- | --- |
| (uživatel root) | Umístění pro soubor readme.txt | Při instalaci balíčku sady Visual Studio zobrazí soubor readme.txt v kořenovém adresáři balíčku. |
| lib/{tfm} | Sestavení (`.dll`), dokumentace ke službě (`.xml`) a symbol (`.pdb`) soubory pro dané cílové rozhraní Framework Moniker (TFM) | Sestavení jsou přidány jako odkazy pro kompilaci, jakož i modul runtime; `.xml` a `.pdb` zkopírovány do složky projektu. Zobrazit [podpora více cílových platforem](supporting-multiple-target-frameworks.md) pro vytvoření dílčí složky specifické pro cílové rozhraní framework. |
| REF / {tfm} | Sestavení (`.dll`) a symbol (`.pdb`) soubory pro dané cílové rozhraní Framework Moniker (TFM) | Sestavení jsou přidány jako odkazy pouze pro kompilaci; Proto nic budou zkopírovány do složky bin projektu. |
| Moduly runtime | Sestavení specifické pro architekturu (`.dll`), symbol (`.pdb`) a nativní prostředky (`.pri`) soubory | Sestavení jsou přidány jako odkazy pouze na modul runtime; Další soubory jsou zkopírovány do složky projektu. By měl vždy být odpovídající (TFM) `AnyCPU` konkrétní sestavení v rámci `/ref/{tfm}` složky zadejte odpovídající sestavení v době kompilace. Zobrazit [podpora více cílových platforem](supporting-multiple-target-frameworks.md). |
| obsah | Různé soubory | Obsah je zkopírován do kořenového adresáře projektu. Představte si, že **obsah** složky jako kořen cílové aplikace, takže v konečném důsledku využívajícího balíček. Balíček v aplikaci prvku přidat obrázek */obrázky* složku, umístěte ho do balíčku *obsah nebo imagí* složky. |
| sestavení | Nástroj MSBuild `.targets` a `.props` soubory | Automaticky vložit do souboru projektu nebo `project.lock.json` (NuGet 3.x+). |
| nástroje | Skripty prostředí PowerShell a programy, které jsou přístupné z konzole Správce balíčků | `tools` Složka je přidána do `PATH` proměnné prostředí pro konzolu Správce balíčků (konkrétně *není* k `PATH` jako sada pro nástroje MSBuild při sestavování projektu). |

Protože vaše struktura složky může obsahovat libovolný počet sestavení pro libovolný počet cílových platforem, tato metoda je nezbytná, při vytváření balíčků, které podporují více platforem.

V každém případě až budete mít struktuře požadované složky na místě, spusťte následující příkaz v této složce vytvořte `.nuspec` souboru:

```cli
nuget spec
```

Znovu, vygenerované `.nuspec` neobsahuje žádné explicitní odkazy na soubory v této struktuře. NuGet automaticky obsahuje všechny soubory, když se balíček vytvoří. Nevyhnete se ale upravit zástupné hodnoty v ostatních částech v manifestu.

### <a name="from-an-assembly-dll"></a>Ze sestavení knihovny DLL

V jednoduchém případě vytvoření balíčku ze sestavení, můžete vygenerovat `.nuspec` soubor z metadat sestavení pomocí následujícího příkazu:

```cli
nuget spec <assembly-name>.dll
```

Použití této formy nahradí několik zástupných symbolů v manifestu konkrétní hodnoty ze sestavení. Například `<id>` je nastavena na název sestavení, a `<version>` je nastavené na verzi sestavení. Další vlastnosti v manifestu, ale nepoužíváte porovnání hodnot v sestavení a stále tedy obsahovaly zástupné symboly.

### <a name="from-a-visual-studio-project"></a>Z projektu sady Visual Studio

Vytváření `.nuspec` z `.csproj` nebo `.vbproj` souboru je pohodlné, protože další balíčky, které byly nainstalovány do těchto projektu jsou automaticky odkazována jako závislosti. Jednoduše použijte následující příkaz ve stejné složce jako soubor projektu:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Výsledná `<project-name>.nuspec` soubor obsahuje *tokeny* , která se nahradí v době vytváření balíčků hodnotami z projektu, včetně odkazů na další balíčky, které jsou již nainstalovány.

Token je oddělen složenými `$` symboly na obou stranách vlastnosti projektu. Například `<id>` hodnota v manifestu generované v tomto stejně, jako obvykle se zobrazí takto:

```xml
<id>$id$</id>
```

Tento token nahrazen `AssemblyName` hodnotu ze souboru projektu v balení čas. Pro přesné mapování hodnot projektu k `.nuspec` tokeny, najdete v článku [odkazovat na náhradní tokeny](../reference/nuspec.md#replacement-tokens).

Tokeny můžete snížit z by bylo potřeba aktualizovat klíčové hodnoty jako číslo verze v `.nuspec` při aktualizaci projektu. (Můžete vždy nahradit tokeny literálových hodnot v případě potřeby). 

Všimněte si, že existuje několik dalších balení možností k dispozici při práci v projektu sady Visual Studio, jak je popsáno v [spuštění balíčku nuget pro generování souboru .nupkg](#running-nuget-pack-to-generate-the-nupkg-file) později.

#### <a name="solution-level-packages"></a>Balíčky na úrovni řešení

*NuGet 2.x pouze. Ve Správci NuGet 3.0 není k dispozici.*

NuGet 2.x nepodporuje rozeznávání úrovni řešení balíček, který nainstaluje nástroje nebo další příkazy pro konzolu Správce balíčků (obsah `tools` složky), ale přidejte odkazy na obsah, nebo vlastní nastavení pro všechny projekty v sestavení řešení. Tyto balíčky obsahují žádné soubory v její přímé `lib`, `content`, nebo `build` složky a žádný z jejích závislostí mít soubory v jejich `lib`, `content`, nebo `build` složky.

Sleduje NuGet, nainstalované balíčky úrovni řešení v `packages.config` ve `.nuget` složky, nikoli projektu `packages.config` souboru.

### <a name="new-file-with-default-values"></a>Nový soubor s výchozími hodnotami.

Následující příkaz vytvoří výchozí manifest se zástupnými symboly, které zajistí, že začnete s správná struktura:

```cli
nuget spec [<package-name>]
```

Vynecháte-li \<název balíčku\>, je výsledný soubor `Package.nuspec`. Pokud je třeba zadat název `Contoso.Utility.UsefulStuff`, soubor je `Contoso.Utility.UsefulStuff.nuspec`.

Výsledná `.nuspec` obsahuje zástupné symboly pro hodnoty, jako jsou `projectUrl`. Ujistěte se, než je použijete k vytvoření poslední úpravy souboru `.nupkg` souboru.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Výběr balíčku jedinečný identifikátor a nastaví číslo verze

Identifikátor balíčku (`<id>` element) a číslo verze (`<version>` element) jsou dvě nejdůležitější hodnoty v manifestu, protože jednoznačně identifikují přesný kód, který je součástí balíčku.

**Osvědčené postupy pro identifikátor balíčku:**

- **Jedinečnost**: Identifikátor musí být jedinečný mezi nuget.org nebo libovolné galerii hostitelem balíčku. Než se rozhodnete u identifikátoru Prohledat galerii použít ke kontrole, zda název je již používán. Aby nedocházelo ke konfliktům, je použít název vaší společnosti jako první část identifikátoru, jako dobrý vzorek `Contoso.`.
- **Namespace jako názvy**: Postupujte podle vzoru podobný obory názvů v rozhraní .NET, pomocí zápisu s tečkou místo pomlčky. Například použít `Contoso.Utility.UsefulStuff` spíše než `Contoso-Utility-UsefulStuff` nebo `Contoso_Utility_UsefulStuff`. Příjemci také užitečné, když identifikátor balíčku shoduje s obory názvů používané v kódu.
- **Ukázkové balíčky**: Pokud možno vytvořit balíček ukázek kódu, který ukazuje, jak použít jiný balíček, připojit `.Sample` jako příponu k identifikátoru, jako v `Contoso.Utility.UsefulStuff.Sample`. (Ukázkového balíčku by samozřejmě mít závislost na jiný balíček.) Při vytváření balíčku vzorku, použijte podle úmluvy pracovní adresář metody popsané dříve. V `content` složky, uspořádat ukázkový kód do složky s názvem `\Samples\<identifier>` stejně jako v `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Osvědčené postupy pro verze balíčku:**

- Obecně platí nastavte verzi balíčku tak, aby odpovídaly knihovny, i když to není nezbytně nutné. Toto je jednoduché když omezíte balíčku do jednoho sestavení, jak je popsáno výše v [rozhodování o tom, která sestavení do balíčku](#deciding-which-assemblies-to-package). Celkově nezapomeňte, že NuGet, samotné se zabývá verze balíčků při řešení závislostí, nikoli verze sestavení.
- Při použití schématu nestandardní verze, být potřeba vzít v úvahu pravidla NuGet správy verzí, jak je vysvětleno v [Správa verzí balíčků](../reference/package-versioning.md).

> Následující řadu stručný blogové příspěvky jsou také užitečné k pochopení správy verzí:
>
> - [Část 1: S ohledem na knihoven DLL](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Část 2: Základní algoritmus](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [3. část: Sjednocení prostřednictvím přesměrování vazeb](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Nastavení typ balíčku

Nuget 3.5 +, může být označený balíčky s konkrétním *typ balíčku* označující jeho zamýšlené použití. Balíčky není označena jako s typem, včetně všech balíčků, které jsou vytvořené pomocí starší verze balíčku nuget, ve výchozím nastavení `Dependency` typu.

- `Dependency` balíčky typ sestavení nebo runtime prostředky přidat do knihovny a aplikace a může být nainstalován v libovolným typem projektu (za předpokladu, že jsou kompatibilní).

- `DotnetCliTool` Typ balíčky jsou rozšíření [.NET CLI](/dotnet/articles/core/tools/index) a jsou vyvolány z příkazového řádku. Tyto balíčky můžete nainstalovat jenom v projektech .NET Core a nemají žádný vliv na operace obnovení. Další podrobnosti o těchto rozšířeních jednotlivých projektů jsou dostupné v [rozšiřitelnost .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentaci.

- Vlastní typ balíčky pomocí libovolného typu identifikátor, který odpovídá stejná pravidla formát jako ID balíčku. Jakýkoli typ jiný než `Dependency` a `DotnetCliTool`, ale nejsou rozpoznány v aplikaci Správce balíčků NuGet v sadě Visual Studio.

Typy balíčků jsou nastaveny `.nuspec` souboru. Je nejvhodnější pro zpětnou kompatibilitu s *není* explicitně nastaveno `Dependency` zadejte a místo toho přináší setrvávání u NuGet tohoto typu, pokud žádný typ za předpokladu, že je zadán.

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

## <a name="adding-a-readme-and-other-files"></a>Přidání souboru readme a další soubory

Pokud chcete přímo zadat soubory, které chcete zahrnout do balíčku, použijte `<files>` uzlu v `.nuspec` souboru, který *následuje* `<metadata>` značky:

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
> Při použití přístup podle úmluvy pracovní adresář, můžete umístit readme.txt ve svém kořenu a další obsah `content` složky. Ne `<file>` prvky jsou nezbytné v manifestu.

Pokud zahrnete soubor s názvem `readme.txt` v kořenovém adresáři balíčku sady Visual Studio zobrazí obsah tohoto souboru jako prostý text okamžitě po instalaci balíčku přímo. (Soubory Readme nejsou zobrazeny pro balíčky nainstalované jako závislosti). Tady je například jak se zobrazí v souboru readme HtmlAgilityPack balíčku:

![Zobrazit soubor readme pro balíček NuGet při instalaci](media/Create_01-ShowReadme.png)

> [!Note]
> Zadáte-li prázdné `<files>` uzlu `.nuspec` souboru NuGet neobsahuje žádný jiný obsah v balíčku, než co je v `lib` složky.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>Včetně cíle a vlastnosti nástroje MSBuild v balíčku

V některých případech můžete chtít přidat vlastní sestavení cíle nebo vlastnosti v projektech, které využívají vašeho balíčku, například spuštěním vlastní nástroje nebo procesu během sestavování. To provedete tak, že soubory ve formě `<package_id>.targets` nebo `<package_id>.props` (například `Contoso.Utility.UsefulStuff.targets`) v rámci `\build` složky projektu.

Soubory v kořenové složce `\build` složky jsou považovány za vhodný pro všechny cílové architektury. Pro poskytování souborů specifické pro architekturu, nejprve umístíte do příslušné podsložky, jako je následující:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Potom v `.nuspec` souboru, je nutné k odkazování na tyto soubory `<files>` uzlu:

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

Včetně cíle a vlastnosti nástroje MSBuild v balíčku byl [představeny s nástrojem NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), proto se doporučuje přidat `minClientVersion="2.5"` atribut `metadata` element označující minimální verzi klienta NuGet potřeba využívat balíček.

Po instalaci balíček NuGet `\build` soubory, přidá MSBuild `<Import>` elementy v souboru projektu, přejdete `.targets` a `.props` soubory. (`.props` je přidán v horní části souboru projektu. `.targets` je přidán v dolní části.) Samostatné podmíněné MSBuild `<Import>` prvek přidán pro každou cílovou architekturu.

Nástroj MSBuild `.props` a `.targets` soubory pro cílení na různé architektury je možné umístit `\buildMultiTargeting` složky. Během instalace balíčku NuGet přidá odpovídající `<Import>` prvků, které se soubor projektu s podmínkou, která Cílová architektura, která není nastavena (vlastnost MSBuild `$(TargetFramework)` musí být prázdný).

Nuget 3.x cíle nebyly přidány do projektu, ale místo toho jsou k dispozici prostřednictvím `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>Vytváření balíčků pomocí sestavení vzájemné spolupráce COM

Balíčky, které obsahují sestavení vzájemné spolupráce COM musí obsahovat odpovídající [soubor cílů](#including-msbuild-props-and-targets-in-a-package) tak, aby správné `EmbedInteropTypes` do projektů s použitím formátu PackageReference se přidají metadata. Ve výchozím nastavení `EmbedInteropTypes` metadat má vždy hodnotu false pro všechna sestavení zadáním PackageReference tak soubor cílů přidá tato metadata explicitně. Aby nedocházelo ke konfliktům, cílový název by měl být jedinečný; v ideálním případě by použít kombinaci váš název balíčku a sestavení jsou vložené a nahraďte `{InteropAssemblyName}` v níže uvedeném příkladu s danou hodnotou. (Viz také [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) příklad.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Všimněte si, že při použití `packages.config` formátu správy přidávání odkazů na sestavení z balíčků způsobí, že NuGet a sady Visual Studio vyhledat sestavení vzájemné spolupráce COM a nastavit `EmbedInteropTypes` na hodnotu true v souboru projektu. V tomto případě cíle, které jsou přepsaný.

Kromě toho ve výchozím nastavení [tok prostředky sestavení není přechodně](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Balíčky vytvořené podle postupu popsaného tady pracovní odlišně při se berou jako přechodné závislosti z odkazu typu projekt na projekt. Příjemce balíčku můžete zajistí, aby tok tak, že upravíte výchozí hodnotu PrivateAssets tak, aby nezahrnovala sestavení.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>Spuštění balíčku nuget pro generování souboru .nupkg

Při použití sestavení nebo pracovního adresáře založené na konvenci, vytvořit balíček spuštěním `nuget pack` s vaší `.nuspec` souboru, nahradí `<project-name>` s vaší konkrétní název souboru:

```cli
nuget pack <project-name>.nuspec
```

Při použití projektu sady Visual Studio, spusťte `nuget pack` pomocí souboru projektu, který automaticky načte projektu `.nuspec` souboru a nahradí všechny tokeny pomocí hodnot v souboru projektu:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Přímo pomocí souboru projektu je nezbytné pro nahrazování tokenů, protože projekt je zdrojové hodnoty tokenu. Nahrazování tokenů neodehrává používáte `nuget pack` s `.nuspec` souboru.

Ve všech případech `nuget pack` vyloučí složek, které začínají tečkou, jako například `.git` nebo `.hg`.

NuGet uvádí, jestli jsou všechny chyby `.nuspec` soubor, který vyžadují opravu, jako je například zapomínání Chcete-li změnit hodnoty zástupných symbolů v manifestu.

Jednou `nuget pack` proběhne úspěšně, je nutné `.nupkg` souborů, které můžete publikovat do vhodný galerie, jak je popsáno v [publikování balíčku](../create-packages/publish-a-package.md).

> [!Tip]
> Užitečný způsob, jak prozkoumat balíčku po jeho vytvoření je otevřít v [Průzkumníku balíčků](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) nástroj. To poskytuje grafické zobrazení obsahu balíčku a jeho manifestu. Můžete také přejmenovat, výsledná `.nupkg` do souboru `.zip` soubor a seznamte se s jeho obsahem přímo.

### <a name="additional-options"></a>Další možnosti

Můžete použít různé přepínače příkazového řádku s `nuget pack` vyloučit soubory, přepíše číslo verze v manifestu a změňte výstupní složky, kromě jiných funkcí. Úplný seznam najdete [pack informace o příkazech](../tools/cli-ref-pack.md).

Několik, která jsou běžné u projektů sady Visual Studio jsou následující možnosti:

- **Odkazované projekty**: Pokud projekt odkazuje na jiné projekty, můžete přidat odkazované projekty v rámci balíčku, nebo jako závislosti, s použitím `-IncludeReferencedProjects` možnost:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Tento proces zařazení je rekurzivní, pokud tedy `MyProject.csproj` odkazy na projekty B a C a projekty odkazovat D, E a F a soubory z B, C, D, E a F jsou součástí balíčku.

    Pokud obsahuje odkazovaný projekt `.nuspec` soubor sama, pak NuGet přidá tento Odkazovaný projekt jako závislost místo.  Budete muset balíček a publikujte tento projekt samostatně.

- **Konfigurace sestavení**: Standardně používá NuGet výchozí konfigurace sestavení, nastavte v souboru projektu, obvykle *ladění*. Aby zabalil soubory z jiné sestavení konfigurace, jako například *verze*, použijte `-properties` možnost s konfigurací:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symboly**: Chcete-li zahrnout symboly, které umožňují uživatelům procházet kódem balíčku v ladicím programu, použijte `-Symbols` možnost:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Testování instalace balíčku

Před publikováním balíčku se obvykle chcete otestovat proces instalace balíčku do projektu. Testy, zkontrolujte, zda nutně soubory všechny ukládaly do jejich správné umístění v projektu.

Můžete testovat zařízení ručně v sadě Visual Studio nebo na příkazovém řádku pomocí běžných [balíček instalační postup, který](../consume-packages/ways-to-install-a-package.md).

Pro automatizované testování základní proces je následujícím způsobem:

1. Kopírovat `.nupkg` soubor do místní složky.
1. Přidat složku do vašeho zdroje balíčků pomocí `nuget sources add -name <name> -source <path>` příkazu (naleznete v tématu [zdroje nuget](../tools/cli-ref-sources.md)). Všimněte si, že budete potřebovat pouze nastavit tento místní zdroj jednou na jakémkoli daném počítači.
1. Nainstalovat balíček z tohoto zdroje pomocí `nuget install <packageID> -source <name>` kde `<name>` odpovídá názvu zdroje uvedeným `nuget sources`. Zadání zdrojové zajišťuje, že je balíček nainstalován z tohoto zdroje samostatně.
1. Prozkoumání systému souborů ke kontrole, zda jsou správně nainstalovány soubory.

## <a name="next-steps"></a>Další kroky

Jakmile vytvoříte balíček, který je `.nupkg` souboru ji také publikovat podle vašeho výběru v galerii podle popisu v [publikování balíčku](../create-packages/publish-a-package.md).

Můžete také chtít rozšířit možnosti vašeho balíčku nebo jinak podporovala jiné scénáře, jak je popsáno v následujících tématech:

- [Správa verzí balíčků](../reference/package-versioning.md)
- [Podpora více cílových architektur](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformace zdrojového a konfiguračních souborů](../create-packages/source-and-config-file-transformations.md)
- [Lokalizace](../create-packages/creating-localized-packages.md)
- [Předběžné verze](../create-packages/prerelease-packages.md)

Dostupné jsou i další balíčky typů je potřeba vědět:

- [Nativní balíčky](../create-packages/native-packages.md)
- [Balíčky symbolů](../create-packages/symbol-packages.md)
