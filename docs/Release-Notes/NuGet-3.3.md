---
title: Poznámky k verzi NuGet 3.3 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Poznámky k verzi pro NuGet 3.3 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
keywords: NuGet 3.3 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ab5e1ca550297c608017cb56dff32f4bd4bbb885
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-33-release-notes"></a>Poznámky k verzi 3.3 NuGet

[Poznámky k verzi NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC poznámky](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 byla vydána 30. listopadu 2015 se velký počet aktualizace uživatelského rozhraní a funkcí příkazového řádku, jakož i kolekce užitečné opravy pro klienty NuGet.

## <a name="new-features"></a>Nové funkce

* Byly zavedeny poskytovatelé přihlašovacích údajů, které umožňují klienty NuGet příkazového řádku moct pracovat s ověřené informačního kanálu. [Pokyny k instalaci Visual Studio Team Services přihlašovací údaje poskytovatele ](../api/nuget-exe-credential-providers.md) a nakonfigurujte NuGet klientům použít je k dispozici v NuGet dokumentace.

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Samostatné karty Procházet, nainstalovaná a k dispozici aktualizace
* Aktualizace k dispozici oznámení, která určuje počet balíčků, které jsou dostupné aktualizace
* Balíček odznaky v seznamu balíček k označení, pokud je balíček nainstalován, nebo má k dispozici aktualizace.
* Stáhněte si počet a Autor přidán do seznamu balíčku
* Nejvyšší číslo verze k dispozici a aktuálně nainstalované verze číslo na seznam balíčků
* Akce tlačítka umožňující rychlé instalace, aktualizovat a odinstalovat ze seznamu balíčku
* Jasnější akce tlačítka na panelu podrobností balíčku
* Datum aktualizace balíčku na panelu podrobností balíčku
* Konsolidovat panelu v zobrazení řešení
* Řazení mřížky projekty a nainstalovaná verze číslic v zobrazení řešení

## <a name="new-command-line-features"></a>Nové funkce příkazového řádku

V této verzi zavedli jsme `add` a `init` příkazy k chybě při inicializaci úložiště založené na složku, jak je popsáno v [nuget.exe odkaz](../tools/nuget-exe-cli-reference.md). Struktury úložiště, které jsou vytvořená a udržovaná tato složka se [poskytovat výrazný výkon](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) jak je uvedeno v našem blogu.

## <a name="contentfiles"></a>contentFiles

Obsah se teď podporuje v `project.json` spravované projekty prostřednictvím nové `contentFiles` složky a `.nuspec` `contentFiles` element zápis.  Tento obsah může být více přímo určena autora balíčku pro interakce se systémy projektu.  Další informace o tom, jak nakonfigurovat contentFiles v `.nuspec` dokument lze najít v [příponou .nuspec odkaz](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Místní hodnoty – NuGet mezipaměti správy

Informace o tom, jak spravovat místní mezipaměti na pracovní stanici je aktualizovaná NuGet příkazového řádku.  Další informace o příkazu místní hodnoty – je k dispozici v [reference k příkazovému řádku NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Opravené problémy

**Významné problémy**

* Nástroje příkazového řádku obnovené NuGet pro obnovení balíčků s soubor řešení na Mono - [. 1543](https://github.com/NuGet/Home/issues/1543)

Úplný seznam problémů, které byly vyřešeny ve verzi 3.3 najdete na Githubu v části [3.3 milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Seznam chyby v 3.3 příkazového řádku verze se zaznamenávají [3.3 příkazového řádku milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Známé problémy

Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)