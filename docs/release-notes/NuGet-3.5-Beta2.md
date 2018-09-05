---
title: 3.5 zpráva k vydání verze Beta2
description: Zpráva k vydání verze NuGet 3.5 Beta 2, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551988"
---
# <a name="nuget-35-beta2-release-notes"></a>Zpráva k vydání verze NuGet 3.5 Beta2

[Poznámky k verzi 3.5 Beta verze NuGet](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC poznámky](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM bylo vydáno 27. června 2016 pro Visual Studio 2013 a nuget.exe

[Úplný protokol změn](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Seznam problémů](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Opravy chyb

* Aktualizované chybové zprávy chybějící podpora jazyků decrpytion heslo v .NET Core pro ověřené informační kanály - [#2942](https://github.com/NuGet/Home/issues/2942)

* Konzola správce balíčků Get-balíčku selže, pokud projekt .NET Core je open - [#2932](https://github.com/NuGet/Home/issues/2932)

* Opravte nesprávné zpracování 403 v příkazu push NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Opravte problémy v odinstalaci balíčky v řešení připojit ke správě zdrojů TFS při disableSourceControlIntegration je nastavena na hodnotu true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Oprava aktualizace balíčku bude trvat do balíčků bez cílového účtu – [#2724](https://github.com/NuGet/Home/issues/2724)

* Pomocí nástroje MSBuild s úrovní podrobností můžete nastavit úroveň protokolování pro správce balíčků Nuget akce uživatelského rozhraní – [#2705](https://github.com/NuGet/Home/issues/2705)

* Oprava NuGet konfigurace je neplatná chyby v projektech web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Opravte problémy s aktualizací Service pack z `.csproj` když soubory obsahu jsou zahrnuty - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource v `NuGetDefaults.Config` (`ProgramData\NuGet`) nefunguje - [#2653](https://github.com/NuGet/Home/issues/2653)

* Odstraňte problém na vydání Nuget 3.4.3 - hodnota nemůže být null při vytváření balíčku - [#2648](https://github.com/NuGet/Home/issues/2648)

* Obnovení používá uložené přihlašovací údaje ze souboru Nuget.Config pro informační kanály VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Výkon - nadměrného přidělení pro opravu v porovnání kód verze - [#2632](https://github.com/NuGet/Home/issues/2632)

* Řešení problémů, pokud více instancí nuget.exe pokusí nainstalovat stejného balíčku paralelně - [#2628](https://github.com/NuGet/Home/issues/2628)

* Výkon - mezipaměť informací o závislostech pro operace více projektů - [#2619](https://github.com/NuGet/Home/issues/2619)

* Tento problém vyřešit tam, kde balíček zdrojů nelze přidat z nastavení, pokud seznam zdrojů je prázdný - [#2617](https://github.com/NuGet/Home/issues/2617)

* Opravte chybu Misleading při pokusu o instalaci balíčku, který závisí na návrhu fasády - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalace balíčku z konzoly PackageManager s nastavením "All" pokusí pouze první zdroj - [#2557](https://github.com/NuGet/Home/issues/2557)

* Řešení problémů s balíčky, které mají soubory s časem zápisu v budoucnu (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Zobrazit výjimky, když dojde k selhání vyhledávání projektů v příkazu update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Balíček obsahu není správně obnovena, při instalaci balíčku z nuget v3.3 + informačního kanálu s argumentem - NoCache, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)

* Oprava potíží s balíček nainstalovat (všechny zdroje), když ze zdroje 1 - chybí balíček [#2322](https://github.com/NuGet/Home/issues/2322)

* Nainstalovat bloky, pokud je jediným zdrojem selhání autorizace – [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` verze rozsah by měl přepsat - IncludeReferencedProjects verze - [#1983](https://github.com/NuGet/Home/issues/1983)

* Aktualizace NuGet 3.3.0 selže s '... Další omezení definované v souboru packages.config téhle operaci brání. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* aktualizace nuget.exe zahodí silný název sestavení a privátní atribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Oprava problémů se relativní cesta k souboru pro "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Zlepšení zprávy o neúspěchu překladač Update - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Funkce a změny chování

* nabízené nuget.exe – parametr časového limitu nefunguje - [#2785](https://github.com/NuGet/Home/issues/2785)

* obnovení nuget.exe nevytvoří `.props` a `.targets` soubory pro `.nuproj` projekty (Regrese v v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Třeba rozšíření rozhraní API pro porovnání architektur s importovanými daty – [#2633](https://github.com/NuGet/Home/issues/2633)

* Skrýt možnosti závislostí při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Vytiskne nuget.exe verze záhlaví podrobný výstup - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet by měl přidat podporu pro /nativeassets/ /runtimes/ {identifikátorů rid} {txm} / – [#2782](https://github.com/NuGet/Home/issues/2782)