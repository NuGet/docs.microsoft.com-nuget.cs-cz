---
title: Poznámky k verzi NuGet 3.4.2
description: Poznámky k verzi pro NuGet 3.4.2, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780257"
---
# <a name="nuget-342-release-notes"></a>Poznámky k verzi NuGet 3.4.2

Poznámky k verzi [NuGet 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Poznámky k verzi NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

3.4.2 NuGet byl vydaný 8. dubna 2016, který řeší několik problémů, které byly zjištěny ve verzi 3,4 a 3.4.1.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC je teď k dispozici

Release Candidate nuget.exe 3.4.2 si můžete stáhnout [tady](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Výrazně jsme vylepšili výkon aktualizací v konkrétním scénáři, kdy aktualizace balíčků s grafy s hloubkou závislostí trvaly hodně času a reagují na Visual Studio.
* obnovení NuGet bez síťového provozu je 2,5 × – 3x rychlejší v rámci sady Visual Studio.
* Kromě této změny jsme vyřešili problém, kdy jsme při načítání počtu aktualizací v uživatelském rozhraní VS používali síť dvakrát. Toto bylo částečně zodpovědné za určitý časový limit pro zákazníky, kteří se setkali v 3.4/3.4.1.
* Přidání podpory pro no_proxy nastavení

## <a name="fixes"></a>Opravy

* Opravili jsme problém, kdy v nastaveních NuGet nebo v konfiguraci 3.4.1 chybí zdroj nuget.org po aktualizaci na.
* Opravili jsme problém, kdy se velká a malá písmena mění na FindPackagesById v 3.4.1 Breaks Artifactory.
* Byl opraven problém se standardem FIPS, který způsobil selhání při obnovení NuGet s nuget.exe.
* Při procházení zdrojů s neplatnou adresou URL ikony došlo k chybě.
* Opravili jsme problémy se sloučením verzí a záznamů ze všech zdrojů.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Známé problémy v příkazovém řádku 3.4.2 Windows x86 (RC)

Tyto problémy budou v brzkém příštím týdnu opraveny, než zahájíme RTM.

*  Pokud je soubor řešení umístěný v nižší hierarchii složky než soubory projektu, spuštění obnovení NuGet na řešení se nezdaří.
*  Spuštění příkazu NuGet DELETE na balíčku pomocí informačního kanálu v2 se nezdaří. Místo toho použijte informační kanál v3.


Úplný seznam oprav a vylepšení v této [verzi najdete v seznamu problémů.](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)