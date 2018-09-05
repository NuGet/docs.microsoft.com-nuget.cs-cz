---
title: Poznámky k verzi 2.5 NuGet
description: Zpráva k vydání verze pro NuGet 2.5 včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550480"
---
# <a name="nuget-25-release-notes"></a>Poznámky k verzi 2.5 NuGet

[Zpráva k vydání verze NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [zpráva k vydání verze NuGet 2.6](../release-notes/nuget-2.6.md)

25. dubna 2013 byla vydána NuGet 2.5. Tato verze byla tak velká, jsme popisovač compelled přeskočit verze 2.3 a 2.4! Do dnešního dne, jedná se o nejvyšší verzi už nějakou dobu NuGet, se přes [160 pracovní položky](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) ve vydané verzi.

## <a name="acknowledgements"></a>Potvrzení

Rádi bychom vám chceme poděkovat následující externí přispěvatele pro své důležité příspěvky na NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) – přidání MonoAndroid MonoTouch a MonoMac do seznamu známých cílové rozhraní framework identifikátory.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -Opravte pravopis `NuGet.targets` pro velká a malá písmena operačního systému
3. [David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Sestavit řešení sestavit v Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Opravte testování částí v Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -pack příkaz nuget.exe nešíří vlastnosti nástroje MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) – upravit XML kód pro zpracování zachovat formátování.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Přidat rozpoznaná slova do vlastního slovníku umožňující build.cmd proběhla úspěšně.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Opravte testů jednotek při spuštění v lokalizovaných VS.
9. [Garetha Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Extrahované rozhraní z PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -řešit závislosti projektu při balení
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) – podpora vymazat Text heslo při ukládání přihlašovacích údajů ke zdroji balíčku v souborech nuget.cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package opravit Nápověda popis

Tyto jednotlivce vážíme také pro hledání chyb s NuGet 2.5 Beta nebo RC, která byla schválena a opravena dříve než ve finální verzi:

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) – MSTest vs15.6.0 nejnovější NuGet 2.4 a 2,5 sestavení

## <a name="notable-features-in-the-release"></a>Důležité funkce ve verzi

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Povolit uživatelům přepsat soubory obsahu, které již existují.

Jedna z nejžádanějších funkcí celou dobu se stále možnost přepsat soubory obsahu, které již existují na disku, obsažen v balíčku NuGet. Od verze NuGet 2.5, jsou označeny tyto konflikty a zobrazí se výzva k přepsání souborů, zatímco dříve byly tyto soubory vždy přeskočeny.

![Přepsat soubory obsahu](./media/NuGet-2.5/overwrite-file.png)

"nuget.exe aktualizace" a "Install-Package", teď mají novou možnost '-FileConflictAction "můžete nastavit některé výchozí pro scénáře, příkazového řádku.

Nastavte výchozí akce, soubor z balíčku již existuje v na cílový projekt. Nastavte na "Přepsat" vždy přepsat soubory. Chcete-li přeskočit soubory nastavena na hodnotu 'Ignorovat'. Pokud není zadán, bude zadání jednotlivých konfliktních souborů.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatický import MSBuild cíle a soubory vlastností

Na nejvyšší úrovni balíčku NuGet se vytvořila nová složka konvenční.  Jako partnera, který `\lib`, `\content`, a `\tools`, nyní můžete zahrnout `\build` složky v balíčku.  V této složce, můžete umístit dva soubory se přiděleny pevně určené názvy, `{packageid}.targets` nebo `{packageid}.props`. Tyto dva soubory mohou být buď přímo v rámci `build` nebo ve složkách specifické pro architekturu, stejně jako ostatní složky. Pravidlo pro výběr složky nejlépe odpovídající framework je přesně stejné jako ty.

Při instalaci balíčku NuGet se soubory \build přidá MSBuild `<Import>` element v souboru projektu, přejdete `.targets` a `.props` soubory. `.props` Přidá soubor v horní části, že `.targets` přidá soubor do dolní části.

### <a name="specify-different-references-per-platform-using-references-element"></a>Zadejte jiné odkazy na platformě pomocí `<References/>` – element

Před 2.5 v `.nuspec` souboru, uživatele můžete pouze zadat odkaz na soubory, přidat pro všechna rozhraní. Teď s touto novou funkcí v 2.5, lze vytvářet uživatele `<reference/>` – element pro každou podporovanou platformu, například:

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

Tady je postup jak NuGet přidá odkazy na projekty na základě `.nuspec` souboru:

1. Najít `lib` složku, která je vhodné pro cílovou architekturu a získat seznam sestavení z této složky
1. Samostatně najít odkazy na skupinu, která je vhodná pro cílovou architekturu a získat seznam sestavení z dané skupiny. Referenční skupiny bez zadaná Cílová architektura je skupině pro použití náhradní lokality.
1. Zjistí průnik dvou seznamů a použít je jako odkazy pro přidání

Tato nová funkce vám umožní autory balíčku používat funkci odkazy na používání podmnožiny sestavení pro různé platformy, když byste jinak potřebovali pro přenesení duplicitní sestavení ve více `lib` složek.

Poznámka: musí v současné době používáte nuget.exe pack pro použití této funkce; NuGet – Průzkumník balíčků ještě nepodporuje.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Aktualizovat všechny tlačítko pro aktualizaci všech balíčků najednou

Řada z vás vědět o rutině prostředí PowerShell "Update-Package" aktualizovat všechny balíčky; Nyní je snadný způsob, jak to provést prostřednictvím uživatelského rozhraní i.

Vyzkoušet tuto funkci:

1. Vytvoření nové aplikace ASP.NET MVC
1. Spuštění dialogového okna spravovat balíčky NuGet
1. Vyberte možnost aktualizace.
1. Klikněte na tlačítko Aktualizovat vše

![Aktualizovat všechny tlačítko v dialogovém okně](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Vylepšené projektu odkaz na podporu pro nuget.exe Pack

Nyní nuget.exe pack příkaz procesy odkazované projekty pomocí následujících pravidel:

1. Pokud má odkazovaného projektu odpovídající `.nuspec` souboru, například existuje soubor s názvem `proj1.nuspec` ve stejné složce jako `proj1.csproj`, pak tento projekt je přidán jako závislost pro balíček s použitím id a verze číst z `.nuspec` souboru.
1. V opačném případě jsou spojeny soubory odkazovaného projektu do balíčku. Potom projekty odkazuje tento projekt se zpracuje pomocí způsobu rekurzivně sames pravidla.
1. Všechny knihovny DLL, `.pdb`, a `.exe` se přidají soubory.
1. Všechny ostatní soubory obsahu budou přidány.
1. Všechny závislosti jsou sloučeny.

To umožňuje odkazovaného projektu jsou považovány za závislosti, dojde-li `.nuspec` souboru, v opačném případě se stává součástí balíčku.

Další podrobnosti tady: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Přidání vlastnosti "Minimální verze NuGet" k balíčkům

Nový atribut metadat nazývá 'minClientVersion' můžete teď určit minimální verzi klienta NuGet využívat balíček nepotřebujete k tomu.

Tato funkce pomáhá autora balíčku k určení, že balíček bude fungovat až po konkrétní verzi balíčku nuget. Jako nové `.nuspec` funkce byly přidány po NuGet 2.5 balíčky budou moci deklarace identity minimální verze NuGet.

```xml
<metadata minClientVersion="2.6">
```

Pokud má uživatel 2.5 NuGet, nainstalované a balíček je identifikován jako vyžadující 2.6, uživateli zprávu, že nebudou instalovat balíček dostanou vizuální prvky. Uživatel pak by se zobrazil pokyn k aktualizaci jejich verze balíčku nuget.

To bude vylepšují existující prostředí, kde začít balíčky nainstalovat, ale dojde k selhání oznamující, že byl identifikován Nerozpoznaná verze schématu.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Během instalace balíčku už zbytečně aktualizovat závislosti

Před NuGet 2.5 Pokud nainstaloval balíček, který závisí na balíčku již nainstalována v projektu, závislost by aktualizovat jako součást nové instalace i v případě, že stávající verzi vyhověla závislosti.

Od verze NuGet 2.5 při splnění závislostí verze se už, nebudou aktualizovány závislost během instalace dalších balíčků.

**Scénář:**

1. Zdrojové úložiště obsahuje balíček B verze 1.0.0 a 1.0.2. Obsahuje také balíček A závislý na B (> = 1.0.0).
1. Předpokládejme, že aktuální projekt již obsahuje balíček B verze 1.0.0 nainstalované. Chcete nyní nainstalovat balíček A.

**Ve Správci NuGet 2.2 a starší:**

* Při instalaci A balíčku NuGet se automatické aktualizace B 1.0.2, i v případě, že stávající verze 1.0.0 již splňuje omezení verze závislosti, což je > = 1.0.0.

**Ve Správci NuGet 2.5 a novější:**

* NuGet už aktualizuje B, protože rozpozná, že stávající verze 1.0.0 splňuje omezení verze závislosti.

Další informace o této změně najdete podrobné [pracovní položku](http://nuget.codeplex.com/workitem/1681) a také související [diskusní vlákna](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe výstupů požadavky http s podrobnou úroveň podrobností

Pokud řešíte nuget.exe nebo právě zvědaví jaké požadavky HTTP jsou prováděny během operace, "-podrobností podrobné" přepínač se teď výstup všechny požadavky HTTP, které jsou vytvořené.

![Výstup protokolu HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe push nyní podporuje UNC a složku zdroje

Před NuGet 2.5 Pokud se pokus o spuštění "nuget.exe push" ke zdroji balíčku na základě cesty UNC nebo místní složku, že nasdílení změn selže. Díky funkci naposledy přidané hierarchické konfigurace má stát běžné, že nuget.exe potřebovat cílit na zdroji UNC nebo složku nebo založené na protokolu HTTP Galerie NuGet.

Od verze NuGet 2.5, pokud nuget.exe identifikuje zdroj UNC nebo složku, provede kopírování souborů do zdroje.

Následující příkaz bude nyní fungovat:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe podporuje explicitně zadán konfigurační soubory

podporují novou nuget.exe příkazy, které teď přístup ke konfiguraci (všechny s výjimkou "specifikace" a "aktualizací Service pack") "-ConfigFile' možnost, která vynutí konkrétní konfigurační soubor, který se má použít místo výchozí konfigurační soubor v umístění % AppData%\nuget\Nuget.Config.

Příklad:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Podpora pro nativní projekty

NuGet 2.5 nástroje NuGet se teď k dispozici u nativních projektů v sadě Visual Studio. Očekáváme, že většina nativní balíčky budou využívat funkci MSBuild importy výše, pomocí nástroje, vytvořené [CoApp projektu](http://coapp.org). Další informace najdete v článku [podrobné informace o nástroji](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na webu coapp.org.

Název cílového rozhraní framework "nativní" se používá pro balíčky, které mají zahrnout soubory \build \content a \tools při instalaci balíčku do nativního projektu.  \`Lib "složky se nepoužívá pro nativní projekty.
