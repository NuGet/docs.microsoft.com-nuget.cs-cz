---
title: "Poznámky k verzi RTM NuGet 4.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 4.3 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 4.3 RTM poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 02b8f6df08438db42e73cc761acc486b7fa13919
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-43-rtm-release-notes"></a>Poznámky k verzi 4.3 RTM NuGet

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s NuGet 4.3 RTM, která přidává podporu pro nové scénáře, jako je například .NET Standard 2.0 nebo .NET Core 2.0, obsahuje opravy mnoha kvality a zvyšuje výkon. Tato verze přináší také několik vylepšení, jako je podpora pro sémantické verze 2.0.0, integrace nástroje MSBuild NuGet upozornění a chyb a další.

## <a name="known-issues"></a>Známé problémy

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>Při obnovení NuGet se v některých případech může se zakázanými zdroji balíčků zacházet, jako by byly povolené

#### <a name="issue"></a>Problém

Následující obnovení příkazového řádku techniky považovat Zakázané balíčky zdroje jako povolené. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore`(buď pomocí dotnet.exe který se dodává s VS nebo ten, který se dodává s NetCore SDK 2.0.0)

#### <a name="workaround"></a>Alternativní řešení

1. Používejte Visual Studio ve verzi 2017 (sestavení 15.3 nebo novější) nebo nástroj NuGet.exe ve verzi 4.3.0 nebo novější.
1. Zakázaný zdroj odstraňte a dál používejte příkazy msbuild nebo dotnet.exe.
1. Ve svém řešení můžete do konfigurace NuGet.config vložit element Clear a pak definovat zdroje potřebné v daném řešení.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Při používání konzoly Správce balíčků nemusí fungovat klávesa Enter

#### <a name="issue"></a>Problém

V konzole Správce balíčků občas nefunguje klávesa Enter. Když toto chování zpozorujete, zjistěte prosím, jak to vypadá s opravou, a poskytněte jakékoli další užitečné informace o postupu, jak tuto chybu reprodukovat. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Alternativní řešení

Před otevřením řešení restartujte Visual Studio a otevřete konzolu PMC. Případně, zkuste odstranit `project.lock.json` a opakujte obnovení.

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Pomocí Správce balíčků Nuget nebudete moct zobrazit, přidat ani aktualizovat DotNetCLITools

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>Chyby v období NuGet 4.3 RTM

[K vydání verze RTM 4.0 NuGet](../release-notes/nuget-4.0-RTM.md) -jsou uvedené všechny problémy opravě pro NuGet 4.0 RTM

### <a name="features"></a>Funkce

- Zlepšení výkonu obnovení NuGet - implementace chytřejší nedojde k žádné akci pro obnovení příkazového řádku - a VS [#5080](https://github.com/NuGet/Home/issues/5080)

- Jádro Asp.net 2.0: Produkt VS/Dotnet rozhraní příkazového řádku by se měl spustit pomocí stávajících funkcí NuGet: záložní složky - [#4939](https://github.com/NuGet/Home/issues/4939)

- Jádro Asp.net 2.0: Povolit uživatelům ignorovat upozornění konkrétní obnovení (nebo zvýšení oprávnění na chybu) - [#4898](https://github.com/NuGet/Home/issues/4898)

- Jádro Asp.net 2.0: Rozhraní příkazového řádku lokalizované sestavení - [#4896](https://github.com/NuGet/Home/issues/4896)

- Jádro Asp.net 2.0: registrace všech upozornění nebo chyby do souboru prostředků (včetně PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

- Povolit podporu TFM: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- Snižte počet NuGet.Core a NuGet.Client projekty (a tedy knihovny DLL) - [#2446](https://github.com/NuGet/Home/issues/2446)

- Přidat možnost označte nuget upozornění jako chyby – [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Chyby

- není podporována selže /t:pack MSBuild s parametrem "DevelopmentDependency" úloha "PackTask" - [#5584](https://github.com/NuGet/Home/issues/5584)

- Průmětu struktury adresářů pro soubory obsahu, pokud nebudou přidány oddělovače adresáře systému Windows na konci PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)

- projekty netcore nepodporují nastavení jako developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage načítá synchronně který blokovaný vlákna uživatelského rozhraní a zablokována VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- DotNet obnovení (& proto msbuild /t:restore) přeskočí projekty s závislosti projektu explicitní řešení [#4578](https://github.com/NuGet/Home/issues/4578)

- Pokud má vaše řešení projectreferences, která odkazují na stejný projekt v různých velká a malá písmena, nemusí obnovení fungovat. To ovlivní také různé relativní cesty bez rozdíl v velká a malá písmena - [#4574](https://github.com/NuGet/Home/issues/4574)

- Spustitelné soubory obnovení ze balíčky NuGet jsou již spustitelný soubor s .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe swallows podrobnosti o výjimce, při analýze souboru řešení - [#4411](https://github.com/NuGet/Home/issues/4411)

- Pack převádí soubory obsahu na nesprávné umístění, pokud ContentTargetFolders obsahuje cestu, která ukončí lomítkem (/) v systému Windows - [#4407](https://github.com/NuGet/Home/issues/4407)

- Nelze obnovit DotNetCliToolReference nástrojů balíčků tohoto cíle netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)

- Aktualizace Nuget rozhraní příkazového řádku ponechá starý stav verze balíčku v souboru projektu (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCRs

- Čtení DotnetCliToolTargetFramework z CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)

- Kontrola TPMinV by měla fungovat pro styl pj UWP - [#4763](https://github.com/NuGet/Home/issues/4763)

- Zlepšení uživatelského rozhraní Popis balíčků AutoReferenced - [#4471](https://github.com/NuGet/Home/issues/4471)

- Obnovení NuGet je výběr kompilace prostředky z části modulu runtime. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Uveďte Diagnostika závislostí v souboru zámku - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>Odkazy na Githubu chyby v 4.3 RTM

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
