---
title: zpráva k vydání verze NuGet 5,10
description: poznámky k verzi NuGet 5,10, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726948"
---
# <a name="nuget-510-release-notes"></a>zpráva k vydání verze NuGet 5,10

NuGet distribučních vozidel:

| verze NuGet | k dispozici ve verzi Visual Studio | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [verze Visual Studio 2019 16,10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> nainstalovaná s Visual Studio 2019 s úlohou .net Core
  
> [!NOTE]
> Visual Studio 16,10, MSBuild 16,10 a .net 5.0.300 + vyžaduje NuGet.exe 5,10 nebo novější.

## <a name="summary-whats-new-in-510"></a>Shrnutí: Novinky v 5,10

* Podepisování: implementace příkazu dotnet Trusted-Signer- [#8053](https://github.com/NuGet/Home/issues/8053)

* nastavit výchozí ověřování v systému Linux, ale ve výchozím nastavení povoleno v Windows- [#10713](https://github.com/NuGet/Home/issues/10713)

* Přidání proměnné ENV pro ověření podpisu balíčku na .NET 5 + Linux/MAC – [#10742](https://github.com/NuGet/Home/issues/10742)

* Zlepšení výkonu při instalaci nového balíčku pro velká řešení – [#10166](https://github.com/NuGet/Home/issues/10166)

* Přidejte typ projektu `nfproj` do seznamu supportedProjectExtensions pro rozhraní příkazového řádku NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Potlačit `<requireLicenseAcceptance>` element při balení projektu – [#5133](https://github.com/NuGet/Home/issues/5133)

* V příkazu dotnet CLI- [#10226](https://github.com/NuGet/Home/issues/10226) by mělo být zobrazeno upozornění verze Preview [CPVM].

* Aktualizovat barevné tokeny pozadí a popředí PMUI na CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608)

* [Chyba bash] Chyba "operace byla zrušena uživatelem" v Seznam chyb okně při rychlém přepínání mezi kartami v uživatelském rozhraní PM – [#10671](https://github.com/NuGet/Home/issues/10671)

* Uživatelské rozhraní PM: Vylepšete výkon instalace balíčku na úrovni řešení – [#10210](https://github.com/NuGet/Home/issues/10210)

* Nahraďte GetService GetServiceAsync všude v NuGet. Klienti – [#3784](https://github.com/NuGet/Home/issues/3784)

* Problém s výkonem NuGet.exe Pack s `..` relativní cestou – [#5016](https://github.com/NuGet/Home/issues/5016)

* Výkon "sady NuGet Pack" se zmenší se zvýšenými úrovněmi ve zdrojových cestách – [#5706](https://github.com/NuGet/Home/issues/5706)

* při vytváření balíčků nuspec s duplicitními soubory není NuGet chyba. - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet pack "zadanou hodnotu DateTimeOffset nelze převést na časové razítko souboru Zip"- [#7001](https://github.com/NuGet/Home/issues/7001)

* Časová razítka souboru zabalených balíčků jsou posunuta podle časového pásma – [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 by měl obsahovat další informace, [#7696](https://github.com/NuGet/Home/issues/7696)

* [Chyba bash] [Selhání testu] Při spuštění dotnet restore--use-Lock-File--uzamčený režim by se neměl aktualizovat prázdný nebo poškozený soubor zámku- [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange umožňuje analyzovat logicky nesprávné rozsahy – [#9145](https://github.com/NuGet/Home/issues/9145)

* Uživatelské rozhraní PM nemůže zobrazit rozlišitelné barvy pozadí mezi vybranými a zdrojovými balíčky s najetím myší – [#9538](https://github.com/NuGet/Home/issues/9538)

* Zaškrtávací políčko pro výběr projektů k instalaci, které se nečtou čtečkou obrazovky – [#9578](https://github.com/NuGet/Home/issues/9578)

* Výchozí nastavení rozevíracího seznamu verze podokna podrobností je třeba nainstalovat/LatestStable na kartách installed/updates- [#9887](https://github.com/NuGet/Home/issues/9887)

* Odebrání účtu alternativního řešení pro některé sady SDK .NET 5 TargetPlatformMoniker sestav ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* příkaz dotnet NuGet Verify je příliš tichý – [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange nemůže analyzovat rozsahy s jednou číslicí – [#10342](https://github.com/NuGet/Home/issues/10342)

* Správce řešení VS během ladění vyvolá výjimku null – [#10352](https://github.com/NuGet/Home/issues/10352)

* Přesunout zprávy o výjimce CLI do řetězcových souborů prostředků – [#10392](https://github.com/NuGet/Home/issues/10392)

* Odebrat mrtvý kód (TabItemButtonAutomationPeer) – [#10435](https://github.com/NuGet/Home/issues/10435)

* Příkaz Aktualizovat kontextovou nabídku by měl přejít na první vybranou položku – [#10498](https://github.com/NuGet/Home/issues/10498)

* Podrobnosti PMUI řešení mají překrývající vodorovný pruh – [#10533](https://github.com/NuGet/Home/issues/10533)

* Podepisování: podrobnosti primárního podpisu se nezobrazují, pokud vypršela platnost certifikátu a časové razítko není důvěryhodné- [#10535](https://github.com/NuGet/Home/issues/10535)

* Nepovolené zdroje brání v zobrazení uživatelského rozhraní pro ODP. [#10541](https://github.com/NuGet/Home/issues/10541)

* Metadata balíčku (podrobnosti, vyřazení) se někdy nevyžadují z nuget.org v CodeSpaces – [#10549](https://github.com/NuGet/Home/issues/10549)

* Inicializace PMUI se nezdařila s výjimkou během relace ladění – [#10559](https://github.com/NuGet/Home/issues/10559)

* Výsledkem obnovení NuGet je selhání kontroly integrity balíčku v systému big endian – [#10567](https://github.com/NuGet/Home/issues/10567)

* Je vyvolána výjimka FormatException místo PackagingException- [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM – problémy s Concurrency v grafu předávání algoritmu – [#10598](https://github.com/NuGet/Home/issues/10598)

* Přidání telemetrie verze PMC PowerShellu – [#10609](https://github.com/NuGet/Home/issues/10609)

* Zlepšení výkonu řazení NuGetVersion – [#10611](https://github.com/NuGet/Home/issues/10611)

* Přidání důvěryhodných přihlášení má nekonzistentní argumenty – [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0: přepnutí tabulátorů v NuGet Správce balíčků z části aktualizace na "nainstalované" neaktualizuje rámec. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Odebere "v" z čísla verze v PMUI- [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService. GetInstalledPackagesAsync vyvolá před přijetím jmenování systému projektu CPS- [#10681](https://github.com/NuGet/Home/issues/10681)

* vložené ikony způsobí, že přístup byl odepřen ze zdroje Microsoft Visual Studio Offline balíčky na kartě procházet – [#10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService. GetInstalledPackagesAsync vyvolá v případě, že MSBuildProjectExtensionsPath není nastaven- [#10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet NuGet Remove source nuget.org" při prvním [#10745](https://github.com/NuGet/Home/issues/10745) nefunguje

* NuGet blokuje vlákno nevláken v asynchronní metodě, která provádí synchronní volání vlákna uživatelského rozhraní [#10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` je mrtvý kód a neubližujeme výkon – [#10790](https://github.com/NuGet/Home/issues/10790)

* použití vložené ikony v balíčcích NuGet SDK – [#10795](https://github.com/NuGet/Home/issues/10795)

* Aktualizace seznamu licencí SPDX – [#10806](https://github.com/NuGet/Home/issues/10806)

**[Seznam všech problémů opravených v této verzi – 5,10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Seznam potvrzení v tomto vydání – 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Komunitní příspěvky

děkujeme všem přispěvatelům, kteří vám pomohl tuto NuGet vydávat.

|Kdo|PR|Problémy|
|----|----|----|
[Louis – z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange nemůže analyzovat rozsahy s jednou číslicí – [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet. Build.sh klienta je přerušená – [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet. Build.sh klienta je přerušená – [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Výkon "sady NuGet Pack" se zmenší se zvýšenými úrovněmi ve zdrojových cestách – [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Problém s výkonem sady NuGet.exe Pack s nástrojem.. relativní cesta – [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM – problémy s Concurrency v grafu předávání algoritmu – [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Přidejte typ projektu nfproj do seznamu supportedProjectExtensions pro NuGet CLI. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Úvodní názory

Váš názor je pro nás důležitý.  pokud se v této verzi vyskytnou nějaké problémy, podívejte se na naše [problémy s GitHub](https://github.com/NuGet/Home/issues) a [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) pro stávající problémy.  V případě nových problémů v NuGet nahlásit problém [GitHub problémy.](https://github.com/NuGet/Home/issues/new)
V případě obecných NuGet problémů s prostředím nám dejte vědět prostřednictvím možnosti Nahlásit problém, která se nachází ve vašem oblíbeném integrovaném vývojovém prostředí (IDE) **v části Nápověda > Nahlásit problém.** [](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)
