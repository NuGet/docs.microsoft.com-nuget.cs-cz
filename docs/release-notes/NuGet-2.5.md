---
title: Zpráva k vydání verze NuGet 2,5
description: Poznámky k verzi pro NuGet 2,5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: efcfb9767772c9e27372b4616f817656d51efed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776860"
---
# <a name="nuget-25-release-notes"></a>Zpráva k vydání verze NuGet 2,5

Poznámky k verzi [NuGet 2.2.1](../release-notes/nuget-2.2.1.md)  |  Zpráva k [vydání verze NuGet 2,6](../release-notes/nuget-2.6.md)

NuGet 2,5 byl vydán 25. dubna 2013. Tato verze byla tak velká, budeme nuceni proto přeskočit verze 2,3 a 2,4! To je největší vydání, které jsme měli pro NuGet, s více než [160 pracovními položkami](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) v této verzi.

## <a name="acknowledgements"></a>Poděkování

Rádi bychom pro své významné příspěvky k NuGet 2,5 měli Děkujeme za tyto externí přispěvatele:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )
    - [#2847](https://nuget.codeplex.com/workitem/2847) – přidejte MonoAndroid, MonoTouch a MonoMac do seznamu známých identifikátorů cílových rozhraní .NET Framework.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )
    - [#2865](https://nuget.codeplex.com/workitem/2865) – Oprava pravopisu `NuGet.targets` pro operační systém s rozlišováním velkých a malých písmen
3. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - Zpřístupněte řešení na mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )
    - Opravte selhání testů jednotek mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )
    - příkaz [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack nešíří vlastnosti do nástroje MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#1511](https://nuget.codeplex.com/workitem/1511) – upravený kód pro zpracování XML pro zachování formátování.
7. [Adam petrpo](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - Do vlastního slovníku byla přidána rozpoznaná slova, která umožňují úspěšné sestavení. cmd.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Opravte testy jednotek při spuštění v lokalizovaných VS.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Rozhraní extrahované z PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )
     - [#936](https://nuget.codeplex.com/workitem/936) – zpracovat závislosti projektu při balení
11. [Xavier denákler](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) – při ukládání přihlašovacích údajů ke zdroji balíčků do souborů NuGet. cofig se nepodporuje heslo pro nešifrovaný text.
12. [James obsazení](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )
     - [](http://nuget.codeplex.com/workitem/3190)popis #3190 [#3191](http://nuget.codeplex.com/workitem/3191) opravy Get-Package

Oceňujeme také následující jednotlivce pro vyhledávání chyb s NuGet 2,5 beta/RC, které byly schváleny a opraveny před poslední verzí:

1. [Adam zeď](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )
    - [#3200](https://nuget.codeplex.com/workitem/3200) – MSTest se přerušila s posledními sestaveními NuGet 2,4 a 2,5.

## <a name="notable-features-in-the-release"></a>Významné funkce v této verzi

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Umožní uživatelům přepsat soubory obsahu, které už existují.

Jednou z nejvíce požadovaných funkcí všech možností je možnost přepsat soubory obsahu, které už na disku existují, když jsou zahrnuté v balíčku NuGet. Počínaje verzí NuGet 2,5 se tyto konflikty identifikují a budete vyzváni k přepsání souborů, zatímco předchozí soubory byly vždycky přeskočeny.

![Přepsat soubory obsahu](./media/NuGet-2.5/overwrite-file.png)

nuget.exe Update a Install-Package teď mají novou možnost-FileConflictAction pro nastavení některých výchozích možností pro scénáře příkazového řádku.

Nastaví výchozí akci, když soubor z balíčku již v cílovém projektu existuje. Pokud chcete soubory vždycky přepsat, nastavte na overwrite. Pokud chcete přeskočit soubory, nastavte na Ignore. Pokud není zadaný, zobrazí se výzva k zadání každého kolidujícího souboru.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatický import cílů a souborů props nástroje MSBuild

Na nejvyšší úrovni balíčku NuGet se vytvořila nová konvenční složka.  Jako partner `\lib` , `\content` a `\tools` můžete teď do `\build` balíčku přidat složku.  V rámci této složky můžete umístit dva soubory s pevnými názvy `{packageid}.targets` nebo `{packageid}.props` . Tyto dva soubory mohou být buď přímo pod, `build` nebo pod rámec rozhraní specifického pro rozhraní, stejně jako ostatní složky. Pravidlo pro vybírání složky rozhraní, které nejlépe odpovídá, je přesně stejné jako v těchto.

Když NuGet nainstaluje balíček se soubory \Build, přidá `<Import>` do souboru projektu element MSBuild, který odkazuje na `.targets` `.props` soubory a. `.props`Soubor se přidá v horní části, zatímco `.targets` soubor se přidá do dolní části.

### <a name="specify-different-references-per-platform-using-references-element"></a>Zadejte různé odkazy na platformu pomocí `<References/>` elementu.

Před 2,5, v `.nuspec` souboru může uživatel určit pouze referenční soubory, které mají být přidány pro všechna rozhraní. Nyní s touto novou funkcí v 2,5 může uživatel vytvořit `<reference/>` element pro každou podporovanou platformu, například:

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

Tady je postup, jak NuGet přidává odkazy na projekty založené na `.nuspec` souboru:

1. Vyhledejte `lib` složku, která je vhodná pro cílovou architekturu a získejte seznam sestavení z této složky.
1. Samostatně najít skupinu odkazů, která je vhodná pro cílovou architekturu a získat seznam sestavení z této skupiny. Referenční skupina bez cílového rozhraní je určená pro záložní skupinu.
1. Vyhledejte průnik dvou seznamů a použijte je jako odkazy na přidání.

Tato nová funkce umožní autorům balíčků použít funkci References k použití dílčích sad sestavení v různých rozhraních, pokud by jinak musela přenášet duplicitní sestavení ve více `lib` složkách.

Poznámka: k použití této funkce je nutné, abyste používali sadu nuget.exe Pack. Průzkumník balíčků NuGet ho ještě nepodporuje.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Tlačítko Aktualizovat vše, aby bylo možné aktualizovat všechny balíčky najednou

Spousta informací o rutině Update-Package prostředí PowerShell pro aktualizaci všech balíčků; Teď je to snadný způsob, jak to provést také v uživatelském rozhraní.

Tuto funkci můžete vyzkoušet takto:

1. Vytvoření nové aplikace ASP.NET MVC
1. Spuštění dialogového okna spravovat balíčky NuGet
1. Vybrat aktualizace
1. Klikněte na tlačítko Aktualizovat vše.

![Tlačítko Aktualizovat vše v dialogovém okně](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Vylepšená podpora odkazů na projekt pro sadu nuget.exe Pack

Nyní nuget.exe procesy příkazu Pack na odkazované projekty s následujícími pravidly:

1. Pokud má odkazovaný projekt odpovídající `.nuspec` soubor, například soubor `proj1.nuspec` s názvem ve stejné složce jako `proj1.csproj` , pak je tento projekt přidán jako závislost k balíčku pomocí ID a verze načtené ze `.nuspec` souboru.
1. V opačném případě jsou soubory odkazovaného projektu seskupeny do balíčku. Projekty, na které se odkazuje tento projekt, budou zpracovávány pomocí rekurzivních pravidel.
1. `.pdb`Jsou přidány všechny soubory DLL, a `.exe` .
1. Všechny ostatní soubory obsahu jsou přidány.
1. Všechny závislosti jsou sloučeny.

To umožňuje, aby odkazovaný projekt byl považován za závislost, pokud je `.nuspec` soubor, v opačném případě se jedná o součást balíčku.

Další podrobnosti najdete tady: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Přidejte do balíčků vlastnost minimální verze NuGet.

Nový atribut metadat nazvaný "minClientVersion" teď může indikovat minimální verzi klienta NuGet, která se vyžaduje ke spotřebování balíčku.

Tato funkce pomáhá autorovi balíčku určit, že balíček bude fungovat až po konkrétní verzi NuGetu. `.nuspec`Po přidání nových funkcí po NuGet 2,5 budou balíčky schopné vyžádat si minimální verzi NuGet.

```xml
<metadata minClientVersion="2.6">
```

Pokud má uživatel nainstalovanou NuGet 2,5 a balíček je identifikovaný jako vyžadování 2,6, budou se uživatelům, kteří budou k balíčku instalovat, přidávat vizuální pomůcky. Uživatel pak bude s asistencí aktualizovat verzi NuGet.

Tím se vylepšit existující prostředí, ve kterém se balíčky začnou instalovat, ale pak selže, což znamená, že byla zjištěna Nerozpoznaná verze schématu.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Závislosti se už nemusejí aktualizovat při instalaci balíčku.

Po instalaci balíčku NuGet 2,5, který je závislý na balíčku, který už je v projektu nainstalovaný, by se závislost aktualizovala jako součást nové instalace, i když existující verze splnila závislost.

Počínaje verzí NuGet 2,5, pokud je už verze závislosti splněná, závislost se během dalších instalací balíčku neaktualizuje.

**Scénář:**

1. Zdrojové úložiště obsahuje balíček B s verzí 1.0.0 a 1.0.2. Obsahuje také balíček A, který má závislost na B (>= 1.0.0).
1. Předpokládejme, že aktuální projekt již má nainstalován balíček B verze 1.0.0. Nyní chcete nainstalovat balíček A.

**V NuGet 2,2 a starší:**

* Při instalaci balíčku A se NuGet automaticky aktualizuje B na 1.0.2, i když existující verze 1.0.0 už splňuje omezení verze závislosti, což je >= 1.0.0.

**V NuGet 2,5 a novějších verzích:**

* NuGet už nebude aktualizovat B, protože detekuje, že stávající verze 1.0.0 splňuje omezení verze závislosti.

Pro další informace o této změně si přečtěte podrobnou [pracovní položku](http://nuget.codeplex.com/workitem/1681) a související [diskusní vlákno](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe výstup požadavků HTTP s detailní podrobností

Pokud řešíte řešení potíží nuget.exe nebo stačí zajímá, jaké požadavky HTTP jsou během operací provedeny, přepínač "-detailed Details" nyní vypíše všechny provedené požadavky HTTP.

![Výstup HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe push teď podporuje zdroje ve formátu UNC a složky

Pokud se při pokusu o spuštění příkazu ' nuget.exe push ' do zdroje balíčku na základě cesty UNC nebo místní složky pokusíte spustit příkaz ' push ', nabízená oznámení selže. 2,5 Díky funkci nedávno přidané hierarchické konfigurace se stala společná nuget.exe, aby bylo potřeba cílit buď na zdroj UNC nebo složku, nebo na galerii NuGet založenou na protokolu HTTP.

Pokud nuget.exe identifikuje zdroj UNC nebo složky, počínaje verzí NuGet 2,5, provede kopírování souborů do zdroje.

Nyní bude fungovat následující příkaz:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe podporuje explicitně zadané konfigurační soubory.

nuget.exe příkazy, které přistupují ke konfiguraci (vše kromě "spec" a "Pack"), teď podporují novou možnost-ConfigFile, která vynutí použití konkrétního konfiguračního souboru místo výchozího konfiguračního souboru v% data% \nuget\Nuget.Config.

Příklad:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Podpora pro nativní projekty

S NuGet 2,5 je teď k dispozici nástroj NuGet pro nativní projekty v aplikaci Visual Studio. Očekáváme, že většina nativních balíčků bude používat funkci importu MSBuild výše, a to pomocí nástroje vytvořeného [projektem CoApp](http://coapp.org). Další informace najdete v [podrobnostech o nástroji](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na webu coapp.org.

V případě, že se balíček nainstaluje do nativního projektu, zavádí se pro balíčky, které obsahují soubory v \Build, \Content a \Tools, název cílového rozhraní Framework "Native".  \`Složka lib se nepoužívá pro nativní projekty.
