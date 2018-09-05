---
title: NuGet 3.3 poznámky
description: Zpráva k vydání verze NuGet 3.3 včetně známých problémů, opravy chyb, nové funkce a chcete
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546644"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 poznámky

[Poznámky k verzi NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC poznámky](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 bylo vydáno 30. listopadu 2015 se velký počet aktualizace uživatelského rozhraní a funkcí příkazového řádku, stejně jako kolekce užitečné opravy klientům NuGet.

## <a name="new-features"></a>Nové funkce

* Byly zavedeny poskytovatelé přihlašovacích údajů, které umožňují klientům příkazového řádku NuGet, abyste mohli bez problému fungují s ověřené informační kanál. [Návod, jak nainstalovat Visual Studio Team Services poskytovatele přihlašovacích ](../api/nuget-exe-credential-providers.md) a nakonfigurovat NuGet klientů jsou k dispozici na webu NuGet Docs.

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Samostatných kartách procházet, instalace a k dispozici aktualizace
* Aktualizace k dispozici oznámení "BADGE" označující počet balíčků dostupných aktualizací
* Balíček odznaky v seznamu balíčků k označení, zda je nainstalován balíček nebo má k dispozici aktualizace.
* Stáhněte si počet a autor se přidá do seznamu balíčků
* Nejvyšší číslo verze k dispozici a aktuálně nainstalovanou verzi číslo v seznamu balíčků
* Akce tlačítka umožňující rychlé instalace aktualizace i odinstalace ze seznamu balíčků
* Jasnější akce tlačítka na panelu podrobností balíčku
* Datum aktualizace balíčku na panelu podrobností balíčku
* Slučování panelu v zobrazení řešení
* Řazení mřížky projektů a čísel nainstalovaných verzí v zobrazení řešení

## <a name="new-command-line-features"></a>Nové funkce příkazového řádku

V této verzi jsme představili `add` a `init` příkazy inicializace založený na složce úložiště, jak je popsáno v [referenční informace o nuget.exe](../tools/nuget-exe-cli-reference.md). Struktury úložiště, která jsou vytvořena a udržuje k této složce budou [poskytovat výhody výkonu](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) jak je popsáno na našem blogu.

## <a name="contentfiles"></a>contentFiles

Obsah je nyní podporována v `project.json` spravované projekty prostřednictvím nového `contentFiles` složky a `.nuspec` `contentFiles` zápisu elementu.  Tento obsah je možné zadat více přímo tak autora balíčku pro interakce se systémy.  Další informace o tom, jak nakonfigurovat contentFiles v `.nuspec` najdete v dokumentu [souboru .nuspec odkaz](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Správa mezipaměti NuGet Locals

Informace o tom, jak spravovat místní mezipaměti na pracovní stanici byla aktualizována NuGet příkazového řádku.  Další informace o místních hodnot příkazu je k dispozici v [odkaz na příkazový řádek NuGet](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Opravené problémy

**Významné problémy**

* Příkazový řádek obnovená podpora NuGet pro obnovení balíčků s soubor řešení v Mono - [. 1543](https://github.com/NuGet/Home/issues/1543)

Úplný seznam problémů, které se řeší verze 3.3 najdete na Githubu v části [3.3 milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Seznam opravených chybách v 3.3 verzi příkazového řádku se zaznamenávají do [3.3 příkazového řádku milník](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Známé problémy

Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)