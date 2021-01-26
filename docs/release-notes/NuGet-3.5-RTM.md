---
title: Poznámky k verzi NuGet 3,5 RTM
description: Poznámky k verzi pro NuGet 3,5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776347"
---
# <a name="nuget-35-release-notes"></a>Zpráva k vydání verze NuGet 3,5

Poznámky k verzi [pro NuGet 3,5 – RC](../release-notes/nuget-3.5-RC.md)  |  [Poznámky k verzi NuGet 4,0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Opravy chyb

* Pack nepoužívá MSBuild 14,1 na mono- [#3550](https://github.com/NuGet/Home/issues/3550)

* Karta aktualizace nevybere nejnovější dostupnou verzi, kterou chcete aktualizovat místo toho vyberte možnost aktuální nainstalovaná verze – [#3498](https://github.com/NuGet/Home/issues/3498)

* Opravte chybu po ověření privátního informačního kanálu v2 MyGet a kliknutím na Zobrazit x další výsledky – [#3469](https://github.com/NuGet/Home/issues/3469)

* Zprávy protokolu se zdají být v opačném pořadí pro uživatelské rozhraní [#3446](https://github.com/NuGet/Home/issues/3446)

* v 3.4.4 – obnovení NuGet vyvolá "formát dané cesty se nepodporuje"- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3,6 beta nedodržuje-Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* IKVM zpomalit instalaci na velký projekt – [#3428](https://github.com/NuGet/Home/issues/3428)

* Aktualizace nuget.exe – sám sebe zachovává aktualizaci sebe sama [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 instalace/obnovení ze sdílené složky UNC má na výkon regresi z 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355)

* Chyba při instalaci MOQ z uživatelského rozhraní pro správu balíčků pro projekt net451 – [#3349](https://github.com/NuGet/Home/issues/3349)

* Karta instalovat na úrovni řešení nezobrazuje verzi balíčku [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` aktualizace z nainstalované karty ztratí stav – [#3303](https://github.com/NuGet/Home/issues/3303)

* Sada NuGet Pack na `.csproj` ignorování prázdných souborů v `.nuspec` souboru [#3257](https://github.com/NuGet/Home/issues/3257)

* Projekty webů hostované ve službě IIS by neměly způsobit selhání obnovení- [#3235](https://github.com/NuGet/Home/issues/3235)

* Pověření nebyla načtena z Nuget.Config, když hodnota V3 Endpoint přesměrovává na v2- [#3179](https://github.com/NuGet/Home/issues/3179)

* Sada NuGet Pack nemůže přeložit sestavení při načítání metadat přenositelného sestavení- [#3128](https://github.com/NuGet/Home/issues/3128)

* NuGet nejde najít `msbuild.exe` na mono- [#3085](https://github.com/NuGet/Home/issues/3085)

* Sada nuget.exe Pack nepovoluje značku předběžného vydání, která začíná čísly- [#1743](https://github.com/NuGet/Home/issues/1743)

* instalace balíčku NuGet se na VS2015E nezdařila – [#1298](https://github.com/NuGet/Home/issues/1298)

* Hodnota allowedversions filtr nepracuje na úrovni řešení – [#333](https://github.com/NuGet/Home/issues/333)

* Operace obnovení se náhodně nezdařila, protože položka se stejným klíčem již byla přidána. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nejde nainstalovat NuGet. Common v `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635) .

* Když použijete uživatelské rozhraní k vyhledání zdroje v2, FindPackagesById se pro každé ID – pojmenuje dvakrát. – [#2517](https://github.com/NuGet/Home/issues/2517)

* Balíčky nemůžou záviset na projektech – [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack – vyloučení je dokumentováno, ale není podporováno – [#2284](https://github.com/NuGet/Home/issues/2284)

* Problémy s chybovými zprávami, pokud je oddíl ' contentFiles ' `.nuspec` neplatný – [#1686](https://github.com/NuGet/Home/issues/1686)

* Push vždycky odesílá celý balíček dvakrát pomocí ověřených zdrojů balíčků – [#1501](https://github.com/NuGet/Home/issues/1501)

* Nebyly zadány žádné informace při volání nuget.exe Update *. csproj, ale projekt nemá `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` obnovení se neopakuje u stavových kódů 5xx ze zdrojů v2 – [#1217](https://github.com/NuGet/Home/issues/1217)

* Dvojitá tečka v souboru src v `.nuspec` nefunguje – [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR Restore musí ignorovat informační kanály s [#2942](https://github.com/NuGet/Home/issues/2942) šifrování.

* Zpracování 403 nuget.exe push – nesprávné zobrazení výzvy k zadání přihlašovacích údajů – [#2910](https://github.com/NuGet/Home/issues/2910)

* Aktualizace NuGet prostřednictvím Správce balíčků odebere z `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888) vlastnosti.

* NuGet. PackageManagement. VisualStudio se pokusí načíst "NuGet. TeamFoundationServer14", ale název této knihovny DLL se změnil na "NuGet. TeamFoundationServer"- [#2857](https://github.com/NuGet/Home/issues/2857)

* Uživatelské rozhraní Správce balíčků nezobrazuje nově aktualizovanou verzi [#2828](https://github.com/NuGet/Home/issues/2828)

* Update-Package pokus o použití PackageID, verze místo balíčku. Version- [#2771](https://github.com/NuGet/Home/issues/2771)

* v případě, že projekt nepoužívá NuGet ( `packages.config` nebo `project.json` ) – [#2766](https://github.com/NuGet/Home/issues/2766) , by se měla chyba NuGet Restore csproj.

* Chyba TFS "[soubor] není ve vašem pracovním prostoru nalezena, nebo nemáte oprávnění k přístupu" během upgradu nebo odinstalace, když je řešení/projekt svázán se správou zdrojových kódů TFS- [#2739](https://github.com/NuGet/Home/issues/2739)

* balíček aktualizace nezíská závislosti pro balíčky, které nejsou cílové, [#2724](https://github.com/NuGet/Home/issues/2724)

* Neexistuje žádný způsob, jak nastavit úroveň podrobností protokolů pro akce uživatelského rozhraní Správce balíčků NuGet – [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfigurace NuGet je neplatná – VS 2015 VSIX (v 3.4.3) – [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nefunguje [#2653](https://github.com/NuGet/Home/issues/2653)

* vydaná verze NuGet 3.4.3-získání hodnoty nemůže být null při sestavení balíčku- [#2648](https://github.com/NuGet/Home/issues/2648)

* příkaz Restore nepoužívá uložená pověření z Nuget.Config pro informační kanály VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--ConfigFile je relativní k projektu dir místo příkazového řádku cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)

* Nadměrný příděl v comparsion kódu verze – [#2632](https://github.com/NuGet/Home/issues/2632)

* Víc instancí nuget.exe, který se pokouší nainstalovat stejný balíček paralelně, způsobí [#2628](https://github.com/NuGet/Home/issues/2628) typu Double-Write.

* Informace o závislostech nejsou ukládány do mezipaměti pro operace více projektů – [#2619](https://github.com/NuGet/Home/issues/2619)

* Nainstalovat a aktualizovat balíčky pro stahování bez kontroly složky balíčků jako první [#2618](https://github.com/NuGet/Home/issues/2618)

* Pokud je seznam zdrojů balíčků prázdný, nejde přidat zdroj balíčku prostřednictvím uživatelského rozhraní (NuGet 3.4. x) – [#2617](https://github.com/NuGet/Home/issues/2617)

* Zavádějící Chyba při pokusu o instalaci balíčku, který závisí na době návrhu Facade- [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalace balíčku z konzoly PackageManager s nastavením "vše" se snaží pouze první zdroj – [#2557](https://github.com/NuGet/Home/issues/2557)

* Nejnovější beta verze rozzipovává ModernHttpClient – [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 chyby při spuštění s využitím samočinně připraveného 3.4.1U NuGet- [#2419](https://github.com/NuGet/Home/issues/2419)

* Příkaz Update může být trochu podrobnější, pokud si ho vyžádáme...- [#2418](https://github.com/NuGet/Home/issues/2418)

* Místně sestavený VSIX by měl mít stejné knihovny DLL a soubory jako sestavení CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Oprava upozornění na downgrade NuGet v sestavení – [#2396](https://github.com/NuGet/Home/issues/2396)

* Neúspěšné ověření zdroje balíčku (3 časy) je blokované [#2362](https://github.com/NuGet/Home/issues/2362)

* Obsah balíčku se neobnovil správně při instalaci balíčku z kanálu NuGet v 3.3 + s argumentem-bez mezipaměti, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)

* Instalace NuGet se všemi zdroji balíčků, ale chybějící balíček v 1 zdroji, [#2322](https://github.com/NuGet/Home/issues/2322) se nezdařil.

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt; c__DisplayClass_0 + &lt; &lt; AddReference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Nainstalovat bloky v případě neúspěšného ověření u jednoho zdroje – [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Rozsah verze by měl přepsat-IncludeReferencedProjects verze- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package velmi pomalu – probíhá pokus o shromáždění informací o závislostech "- [#1909](https://github.com/NuGet/Home/issues/1909)

* Balíček NuGet s degradací downgrade se zabalí, když dávka aktualizuje své závislosti – [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe Update zruší silný název sestavení a soukromý atribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Relativní cesta k souboru pro "DefaultPushSource" – [#1746](https://github.com/NuGet/Home/issues/1746)

* Vylepšit zprávy o chybách překladače – [#1373](https://github.com/NuGet/Home/issues/1373)

* příkaz Update-Package v v3 se nezdařil s balíčky, které nejsou v zadaném zdrojovém [#1013](https://github.com/NuGet/Home/issues/1013) .

* Používání relativních cest pro zdroje balíčků je problematické při použití [#865](https://github.com/NuGet/Home/issues/865)

* Chybějící závislost v NUPKG-File vygenerované z projektu, pokud již existuje nepřímá závislost s požadavkem nižší verze – [#759](https://github.com/NuGet/Home/issues/759)

* Odstranění projektu zavře odpovídající okno uživatelského rozhraní, ale Přejmenování projektu nejmenuje okno uživatelského rozhraní. Všimněte si, že PMC naslouchat Přejmenování projektu a události odebrání projektu – [#670](https://github.com/NuGet/Home/issues/670)

* [Webové zatížení Willow] Vytváření zablokování Razor V3 WSP – [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalace nebo obnovení určitého balíčku se nezdařila s názvem "balíček obsahuje více souborů nuspec". - [#3231](https://github.com/NuGet/Home/issues/3231)

* Malá ID & `packages.config` scénářích – [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5 – beta2] Při obnovení balíčku se nepovedlo obnovit starší balíčky – [#3208](https://github.com/NuGet/Home/issues/3208)

* sada NuGet Pack nuceně přidává soubory. TT do složky obsahu bez ohledu na to, co [#3203](https://github.com/NuGet/Home/issues/3203)

* aktualizace – balíček webové aplikace ASP.NET generuje upozornění související se souborem: Source- [#3194](https://github.com/NuGet/Home/issues/3194)

* Chyba sady NuGet Pack csproj (with `project.json` ), pokud v souboru JSON nejsou žádné packOptions a Owner – [#3180](https://github.com/NuGet/Home/issues/3180)

* sada NuGet Pack pro `project.json` ignoruje značky packOptions, jako jsou souhrn, autoři, vlastníci atd. [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException přes NuGet. balení. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160)

* Sada NuGet Pack ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizace více balíčků s vrácením změn ponechá projekt v nefunkčním stavu – [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles v případě, že nejsou přidány pro projekty netstandard – [#3118](https://github.com/NuGet/Home/issues/3118)

* Nelze zabalit správně cílení knihovny na .NET standard- [#3108](https://github.com/NuGet/Home/issues/3108)

* Soubor – > nový projekt – > knihovna tříd (přenosná) projekt se nezdařil v VS2015 a Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)

* Chyba nuGet – 1.0.0-* není platný řetězec verze – [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package se nepovede zobrazit, ale funguje Install-Package [#3068](https://github.com/NuGet/Home/issues/3068)

* Chyba při instalaci balíčku jQuery. ověření na dev15- [#3061](https://github.com/NuGet/Home/issues/3061)

* sada NuGet Pack pro xproj je nastavená na neplatnou cílovou cestu – [#3060](https://github.com/NuGet/Home/issues/3060)

* Při instalaci VS 2015 Update 3 na VS, kde se používá chyba NuGet verze 3.5.0 – [#3053](https://github.com/NuGet/Home/issues/3053)

* "Blokováno packages.config" v `project.json` (projekt UWP, a. k. a integrovaná sestavení) – [#3046](https://github.com/NuGet/Home/issues/3046)

* Aktualizujte rozhraní příkazového řádku dotnet nainstalovaného skriptem sestavení na preview2-003121, což je oficiální sestavení preview2. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Uživatelské rozhraní Správce balíčků: po aktualizaci balíčku nezobrazuje novou verzi [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey při odstraňování příkazového řádku není přečten/odeslán v 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)

* Nesprávný řetězec: stabilní verze balíčku by neměla mít v závislosti na předběžné verzi. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage cache opouští prázdné složky – [#3029](https://github.com/NuGet/Home/issues/3029)

* Vytváření projektu PCL (net46 a Windows 10) pro získání výjimky NullRef. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizace NuGet by měla poskytnout informativní zprávu, pokud je vyšší verze omezená omezením hodnota allowedversions- [#3013](https://github.com/NuGet/Home/issues/3013)

* Problémy s obnovením NuGet V3 – [#2891](https://github.com/NuGet/Home/issues/2891)

* Modul plug-in přihlašovacích údajů se ukončil s chybou-1/při stahování balíčku při použití zprostředkovatelů přihlašovacích údajů s více zdroji – [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` obnovení NuGet způsobí opětovnou kompilaci, když se nic nezměnilo – [#2817](https://github.com/NuGet/Home/issues/2817)

* Balíčky symbolů by se neměly nikdy používat při instalaci nebo aktualizaci – [#2807](https://github.com/NuGet/Home/issues/2807)

* VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe) – [#2763](https://github.com/NuGet/Home/issues/2763)

* Označení neoznačených prvků UIElement v uživatelském rozhraní Správce balíčků pro usnadnění přístupu [#2745](https://github.com/NuGet/Home/issues/2745)

* Přenosná rozhraní s rozdělenými profily se odmítnou. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Správce balíčků NuGet by měl zrušit zaškrtnutí tohoto seznamu možností v podrobnostech balíčků se nevztahuje na `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe push/Delete nepoužívá klíč rozhraní API – [#2627](https://github.com/NuGet/Home/issues/2627)

* Odeberte uzamčenou vlastnost ze souboru zámku – [#2379](https://github.com/NuGet/Home/issues/2379)

* Aktualizace NuGet 3.3.0 se nezdařila s dodatečným omezením... definované v packages.config zabrání této operaci. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalace balíčku z místního zdroje, který neexistuje, vyvolá nefalešnou zprávu- [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr dostupný k upgradu zobrazuje upgrady, které porušují omezení verze – [#1094](https://github.com/NuGet/Home/issues/1094)

* Nativní balíčky nelze aktualizovat – [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funkce

* Podpora nastavení CopyLocal na hodnotu false u odkazů přidaných pomocí NuGet- [#329](https://github.com/NuGet/Home/issues/329)

* Podpora nuget.exe pro MSBuild 15- [#1937](https://github.com/NuGet/Home/issues/1937)

* Podpora balíčku pro.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Zakázat akci uživatele, když se spustí akce uživatele – [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet by měl přidat podporu pro `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* V NuGet 2. x chybí kompatibility rozhraní, které jsou už v 3. x, [#2720](https://github.com/NuGet/Home/issues/2720)

* Podpora pro složky záložních balíčků – [#2899](https://github.com/NuGet/Home/issues/2899)

* Navrhněte a implementujte fiktivní typ balíčku, který podporuje balíčky nástrojů – [#2476](https://github.com/NuGet/Home/issues/2476)

* Přidejte rozhraní API, abyste získali cestu ke složce globálních balíčků – [#2403](https://github.com/NuGet/Home/issues/2403)

* Povolit SemVer 2.0.0 v balíčku – [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Chcete odeslat obecnou

* Parametr push-timeout nuget.exe nefunguje – [#2785](https://github.com/NuGet/Home/issues/2785)

* Text popisu balíčku by měl být vybrán – [#1769](https://github.com/NuGet/Home/issues/1769)

* Povolení nuget.exe vytváření `.props` a `.targets` souborů pro `.nuproj` projekty [#2711](https://github.com/NuGet/Home/issues/2711)

* Přidání rozhraní API rozšíření pro porovnání platforem s importy – [#2633](https://github.com/NuGet/Home/issues/2633)

* Skrýt možnosti závislosti při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Vytisknout nuget.exe záhlaví verze v podrobném výstupu – [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet potřebuje, aby uživatelé věděli, že při upgradu nebo instalaci v dotnet TFM může dojít k problémům – [#3138](https://github.com/NuGet/Home/issues/3138)

* Upozorňovat na neplatnou instalaci/upgrade pro Project w/TFM = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Řešení potíží s výkonem pomocí nástroje reformer a NuGet pro Update- [#3044](https://github.com/NuGet/Home/issues/3044)

* Přidání podpory netcoreapp11 a netstandard17 – [#2998](https://github.com/NuGet/Home/issues/2998)

* Využití atributu AssemblyMetadata – pro `.nuspec` nahrazení tokenů – [#2851](https://github.com/NuGet/Home/issues/2851)
