---
title: Zpráva k vydání verze NuGet 4.5 RTM
description: Zpráva k vydání verze pro NuGet 4.5 RTM, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 01ecd8c7de1a0f713766e3c413d889038522bac7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548293"
---
# <a name="nuget-45-rtm-release-notes"></a>Zpráva k vydání verze NuGet 4.5 RTM

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) součástí [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET Standard 2.0 pomocí rozhraní .NET Framework a NuGet 

.NET standard a jeho nástroje je navržená tak, že projekty cílené na rozhraní .NET Framework 4.6.1 může spotřebovat balíčky NuGet & projekty cílené na .NET Standard 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře plánu pro účely řešení a alternativní řešení můžete nasadit s dnešní stavu nástrojů.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Balíček v projektu .NET Core, který obsahuje sestavení s neplatným podpisem, může aktivovat nekonečnou smyčku obnovení

#### <a name="issue"></a>Problém

V některých případech použijete balíček, který obsahuje sestavení s neplatným podpisem, nebo když se verze balíčku nastaví pomocí časovače "DateTime, může to způsobí, že automaticky – obnovení balíčku občas způsobit nekonečnou smyčku [dotnet/project-system #1457](https://github.com/dotnet/project-system/issues/1457).

#### <a name="workaround"></a>Alternativní řešení

Pro tento problém zatím neexistuje alternativní řešení.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>Problémy opravené ve verzi RTM 4.5 NuGet časový rámec

Problémy opravené ve verzi RTM 4.4 NuGet, najdete [4.4 RTM poznámkách k verzi NuGet](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>Funkce

- Zakázat automatické nabízené oznámení balíčku symbolů - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Chyby

- [Regrese] v 15.5p1: Portable0.0 se přeskočila - [#6105](https://github.com/NuGet/Home/issues/6105)
- Po obnovení – chybí prostředky z balíčků [#5995](https://github.com/NuGet/Home/issues/5995)
- Poskytovatelé přihlašovacích údajů modulu plug-in, nebudou fungovat s identifikátory URI obsahující mezery – [#5982](https://github.com/NuGet/Home/issues/5982)
- Pokud balíček se nepovedlo obnovit, chyba by měl vytisknout ve výstupu i s minimální úroveň podrobností ON - [#5658](https://github.com/NuGet/Home/issues/5658)
- DotNet
  - dotnetcore obnovení na úrovni řešení není postupujte z ProjectReference s ReferenceOutputAssembly false nejlepší náhodné sestavení selhání - [#5490](https://github.com/NuGet/Home/issues/5490)
- Automatické dokončování ve PMC funguje správně pomocí metody objektu - [#4800](https://github.com/NuGet/Home/issues/4800)
- nuget.exe obnovení se nezdaří pomocí nástrojů Visual Studio 2015 – [#4713](https://github.com/NuGet/Home/issues/4713)
- výkonu – pmc je náročné vytvořit instanci v vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)
- Pomalá závislost informace o pomalé připojení - [#4089](https://github.com/NuGet/Home/issues/4089)
- odinstalovat balíček plánovaným bodem obnovení kratším - RemoveDependencies selže, pokud více balíčků sdílejí společné závislosti - [#4026](https://github.com/NuGet/Home/issues/4026)
- Dokončení NuGet.Core.nupkg pro publikování – [#3581](https://github.com/NuGet/Home/issues/3581)
- Balíček NuGet řeší závislosti ID z názvu adresáře v případě - IncludeProjectReferences se používá pro csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)
- Inicializační metoda typu 'NuGet.ProxyCache' došlo k výjimce – [#3144](https://github.com/NuGet/Home/issues/3144)
- problémy s výkonem obnovení nuget pomocí kudu - [#3087](https://github.com/NuGet/Home/issues/3087)
- Uživatelské rozhraní klienta nepovede zobrazíte všechny chyby nebo upozornění při hledání náskok před registrací objekty BLOB – [#2149](https://github.com/NuGet/Home/issues/2149)
- -Aktualizace generuje nesprávný - Get-Packages [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>Odkazy na problémy Githubu Vyřešeno ve verzi 4.5 RTM

[Seznam problémů](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
