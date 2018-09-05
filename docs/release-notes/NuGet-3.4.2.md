---
title: Zpráva k vydání verze NuGet 3.4.2
description: Zpráva k vydání verze pro NuGet 3.4.2 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549148"
---
# <a name="nuget-342-release-notes"></a>Zpráva k vydání verze NuGet 3.4.2

[Zpráva k vydání verze NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [zpráva k vydání verze NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

8. dubna 2016 několik problémů, které jste identifikovali 3.4 a 3.4.1 byla vydána NuGet 3.4.2 release.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC je teď k dispozici

Můžete si stáhnout verzi Release candidate programu nuget.exe 3.4.2 [tady](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Výrazně jsme vylepšili provádění aktualizací v konkrétní scénář, ve kterém aktualizací na balíčky pomocí grafů závislosti hloubkové trvalo skutečně dlouhou dobu a zablokování sady Visual Studio.
* obnovení nuget bez síťový provoz je 2,5 × – 3 x rychlejší v sadě Visual Studio.
* Kromě této změny jsme vyřešili problém kde jsme byly dvakrát při načítání aktualizace v Uživatelském rozhraní VS počet dosažení sítě. Toto je částečně odpovědná za časový limit problémy zákazníci, kteří zkušenosti s 3.4/3.4.1.
* Přidání podpory pro nastavení no_proxy

## <a name="fixes"></a>Opravy

* Opravili jsme problém, kdy nuget.org zdroj nebyl nalezen v nastavení NuGet config po aktualizaci verze 3.4.1.
* Opravili jsme problém, pokud malá a velká písmena změnu FindPackagesById v 3.4.1 přeruší Artifactory.
* Byl opraven problém s FIPS, která způsobovala chyby s obnovení NuGet se nuget.exe.
* Oprava chyby při procházení zdroje se neplatná ikona adresy URL.
* Opravené problémy s sloučení verze a položky z "Všechny zdroje".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Známé problémy v 3.4.2 příkazového řádku Windows x86 (RC)

Tyto problémy budou vyřešeny předčasné příští týden před nedosáhne RTM.

*  Spuštění obnovení nuget v řešení se nezdaří, pokud v hierarchii složek nižší než soubory projektu je umístěn soubor řešení.
*  Spuštění příkazu delete nuget na balíčku pomocí kanálu V2 se nezdaří. Místo toho použijte V3 informačního kanálu.


Pro úplný seznam oprav chyb a vylepšení v této verzi, projděte si seznam problémů [tady](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).