---
title: Zpráva k vydání verze NuGet 4.9 RTM
description: Zpráva k vydání verze pro NuGet 4.9 včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: aa9bf87504477506dbb1e9ac10d5c1d5841c224f
ms.sourcegitcommit: 885973352d31808e3ddbb45da6d6e54d1e4fca9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/13/2019
ms.locfileid: "56224941"
---
# <a name="nuget-49-release-notes"></a>Zpráva k vydání verze 4.9 NuGet

Distribuce vozidel NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v rozhraní .NET SDK, pomocí kterých|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 verze 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | není k dispozici | není k dispozici |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 version 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 verze 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Shrnutí: Co je nového v 4.9.0

* Podpis: Povolit ClientPolicies vyžadují použití sady úložišť uvedené v souboru NuGet.Config – a důvěryhodné autoři [#6961](https://github.com/NuGet/Home/issues/6961), [blogový příspěvek](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* Vytvoření souborů ".snupkg" obsahovat symboly v sadě – vylepšovat nabízené pochopit protokol nuget tak, aby přijímal soubory snupkg pro server symbolů - [#6878](https://github.com/NuGet/Home/issues/6878), [blogový příspěvek](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* Plugin přihlašovacích údajů NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)

* Samostatné balíčky NuGet - licence - [#4628](https://github.com/NuGet/Home/issues/4628), [oznámení](https://github.com/NuGet/Announcements/issues/32)

* Umožňují vyjádřit výslovný souhlas metadat "GeneratePathProperty" na PackageReference ke generování jednu vlastnost MSBuild balíčku na "Foo.Bar\1.0\" directory – [#6949](https://github.com/NuGet/Home/issues/6949)

* Zlepšení úspěchy zákazníků s operacemi NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)

* Povolení opakovatelných balíček obnovení pomocí zámek souboru - [#5602](https://github.com/NuGet/Home/issues/5602), [oznámení](https://github.com/NuGet/Announcements/issues/28), [blogový příspěvek](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Upozornění na chyby (prostřednictvím WarnAsErrors) vyvolané PackageExtraction by nikdy neopustí extrahované balíček kolem - [#7445](https://github.com/NuGet/Home/issues/7445)

* Nesprávně podepsané balíčky by neměl ukládaly do složky globálních balíčků - [#7423](https://github.com/NuGet/Home/issues/7423)

* vytváření přesměrování vazby neměli přeskočit sestavení průčelí - [#7393](https://github.com/NuGet/Home/issues/7393)

* Rovná VersionRange nebude porovnání s plovoucí desetinnou čárkou rozsahy - [#7324](https://github.com/NuGet/Home/issues/7324)

* Obnovení: zásobník regrese výkonu pomocí nového rozhraní .NET Core 2.1 HTTP - [#7314](https://github.com/NuGet/Home/issues/7314)

* Aktualizace balíčku neměli měnit PrivateAssets PackageReference – [#7285](https://github.com/NuGet/Home/issues/7285)

* Podepisování: podepisování musí selhat, pokud balíček obsahuje příliš mnoho položek balíčku (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)

* cestu "dotnet nuget push" by měl podporu nového poskytovatele přihlašovacích údajů – [#7233](https://github.com/NuGet/Home/issues/7233)

* Podpora provádění modulů plug-in pomocí neutrální jazykové verze (stejně jako se stane v dockeru) - [#7223](https://github.com/NuGet/Home/issues/7223)

* Přidání zdroje nuget by neměla odstranit přihlašovací údaje ze souboru NuGet.config – [#7200](https://github.com/NuGet/Home/issues/7200)

* instalace devDependency PackageReference by ve výchozím nastavení excludeassets = kompilace - [#7084](https://github.com/NuGet/Home/issues/7084)

* oprava možnosti migrator má být zobrazen pro všechny projekty a zobrazit chybu, pokud projekt není kompatibilní - [#6958](https://github.com/NuGet/Home/issues/6958)

* "příkaz dotnet add package" musí potvrdit obnovení provádí do souboru prostředků – [#6928](https://github.com/NuGet/Home/issues/6928)

* Podepisování: zlepšení podpisový související chybové zprávy – [#6906](https://github.com/NuGet/Home/issues/6906)

* [Selhání testu] [zh-TW] V konzole Správce balíčků - nebude lokalizovat řetězce "Konzola správce balíčků" [#6381](https://github.com/NuGet/Home/issues/6381)

* Chybová zpráva kolem "Nepodařilo se najít informace o projektu" by měl být mírně konkrétnější v sadě VS - [#5350](https://github.com/NuGet/Home/issues/5350)

* Neužitečné chybové zprávy, pokud nesprávně tagu nuspec verze balíčku nuget - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR – podepisování: podporují protokol NuGet: Prostředek RepositorySignatures/4.9.0 – [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR –. během extrakce balíčku - obsahuje "content-hash" - se nyní vytvoří soubor nupkg.metadata [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - přeskočit ověření pomocí technologie authenticode pro moduly plug-in při provádění v Mono - [#7222](https://github.com/NuGet/Home/issues/7222)

[Seznam všech problémů, které jsou opravené v této verzi 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Shrnutí: Co je nového v 4.9.1

* Přidání podpory pro čtení zápis do souboru nuget.config prostřednictvím nový příkaz důvěryhodné – podepisující osoby - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Oprava generování odkazů licence - [#7515](https://github.com/NuGet/Home/issues/7515)

* Kódy chyb pro ověřování podpisů regrese- [#7492](https://github.com/NuGet/Home/issues/7492)

* Balíček NuGet.Build.Tasks.Pack nemá žádné informace o licencích - [#7379](https://github.com/NuGet/Home/issues/7379)

[Seznam všech problémů, které jsou opravené v této verzi 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Shrnutí: Co je nového v 4.9.2

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Obnovení VS/dotnet.exe/nuget.exe/msbuild.exe nepoužívá přihlašovacích údajů, když název zdroje obsahuje prázdný znak - [#7517](https://github.com/NuGet/Home/issues/7517)

* Problémů s dostupností LicenseFileWindow a LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)

* Oprava FormatException v DateTime.Parse z DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)

[Seznam všech problémů, které jsou opravené v této verzi 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Shrnutí: Co je nového v 4.9.3

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>Problémy s "Opakovatelné balíček obnovení pomocí souboru zámku"

* Uzamčeném režimu nebudou fungovat podle hodnoty hash se počítá nesprávně pro dříve uložené v mezipaměti balíčky - [#7682](https://github.com/NuGet/Home/issues/7682)

* Obnovení se překládá na jinou verzi než definované v `packages.lock.json` soubor – [#7667](https://github.com/NuGet/Home/issues/7667)

* "--uzamčen režim / RestoreLockedMode' způsobuje nesprávné selhání obnovení, když se podílejí projectreferences má za následek - [#7646](https://github.com/NuGet/Home/issues/7646)

* Překladač sady MSBuild SDK se pokusí ověřit SHA pro balíček sady SDK, které při používání packages.lock.json – se nezdaří obnovení [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>Problémy s "Zamknout závislostí pomocí vztahu důvěryhodnosti Konfigurovatelné zásady"
* DotNet.exe by neměl vyhodnotit důvěryhodné podepisující osoby, zatímco podepsané balíčky nejsou podporovány - [#7574](https://github.com/NuGet/Home/issues/7574)

* Pořadí trustedSigners v konfiguračním souboru ovlivňuje vyhodnotit důvěryhodnost - [#7572](https://github.com/NuGet/Home/issues/7572)

* Nejde implementovat ISettings [způsobené refaktoring nastavení rozhraní API k podpoře funkce zásady důvěryhodnosti]- [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>Problémy s "Vylepšené možnosti ladění"

* Nejde publikovat balíček symbolů pro globální nástroji .NET Core – [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>Problémy s "Balíčky NuGet samostatná - licence"

* Chyba při sestavování .snupkg balíček symbolů při použití vložený soubor s licencí - [#7591](https://github.com/NuGet/Home/issues/7591)

[Seznam všech problémů, které jsou opravené v této verzi 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a>Známé problémy

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>DotNet nuget příkaz push--interaktivní vrátí chybu v systému Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problém
`--interactive` Argument není předávaná pomocí rozhraní příkazového řádku dotnet což vede k chybě `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Alternativní řešení
Spuštění další příkaz dotnet pomocí interaktivní možnosti, jako `dotnet restore --interactive` a provést ověření. Ověřování potom může do mezipaměti podle poskytovatele přihlašovacích údajů. Potom spusťte `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problém
Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu. To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.

#### <a name="workaround"></a>Alternativní řešení
Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` na hodnotu nothing. `<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.
