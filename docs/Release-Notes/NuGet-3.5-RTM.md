---
title: "Poznámky k verzi Beta NuGet 3.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 082a96b9-607b-4225-864d-e1cea537f591
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 3.5 NuGet."
keywords: "NuGet 3.5 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0a0f039d2529e1d41bbc0c7f9ac3f76f51f96ce5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
#<a name="nuget-35-release-notes"></a>Poznámky k verzi 3.5 NuGet

[Poznámky k verzi 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md) | [poznámky k verzi RC NuGet 4.0](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Opravy chyb

* Pack nepoužívá MSBuild 14.1 na mono - [#3550](https://github.com/NuGet/Home/issues/3550)

* Aktualizace není vyberte na nejnovější dostupnou verzi aktualizovat místo toho vyberte aktuální nainstalovaná verze - [#3498](https://github.com/NuGet/Home/issues/3498)

* Opravte havárií poté ověřování privátní v2 MyGet kanálu a kliknutím na "Zobrazit x více výsledků"- [#3469](https://github.com/NuGet/Home/issues/3469)

* Zprávy protokolu se zdá, že se v obráceném pořadí pro uživatelské rozhraní – [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - Nuget restore vyvolá "dané cesty formát není podporován" - [#3442](https://github.com/NuGet/Home/issues/3442)

* Beta cmdLine 3.6 NuGet nectí - konfigurace Prop = verze – [#3432](https://github.com/NuGet/Home/issues/3432)

* Nuget IKVM pomalé instalace na velké projekt – [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe aktualizace - Self udržuje na aktualizace samotné - [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 instalace a obnovení ze sdílené složky UNC má výkonu regrese z 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Chyba při instalaci Moq z uživatelské rozhraní správy balíčků pro projekt net451 - [#3349](https://github.com/NuGet/Home/issues/3349)

* Karta instalace na úrovni řešení nezobrazí verze balíčku - [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` aktualizace z karty nainstalovaná ztratí stav – [#3303](https://github.com/NuGet/Home/issues/3303)

* Pack NuGet na `.csproj` ignoruje element prázdné soubory v `.nuspec` soubor - [#3257](https://github.com/NuGet/Home/issues/3257)

* Projekty web hostovaný ve službě IIS by nemělo způsobit obnovení selhání - [#3235](https://github.com/NuGet/Home/issues/3235)

* Pověření nebyla načtena z Nuget.Config, pokud koncový bod v3 přesměruje na v2 - [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet pack nepodaří vyřešit sestavení při načítání metadat přenosné sestavení - [#3128](https://github.com/NuGet/Home/issues/3128)

* Nelze najít Nuget `msbuild.exe` na Mono - [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe pack neumožňuje značku předběžné verze, která začíná čísla – [#1743](https://github.com/NuGet/Home/issues/1743)

* dojde k selhání instalace balíčku nuget v VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)

* Hodnota allowedVersions filtru není funkční úrovni řešení - [#333](https://github.com/NuGet/Home/issues/333)

* Obnovení náhodně selže s položku se stejným klíčem již byla přidána. - [#2646](https://github.com/NuGet/Home/issues/2646)

* Nelze nainstalovat Nuget.Common v `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Při použití uživatelského rozhraní pro hledání V2 zdroj, se nazývá FindPackagesById dvakrát pro daná ID - [#2517](https://github.com/NuGet/Home/issues/2517)

* Balíčky nemohou mít závislosti na projekty - [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe pack - vyloučení je popsané, ale nepodporují - [#2284](https://github.com/NuGet/Home/issues/2284)

* Problémy s chybou zprávy při část 'contentFiles' `.nuspec` je neplatný – [#1686](https://github.com/NuGet/Home/issues/1686)

* Nabízená vždy odesílá celý balíček dvakrát u ověření zdroje balíčků - [#1501](https://github.com/NuGet/Home/issues/1501)

* Žádné informace byla zadána při volání metody nuget.exe aktualizace *.csproj při projektu nemá `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config`obnovení na stavové kódy 5xx z V2 zdrojů – neopakuje [#1217](https://github.com/NuGet/Home/issues/1217)

* Dvojité tečky v souboru src v `.nuspec` nefunguje - [#2947](https://github.com/NuGet/Home/issues/2947)

* Obnovení CoreCLR musí ignorovat informační kanály šifrováním - [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe push 403 zpracování - nesprávně výzvy k zadání pověření - [#2910](https://github.com/NuGet/Home/issues/2910)

* Odebere vlastnosti z NuGet aktualizace prostřednictvím Správce balíčků `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio pokusí načíst "NuGet.TeamFoundationServer14", ale že název DLL změnila na "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)

* Správce balíčků uživatelského rozhraní nezobrazí nově aktualizované verze - [#2828](https://github.com/NuGet/Home/issues/2828)

* balíček aktualizace pokouší použít ID balíčku, verzi místo package.version - [#2771](https://github.com/NuGet/Home/issues/2771)

* nuget restore csproj by chyby, pokud projekt není pomocí nástroje nuget (`packages.config` nebo `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* Chyba sady TFS "[soubor] není možné najít v pracovním prostoru, nebo nemáte oprávnění k přístupu" během aktualizovat nebo odinstalovat při řešení/projekt je vázán k řízení zdrojů TFS - [#2739](https://github.com/NuGet/Home/issues/2739)

* balíček aktualizace není získat závislosti pro balíčky jiných cílových - [#2724](https://github.com/NuGet/Home/issues/2724)

* Neexistuje žádný způsob, jak nastavit úroveň podrobností protokoly pro akce uživatelského rozhraní Správce balíčků Nuget - [#2705](https://github.com/NuGet/Home/issues/2705)

* Konfigurace nuget je neplatná - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* DefaultPushSource v `NuGetDefaults.Config` (`ProgramData\NuGet`) nefunguje - [#2653](https://github.com/NuGet/Home/issues/2653)

* verze nuget 3.4.3 – získávání hodnota nemůže být null při sestavování balíček - [#2648](https://github.com/NuGet/Home/issues/2648)

* obnovení nepoužívá uložené přihlašovací údaje ze souboru Nuget.Config pro informační kanály služby VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet obnovení] – configfile je relativní vzhledem k projektu dir místo cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)

* Nadměrné přidělení v kódu porovnání verze - [#2632](https://github.com/NuGet/Home/issues/2632)

* Více instancí nuget.exe pokusu o instalaci stejný balíček v paralelní příčiny dvojité zápisu - [#2628](https://github.com/NuGet/Home/issues/2628)

* Informace o závislostech nejsou uloženy v mezipaměti pro operace vícenásobného projektu - [#2619](https://github.com/NuGet/Home/issues/2619)

* Instalace a aktualizace stáhnout balíčky bez kontroly složce balíčků nejprve - [#2618](https://github.com/NuGet/Home/issues/2618)

* Pokud seznam zdrojů balíčku je prázdná, nelze přidat zdroj balíčku prostřednictvím uživatelského rozhraní (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Zavádějící Chyba při pokusu o instalaci balíčku, který závisí na průčelí návrhu - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalace balíčku z konzoly PackageManager s nastavení "Všechny" pokusí pouze první zdroj - [#2557](https://github.com/NuGet/Home/issues/2557)

* Nejnovější beta není rozbalení ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* Havárie VS2015 při spuštění s samoobslužné integrovaný NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)

* Příkaz aktualizace může být trochu podrobnější, pokud i požádá ji, aby se nezdaří... - [#2418](https://github.com/NuGet/Home/issues/2418)

* Integrovaný místně VSIX musí mít stejné knihovny DLL a soubory jako položky konfigurace sestavení. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Opravte NuGet přechod na starší verzi upozornění v sestavení - [#2396](https://github.com/NuGet/Home/issues/2396)

* Nedaří se ověřit zdroj balíčku (3krát) je blokovaný navždy - [#2362](https://github.com/NuGet/Home/issues/2362)

* Obsah balíčku není správně obnoveny při instalaci balíčku z v3.3 nuget + kanálu s argumentem - NoCache, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)

* Instalace Nuget s všechny zdroje balíčků, ale balíček chybí 1 zdroje, selže - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Nainstalovat bloky v případě, že jednoho zdroje vyvolá chybu autorizace - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`verze rozsahu by měly přepsat verze - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* Balíček aktualizace super zpomalit - "pokus o získání informací o závislostech" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Balíček NuGet skrytá dírám, kdy batch aktualizace jeho závislé součásti - [#1903](https://github.com/NuGet/Home/issues/1903)

* aktualizace nuget.exe zahodí silný název sestavení a privátní atributu. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Relativní cesta k souboru pro "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Zlepšení zprávy o selhání překladač - [#1373](https://github.com/NuGet/Home/issues/1373)

* balíček aktualizace v v3 selže s balíčky nejsou v zadaném zdroji - [#1013](https://github.com/NuGet/Home/issues/1013)

* Pomocí relativní cesty zdroje balíčku je problém pomocí - [#865](https://github.com/NuGet/Home/issues/865)

* Chybějící závislost v soubor NUPKG vygenerovat z projektu, pokud se požadavek na nižší verzi - již existuje nepřímou závislost [#759](https://github.com/NuGet/Home/issues/759)

* Odstranění projektu zavře okno odpovídající uživatelského rozhraní, ale Přejmenování projektu nepřejmenuje okno uživatelského rozhraní. Všimněte si, že pomocí PMC naslouchá Přejmenování projektu a události projektu remove - [#670](https://github.com/NuGet/Home/issues/670)

* [Willow webové úlohy] Vytváření Razor v3 WSP zasekne - [#3241](https://github.com/NuGet/Home/issues/3241)

* Instalace a obnovení konkrétní balíčku selže s "Balíček obsahuje několik souborů nuspec." - [#3231](https://github.com/NuGet/Home/issues/3231)

* Malá písmena ID & `packages.config` scénáře - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2] Obnovení balíčků nepodaří obnovit "starší" balíčky - [#3208](https://github.com/NuGet/Home/issues/3208)

* soubory .tt nuget pack vynuceně přidá do složky obsahu bez ohledu na to, co - [#3203](https://github.com/NuGet/Home/issues/3203)

* balíček aktualizace webové aplikace ASP.NET generuje upozornění související s souboru: zdroj - [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget pack csproj (s `project.json`) dojde k chybě, pokud nejsou žádné packOptions a vlastníka v souboru JSON - [#3180](https://github.com/NuGet/Home/issues/3180)

* balíček nuget pro `project.json` ignoruje packOptions značky souhrn, autoři, vlastníky atd - [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException prostřednictvím NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet pack ignoruje závislosti ve výstupu `.nuspec` pro `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Aktualizaci více balíčků s vrácení ponechá projektu v narušeném stavu - [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles ve všech nebyly přidány pro projekty monikerů netstandard - [#3118](https://github.com/NuGet/Home/issues/3118)

* Nelze vytvořit balíček knihovny cílení na rozhraní .net standardní správně – [#3108](https://github.com/NuGet/Home/issues/3108)

* Soubor -> Nový Projekt -> selže projektu knihovny tříd (přenositelností) v VS2015 a Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)

* Chyba nuGet - 1.0.0-* není platný řetězec verze - [#3070](https://github.com/NuGet/Home/issues/3070)

* Najít balíček nepodaří zobrazení, ale funguje Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Chyba při "Install-Package jquery.validation" na dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Neplatný cíl cesta - tuto sadu nuget pack xproj [#3060](https://github.com/NuGet/Home/issues/3060)

* Pokud je nainstalované VS 2015 s aktualizací 3 na VS, které používá NuGet dojde k chybě verze 3.5.0 - [#3053](https://github.com/NuGet/Home/issues/3053)

* "Blokována souboru packages.config" `project.json` (UPW, známé jako sestavení integrované) projekt – [#3046](https://github.com/NuGet/Home/issues/3046)

* aktualizace nainstalované ve skriptu buildu k preview2 003121, což je oficiální preview2 sestavení rozhraní příkazového řádku dotnet. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Balíček uživatelského rozhraní správce: po aktualizaci balíčku nezobrazuje nová verze- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey na odstranění příkazového řádku pro čtení nebo neposílají v 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)

* Nesprávný řetězec: stabilní verze balíčku by neměla mít na závislost na předběžné verzi. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage mezipaměti zůstane prázdné složky - [#3029](https://github.com/NuGet/Home/issues/3029)

* Vytvoření projektu get PCL (net46 a windows 10) NullRef výjimka. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Aktualizace Nuget by měl poskytovat informativní zprávy, když hodnota allowedVersions omezení - je omezený na vyšší verzi [#3013](https://github.com/NuGet/Home/issues/3013)

* Problémy obnovení v3 Nuget - [#2891](https://github.com/NuGet/Home/issues/2891)

* Modul plug-in přihlašovacích údajů byl ukončen s chybou -1 / Chyba stahování balíčku při použití poskytovatelé přihlašovacích údajů pro více zdrojů - [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json`nuget restore způsobí, že rekompilace při nic změnit - [#2817](https://github.com/NuGet/Home/issues/2817)

* Symboly balíčky by neměl být nikdy použit v instalace nebo aktualizace - [#2807](https://github.com/NuGet/Home/issues/2807)

* VS nepodporuje proměnné prostředí v repositoryPath (nuget.exe nemá) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Popisek bez popisku prvky uživatelského rozhraní v uživatelském rozhraní Správce balíčků pro usnadnění - [#2745](https://github.com/NuGet/Home/issues/2745)

* Přenosné rozhraní s rozděleným profily byly zamítnuty. - [#2734](https://github.com/NuGet/Home/issues/2734)

* Správce balíčků NuGet by mělo být zřejmé tento seznam možností v balíčcích podrobností se nevztahuje na `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe nabízené nebo odstranění nebude používat klíč API - [#2627](https://github.com/NuGet/Home/issues/2627)

* Odebrat vlastnost uzamčeném zámek souboru - [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 aktualizace nezdaří s ' dodatečné omezení... definované v souboru packages.config téhle operaci brání. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* Instalace balíčku z místního zdroje, který neexistuje vyvolává neplatnou zpráva – [#1674](https://github.com/NuGet/Home/issues/1674)

* "Upgrade k dispozici" filtr zobrazuje upgrady, které porušují omezení verze - [#1094](https://github.com/NuGet/Home/issues/1094)

* Nelze aktualizovat nativní balíčky - [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Funkce

* Podpora CopyLocal nastavení na hodnotu false na odkazy přidal NuGet - [#329](https://github.com/NuGet/Home/issues/329)

* Podpora nuget.exe MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)

* Podpora Pack.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Zakázat akce uživatele, když jsou uživatelské akce spouštěna- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet měli přidat podporu pro `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Přidat framework kompatibility v NuGet chybí 2.x (které jsou již v 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)

* Podporu pro záložní balíček složky - [#2899](https://github.com/NuGet/Home/issues/2899)

* Návrh a implementaci představu o typu balíčku pro podporu nástroje balíčky - [#2476](https://github.com/NuGet/Home/issues/2476)

* Přidání rozhraní API získání cesty ke složce globální balíčky - [#2403](https://github.com/NuGet/Home/issues/2403)

* Povolit SemVer 2.0.0 sadě - [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Chcete

* nuget.exe nabízené - parametr časového limitu nefunguje - [#2785](https://github.com/NuGet/Home/issues/2785)

* Balíček Popis text by měl být volitelný - [#1769](https://github.com/NuGet/Home/issues/1769)

* Povolit nuget.exe k vytvoření `.props` a `.targets` soubory pro `.nuproj` projekty [#2711](https://github.com/NuGet/Home/issues/2711)

* Přidání rozšíření rozhraní API k porovnání rozhraní s importovanými daty - [#2633](https://github.com/NuGet/Home/issues/2633)

* Skrýt možnosti závislostí při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Tiskové out hlavičkou verze nuget.exe podrobný výstup - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet je potřeba upozornit uživatele, že upgrade nebo instalace v dotnet tfm, na základě PCL může způsobit problémy - [#3138](https://github.com/NuGet/Home/issues/3138)

* Upozornit chybná instalace nebo aktualizace pro projekt s tfm = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Oprava problémů s výkonem se ReShaper a NuGet pro aktualizaci - [#3044](https://github.com/NuGet/Home/issues/3044)

* Přidání podpory netcoreapp11 a netstandard17 - [#2998](https://github.com/NuGet/Home/issues/2998)

* Assemblymetadata – atribut využívají pro `.nuspec` token náhrady - [#2851](https://github.com/NuGet/Home/issues/2851)
