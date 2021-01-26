---
title: Poznámky k verzi NuGet 4,9 RTM
description: Poznámky k verzi pro NuGet 4,9, včetně známých problémů, oprav chyb, nových funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780144"
---
# <a name="nuget-49-release-notes"></a>Zpráva k vydání verze NuGet 4,9

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 verze 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | Není k dispozici | Není k dispozici |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 verze 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 verze 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Shrnutí: co je nového v 4.9.0

* Podepisování: Povolte ClientPolicies, aby vyžadovala použití sady důvěryhodných autorů a úložišť uvedených v NuGet.Config- [#6961](https://github.com/NuGet/Home/issues/6961), [Blogový příspěvek](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html) .

* Vytvoření souborů. snupkg, které obsahují symboly v sadě Pack – vylepší nabízení oznámení protokolu NuGet pro příjem souborů snupkg pro symbol server – [#6878](https://github.com/NuGet/Home/issues/6878), [Blogový příspěvek](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* Modul plug-in přihlašovacích údajů NuGet v2 – [#6642](https://github.com/NuGet/Home/issues/6642)

* Self-Contained balíčků NuGet – License- [#4628](https://github.com/NuGet/Home/issues/4628), [oznámení](https://github.com/NuGet/Announcements/issues/32)

* Povolení výslovných GeneratePathProperty metadat na PackageReference pro vygenerování vlastnosti MSBuild pro balíček do adresáře foo. Bar\1.0 \" – [#6949](https://github.com/NuGet/Home/issues/6949)

* Zlepšení úspěšnosti zákazníků pomocí operací NuGet – [#7108](https://github.com/NuGet/Home/issues/7108)

* Povolit opakovaně obnovitelné balíčky pomocí zámku souboru – [#5602](https://github.com/NuGet/Home/issues/5602), [oznámení](https://github.com/NuGet/Announcements/issues/28), [Blogový příspěvek](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Upozornění se zvýšenými oprávněními (přes WarnAsErrors) vyvolaná PackageExtraction by nikdy neměla opustit extrahovaný balíček [#7445](https://github.com/NuGet/Home/issues/7445)

* Nesprávně podepsané balíčky by neměly končit ve složce globálních balíčků – [#7423](https://github.com/NuGet/Home/issues/7423)

* generování přesměrování vazby by nemělo přeskočit sestavení fasády – [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals se nerovná plovoucí rozsahy – [#7324](https://github.com/NuGet/Home/issues/7324)

* Obnovení: regrese výkonu pomocí nového rozhraní .NET Core 2,1 HTTP Stack- [#7314](https://github.com/NuGet/Home/issues/7314)

* Aktualizace balíčku by neměla upravovat PrivateAssets PackageReference- [#7285](https://github.com/NuGet/Home/issues/7285)

* Podepisování: když má balíček příliš mnoho položek balíčku (>65534), podpis by se nezdařil. [#7248](https://github.com/NuGet/Home/issues/7248)

* "dotnet NuGet push" codepath by měl podporovat nového poskytovatele pověření – [#7233](https://github.com/NuGet/Home/issues/7233)

* Podpora spouštění modulů plug-in s invariantní jazykovou verzí (jak se děje v Docker) – [#7223](https://github.com/NuGet/Home/issues/7223)

* Přidání zdrojů NuGet by nemělo odstraňovat přihlašovací údaje z NuGet.config- [#7200](https://github.com/NuGet/Home/issues/7200)

* instalace devDependency PackageReference by měla být standardně excludeassets = Compile- [#7084](https://github.com/NuGet/Home/issues/7084)

* Oprava možnosti migrace, která se zobrazí pro všechny projekty a zobrazí chybu, pokud je projekt nekompatibilní – [#6958](https://github.com/NuGet/Home/issues/6958)

* příkaz dotnet Add Package by měl potvrdit jeho obnovení do souboru prostředků – [#6928](https://github.com/NuGet/Home/issues/6928)

* Podepisování: Vylepšete chybové zprávy související s podepisováním – [#6906](https://github.com/NuGet/Home/issues/6906)

* [Selhání testu] [zh-TW] Řetězec "Konzola správce balíčků" není lokalizována do konzoly Správce balíčků – [#6381](https://github.com/NuGet/Home/issues/6381)

* Chybová zpráva: Nepodařilo se najít informace o projektu, musí být v sadě VS- [#5350](https://github.com/NuGet/Home/issues/5350) o něco konkrétnější.

* Chybná chybová zpráva, pokud je nesprávně použita značka verze nuspec sady NuGet Pack- [#2714](https://github.com/NuGet/Home/issues/2714)

* Registrace pro DCR: podpora protokolu NuGet: RepositorySignatures/4.9.0 Resource- [#7421](https://github.com/NuGet/Home/issues/7421)

* Soubor DCR-. nupkg. Metadata se teď vytvoří během extrakce balíčku – obsahuje Content-hash- [#7283](https://github.com/NuGet/Home/issues/7283) .

* DCR – přeskočení ověřování Authenticode pro moduly plug-in při spuštění na mono- [#7222](https://github.com/NuGet/Home/issues/7222)

[Seznam všech problémů opravených v této verzi 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Shrnutí: co je nového v 4.9.1

* Přidání podpory pro čtení zápisu do nuget.config pomocí nového příkazu Trusted-signers- [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* Oprava generování odkazu na licenci – [#7515](https://github.com/NuGet/Home/issues/7515)

* Regrese chybových kódů pro ověřování podpisů – [#7492](https://github.com/NuGet/Home/issues/7492)

* Balíček NuGet. Build. Tasks. Pack neobsahuje informace o licenci – [#7379](https://github.com/NuGet/Home/issues/7379)

[Seznam všech problémů opravených v této verzi 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Shrnutí: co je nového v 4.9.2

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

* VS/dotnet.exe/nuget.exe/msbuild.exe obnovení nepoužívá přihlašovací údaje, pokud název zdroje obsahuje prázdný znak [#7517](https://github.com/NuGet/Home/issues/7517)

* Problémy s přístupností LicenseAcceptanceWindow a LicenseFileWindow – [#7452](https://github.com/NuGet/Home/issues/7452)

* Oprava FormatException v DateTime. Parse z DateTimeConverter- [#7539](https://github.com/NuGet/Home/issues/7539)

[Seznam všech problémů opravených v této verzi 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Shrnutí: co je nového v 4.9.3

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>"Opakované obnovení balíčku pomocí souboru zámku" problémy

* Uzamčený režim nefunguje, protože hash je nesprávně počítaný pro předchozí balíčky v mezipaměti – [#7682](https://github.com/NuGet/Home/issues/7682)

* Obnovení se překládá na jinou verzi, než je definované v `packages.lock.json` souboru – [#7667](https://github.com/NuGet/Home/issues/7667)

* '--Locked-Mode/RestoreLockedMode ' způsobuje selhání obnovení spurious, když jsou zapojeny ProjectReferences – [#7646](https://github.com/NuGet/Home/issues/7646)

* Překladač sady MSBuild SDK se pokusí ověřit SHA pro balíček sady SDK, který při použití packages.lock.jspři [#7599](https://github.com/NuGet/Home/issues/7599) se nezdařil.

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>"Jak uzamknout závislosti pomocí konfigurovatelných zásad důvěryhodnosti"
* dotnet.exe by neměl vyhodnocovat důvěryhodné podepsané, zatímco podepsané balíčky nejsou podporovány – [#7574](https://github.com/NuGet/Home/issues/7574)

* Pořadí trustedSigners v konfiguračním souboru má vliv na vyhodnocení důvěryhodnosti – [#7572](https://github.com/NuGet/Home/issues/7572)

* Nejde implementovat ISettings [způsobené refaktoringem rozhraní API nastavení pro podporu zásad důvěryhodnosti funkce]- [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>"Vylepšené možnosti ladění"

* Nelze publikovat balíček symbolů pro globální nástroj .NET Core – [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>Problémy "samostatné balíčky NuGet – licence"

* Při sestavování balíčku symbol. snupkg při použití vloženého souboru licence došlo k chybě – [#7591](https://github.com/NuGet/Home/issues/7591)

[Seznam všech problémů opravených v této verzi 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Shrnutí: co je nového v 4.9.4

* Oprava zabezpečení: oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .


## <a name="known-issues"></a>Známé problémy

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>dotnet NuGet push--Interactive poskytuje chybu v počítači Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Problém
Rozhraní příkazového `--interactive` řádku dotnet nepřesměrovává na argument a výsledkem je chyba. `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Alternativní řešení
Spusťte jakýkoli jiný příkaz dotnet s interaktivní možností, jako je například `dotnet restore --interactive` a ověřování. Ověřování pak může poskytovatel přihlašovacích údajů Uložit do mezipaměti. Potom spusťte `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>Balíčky v FallbackFolders nainstalované pomocí .NET Core SDK jsou vlastní instalace a ověření podpisu při selhání. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Problém
Při použití dotnet.exe 2. x k obnovení projektu, který má více cílů netcoreapp 1. x a netcoreapp 2. x, se záložní složka považuje za informační kanál souboru. To znamená, že při obnovení NuGet vybere balíček ze záložní složky a pokusí se ho nainstalovat do složky globálních balíčků a provede běžné ověřování podpisů, které selže.

#### <a name="workaround"></a>Alternativní řešení
Zakažte použití záložní složky nastavením na `RestoreAdditionalProjectSources` hodnotu Nothing. `<RestoreAdditionalProjectSources/>` Postupujte opatrně, protože to způsobí stažení velkého množství balíčků z NuGet.org, které by jinak bylo obnoveno ze záložní složky.
