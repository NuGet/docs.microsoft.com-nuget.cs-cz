---
title: Zpráva k vydání Beta verze NuGet 3.5
description: Zpráva k vydání verze pro NuGet 3.5, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550681"
---
# <a name="nuget-35-release-notes"></a>Zpráva k vydání verze 3.5 verze NuGet

[Poznámky k verzi 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [zpráva k vydání verze NuGet 4.0 RC](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Opravy chyb

* Balíček nepoužívá MSBuild 14.1 v mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Kartu aktualizace nevybere na nejnovější dostupnou verzi aktualizovat místo toho vyberte aktuální nainstalovaná verze - [#3498](https://github.com/NuGet/Home/issues/3498)

* Po ověření privátního v2 MyGet kanálu a klepnutím na tlačítko "Zobrazit x více výsledků" byla opravena chyba vyskytující- [#3469](https://github.com/NuGet/Home/issues/3469)

* Zprávy protokolu zdá se, že se v obráceném pořadí pro uživatelské rozhraní – [#3446](https://github.com/NuGet/Home/issues/3446)

* "Formát zadané cestě se nepodporuje" - v3.4.4 – obnovení Nuget vyvolá [#3442](https://github.com/NuGet/Home/issues/3442)

* Beta verze NuGet cmdLine 3.6 nerespektuje – konfigurace Prop = vydání – [#3432](https://github.com/NuGet/Home/issues/3432)

* Pomalé IKVM Nuget nainstalovat velkého projektu – [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe Update - Self udržuje na aktualizace samotné - [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 instalace a obnovení ze sdílené složky UNC má výkon regrese z 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Chyba při instalaci Moq z uživatelské rozhraní správy balíčků pro projekt net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Instalace kartu na úrovni řešení nezobrazí verze balíčku - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` ztratí stav – aktualizace z karty nainstalované [#3303](https://github.com/NuGet/Home/issues/3303)

* Balíček NuGet na `.csproj` ignoruje prázdné soubory element v `.nuspec` soubor – [#3257](https://github.com/NuGet/Home/issues/3257)

* Projekty webových stránek, které jsou hostované ve službě IIS by nemělo způsobit obnovení selže - [#3235](https://github.com/NuGet/Home/issues/3235)

* Pověření nebyla načtena z Nuget.Config, když se koncový bod v3 přesměruje na v2 – [#3179](https://github.com/NuGet/Home/issues/3179)

* Balíček NuGet se nepodařilo přeložit sestavení při načítání metadat přenosné sestavení - [#3128](https://github.com/NuGet/Home/issues/3128)

* Nejde najít Nuget `msbuild.exe` v Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* neumožňuje balíček nuget.exe značku předběžné verze, která začíná čísla – [#1743](https://github.com/NuGet/Home/issues/1743)

* instalace balíčku nuget je neúspěšná na VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* Hodnota allowedVersions filtrování není funkční úrovni řešení - [#333](https://github.com/NuGet/Home/issues/333)

* Obnovení náhodně nezdaří a zobrazí se položka se stejným klíčem již byla přidána. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nelze nainstalovat Nuget.Common v `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Při použití uživatelského rozhraní pro hledání zdroje V2, FindPackagesById je volána dvakrát pro každé ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Balíčky nemohou záviset na projektech - [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe pack - vyloučení je uvedeno, ale není podporována – [#2284](https://github.com/NuGet/Home/issues/2284)

* Problémy s chybou zprávy, když "contentFiles" část `.nuspec` je neplatná – [#1686](https://github.com/NuGet/Home/issues/1686)

* Vždy posílá nabízená celý balíček dvakrát se ověřené zdroje balíčků, - [#1501](https://github.com/NuGet/Home/issues/1501)

* Předal se žádné informace o volání aktualizace *.csproj nuget.exe při projekt nemá `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` obnovení na stavové kódy 5xx z V2 zdrojů – neopakuje [#1217](https://github.com/NuGet/Home/issues/1217)

* Dvě tečky v souboru src v `.nuspec` nefunguje - [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR obnovení je potřeba ignorovat informačních kanálů prostřednictvím šifrování – [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe push 403 zpracování - nesprávně vás vyzve k zadání přihlašovacích údajů – [#2910](https://github.com/NuGet/Home/issues/2910)

* Odebere vlastnosti z NuGet aktualizace přes Správce balíčků `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* Pokus o načtení "NuGet.TeamFoundationServer14", ale, že název knihovny DLL změnila na "NuGet.TeamFoundationServer" - NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)

* Nově nezobrazí uživatelské rozhraní Správce balíčků aktualizovanou verzi - [#2828](https://github.com/NuGet/Home/issues/2828)

* balíček aktualizace pokouší použít ID balíčku, verzi místo package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* csproj obnovení nuget by měla chyba, pokud projekt nepoužívá nuget (`packages.config` nebo `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Chyby TFS "[soubor] nebyly nalezeny ve vašem pracovním prostoru, nebo nemáte oprávnění k přístupu" během upgradovat nebo odinstalovat, když je vázán řešení nebo projektu do správy verzí TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* balíček aktualizace nebude získání závislostí pro balíčky bez target - [#2724](https://github.com/NuGet/Home/issues/2724)

* Neexistuje žádný způsob, jak nastavit úroveň podrobností protokolů pro akce uživatelského rozhraní Správce balíčků Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfigurace nuget je neplatná - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource v `NuGetDefaults.Config` (`ProgramData\NuGet`) nefunguje - [#2653](https://github.com/NuGet/Home/issues/2653)

* vydání nuget 3.4.3 – získání vyšší hodnoty nemůže být null při sestavování balíčku - [#2648](https://github.com/NuGet/Home/issues/2648)

* obnovení nepoužívá uložené přihlašovací údaje ze souboru Nuget.Config pro informační kanály VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore] - configfile je relativní vzhledem k projektu dir místo cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Nadměrného přidělení v kódu porovnání verze - [#2632](https://github.com/NuGet/Home/issues/2632)

* Více instancí nuget.exe pokusu o instalaci stejný balíček v paralelní způsobí, že dvojité zápis – [#2628](https://github.com/NuGet/Home/issues/2628)

* Informace o závislostech neukládá do mezipaměti pro operace víceprojektové – [#2619](https://github.com/NuGet/Home/issues/2619)

* Instalace a aktualizace stáhnout balíčky bez kontroly složku packages first – [#2618](https://github.com/NuGet/Home/issues/2618)

* Pokud je seznam zdrojů balíčku je prázdné, nejde přidat zdroj balíčku prostřednictvím uživatelského rozhraní (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Při pokusu o instalaci balíčku, který závisí na návrhu fasády - zavádějící chyba [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalace balíčku z konzoly PackageManager s nastavením "All" pokusí pouze první zdroj - [#2557](https://github.com/NuGet/Home/issues/2557)

* Nejnovější verze beta není rozzipovávání ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 chyb při spuštění sami sestavili nuget 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Příkaz Update může být trochu více podrobné i otázky bude zaslána.. - [#2418](https://github.com/NuGet/Home/issues/2418)

* VSIX sestaven místně by měl mít stejné knihovny DLL a soubory jako sestavení CI. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Opravit upozornění downgrade NuGet v sestavení – [#2396](https://github.com/NuGet/Home/issues/2396)

* Nedaří ověřit zdroj balíčku (3 x) je blokován navždy - [#2362](https://github.com/NuGet/Home/issues/2362)

* Balíček obsahu není správně obnovena, při instalaci balíčku z nuget v3.3 + informačního kanálu s argumentem - NoCache, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)

* Instalace Nuget se všechny zdroje balíčků, ale v balíčku chybí ze zdroje 1, selže - [#2322](https://github.com/NuGet/Home/issues/2322)

* [Nástroj PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Nainstalovat bloky, pokud je jediným zdrojem selhání autorizace – [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` verze rozsah by měl přepsat - IncludeReferencedProjects verze - [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package velmi pomalé, - "pokus o získání informací o závislostech" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Když balíček NuGet neviditelný downgrady batch aktualizace závislých - [#1903](https://github.com/NuGet/Home/issues/1903)

* aktualizace nuget.exe zahodí silný název sestavení a privátní atribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Relativní cesta k souboru pro "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Zlepšení zpráv o chybách překladač - [#1373](https://github.com/NuGet/Home/issues/1373)

* balíček aktualizací ve verzi 3 nepodaří s balíčky nejsou v zadaném zdroji - [#1013](https://github.com/NuGet/Home/issues/1013)

* Pomocí relativní cesty pro zdroje balíčků jen těžko se má použít – [#865](https://github.com/NuGet/Home/issues/865)

* Chybějící závislost v generované z projektu, pokud se požadavek na nižší verzi - již existuje nepřímou závislost soubor NUPKG [#759](https://github.com/NuGet/Home/issues/759)

* Odstraňuje se projekt zavře okno odpovídající uživatelské rozhraní, ale Přejmenování projektu nedojde k přejmenování okno uživatelského rozhraní. Všimněte si, že PMC naslouchá Přejmenování projektu a projekt události remove - [#670](https://github.com/NuGet/Home/issues/670)

* [Willow webových úloh] Vytváří se soubor WSP Razor v3 přestane reagovat - [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalace a obnovení konkrétního balíčku selže s "Balíček obsahuje několik souborů nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Malá písmena ID & `packages.config` scénáře - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5 beta2] Obnovení balíčku se nepovede obnovit balíčky "starší" - [#3208](https://github.com/NuGet/Home/issues/3208)

* balíček nuget vynuceně přidá soubory .tt do složky obsahu bez ohledu na to, co - [#3203](https://github.com/NuGet/Home/issues/3203)

* aktualizace webové aplikace ASP.NET generuje upozornění týkající se do souboru: zdroj - [#3194](https://github.com/NuGet/Home/issues/3194)

* balíček nuget souboru csproj (s `project.json`) dojde k chybě, pokud neexistují žádné packOptions a vlastník v souboru JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* balíček nuget pro `project.json` packOptions značky jako souhrn, autory, vlastníci atd – ignoruje [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException prostřednictvím NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* Balíček NuGet ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizaci více balíčků s vrácení zpět opustí projektu je porušený - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles za nejsou přidány pro projekty netstandard – [#3118](https://github.com/NuGet/Home/issues/3118)

* Nelze vytvořit balíček knihovny cílené na .net Standard správně – [#3108](https://github.com/NuGet/Home/issues/3108)

* Soubor -> Nový Projekt -> selže projekt knihovny tříd (přenosná) ve VS2015 a odkaz na Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Chyba nuGet – 1.0.0-* není platný řetězec verze - [#3070](https://github.com/NuGet/Home/issues/3070)

* Vyhledání balíčku selže zobrazení, ale funguje Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Chyba při "Install-Package jquery.validation" na odkaz na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* balíček nuget z xproj je jako výchozí se použije Neplatná cílová cesta - [#3060](https://github.com/NuGet/Home/issues/3060)

* Při nainstalované VS 2015 s aktualizací 3 na VS, které používá NuGet dojde k chybě verze 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* "Blokován branou souboru packages.config" `project.json` (UPW, známé jako sestavení integrovaný režim) projekt – [#3046](https://github.com/NuGet/Home/issues/3046)

* aktualizace rozhraní příkazového řádku dotnet nainstaloval skript sestavení, aby preview2 003121, což je oficiální preview2 sestavení. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Uživatelské rozhraní Správce balíčků: Nová verze nezobrazuje po aktualizaci balíčku- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na příkazovém řádku delete není pro čtení/poslaná 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Řetězce není správný: stabilní verze balíčku by neměla mít na předběžnou verzi závislosti. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Mezipaměť OptimizedZipPackage opustí prázdné složky - [#3029](https://github.com/NuGet/Home/issues/3029)

* Vytváří se získat projekt PCL (net46 a windows 10) NullRef výjimky. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget aktualizace by měla poskytnout informativní zprávy, když hodnota allowedVersions omezení – je omezený na vyšší verzi rozhraní [#3013](https://github.com/NuGet/Home/issues/3013)

* Problémy obnovení Nuget v3 - [#2891](https://github.com/NuGet/Home/issues/2891)

* Plugin přihlašovacích údajů se ukončil s chybou -1 / Chyba při stahování balíčku při použití poskytovatelé přihlašovacích údajů s více zdroji - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` obnovení nuget způsobí, že rekompilace když nic změněno - [#2817](https://github.com/NuGet/Home/issues/2817)

* Balíčky symbolů by neměl být nikdy použita instalace nebo aktualizace - [#2807](https://github.com/NuGet/Home/issues/2807)

* VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe nepodporuje) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Popisek bez popisku prvky uživatelského rozhraní v uživatelském rozhraní Správce balíčků pro usnadnění přístupu – [#2745](https://github.com/NuGet/Home/issues/2745)

* Přenosná rozhraní s pomlčkou profily odmítají. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Správce balíčků NuGet by mělo být zřejmé tento seznam možností v balíčcích podrobností se nedá použít u `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe nabízených oznámení nebo odstranění nebude používat klíč rozhraní API – [#2627](https://github.com/NuGet/Home/issues/2627)

* Odeberte vlastnost uzamčená ze souboru zámku – [#2379](https://github.com/NuGet/Home/issues/2379)

* Aktualizace NuGet 3.3.0 selže s '... Další omezení definované v souboru packages.config téhle operaci brání. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalace balíčku z místního zdroje, který neexistuje, vyvolá výjimku neplatného zpráva – [#1674](https://github.com/NuGet/Home/issues/1674)

* Filtr "K dispozici je upgrade" zobrazuje upgrady, které narušují omezení verze - [#1094](https://github.com/NuGet/Home/issues/1094)

* Nepovedlo se aktualizovat nativní balíčky - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funkce

* Podpora nastavení CopyLocal na hodnotu false na odkazy přidal NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* Podpora nuget.exe MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Podpora balíčku.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Zakázat akce uživatele, když jsou uživatelské akce spouštěna- [#1440.](https://github.com/NuGet/Home/issues/1440)

* NuGet by měl přidat podporu pro `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Přidat rozhraní framework kompatibility chybí ve Správci NuGet 2.x (které jsou již ve 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Podpora pro použití náhradní lokality balíček složky – [#2899](https://github.com/NuGet/Home/issues/2899)

* Návrh a implementace hodnoty typu balíčku pro podporu nástroje balíčky - [#2476](https://github.com/NuGet/Home/issues/2476)

* Přidání rozhraní API k získání cesty ke složce globálních balíčků - [#2403](https://github.com/NuGet/Home/issues/2403)

* Povolit SemVer 2.0.0 v balíčku - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Chcete

* nabízené nuget.exe – parametr časového limitu nefunguje - [#2785](https://github.com/NuGet/Home/issues/2785)

* Text popisu balíčku by měla být volitelný - [#1769](https://github.com/NuGet/Home/issues/1769)

* Povolit vytvoří nuget.exe `.props` a `.targets` soubory pro `.nuproj` projekty [#2711](https://github.com/NuGet/Home/issues/2711)

* Přidat rozšíření rozhraní API pro porovnání architektur s importovanými daty - [#2633](https://github.com/NuGet/Home/issues/2633)

* Skrýt možnosti závislostí při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Vytiskne nuget.exe verze záhlaví podrobný výstup - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet je potřeba uživatelům sdělit, že upgrade nebo instalace v dotnet tfm na základě PCL může způsobit problémy se - [#3138](https://github.com/NuGet/Home/issues/3138)

* Upozornit chybný instalace/aktualizace pro projekt plánovaným bodem obnovení kratším tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Řešení problémů s výkonem s ReShaper a NuGet pro sadu Vs11 – [#3044](https://github.com/NuGet/Home/issues/3044)

* Přidání podpory netcoreapp11 a netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Využijte assemblymetadata – atribut pro `.nuspec` token nahrazení - [#2851](https://github.com/NuGet/Home/issues/2851)
