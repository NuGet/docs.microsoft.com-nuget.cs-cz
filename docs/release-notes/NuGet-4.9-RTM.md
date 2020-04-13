---
title: NuGet 4.9 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.9 včetně známých problémů, oprav chyb, nových funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496465"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 Poznámky k verzi

Distribuční vozidla NuGet:

| NuGet verze | K dispozici ve verzi sady Visual Studio| K dispozici v sadach .NET SDK|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 verze 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | neuvedeno | neuvedeno |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 verze 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 verze 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Shrnutí: Co je nového v 4.9.0

* Podepisování: Povolit zásadám ClientPolicies vyžadovat použití sady důvěryhodných autorů a úložišť uvedených v souboru NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [příspěvku blogu](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* vytvořit ".snupkg" soubory, které obsahují symboly v balení - zvýšit push pochopit nuget protokol přijímat snupkg soubory pro symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet přihlašovací plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* Samostatné balíčky NuGet - Licence - [#4628](https://github.com/NuGet/Home/issues/4628), [oznámení](https://github.com/NuGet/Announcements/issues/32)

* Povolte přihlášení metadata "GeneratePathProperty" na PackageReference pro generování vlastnosti MSBuild na balíček\" do adresáře Foo.Bar\1.0 - [#6949](https://github.com/NuGet/Home/issues/6949)

* Zlepšete úspěch zákazníků s operacemi NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)

* Povolení opakovatelných obnovení balíčků pomocí souboru zámku - [#5602](https://github.com/NuGet/Home/issues/5602), [oznámení](https://github.com/NuGet/Announcements/issues/28), [příspěvek blogu](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Upozornění zvýšené na chyby (přes WarnAsErrors) vyvolané PackageExtraction by nikdy opustit extrahovaný balíček kolem - [#7445](https://github.com/NuGet/Home/issues/7445)

* Špatně podepsané balíčky by neměly skončit ve složce globálních balíčků - [#7423](https://github.com/NuGet/Home/issues/7423)

* generování přesměrování vazby by nemělo přeskočit sestavy fasád - [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals neporovnává plovoucí rozsahy - [#7324](https://github.com/NuGet/Home/issues/7324)

* Obnovení: regrese výkonu pomocí nového zásobníku HTTP .NET Core 2.1 - [#7314](https://github.com/NuGet/Home/issues/7314)

* Aktualizace Package by neměla měnit PrivateAssets PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)

* Podepisování: podepisování by mělo selhat, pokud balíček má příliš mnoho položek balíčku (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)

* "dotnet nuget push" kódová cesta by měla podporovat nového zprostředkovatele pověření - [#7233](https://github.com/NuGet/Home/issues/7233)

* Podpora provádění pluginů s invariantní jazykovou verzí (jak se děje v dockeru) - [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget zdroje přidat by neměl a odstranit pověření z NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)

* instalace devDependency PackageReference by měla být výchozí pro excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)

* opravit možnost migrator, která má být zobrazena pro všechny projekty a zobrazit chybu, pokud je projekt nekompatibilní - [#6958](https://github.com/NuGet/Home/issues/6958)

* "dotnet add package" by měl potvrdit obnovení, které provádí do souboru datových zdrojů - [#6928](https://github.com/NuGet/Home/issues/6928)

* Podepisování: zlepšit podepisování související choujecí zprávy - [#6906](https://github.com/NuGet/Home/issues/6906)

* [Selhání testu] To je v pořádku. Řetězec "Konzola správce balíčků" není lokalizovat na konzoli Správce balíčků - [#6381](https://github.com/NuGet/Home/issues/6381)

* Chybová zpráva kolem "Nelze najít informace o projektu" by měla být trochu konkrétnější uvnitř VS - [#5350](https://github.com/NuGet/Home/issues/5350)

* Neužitečné chybové hlášení při nesprávném použití nuspec verze značky nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - Podepisování: podpora protokolu NuGet: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)

* Soubor DCR - .nupkg.metadata bude nyní vytvořen během extrakce balíčku - obsahuje "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - Přeskočit ověření authenticode pro pluginy při provádění na Mono - [#7222](https://github.com/NuGet/Home/issues/7222)

[Seznam všech problémů opravených v této verzi 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Shrnutí: Co je nového v 4.9.1

* Přidejte podporu pro čtení zápisu do nuget.config pomocí nového příkazu trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Oprava generování licenčního propojení - [#7515](https://github.com/NuGet/Home/issues/7515)

* Regrese kódů chyb pro ověřování podpisů - [#7492](https://github.com/NuGet/Home/issues/7492)

* Balíček NuGet.Build.Tasks.Pack nemá informace o licenci - [#7379](https://github.com/NuGet/Home/issues/7379)

[Seznam všech problémů opravených v této verzi 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Shrnutí: Co je nového v 4.9.2

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* VS/dotnet.exe/nuget.exe/msbuild.exe restore nepoužívá pověření, pokud název zdroje obsahuje mezery - [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow a LicenseFileWindow Problémy s usnadněním přístupnosti - [#7452](https://github.com/NuGet/Home/issues/7452)

* Opravit FormatException v DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)

[Seznam všech problémů opravených v této verzi 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Shrnutí: Co je nového v 4.9.3

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>Problémy s opakováním balíčku se obnoví pomocí uzamykaného souboru

* Uzamčený režim nefunguje tak, jak je hash vypočtena nesprávně pro dříve uložené balíčky - [#7682](https://github.com/NuGet/Home/issues/7682)

* Obnovení se změní na jinou `packages.lock.json` verzi, než je definováno v souboru – [#7667](https://github.com/NuGet/Home/issues/7667)

* '--locked-mode / RestoreLockedMode' způsobuje falešné obnovení selhání při ProjectReferences jsou zapojeny - [#7646](https://github.com/NuGet/Home/issues/7646)

* Překladač sady MSBuild SDK se pokusí ověřit sha pro balíček Sady SDK, který se nezdaří obnovení při použití packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>Problémy s uzamčením závislostí pomocí konfigurovatelných zásad důvěryhodnosti
* dotnet.exe by neměl vyhodnocovat důvěryhodné podepisující, pokud podepsané balíčky nejsou podporovány – [#7574](https://github.com/NuGet/Home/issues/7574)

* Pořadí důvěryhodných typů v konfiguračním souboru ovlivňuje hodnocení důvěryhodnosti - [#7572](https://github.com/NuGet/Home/issues/7572)

* Nelze implementovat ISettings [Způsobené refaktoringnastavení nastavení API pro podporu zásad důvěryhodnosti funkce] - [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>"Vylepšené problémy s laděním"

* Balíček symbolů pro globální nástroj .NET Core nelze publikovat [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>"Samostatné balíčky NuGet - licence" Problémy

* Chyba při vytváření symbolu .snupkg balíček při použití vloženého licenčního souboru - [#7591](https://github.com/NuGet/Home/issues/7591)

[Seznam všech problémů opravených v této verzi 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Shrnutí: Co je nového v 4.9.4

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>Známé problémy

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>dotnet nuget push --interactive dává chybu na Macu. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problém
Argument `--interactive` není předáván dotnet cli a má za následek chybu`error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Alternativní řešení
Spusťte jakýkoli jiný příkaz dotnet `dotnet restore --interactive` s interaktivní volbou, například a ověřte. Ověřování pak může být uloženo do mezipaměti zprostředkovatelem pověření. Potom spusťte `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Balíčky v záložních složkách nainstalované sadou .NET Core SDK jsou nainstalovány na vlastní instalaci a nepodaří se ověření podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problém
Při použití dotnet.exe 2.x obnovit projekt, který více-cíle netcoreapp 1.x a netcoreapp 2.x, záložní složka je považována za soubor krmiva. To znamená, že při obnovení NuGet vybere balíček ze záložní složky a pokusí se jej nainstalovat do složky globální balíčky a provést obvyklé ověření podepisování, které se nezdaří.

#### <a name="workaround"></a>Alternativní řešení
Zakažte použití záložní složky `RestoreAdditionalProjectSources` nastavením na nic. `<RestoreAdditionalProjectSources/>`Používejte to s opatrností, protože to způsobí, že mnoho balíčků ke stažení z NuGet.org které by jinak byly obnoveny ze záložní složky.
