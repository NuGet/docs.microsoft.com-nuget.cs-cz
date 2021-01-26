---
title: Poznámky k verzi NuGet 4,3 RTM
description: Poznámky k verzi pro NuGet 4,3 RTM, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e9b6d15584d875f59ed64fe662944db3e37aeabb
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780175"
---
# <a name="nuget-43-release-notes"></a>Zpráva k vydání verze NuGet 4,3

[Visual Studio 2017 15,3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) obsahuje NUGET 4,3 RTM, který přidává podporu pro nové scénáře, jako je .NET Standard 2.0/. NET Core 2,0, obsahuje mnoho oprav kvality a zvyšuje výkon. Tato verze také přináší několik vylepšení, jako je podpora sémantických verzí 2.0.0, integrace nástroje MSBuild s upozorněními a chybami nástroje NuGet a další.

## <a name="summary-whats-new-in-430"></a>Shrnutí: co je nového v 4.3.0

## <a name="summary-whats-new-in-431"></a>Shrnutí: co je nového ve 4.3.1

* Oprava zabezpečení: oprávnění k souborům vytvořeným uvnitř ~/.NuGet jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) .
* Oprava zabezpečení: soubory uvnitř NUPKGs můžou mít relativní cestu nad [#7906](https://github.com/NuGet/Home/issues/7906) ADRESÁŘem nupkg.

## <a name="known-issues"></a>Známé problémy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Při obnovení NuGet se v některých případech může se zakázanými zdroji balíčků zacházet, jako by byly povolené

#### <a name="issue"></a>Problém

Následující postupy příkazového řádku pro obnovení považují zakázané zdroje balíčků za povolené. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (buď pomocí dotnet.exe, které se dodávají s VS nebo s NetCore SDK 2.0.0)

#### <a name="workaround"></a>Alternativní řešení

1. Používejte Visual Studio ve verzi 2017 (sestavení 15.3 nebo novější) nebo nástroj NuGet.exe ve verzi 4.3.0 nebo novější.
1. Zakázaný zdroj odstraňte a dál používejte příkazy msbuild nebo dotnet.exe.
1. Ve svém řešení můžete do konfigurace NuGet.config vložit element Clear a pak definovat zdroje potřebné v daném řešení.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně zkuste `project.lock.json` obnovení a znovu obnovit.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Pomocí Správce balíčků NuGet nemůžete zobrazit, přidat ani aktualizovat DotNetCLITools.

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení verze cílové architektury může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení verze cílové architektury v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problémy opravené v časovém rámci NuGet 4,3 RTM

Zpráva k [vydání verze nuget 4,0 RTM](../release-notes/nuget-4.0-RTM.md) – seznam všech problémů opravených pro NUGET 4,0 RTM

### <a name="features"></a>Funkce

- Vylepšení výkonu NuGet Restore – implementace inteligentnějšího NoOp pro obnovení z příkazového řádku a VS- [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2,0: VS/dotnet CLI by měly začít používat stávající funkce NuGet: záložní složky- [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2,0: Povolte uživatelům ignorovat konkrétní upozornění na obnovení (nebo se zvýšením oprávnění na chybu) – [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2,0: lokalizovaná sestavení CLI – [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2,0: Zaregistrujte všechna upozornění/chyby do souboru assetů (včetně PackageTargetFallback) – [#4895](https://github.com/NuGet/Home/issues/4895)

- Povolit podporu TFM: NetStandard 2.0, Tizen- [#4892](https://github.com/NuGet/Home/issues/4892)

- Snižte počet NuGet. Core a NuGet. Client Projects (a tak knihovny DLL) – [#2446](https://github.com/NuGet/Home/issues/2446)

- Přidání možnosti označovat upozornění NuGet jako chyby – [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Chyby

- MSBuild/t: sada se nezdařila s parametrem "DevelopmentDependency" není podporován úlohou "PackTask" – [#5584](https://github.com/NuGet/Home/issues/5584)

- Adresářová struktura pro soubory obsahu se sloučí, pokud se nepřidá oddělovač adresářů Windows na konci PackagePath- [#4795](https://github.com/NuGet/Home/issues/4795)

- projekty Netcore nepodporují nastavení jako developmentDependency- [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage se načítá synchronně, což blokuje vlákno uživatelského rozhraní a zablokované VS- [#4679](https://github.com/NuGet/Home/issues/4679) .

- dotnet
  - dotnetcore Restore (& proto MSBuild/t: Restore) přeskočí projekty pomocí explicitní závislosti projektu řešení [#4578](https://github.com/NuGet/Home/issues/4578)

- Pokud má vaše řešení ProjectReferences, které odkazují na stejný projekt s různými velikostmi písmen, obnovení nemusí fungovat. To má vliv i na jiné relativní cesty bez rozdílu v případě [#4574í](https://github.com/NuGet/Home/issues/4574) velkých a malých písmen.

- Spustitelné soubory obnovené z balíčků NuGet už nejsou spustitelné pomocí .NET Core 2,0- [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe požití podrobností o výjimce při analýze souboru řešení – [#4411](https://github.com/NuGet/Home/issues/4411)

- Sada zaznamená soubory obsahu v nesprávném umístění, pokud ContentTargetFolders obsahuje cestu, která končí znakem/v systému Windows- [#4407](https://github.com/NuGet/Home/issues/4407)

- Nejde obnovit DotNetCliToolReference pro balíček nástrojů, který cílí na netcoreapp 1.1- [#4396](https://github.com/NuGet/Home/issues/4396) .

- Rozhraní příkazového řádku aktualizace NuGet opustí původní stav verze balíčku v souboru projektu (C++) – [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>Chcete odeslat obecnou

- Čtení DotnetCliToolTargetFramework z CPS nomation- [#5397](https://github.com/NuGet/Home/issues/5397)

- TPMinV by měla fungovat pro PJ stylu UWP – [#4763](https://github.com/NuGet/Home/issues/4763)

- Vylepšení popisu uživatelského rozhraní pro balíčky s autoreferencí – [#4471](https://github.com/NuGet/Home/issues/4471)

- Obnovení NuGet vybírá možnost kompilovat prostředky z modulu runtime. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Vložit diagnostiku závislostí do souboru zámku – [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Odkazy na problémy GitHubu opravené ve 4,3 RTM

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
