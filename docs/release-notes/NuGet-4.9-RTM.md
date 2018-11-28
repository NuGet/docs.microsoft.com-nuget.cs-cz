---
title: Zpráva k vydání verze NuGet 4.9 RTM
description: Zpráva k vydání verze pro NuGet 4.9 včetně známých problémů, opravy chyb, nových funkcích a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453793"
---
# <a name="nuget-49-release-notes"></a>Zpráva k vydání verze 4.9 NuGet

[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.9.0 funkce.


Příkazový řádek verze stejné funkce jsou také k dispozici:
* NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-490"></a>Souhrn: Co je nového v 4.9.0

* Podepisování: Povolit ClientPolicies vyžadují použití sady úložišť uvedené v souboru NuGet.Config – a důvěryhodné autoři [#6961](https://github.com/NuGet/Home/issues/6961)

* Vytvoření souborů ".snupkg" obsahovat symboly v sadě – vylepšovat nabízené pochopit protokol nuget tak, aby přijímal soubory snupkg pro server symbolů - [#6878](https://github.com/NuGet/Home/issues/6878)

* Plugin přihlašovacích údajů NuGet V2 – [#6642](https://github.com/NuGet/Home/issues/6642)

* Samostatný NuGet balíčky - licence - [#4628](https://github.com/NuGet/Home/issues/4628)

* Umožňují vyjádřit výslovný souhlas metadat "GeneratePathProperty" na PackageReference ke generování jednu vlastnost MSBuild balíčku na "Foo.Bar\1.0\" directory – [#6949](https://github.com/NuGet/Home/issues/6949)

* Zlepšení úspěchy zákazníků s operacemi NuGet - [#7108](https://github.com/NuGet/Home/issues/7108)

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

* DCR – podepisování: podporují protokol NuGet: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR –. během extrakce balíčku - obsahuje "content-hash" - se nyní vytvoří soubor nupkg.metadata [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - přeskočit ověření pomocí technologie authenticode pro moduly plug-in při provádění v Mono - [#7222](https://github.com/NuGet/Home/issues/7222)

[Seznam všech problémů, které jsou opravené v této verzi 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Souhrn: Co je nového v 4.9.1

* Přidání podpory pro čtení zápis do souboru nuget.config prostřednictvím nový příkaz důvěryhodné – podepisující osoby - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Oprava generování odkazů licence - [#7515](https://github.com/NuGet/Home/issues/7515)

* Kódy chyb pro ověřování podpisů regrese- [#7492](https://github.com/NuGet/Home/issues/7492)

* Balíček NuGet.Build.Tasks.Pack nemá žádné informace o licencích - [#7379](https://github.com/NuGet/Home/issues/7379)

[Seznam všech problémů, které jsou opravené v této verzi 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a>Známé problémy

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a>DotNet.exe/nuget.exe nepoužívá přihlašovacích údajů, když název zdroje obsahuje prázdný znak - [#7517](https://github.com/NuGet/Home/issues/7517)

#### <a name="issue"></a>Problém
Pokud je prázdný znak v názvu zdroje, nuget.exe vyvolá chybu jako `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`

#### <a name="workaround"></a>Alternativní řešení
Změňte název zdroje nebude obsahovat prázdný znak.

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>DotNet nuget příkaz push--interaktivní vrátí chybu v systému Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problém
`--interactive` Argument není předávaná pomocí rozhraní příkazového řádku dotnet což vede k chybě `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Alternativní řešení
Spuštění další příkaz dotnet pomocí interaktivní možnosti, jako `dotnet restore --interactive` a provést ověření. Ověřování potom může do mezipaměti podle poskytovatele přihlašovacích údajů. Potom spusťte `dotnet nuget push`.

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a>Problémů s dostupností LicenseFileWindow a LicenseAcceptanceWindow - [#7452](https://github.com/NuGet/Home/issues/7452)

#### <a name="issue"></a>Problém
Okno přijetí licence a okno licenční soubor mají problémy s pomocí navigace klávesnicí a komentář pomocí čtečky obrazovky a čtečky JAWS.

#### <a name="workaround"></a>Alternativní řešení
Alternativní řešení neexistuje.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>Balíčky v FallbackFolders nainstalovat sadu .NET Core SDK jsou vlastní nainstalované a selhání ověření podpisu. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problém
Při použití dotnet.exe 2.x tak, aby obnovení této netcoreapp více cílů projektu 1.x a netcoreapp 2.x, záložní složky je považován za soubor informačního kanálu. To znamená, při obnovování, NuGet se vybrat balíček ze záložní složky a zkuste nainstalovat je do složky globálních balíčků a na obvyklé podpisový ověřování, který se nezdaří.

#### <a name="workaround"></a>Alternativní řešení
Zakázat používání složky pro použití náhradní lokality tak, že nastavíte `RestoreAdditionalProjectSources` na hodnotu nothing. `<RestoreAdditionalProjectSources/>` Použití opatrně, protože to způsobí, že mnoho balíčků, které mají být stažené z NuGet.org, který jinak by bylo obnoveno ze záložní složky.
