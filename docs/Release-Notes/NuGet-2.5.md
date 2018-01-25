---
title: "Poznámky k verzi NuGet 2.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 2.5 NuGet."
keywords: "NuGet 2.5 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2c6cf85b9ebccf200be9ef4a2bf96802cffcaea
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-25-release-notes"></a>Poznámky k verzi 2,5 NuGet

[Poznámky k verzi NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 poznámky k verzi](../release-notes/nuget-2.6.md)

NuGet 2.5 byla vydána 25. dubna 2013. Tato verze byla tak velká, jsme popisovač compelled tak, aby přeskočil verze 2.3 a 2.4! Dosud se největší verzi jsme jste měli pro NuGet, se přes [160 pracovní položky](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) ve verzi.

## <a name="acknowledgements"></a>Potvrzení

Rádi bychom se Děkujeme, že následující externí přispěvatele pro jejich významné příspěvky k NuGet 2.5:

1. [ADAM Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -přidat MonoAndroid, MonoTouch a MonoMac do seznamu identifikátorů známé target framework.
1. [G. Aragoneses Andresu](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -Opravte pravopis `NuGet.targets` pro malá a velká písmena operačního systému
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Ujistěte se, vychází z Mono řešení.
1. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Testování částí v Mono opravte.
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe pack příkaz nešířily vlastností nástroje MSBuild
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) – upravit XML kód pro zpracování zachovat formátování.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Přidat rozpoznaný slova slovníku umožňující build.cmd proběhla úspěšně.
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Opravte testů jednotek při spuštění v lokalizovaných VS.
1. [Zařízení Evans Gareth](https://www.codeplex.com/site/users/view/garethevans)
    - Extrahované rozhraní PackageService
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -zpracování závislosti projektu při balení
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -podpora vymazat Text heslo při ukládání přihlašovacích údajů zdroje balíčku v souborech nuget.cofig
1. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) – popis opravte Get-Package nápovědy

Děkujeme také následující jednotlivce pro vyhledání chyby s NuGet 2.5 Beta nebo RC, které byly schválené a opravit dřív, než finální verzi:

1. [ADAM Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) – Mstestu přerušený s nejnovější NuGet 2.4 a 2,5 sestavení

## <a name="notable-features-in-the-release"></a>Upozorňují na důležité funkce ve verzi

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Povolit uživatelům přepsat soubory obsahu, které již existují.

Jednou z nejžádanějších funkcí celou dobu byla možnost přepsat soubory obsahu, které již existují na disku, obsažen v balíčku NuGet. Od verze NuGet 2.5, jsou identifikovány tyto konflikty a zobrazí se výzva k přepsání souborů, zatímco dříve byly tyto soubory vždy přeskočeny.

![Přepsat soubory obsahu](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe aktualizace' a 'Install-Package"teď mají novou možnost '-FileConflictAction, můžete nastavit některé výchozí pro scénáře příkazového řádku.

Nastavte výchozí akce, soubor z balíčku již existuje v cílové projektu. Nastavte na "přepsat, aby vždy přepsat soubory. Přeskočit soubory nastavena na hodnotu 'Ignorovat'. Pokud není zadáno, zobrazí výzvu pro každý konfliktní soubor.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Automatické import MSBuild cíle a soubory props

Byla vytvořena konvenční novou složku na nejvyšší úrovni balíček NuGet.  Jako partnera, který `\lib`, `\content`, a `\tools`, teď můžete zahrnout `\build` složky v balíčku.  V této složce, můžete umístit dva soubory s pevnou názvy `{packageid}.targets` nebo `{packageid}.props`. Tyto dva soubory mohou být buď přímo `build` nebo pod konkrétní rozhraní složky stejně jako jiných složkách. Pravidlo pro výběr nejlépe odpovídající složku je přesně stejné jako ty.

Při instalaci balíčku NuGet se soubory \build přidá MSBuild `<Import>` element v souboru projektu přejdete `.targets` a `.props` soubory. `.props` Soubor přidán v horní části, zatímco `.targets` soubor přidán do dolní části.

### <a name="specify-different-references-per-platform-using-references-element"></a>Zadejte jiný odkazy na platformě pomocí `<References/>` – element

Před 2.5 v `.nuspec` souboru uživatele můžete jenom zadat referenčních souborů, který se má přidat pro všechny framework. Teď pomocí této nové funkce v 2.5, můžete vytvořit uživatele `<reference/>` element pro každou podporovanou platformu, například:

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

Tady je postup pro jak NuGet přidá odkazy na projekty na základě `.nuspec` souboru:

1. Najít `lib` složku, která je vhodná pro cílové rozhraní a získat seznam sestavení z této složky
1. Samostatně najít odkazuje na skupinu, která je vhodná pro cílové rozhraní a získat seznam sestavení z dané skupiny. Referenční dokumentace skupina bez cílovém Frameworku, zadaný je záložní skupina.
1. Zjistí průnik dva seznamy a použít jej jako odkazy pro přidání

Tato nová funkce vám umožní použít funkci odkazy na používání podmnožiny sestavení pro různé architektury, když byste jinak potřebovali pro přenos duplicitní sestavení v několika autorům balíček `lib` složek.

Poznámka: v současné době můžete nuget.exe pack k použití této funkce; Průzkumník balíček NuGet ještě ji nepodporuje.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Aktualizovat všechny tlačítko umožňující aktualizuje všechny balíčky současně

Řada z vás vědět o rutiny prostředí PowerShell "Balíček aktualizace" k aktualizaci všech vašich balíčků; Nyní je snadný způsob, jak to provést prostřednictvím uživatelského rozhraní také.

Můžete vyzkoušet tuto funkci na:

1. Vytvoření nové aplikace ASP.NET MVC
1. Spustit dialogové okno Spravovat balíčky NuGet
1. Vyberte možnost aktualizace.
1. Klikněte na tlačítko Aktualizovat vše

![Aktualizovat všechny tlačítka v dialogovém okně](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Vylepšené projektu odkaz na podporu pro nuget.exe Pack

Nyní nuget.exe pack příkaz procesy odkazuje projekty s následující pravidla:

1. Pokud odkazovaný projekt má odpovídající `.nuspec` souboru, například je do souboru s názvem `proj1.nuspec` ve stejné složce jako `proj1.csproj`, pak je tento projekt přidal jako závislost do balíčku, pomocí id a verzi čtení z `.nuspec` souboru.
1. Soubory odkazované projektu, jinak jsou seskupeny do balíčku. Potom projekty odkazuje tento projekt budou zpracovány pomocí rekurzivně pravidla sames.
1. Všechny knihovny DLL, `.pdb`, a `.exe` soubory budou přidány.
1. Všechny ostatní soubory obsahu budou přidány.
1. Všechny závislosti jsou sloučeny.

To umožňuje odkazované projektu jsou považovány za závislost, pokud dojde `.nuspec` souboru, jinak, stane se součástí balíčku.

Další podrobnosti zde: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Přidat do balíčků vlastnost 'minimální verze NuGet.

Nový atribut metadat volat 'minClientVersion' můžete teď určit minimální verzi klienta NuGet požadované využívat balíček.

Tato funkce vám pomůže balíček autorovi určit, že balíček bude fungovat až po konkrétní verzi NuGet. Nový `.nuspec` funkce jsou přidány po NuGet 2.5 balíčky budou moci deklarace minimální verze NuGet.

```xml
<metadata minClientVersion="2.6">
```

Pokud má uživatel 2.5 NuGet, které jsou nainstalované a balíček je označený jako vyžadující 2.6, bude mu udělená vizuální upozornění na uživatele, což značí, že nebudou instalovat balíček. Uživatele se pak řídí k aktualizaci jejich verze balíčku NuGet.

Tím se zvyšuje na stávající prostředí balíčky, kde začít instalovat, ale pak neúspěšné, což značí, že byla identifikována ve schématu nerozpoznané verzi.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Závislosti jsou už zbytečně aktualizován v průběhu instalace balíčku

Před 2.5 NuGet Pokud byla nainstalována balíček, který závisí na balíčku již nainstalované v projektu, závislost by aktualizovat v rámci nové instalace i v případě, že stávající verze uspokojit závislost.

Od verze NuGet 2.5, pokud je již splnit verze závislosti, závislost nebude aktualizován v průběhu jiné instalace balíčku.

**Scénář:**

1. Zdrojové úložiště obsahuje balíček B s verzí 1.0.0 a 1.0.2. Obsahuje taky balíčku A, který má závislost na B (> = 1.0.0).
1. Předpokládejme, že aktuální projekt již obsahuje verze balíčku B 1.0.0 nainstalována. Teď chcete nainstalovat balíček A.

**V NuGet 2.2 nebo starší:**

* Při instalaci balíčku A, NuGet bude automaticky aktualizován B na verzi 1.0.2, i když stávající verzi 1.0.0 již splňuje omezení verze závislosti, což je > = 1.0.0.

**V NuGet 2,5 a novější:**

* NuGet už zaktualizuje B, protože zjistí, že stávající verzi 1.0.0 splňuje omezení verze závislosti.

Další informace o této změně, najdete v podrobné [pracovní položka](http://nuget.codeplex.com/workitem/1681) a také související [diskusní téma](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe výstupy požadavky http s podrobné podrobností

Pokud jsou řešení potíží s nuget.exe nebo právě zvědaví jaké požadavky HTTP jsou vytvářeny během operací '-podrobností podrobné ' přepínač teď výstup všech požadavků HTTP, které jsou provedeny.

![Výstup HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe nabízené teď podporuje UNC a složku zdroje

Před NuGet 2.5 Pokud jste se pokusili spustit "nuget.exe push" ke zdroji balíčku na základě cesty UNC nebo místní složky nabízeného oznámení skončí s chybou. Nedávno přidané hierarchické konfigurace funkce s měl stát běžné nuget.exe potřebovat cílit na zdroji UNC nebo složku nebo Galerie NuGet založené na protokolu HTTP.

Od verze NuGet 2.5, pokud nuget.exe identifikuje zdroj UNC nebo složku, provede kopírování souborů do zdroje.

Nyní bude fungovat následující příkaz:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe podporuje explicitně zadat konfigurační soubory

podporují novou nuget.exe příkazy, které nyní získat přístup ke konfiguraci, (všechny kromě 'specifikace' a 'pack') '-ConfigFile' možnost, která vynutí konkrétní konfiguračním souboru, který se má použít místo výchozí konfigurační soubor % AppData%\nuget\Nuget.Config.

Příklad:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Podpora pro nativní projekty

S NuGet 2.5 nástrojů NuGet je teď dostupná pro nativní projekty v sadě Visual Studio. Očekáváme, že většina nativní balíčky budou využívat funkci MSBuild importy výš, pomocí nástroje vytvořené [CoApp projektu](http://coapp.org). Další informace najdete v tématu [podrobné informace o nástroji](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na webu coapp.org.

Název cílové rozhraní "nativní" byla zavedená pro balíčky vložení souborů do \build, \content a \tools při instalaci balíčku do k nativnímu projektu.  \`Lib, složky, se nepoužije pro nativní projekty.
