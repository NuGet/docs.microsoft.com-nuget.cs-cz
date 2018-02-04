---
title: "3.5 poznámky k verzi Beta2 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 3.5 Beta 2 včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.5 Beta 2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-beta2-release-notes"></a>Poznámky k verzi 3.5 Beta2 NuGet

[Poznámky k verzi 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md) | [poznámky k verzi 3.5 RC NuGet](../release-notes/nuget-3.5-RC.md)

NuGet 3.5 Beta 2 RTM byla vydána 27. června 2016 pro Visual Studio 2013 a nuget.exe

[Úplné protokol změn](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Seznam problémů](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Opravy chyb

* Aktualizované chybová zpráva k nedostatečná podpora pro decrpytion heslo v .NET Core pro ověřený kanály - [#2942](https://github.com/NuGet/Home/issues/2942)

* Get-balíček konzoly Správce balíčků selže, pokud je projekt .NET Core open - [#2932](https://github.com/NuGet/Home/issues/2932)

* Opravte nesprávné zpracování 403 v příkaz nabízené NuGet [#2910](https://github.com/NuGet/Home/issues/2910)

* Opravte problémy v odinstalaci balíčky v řešení vázána k řízení zdrojů TFS disableSourceControlIntegration nastavena na hodnotu true - [#2739](https://github.com/NuGet/Home/issues/2739)

* Opravte aktualizace balíčku provést do balíčků jiný cílový účet - [#2724](https://github.com/NuGet/Home/issues/2724)

* Pomocí nástroje MSBuild úroveň podrobností můžete nastavit úroveň protokolování pro správce balíčků Nuget akcí uživatelského rozhraní – [#2705](https://github.com/NuGet/Home/issues/2705)

* Oprava NuGet konfigurace je neplatná Chyba v projektech web - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* Vyřešte potíže s aktualizací Service pack z `.csproj` když soubory obsahu jsou zahrnuty - [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource v `NuGetDefaults.Config` (`ProgramData\NuGet`) nefunguje - [#2653](https://github.com/NuGet/Home/issues/2653)

* Odstraňte problém na verze Nuget 3.4.3 - hodnota nemůže být null při vytváření balíčku - [#2648](https://github.com/NuGet/Home/issues/2648)

* Obnovení používá uložené přihlašovací údaje ze souboru Nuget.Config pro informační kanály služby VSTS - [#2647](https://github.com/NuGet/Home/issues/2647)

* Výkon - nadměrné přidělení pro opravu v kódu porovnání verze - [#2632](https://github.com/NuGet/Home/issues/2632)

* Oprava problémů se více instancí nuget.exe pokusí nainstalovat stejného balíčku paralelně - [#2628](https://github.com/NuGet/Home/issues/2628)

* Výkon - mezipaměti informace o závislostech pro operace vícenásobného projektu - [#2619](https://github.com/NuGet/Home/issues/2619)

* Vyřešte problém tam, kde nejde zdroje balíčku přidat z nastavení, pokud je seznam zdrojů je prázdný - [#2617](https://github.com/NuGet/Home/issues/2617)

* Opravte chybu Misleading při pokusu o instalaci balíčku, který závisí na průčelí návrhu - [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalace balíčku z konzoly PackageManager s nastavení "Všechny" pokusí pouze první zdroj - [#2557](https://github.com/NuGet/Home/issues/2557)

* Oprava problémů se balíčky, které mají soubory s časy zápisu v budoucnu (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)

* Zobrazit výjimky, když dojde k selhání s vyhledáním projekty v příkazu update - [#2418](https://github.com/NuGet/Home/issues/2418)

* Obsah balíčku není správně obnoveny při instalaci balíčku z v3.3 nuget + kanálu s argumentem - NoCache, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)

* Opravte problém s balíčkem instalaci (všechny zdroje) 1 zdroji – chybí balíček [#2322](https://github.com/NuGet/Home/issues/2322)

* Nainstalovat bloky v případě, že jednoho zdroje vyvolá chybu autorizace - [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec`verze rozsahu by měly přepsat verze - IncludeReferencedProjects - [#1983](https://github.com/NuGet/Home/issues/1983)

* NuGet 3.3.0 aktualizace nezdaří s ' dodatečné omezení... definované v souboru packages.config téhle operaci brání. " - [#1816](https://github.com/NuGet/Home/issues/1816)

* aktualizace nuget.exe zahodí silný název sestavení a privátní atributu. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Oprava problémů se relativní cesta k souboru pro "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Zlepšení zprávy o selhání překladač aktualizace - [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Funkce a změny chování

* nuget.exe nabízené - parametr časového limitu nefunguje - [#2785](https://github.com/NuGet/Home/issues/2785)

* obnovení nuget.exe neobsahuje `.props` a `.targets` soubory pro `.nuproj` projekty (Regrese v v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)

* Třeba rozšiřitelnost rozhraní API k porovnání rozhraní s importovanými daty - [#2633](https://github.com/NuGet/Home/issues/2633)

* Skrýt možnosti závislostí při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Tiskové out hlavičkou verze nuget.exe podrobný výstup - [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet měli přidat podporu pro /nativeassets/ /runtimes/ {rid} {txm} / - [#2782](https://github.com/NuGet/Home/issues/2782)