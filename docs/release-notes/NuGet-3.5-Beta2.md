---
title: zpráva k vydání verze 3,5 beta2
description: Poznámky k verzi pro NuGet 3,5 beta 2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776391"
---
# <a name="nuget-35-beta2-release-notes"></a>Poznámky k verzi NuGet 3,5 beta2

[NuGet 3,5 – poznámky](../release-notes/nuget-3.5-Beta.md)  |  k verzi beta [Poznámky k verzi pro NuGet 3,5 – RC](../release-notes/nuget-3.5-RC.md)

NuGet 3,5 beta 2 RTM byl vydán 27. června 2016 pro Visual Studio 2013 a nuget.exe

[Úplný protokol změn](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[Seznam problémů](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a>Opravy chyb

* Aktualizovaná chybová zpráva pro nedostatečné podpoře pro decrpytion hesla v .NET Core pro ověřené informační kanály – [#2942](https://github.com/NuGet/Home/issues/2942)

* Konzola správce balíčků Get-Package se nezdařila, pokud je projekt .NET Core otevřený – [#2932](https://github.com/NuGet/Home/issues/2932)

* Opravte nesprávné zpracování 403 v příkazu NuGet push Command [#2910](https://github.com/NuGet/Home/issues/2910)

* Opravte problémy při odinstalaci balíčků v řešení, které je vázané na správu zdrojového kódu TFS, pokud je disableSourceControlIntegration nastavené na true – [#2739](https://github.com/NuGet/Home/issues/2739)

* Oprava aktualizace balíčku pro zohlednění necílových balíčků – [#2724](https://github.com/NuGet/Home/issues/2724)

* Použití úrovně podrobností MSBuild k nastavení úrovně protokolovacího nástroje pro akce uživatelského rozhraní Správce balíčků NuGet – [#2705](https://github.com/NuGet/Home/issues/2705)

* Oprava konfigurace NuGet je neplatná chyba v projektech webů – VS 2015 VSIX (v 3.4.3) – [#2667](https://github.com/NuGet/Home/issues/2667)

* Oprava problémů s balíčkem `.csproj` Při zahrnutí souborů obsahu – [#2658](https://github.com/NuGet/Home/issues/2658)

* DefaultPushSource in `NuGetDefaults.Config` ( `ProgramData\NuGet` ) nefunguje [#2653](https://github.com/NuGet/Home/issues/2653)

* Oprava problému v 3.4.3 vydaných verzí NuGet nemůže mít při vytváření balíčku hodnotu null – [#2648](https://github.com/NuGet/Home/issues/2648)

* Příkaz Restore používá uložená pověření Nuget.Config pro informační kanály VSTS- [#2647](https://github.com/NuGet/Home/issues/2647)

* Výkon – oprava nadměrných přidělení ve verzi comparsion Code- [#2632](https://github.com/NuGet/Home/issues/2632)

* Oprava problémů, když se více instancí nuget.exe pokusí nainstalovat stejný balíček paralelně [#2628](https://github.com/NuGet/Home/issues/2628)

* Informace o závislostech v mezipaměti výkonu pro operace s více projekty – [#2619](https://github.com/NuGet/Home/issues/2619)

* Oprava potíží, kdy se zdroje balíčků nejde do nastavení, když je zdrojový seznam prázdný – [#2617](https://github.com/NuGet/Home/issues/2617)

* Oprava zavádějící chyby při pokusu o instalaci balíčku, který závisí na době návrhu Facade- [#2594](https://github.com/NuGet/Home/issues/2594)

* Instalace balíčku z konzoly PackageManager s nastavením "vše" se snaží pouze první zdroj – [#2557](https://github.com/NuGet/Home/issues/2557)

* Opravte problémy s balíčky, které mají soubory s časem zápisu v budoucnosti (mono) – [#2518](https://github.com/NuGet/Home/issues/2518)

* Zobrazit výjimku, pokud dojde k selhání při hledání projektů v příkazu Update- [#2418](https://github.com/NuGet/Home/issues/2418)

* Obsah balíčku se neobnovil správně při instalaci balíčku z kanálu NuGet v 3.3 + s argumentem-bez mezipaměti, když balíček obsahuje `.nupkg` soubory – [#2354](https://github.com/NuGet/Home/issues/2354)

* Oprava potíží při instalaci balíčku (všechny zdroje), když chybí balíček v 1 zdroji – [#2322](https://github.com/NuGet/Home/issues/2322)

* Nainstalovat bloky v případě neúspěšného ověření u jednoho zdroje – [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Rozsah verze by měl přepsat-IncludeReferencedProjects verze- [#1983](https://github.com/NuGet/Home/issues/1983)

* Aktualizace NuGet 3.3.0 se nezdařila s dodatečným omezením... definované v packages.config zabrání této operaci. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* nuget.exe Update zruší silný název sestavení a soukromý atribut. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Opravte problémy s relativní cestou k souboru pro "DefaultPushSource". [#1746](https://github.com/NuGet/Home/issues/1746)

* Vylepšit zprávy o chybách překladače aktualizace – [#1373](https://github.com/NuGet/Home/issues/1373)

## <a name="features-and-behavior-changes"></a>Změny funkcí a chování

* Parametr push-timeout nuget.exe nefunguje – [#2785](https://github.com/NuGet/Home/issues/2785)

* nuget.exe obnovení nevytváří `.props` a `.targets` soubory pro `.nuproj` projekty (regrese v v 3.4.3.855) – [#2711](https://github.com/NuGet/Home/issues/2711)

* Pro porovnání platforem s importy je nutné rozšiřující rozhraní API [#2633](https://github.com/NuGet/Home/issues/2633)

* Skrýt možnosti závislosti při použití `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Vytisknout nuget.exe záhlaví verze v podrobném výstupu – [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet by měl přidat podporu pro/runtimes/{RID}/nativeassets/{TXM}/- [#2782](https://github.com/NuGet/Home/issues/2782)