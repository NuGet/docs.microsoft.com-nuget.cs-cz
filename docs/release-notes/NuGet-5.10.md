---
title: Zpráva k vydání verze NuGet 5.10
description: Poznámky k verzi pro NuGet 5.10, včetně nových funkcí, oprav chyb a souborů DCR
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356535"
---
# <a name="nuget-510-release-notes"></a>Zpráva k vydání verze NuGet 5.10

Distribuční vozidla NuGet:

| Verze NuGet | K dispozici ve Visual Studio verzi | K dispozici v sadě .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> Nainstalované s Visual Studio 2019 s úlohou .NET Core
  
> [!NOTE]
> Visual Studio verze 16.10, MSBuild 16.10 a .NET 5.0.300+ vyžaduje NuGet.exe 5.10 nebo novější.

## <a name="summary-whats-new-in-510"></a>Shrnutí: Co je nového ve windows 5.10

* Podepisování: Implementujte příkaz dotnet trusted-signers [– #8053](https://github.com/NuGet/Home/issues/8053)

* Zakázat výchozí ověřování v Linuxu, ale ve výchozím nastavení je povolené ve Windows – [#10713](https://github.com/NuGet/Home/issues/10713)

* Přidání proměnné ENV pro ověření podepisování balíčků v .NET 5+ Linux/MAC – [#10742](https://github.com/NuGet/Home/issues/10742)

* Vylepšení výkonu instalace nových balíčků pro velká řešení – [#10166](https://github.com/NuGet/Home/issues/10166)

* Přidejte typ projektu `nfproj` do seznamu supportedProjectExtensions pro rozhraní příkazového řádku NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Potlačení <requireLicenseAcceptance> elementu při balení projektu – [#5133](https://github.com/NuGet/Home/issues/5133)

* Upozornění [CPVM] verze Preview by se měla zobrazit v rozhraní příkazového řádku dotnet – [#10226](https://github.com/NuGet/Home/issues/10226)

* Aktualizujte barevné tokeny pozadí a popředí pmui na CommonDocumentColors – [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash] Při rychlém přepínání mezi kartami v uživatelském rozhraní PM se Seznam chyb chyba Operace byla zrušena uživatelem – [#10671](https://github.com/NuGet/Home/issues/10671)

* Uživatelské rozhraní PM: Zvýšení výkonu instalace balíčku na úrovni řešení – [#10210](https://github.com/NuGet/Home/issues/10210)

* GetService nahraďte GetServiceAsync všude v NuGet.Clients – [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe s výkonem balíčku s `..` relativní cestou – [#5016](https://github.com/NuGet/Home/issues/5016)

* Výkon "balíčku NuGet" se snižuje s rostoucími úrovněmi ve zdrojových cestách – [#5706](https://github.com/NuGet/Home/issues/5706)

* Při balení nuspec s duplicitními soubory se NuGet ne chybně nelišuje. - [#6941](https://github.com/NuGet/Home/issues/6941)

* Balíček NuGet "Zadaný DateTimeOffset nelze převést na časové razítko souboru Zip" – [#7001](https://github.com/NuGet/Home/issues/7001)

* Časová razítka souboru zabalených balíčků se posunou o časové pásmo – [#7395](https://github.com/NuGet/Home/issues/7395)

* Nu1004 by měl obsahovat další informace s možností akce – [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash] [Test Failure] Prázdný nebo poškozený soubor zámku by se neměl aktualizovat při spuštění dotnet restore --use-lock-file --locked-mode – [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange umožňuje parsovat logicky nesprávné rozsahy – [#9145](https://github.com/NuGet/Home/issues/9145)

* Uživatelské rozhraní PM nemůže zobrazit rozlišitelnou barvu pozadí mezi vybranými a najetými zdroji balíčků – [#9538](https://github.com/NuGet/Home/issues/9538)

* Zaškrtávací políčko pro výběr projektů, na které se má nainstalovat, nečte čtečka obrazovky – [#9578](https://github.com/NuGet/Home/issues/9578)

* Výchozí výběr verze podokna podrobností Rozevírací seznam by měl být Nainstalováno/NejnovějšíStable na kartách Nainstalované/Aktualizace [– #9887](https://github.com/NuGet/Home/issues/9887)

* Odebrání účtu alternativního řešení pro některé verze .NET 5 SDK hlásí TargetPlatformMoniker ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget verify is too quiet – [#10316](https://github.com/NuGet/Home/issues/10316)

* Rozsah verzí nemůže parsovat jednociferné rozsahy – [#10342](https://github.com/NuGet/Home/issues/10342)

* Správce řešení VS vyvolá během ladění výjimku null – [#10352](https://github.com/NuGet/Home/issues/10352)

* Přesunutí zpráv o výjimce rozhraní příkazového řádku do souborů prostředků řetězců [– #10392](https://github.com/NuGet/Home/issues/10392)

* Odebrání neschopového kódu (TabItemButtonAutomationPeer) [– #10435](https://github.com/NuGet/Home/issues/10435)

* Místní nabídka Aktualizovat by se měla posunout k první vybrané [položce](https://github.com/NuGet/Home/issues/10498) – #10498

* Podrobnosti PMUI řešení se překrývají vodorovným pruhem – [#10533](https://github.com/NuGet/Home/issues/10533)

* Podepisování: Podrobnosti primárního podpisu se nezobrazují, když vypršela platnost certifikátu a časové razítko je nedůvěryhodné – [#10535](https://github.com/NuGet/Home/issues/10535)

* Pokud žádné povolené zdroje neumožňují zobrazení uživatelského rozhraní PM, [#10541](https://github.com/NuGet/Home/issues/10541)

* Metadata balíčků (podrobnosti, vyněcování) se někdy nečtou z nuget.org v CodeSpaces – [#10549](https://github.com/NuGet/Home/issues/10549)

* Inicializace PMUI selže s výjimkou během ladicí relace – [#10559](https://github.com/NuGet/Home/issues/10559)

* Obnovení nuget vede k selhání kontroly integrity balíčků v systému Big Endian [– #10567](https://github.com/NuGet/Home/issues/10567)

* Místo PackagingException je vyvolána výjimka FormatException [– #10595](https://github.com/NuGet/Home/issues/10595)

* CPVM – Problémy se souběžnosti v algoritmu cházek v grafu – [#10598](https://github.com/NuGet/Home/issues/10598)

* Přidání telemetrie verze PowerShellu PMC – [#10609](https://github.com/NuGet/Home/issues/10609)

* Zvýšení výkonu řazení NuGetVersion – [#10611](https://github.com/NuGet/Home/issues/10611)

* Přidání důvěryhodných podpisů má nekonzistentní argumenty – [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0: Přepnutím karet ve Správce balíčků NuGetu z "Aktualizace" na "Nainstalováno" se rámec ne aktualizován. - [#10654](https://github.com/NuGet/Home/issues/10654)

* Odeberte "v" z čísla verze v PMUI – [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync vyvolá výjimku před přijetím nominace systému projektu CPS – [#10681](https://github.com/NuGet/Home/issues/10681)

* Vložené ikony způsobují odepření přístupu ze zdroje Microsoft Visual Studio offline balíčky na kartě Procházet [– #10687](https://github.com/NuGet/Home/issues/10687)

* INuGetProjectService.GetInstalledPackagesAsync vyvolá výjimku, když není nastavená vlastnost MSBuildProjectExtensionsPath – [#10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org" nefunguje poprvé – [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget blokuje vlákno fondu vláken v asynchronní metodě, která synchronně volá vlákno uživatelského rozhraní – [#10775](https://github.com/NuGet/Home/issues/10775)

* Nástroje – > možnosti –> řetězec Správce balíčků NuGet je zkrácený – [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` je neschůdný kód a snížení výkonu [– #10790](https://github.com/NuGet/Home/issues/10790)

* Použití vložené ikony v balíčcích sady NuGet SDK [– #10795](https://github.com/NuGet/Home/issues/10795)

* Aktualizace seznamu licencí SPDX – [#10806](https://github.com/NuGet/Home/issues/10806)

**[Seznam všech problémů opravených v této verzi – 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[Seznam potvrzení v této verzi – 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>Komunitní příspěvky

Děkujeme všem přispěvatelům, kteří této verzi NuGet pomohli udělat vynikající!

|Kdo|PRS|Problémy|
|----|----|----|
[přidchytá–z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | Rozsah verzí nemůže parsovat jednociferné rozsahy – [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid (id souboru)](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | Nefunkční build.sh NuGet.Client [– #10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | Nefunkční build.sh NuGet.Client [– #10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | Výkon "balíčku NuGet" se snižuje s rostoucími úrovněmi ve zdrojových cestách – [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe s výkonem balíčku . relative path – [#5016](https://github.com/NuGet/Home/issues/5016)
[přichytávka-smyšlová](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM – Problémy se souběžnosti v algoritmu cházek v grafu – [#10598](https://github.com/NuGet/Home/issues/10598)
[přisudky](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | Přidejte typ projektu nfproj do seznamu supportedProjectExtensions pro rozhraní příkazového řádku NuGet. - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>Váš názor – vítejte

Vaše názory jsou pro nás důležité.  Pokud se v této verzi vyskytnou nějaké problémy, podívejte se na naše [problémy GitHubu](https://github.com/NuGet/Home/issues) a [komunitu vývojářů pro Visual Studio](https://developercommunity.visualstudio.com/) , kde najdete stávající problémy.  Pro nové problémy v rámci NuGet ohlaste [problém GitHubu](https://github.com/NuGet/Home/issues/new).
Pro obecné problémy s prostředím NuGet nám dejte informace v části **Help > nahlásit problém** pomocí možnosti [nahlásit problém](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) , která se nachází ve vašem oblíbeném prostředí IDE.
