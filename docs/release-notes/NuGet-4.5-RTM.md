---
title: NuGet 4,5 RTM poznámky k verzi
description: Poznámky k verzi pro NuGet 4.5 RTM včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 321aedb471bc6f86e9c03878093b199267e31195
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496573"
---
# <a name="nuget-45-release-notes"></a>NuGet 4.5 Poznámky k verzi

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) přichází s [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="summary-whats-new-in-450"></a>Shrnutí: Co je nového v 4.5.0

## <a name="summary-whats-new-in-452"></a>Shrnutí: Co je nového v 4.5.2

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-453"></a>Shrnutí: Co je nového v 4.5.3

* Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s rozhraním .NET Standard 2.0 s rozhraním .NET Framework & NuGet 

.NET Standard & jeho nástroje byly navrženy tak, že projekty zaměřené na rozhraní .NET Framework 4.6.1 mohou využívat balíčky NuGet & projekty zaměřené na standard .NET Standard 2.0 nebo starší. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře, plán pro jejich řešení a řešení, která můžete nasadit s dnešním stavem nástrojů.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení

#### <a name="issue"></a>Problém

V některých případech při použití balíčku, který obsahuje sestavení s neplatným podpisem nebo když je verze balíčku nastavena s panelem DateTime, způsobí, že automatické obnovení balíčku bude spuštěno v nekonečné smyčce [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problémy opravené v časovém rámci NuGet 4.5 RTM

Problémy opravené v NuGet 4.4 RTM naleznete v [nuget4.4 RTM poznámky k verzi](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Funkce

- Zakázat automatické nabízení symbolů - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Chyby

- [Regrese] v 15.5p1: Portable0.0 je přeskočeno - [#6105](https://github.com/NuGet/Home/issues/6105)
- Prostředky z balíčků chybí po obnovení - [#5995](https://github.com/NuGet/Home/issues/5995)
- Poskytovatelé pověření pluginů nepracují s identifikátory URI obsahujícími mezery - [#5982](https://github.com/NuGet/Home/issues/5982)
- Pokud se balíček nepodařilo obnovit, chyba by měla být vytištěna ve výstupu i s minimální podrobností ON - [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - dotnetcore obnovení na úrovni řešení nedodržuje ProjectReference s ReferenceOutputAssembly false vedoucí k selhání náhodné sestavení - [#5490](https://github.com/NuGet/Home/issues/5490)
- Automatické dokončování v PMC pracuje nesprávně s objektovými metodami - [#4800](https://github.com/NuGet/Home/issues/4800)
- Obnovení nástroje nuget.exe se nezdaří pomocí sady nástrojů sady nástrojů Sady nástrojů Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc je drahé na konkretizovat v vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)
- Pomalé získání informací o závislostech na pomalém připojení - [#4089](https://github.com/NuGet/Home/issues/4089)
- uninstall-package w/ -RemoveDependencies se nezdaří, pokud více balíčků sdílí společnou závislost - [#4026](https://github.com/NuGet/Home/issues/4026)
- Finalize NuGet.Core.nupkg pro publikování - [#3581](https://github.com/NuGet/Home/issues/3581)
- Sada NuGet pack řeší ID závislostí z názvu adresáře, když se pro csproj + project.js [#3566on](https://github.com/NuGet/Home/issues/3566) používá -IncludeProjectReferences
- Inicializátor typu pro "NuGet.ProxyCache" vyvolal výjimku - [#3144](https://github.com/NuGet/Home/issues/3144)
- nuget obnovení výkonu problém s kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- Klient ui nezobrazí žádnou chybu nebo upozornění, pokud je hledání před objekty BLOB registrace - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages -Updates generuje nesprávný dotaz - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Odkazy na problémy GitHubu opravené v 4.5 RTM

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
