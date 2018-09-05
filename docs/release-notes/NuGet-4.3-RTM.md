---
title: Zpráva k vydání verze NuGet 4.3 RTM
description: Zpráva k vydání verze pro NuGet 4.3 RTM, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 4bee32995884f4c003ebb963d2fd5b2d04363bab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551621"
---
# <a name="nuget-43-rtm-release-notes"></a>Zpráva k vydání verze NuGet 4.3 RTM

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.3 RTM, který přidává podporu pro nové scénáře, jako například .NET Standard 2.0 a .NET Core 2.0, obsahuje řadu oprav kvality a zvyšuje výkon. Tato verze také přináší několik vylepšení jako podporu pro Semantic Versioning 2.0.0, integrace MSBuild NuGet upozornění a chyby a další.

## <a name="known-issues"></a>Známé problémy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Při obnovení NuGet se v některých případech může se zakázanými zdroji balíčků zacházet, jako by byly povolené

#### <a name="issue"></a>Problém

Následující postupy obnovení příkazového řádku s zdroji balíčků zacházet, jako povolené. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (buď s příkazem VS dotnet.exe nebo ten, který je součástí sady NetCore SDK 2.0.0)

#### <a name="workaround"></a>Alternativní řešení

1. Používejte Visual Studio ve verzi 2017 (sestavení 15.3 nebo novější) nebo nástroj NuGet.exe ve verzi 4.3.0 nebo novější.
1. Zakázaný zdroj odstraňte a dál používejte příkazy msbuild nebo dotnet.exe.
1. Ve svém řešení můžete do konfigurace NuGet.config vložit element Clear a pak definovat zdroje potřebné v daném řešení.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Alternativně můžete zkusit odstranění `project.lock.json` a znovu ho obnovit.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nejde zobrazit, přidat ani aktualizovat DotNetCLITools pomocí Správce balíčků Nuget

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Problémy opravené ve verzi RTM 4.3 NuGet časový rámec

[4.0 RTM poznámkách k verzi NuGet](../release-notes/nuget-4.0-RTM.md) – zobrazí seznam všech problémů stanovené pro NuGet 4.0 RTM

### <a name="features"></a>Funkce

- Zlepšení výkonu obnovení NuGet - chytřejší NoOp pro implementace pro obnovení příkazového řádku – a VS [#5080](https://github.com/NuGet/Home/issues/5080)

- .NET Core 2.0: Rozhraní příkazového řádku Dotnet/VS by měla začít používat existující funkce NuGet: záložní složky – [#4939](https://github.com/NuGet/Home/issues/4939)

- .NET Core 2.0: Uživatelům umožnit ignorovat upozornění na konkrétní obnovení (nebo zvýšení oprávnění na chybu) - [#4898](https://github.com/NuGet/Home/issues/4898)

- .NET Core 2.0: Rozhraní příkazového řádku lokalizované sestavení - [#4896](https://github.com/NuGet/Home/issues/4896)

- .NET Core 2.0: zaregistrovat všechna upozornění nebo chyby do souboru prostředků (včetně PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Povolit podporu TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Snižte počet NuGet.Core NuGet.Client projekty (a tedy knihovny DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)

- Přidat možnost označit nuget upozornění jako chyby – [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Chyby

- selže /t:pack MSBuild s parametrem "DevelopmentDependency" nepodporuje úlohou "Packtask se neposkytl" - [#5584](https://github.com/NuGet/Home/issues/5584)

- Plochý adresářovou strukturu souborů obsahu není na konci PackagePath – přidávání oddělovač adresářů Windows [#4795](https://github.com/NuGet/Home/issues/4795)

- projekty netcore nepodporují nastavení jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage načítání synchronně který blokovaná vlákna uživatelského rozhraní a zablokována VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- DotNet
  - dotnetcore obnovení (a tedy msbuild/t: Restore) přeskočí projekty se závislostí projektu řešení explicitní [#4578](https://github.com/NuGet/Home/issues/4578)

- Pokud má vaše řešení projectreferences má za následek odkazují na stejný projekt s jinou velikostí písmen, obnovení nemusí fungovat. To ovlivňuje také jinými relativními cestami, bez rozdílu v malých a velkých písmen - [#4574](https://github.com/NuGet/Home/issues/4574)

- Spustitelné soubory obnovit z balíčků NuGet už nejsou spustitelný soubor s .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe pohltila podrobnosti o výjimce při analýze souboru řešení - [#4411](https://github.com/NuGet/Home/issues/4411)

- Pack umístí soubory obsahu v nesprávném umístění, pokud ContentTargetFolders obsahuje cestu, která skončí s lomítkem (/) ve Windows – [#4407](https://github.com/NuGet/Home/issues/4407)

- Nelze obnovit DotNetCliToolReference nástroje balíčků tohoto cíle netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)

- Aktualizace rozhraní příkazového řádku Nuget opustí podmínka staré verze balíčku v souboru projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>Chcete

- Čtení DotnetCliToolTargetFramework z CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)

- Kontrola TPMinV by mělo fungovat pro styl pj UPW – [#4763](https://github.com/NuGet/Home/issues/4763)

- Vylepšení uživatelského rozhraní Popis balíčků AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- Obnovení NuGet je výběr kompilace prostředků z části modulu runtime. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Diagnostika závislostí do souboru zámku - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Odkazy na Githubu opravených chybách v 4.3 RTM

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
