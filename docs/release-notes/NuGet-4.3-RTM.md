---
title: NuGet 4.3 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.3 RTM včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496594"
---
# <a name="nuget-43-release-notes"></a>NuGet 4.3 Poznámky k verzi

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) je dodáván s NuGet 4.3 RTM, který přidává podporu pro nové scénáře, jako je například .NET Standard 2.0/.NET Core 2.0, obsahuje mnoho oprav kvality a zlepšuje výkon. Tato verze také přináší několik vylepšení, jako je podpora pro sémantické versioning 2.0.0, MSBuild integrace NuGet upozornění a chyby a další.

## <a name="summary-whats-new-in-430"></a>Shrnutí: Co je nového v 4.3.0

## <a name="summary-whats-new-in-431"></a>Shrnutí: Co je nového v 4.3.1

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)
* Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Známé problémy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Při obnovení NuGet se v některých případech může se zakázanými zdroji balíčků zacházet, jako by byly povolené

#### <a name="issue"></a>Problém

Následující techniky obnovení příkazového řádku považují zakázané zdroje balíčků za povolené. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore`(buď s dotnet.exe, který je dodáván s VS, nebo ten, který je dodáván s NetCore SDK 2.0.0)

#### <a name="workaround"></a>Alternativní řešení

1. Používejte Visual Studio ve verzi 2017 (sestavení 15.3 nebo novější) nebo nástroj NuGet.exe ve verzi 4.3.0 nebo novější.
1. Zakázaný zdroj odstraňte a dál používejte příkazy msbuild nebo dotnet.exe.
1. Ve svém řešení můžete do konfigurace NuGet.config vložit element Clear a pak definovat zdroje potřebné v daném řešení.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně zkuste znovu smažit `project.lock.json` a obnovit.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Pomocí Nástroje pro balení Nuget nelze zobrazit, přidat nebo aktualizovat nástroje DotNetCLITools.

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problémy opravené v časovém rámci NuGet 4.3 RTM

[NuGet 4.0 RTM Poznámky k verzi](../release-notes/nuget-4.0-RTM.md) - Seznam všech problémů opravených pro NuGet 4.0 RTM

### <a name="features"></a>Funkce

- Zlepšit NuGet Obnovení Perf - Implementovat chytřejší NoOp pro obnovení příkazového řádku a VS - [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: Rozhraní SE kontinuu VS/Dotnet CLI by mělo začít používat existující funkce NuGet: FallBack složky - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: Umožněte uživatelům ignorovat konkrétní upozornění na obnovení (nebo zvýšit na chybu) - [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: Lokalizovaná sestavení rozhraní SEkat - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: Zaregistrujte všechna upozornění/chyby do souboru datových zdrojů (včetně PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Povolit podporu TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Snížit počet projektů NuGet.Core a NuGet.Client (a tedy knihovny DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)

- Přidat možnost označit nuget upozornění jako chyby - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Chyby

- msbuild /t:pack selže s parametrem "DevelopmentDependency" není podporován úlohou "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)

- Adresářová struktura pro soubory obsahu byla slonována, pokud nepřidáte oddělovač adresářů systému Windows na konci programu PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)

- netcore projekty nepodporují nastavení jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage načítají synchronně, který zablokoval vlákno uživatelského rozhraní a zablokování VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnetcore Restore (& proto msbuild /t:restore) přeskočí projekty s explicitní míchanou závislostí [#4578](https://github.com/NuGet/Home/issues/4578)

- Pokud vaše řešení má odkazy na projekt, které odkazují na stejný projekt, s různými písmeny, obnovení nemusí fungovat. To také ovlivňuje různé relativní cesty, bez rozdílu v pouzdře - [#4574](https://github.com/NuGet/Home/issues/4574)

- Spustitelné soubory obnovené z balíčků NuGet již nejsou spustitelné s rozhraním .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe vypolkne podrobnosti o výjimce při analýzě souboru řešení - [#4411](https://github.com/NuGet/Home/issues/4411)

- Pack umístí soubory obsahu do nesprávného umístění, pokud ContentTargetFolders obsahuje cestu, která končí '/' v systému Windows - [#4407](https://github.com/NuGet/Home/issues/4407)

- Nelze obnovit DotNetCliToolReference pro nástroje balíček, který se zaměřuje netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)

- Cli aktualizace Nuget ponechá podmínku verze starého balíčku v souboru projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>Řadiče domény

- Přečtěte si DotnetCliToolTargetFramework z cps nomation - [#5397](https://github.com/NuGet/Home/issues/5397)

- Kontrola TPMinV by měla fungovat pro pj styl UPW - [#4763](https://github.com/NuGet/Home/issues/4763)

- Zlepšit popis ui pro balíčky AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet obnovení je výběr dat kompilace z runtime oddílu. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Vložit diagnostiku závislostí do souboru zámku - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Odkazy na problémy GitHubu opravené v 4.3 RTM

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
