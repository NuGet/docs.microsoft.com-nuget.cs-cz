---
title: Zpráva k vydání verze NuGet 3,3
description: Poznámky k verzi pro NuGet 3,3, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813777"
---
# <a name="nuget-33-release-notes"></a>Zpráva k vydání verze NuGet 3,3

[Poznámky k verzi NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NUGET 3,4 – RC – poznámky k verzi](../release-notes/nuget-3.4-RC.md)

NuGet 3,3 byl vydán 30. listopadu 2015 s významným počtem aktualizací uživatelského rozhraní a funkcí příkazového řádku a také kolekce užitečných oprav klientů NuGet.

## <a name="new-features"></a>Nové funkce

* Poskytovatelé přihlašovacích údajů se zavedli, aby klienti příkazového řádku NuGet mohli bez problémů pracovat s ověřeným informačním kanálem. [Pokyny k instalaci poskytovatele přihlašovacích údajů Visual Studio Team Services](../reference/extensibility/nuget-exe-credential-providers.md) a konfiguraci klientů NuGet, aby je používali, jsou k dispozici v dokumentaci NuGet.

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Samostatné procházení, instalace a aktualizace karet k dispozici
* Dostupné aktualizace upozorňující na počet balíčků s dostupnými aktualizacemi
* Označení balíčků v seznamu balíčků, aby označovaly, jestli je balíček nainstalovaný nebo má k dispozici aktualizace
* Počet stažení a autor přidaný do seznamu balíčků
* Nejvyšší dostupné číslo verze a aktuálně nainstalované číslo verze v seznamu balíčků
* Tlačítka akcí umožňující rychlou instalaci, aktualizaci a odinstalaci ze seznamu balíčků
* Tlačítka pro vymazání akcí na panelu podrobností balíčku
* Datum aktualizace balíčku na panelu podrobností balíčku
* Sloučit panel v zobrazení řešení
* V zobrazení řešení lze seřaditelné mřížky projektů a čísla nainstalovaných verzí.

## <a name="new-command-line-features"></a>Nové funkce příkazového řádku

V této verzi jsme zavedli příkazy `add` a `init` k inicializaci úložišť založených na složkách, jak je popsáno v [referenčních informacích k NuGet. exe](../reference/nuget-exe-cli-reference.md). Úložiště, která jsou vytvořená a spravovaná pomocí této struktury složek, budou [poskytovat významné výhody](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) z hlediska výkonu, jak je uvedeno na našem blogu.

## <a name="contentfiles"></a>contentFiles

Obsah je nyní podporován v `project.json` spravovaných projektů prostřednictvím nové složky `contentFiles` a `.nuspec` `contentFiles` Notation elementu.  Tento obsah může být přímo určen autorem balíčku pro interakce se systémy projektu.  Další informace o tom, jak nakonfigurovat contentFiles v dokumentu `.nuspec`, najdete v [odkazu. nuspec](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Správa mezipaměti místních prostředí NuGet

Příkazový řádek NuGet byl aktualizován tak, aby obsahoval informace o tom, jak spravovat místní mezipaměti v pracovní stanici.  Další informace o příkazu místní hodnoty jsou k dispozici v [Referenční příručce k příkazovému řádku NuGet](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Opravené problémy

**Významné problémy**

* Obnovená podpora příkazového řádku NuGet pro obnovení balíčků se souborem řešení v mono- [1543](https://github.com/NuGet/Home/issues/1543)

Úplný seznam problémů, které byly řešeny ve verzi 3,3, najdete na webu GitHub pod [milníkem 3,3](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Seznam problémů opravených ve verzi příkazového řádku 3,3 se zaznamenávají do [řádku 3,3 příkazového řádku](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Známé problémy

Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)