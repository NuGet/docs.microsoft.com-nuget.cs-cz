---
title: Zpráva k vydání verze NuGet 4,8 RTM
description: Zpráva k vydání verze pro NuGet 4.8.1 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: d23c4a8874d3d2e1a9ea721c66b15bb458de88a3
ms.sourcegitcommit: 47858da1103848cc1b15bdc00ac7219c0ee4a6a0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/12/2018
ms.locfileid: "44516244"
---
# <a name="nuget-48-rtm-release-notes"></a>Zpráva k vydání verze NuGet 4,8 RTM

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.8 funkce.

Příkazový řádek verze stejné funkce jsou také k dispozici:
* 4.8 - NuGet.exe [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-this-release"></a>Souhrn: Novinky v této verzi
* Longfilenames NuGet.exe teď podporuje ve Windows 10 - [#6937](https://github.com/NuGet/Home/issues/6937)
* Moduly plug-in ověřování nyní pracovat napříč MsBuild, DotNet.exe, NuGet.exe a sady Visual Studio, včetně různé platformy. První generace moduly plug-in ověřování nejsou podporované v nástroji MsBuild, DotNet.exe. Poznámka: Verze Preview VS 2017 15.9 sestavení mají modul plug-in VSTS ověřování zahrnuté. [#6486](https://github.com/NuGet/Home/issues/6486)
* Překladač pro MsBuild SDK nyní sestavení jako součást balíčku nuget a nainstaluje pomocí nástroje NuGet pro VS. Tím se vyhnete si synchronizaci získání verze. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference teď podporuje metadata DevelopmentDependency – [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="known-issues"></a>Známé problémy
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>Na počítači CI nebo v prostředí offline instalace podepsané balíčky trvá déle než obvykle.

#### <a name="issue"></a>Problém
Pokud je počítač omezil přístup k Internetu (například počítač sestavení ve scénáři CI/CD), instalace/obnovuje se balíček nuget podpisem způsobí upozornění ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)) od servery odvolání počítačů nejsou dostupní. To je očekávané chování. Nicméně v některých případech to může mít nežádoucí concequences například balíček instalace a obnovení trvá déle než obvykle.

#### <a name="workaround"></a>Alternativní řešení
Aktualizace sady Visual Studio 15.8.4 a NuGet.exe 4.8.1, kde jsme představili proměnnou prostředí pro přepnutí režimu kontroly odvolání.
Nastavení `NUGET_CERT_REVOCATION_MODE` proměnnou prostředí, aby `offline` vynutí NuGet a zkontrolujte stav odvolání certifikátu pouze proti seznamu odvolaných certifikátů uložené v mezipaměti a NuGet se nepokusí mohly spojit se servery odvolání. Pokud je režim kontroly odvolání nastavená na `offline`, upozornění se downgradovat na informace.

> [!Warning]
> Není doporučeno přepnout režim kontroly odvolání na offline v části obvyklé okolnosti. To způsobí, že správci balíčků NuGet Přeskočit kontrolu odvolání online a provádět pouze kontrolu offline odvolání proti seznamu odvolaných certifikátů uložené v mezipaměti, který může být zastaralá. Tento znamená, že balíčky, kde podpisový certifikát může být odvolán, bude nainstalována nebo obnovit, jinak by nezdařila kontrola odvolání a nebude nainstalován.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` Možnost není k dispozici v místní nabídce klikněte pravým tlačítkem na

#### <a name="issue"></a>Problém

Při prvním otevření projektu NuGet nemusí mít inicializace, dokud se provádí operace NuGet. To způsobí, že není uveden v místní nabídce klikněte pravým tlačítkem na možnost migrace `packages.config` nebo `References`.

#### <a name="workaround"></a>Alternativní řešení

Proveďte některou z následujících akcí NuGet:
* Otevřít uživatelské rozhraní Správce balíčků – klikněte pravým tlačítkem na `References` a vyberte `Manage NuGet Packages...`
* Otevřete konzolu Správce balíčků pro - ze `Tools > NuGet Package Manager`vyberte `Package Manager Console`
* Spuštění obnovení NuGet – klikněte pravým tlačítkem na uzel řešení v Průzkumníku řešení a vyberte `Restore NuGet Packages`
* Sestavte projekt, který také aktivuje obnovení NuGet

Teď by měl být vidět možnost migrace. Všimněte si, že tato možnost není podporována a nezobrazí se pro typy projektů ASP.NET a C++.
Poznámka: Tato chyba byla opravena v sadě VS 2017 15.9 Preview 3

## <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

### <a name="bugs"></a>Chyby
#### <a name="signing"></a>podepisování
* Podepisování: Instalace podepsaný balíček v offline prostředí [#7008](https://github.com/NuGet/Home/issues/7008) – oprava v 4.8.1
* Podepisování: nesprávná adresa URL Kontrola – [#7174](https://github.com/NuGet/Home/issues/7174)
* Podepisování: Kontrola integrity balíčku v RepositorySignatureVerifier při balíčku je úložiště potvrzeným - [#6926](https://github.com/NuGet/Home/issues/6926)
* "Kontrola Integrity balíčku neproběhla úspěšně." musí mít ID balíčku v zprávu (a kódem chyby) - [#6944](https://github.com/NuGet/Home/issues/6944)
* Úložiště podepsané balíčky, které jsou podepsány jiný certifikát – umožňuje ověřování balíčků [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet – podepisování – adresy URL časového razítka nemůže být https://? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Není NullRef v souboru NuSpec balení scénáři, také zlepšit možnosti - [#6866](https://github.com/NuGet/Home/issues/6866)
* Paměť není platný při aktualizaci informací o podepisující osoba při přidávání časové razítko potvrzovací podpis - [#6840](https://github.com/NuGet/Home/issues/6840)
* Podepisování: odebrání výjimky CTL - [#6794](https://github.com/NuGet/Home/issues/6794)
* Podepisování: contentUrl musí používat protokol HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* Podepisování: SignedPackageVerifierSettings.VSClientDefaultPolicy se nepoužívá - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>balíček
* obnovení a sestavení by neměl být potřeba při používání dotnet.exe se zabalit nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)
* Povolit prázdný nahrazení tokeny v NuspecProperties - [#6722](https://github.com/NuGet/Home/issues/6722)
* Packtask se neposkytl NullReferenceException vyvolá, když je zadán NuspecProperties - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Usnadnění
* [Usnadnění] Řetězec "Předběžná verze" pod tlačítko balíčku se bude vztahovat jeho popis balíčku v uživatelském rozhraní odp. - [#4504](https://github.com/NuGet/Home/issues/4504)
* [Usnadnění] Balíček zdroj rozevíracího seznamu a tlačítko nastavení při výběru 'Balíčky společnosti Microsoft Visual Studio Offline' v uživatelském rozhraní odp. - [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Konzola pro správu Powershellu (PMC)
* `Update-Package` ignoruje se rozsah verzí PackageReference – [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` řešení problém zahrnující celou - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` Configuration Manager přeinstaluje všechny balíčky, ne jen pojmenované - [#737](https://github.com/NuGet/Home/issues/737)
* Můžete aktualizovat z konzole Správce balíčků - neuvedené balíček NuGet [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Různé
* Chcete-li vyřešit `NuGet update self` NuGet.Commandline nupkg by neměl být semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* Zlepšení zkušeností s chybami instalace NU1107 - [#7107](https://github.com/NuGet/Home/issues/7107)
* Serializace GetAuthenticationCredentialRequest je nesprávný - [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage se nepodaří načíst při inicializaci mimo vlákno uživatelského rozhraní – [#6976](https://github.com/NuGet/Home/issues/6976)
* Obnovení je vytváření sestav, je potřeba zavádějící chyby s oznámením project.json - [#6959](https://github.com/NuGet/Home/issues/6959)
* Uživatelské rozhraní Správce balíčků: náhled změn, nejsou automaticky nedodržíte pomocí klávesnice – tlačítko ok [#6893](https://github.com/NuGet/Home/issues/6893)
* Pro projekt s odkazy p2p – jsou ignorovány RestoreSources [#6776](https://github.com/NuGet/Home/issues/6776)
* Vytvoření projektu testování částí pomocí rozhraní .NET Framework šablony starší model projektu se otevře soubor packages.config - [#6736](https://github.com/NuGet/Home/issues/6736)
* Povolit odkaz na projekt pro přepsání závislost balíčku - [#6536](https://github.com/NuGet/Home/issues/6536)
* Vystavení v úkolu MSBuild - NoDefaultExcludes [#6450](https://github.com/NuGet/Home/issues/6450)
* Stavová zpráva pro "Vymazat všechny mezipaměti NuGet" může být skrytá okna velikost - [#5938](https://github.com/NuGet/Home/issues/5938)


[Seznam všech problémů, které jsou opravené v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
