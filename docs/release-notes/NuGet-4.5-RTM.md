---
title: Poznámky k verzi 4.5 RTM NuGet
description: Poznámky k verzi pro NuGet 4.5 RTM, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820713"
---
# <a name="nuget-45-rtm-release-notes"></a>Poznámky k verzi 4.5 RTM NuGet

[Visual Studio 2017 15,5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET standardní 2.0 pomocí rozhraní .NET Framework & NuGet 

.NET standard & jeho nástrojů je navržené tak, aby projektech zacílených na rozhraní .NET Framework 4.6.1 může využívat balíčky NuGet & projektech zacílených na standardní rozhraní .NET 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tento scénář, plán pro adresování a alternativní řešení můžete nasadit s je aktuální stav nástrojů.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nelze zobrazit, přidat nebo aktualizovat DotNetCLITools pomocí Správce balíčků Nuget

#### <a name="issue"></a>Problém

Správce balíčků NuGet nezobrazuje a nepovoluje přidat nebo aktualizovat DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Alternativní řešení

V souboru projektu se musí ručně upravit DotNetCLIToolReferences.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Změna cílení cílové verze rozhraní může vést k nekompletnímu IntelliSense

#### <a name="issue"></a>Problém

Změna cílení cílové verze rozhraní v sadě Visual Studio může vést k nekompletnímu IntelliSense. To se stává, když jako formát správce balíčků používáte PackageReferences. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Alternativní řešení

Proveďte ruční obnovení.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení

#### <a name="issue"></a>Problém

V některých případech při použití balíček, který obsahuje sestavení s neplatným podpisem nebo pokud verze balíčku nastavena, DateTime, burzovní způsobuje, že auto obnovení balíčku ke spuštění v nekonečné smyčce [dotnet/projektu systému #1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Chyby v období NuGet 4.5 RTM

Chyby v NuGet 4.4 RTM, naleznete v [NuGet 4.4 RTM poznámky](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Funkce

- Zakázat automatické nabízené symboly balíčku - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Chyby

- [Regrese] v 15.5p1: bylo přeskočeno Portable0.0 - [#6105](https://github.com/NuGet/Home/issues/6105)
- Po obnovení – chybí prostředky z balíčků [#5995](https://github.com/NuGet/Home/issues/5995)
- Poskytovatelé přihlašovacích údajů modulu plug-in nefungují s identifikátory URI obsahující mezery - [#5982](https://github.com/NuGet/Home/issues/5982)
- Pokud balíček se nepodařilo obnovit, chyba by měl být vytištěn v výstupu i s minimálním podrobností ON - [#5658](https://github.com/NuGet/Home/issues/5658)
- DotNet.
  - dotnetcore obnovení na úrovni řešení není podle ProjectReference s ReferenceOutputAssembly false úvodní náhodných sestavení chyby - [#5490](https://github.com/NuGet/Home/issues/5490)
- Automatické dokončování v funguje pomocí PMC nesprávně pomocí metod objektu - [#4800](https://github.com/NuGet/Home/issues/4800)
- nuget.exe obnovení se nezdaří pomocí nástrojů Visual Studio 2015 - [#4713](https://github.com/NuGet/Home/issues/4713)
- výkonu - pomocí pmc je nákladné doložit v vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)
- Pomalé získat informace o závislostech na pomalé připojení - [#4089](https://github.com/NuGet/Home/issues/4089)
- Odinstalace balíčku s - RemoveDependencies se nezdaří, pokud více balíčků sdílejí společné závislost - [#4026](https://github.com/NuGet/Home/issues/4026)
- Dokončení NuGet.Core.nupkg pro publikování - [#3581](https://github.com/NuGet/Home/issues/3581)
- NuGet pack řeší ID závislost z název adresáře v případě - IncludeProjectReferences používá pro csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- Typ inicializátoru pro 'NuGet.ProxyCache' došlo k výjimce - [#3144](https://github.com/NuGet/Home/issues/3144)
- nuget restore výkonu problém s kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- Uživatelské rozhraní klienta nepodaří zobrazit všechny chyby nebo upozornění při hledání je před registrace objekty BLOB - [#2149](https://github.com/NuGet/Home/issues/2149)
- -Aktualizace generuje dotaz nesprávný - Get-balíčky [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Odkazy na Githubu chyby v 4.5 RTM

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
