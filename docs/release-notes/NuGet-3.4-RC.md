---
title: NuGet 3.4 RC poznámky
description: Zpráva k vydání verze pro NuGet 3.4 RC, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546751"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3.4 RC poznámky

[Zpráva k vydání verze NuGet 3.3](../release-notes/nuget-3.3.md) | [zpráva k vydání verze NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC byla vydána 3. března 2016 souběžně s Visual Studio 2015 Update 2 RC a byl sestaven s několika zásady v mozky:

* Podporu pro různé platformy
* Vylepšení výkonu
* Menší vylepšení uživatelského rozhraní

Následující funkce jsou dostupné v této verzi RC další plánované 3.4 finální verzi.

## <a name="new-features"></a>Nové funkce

* Klienti NuGet nyní podporují kódování obsahu gzip z úložišť
* Podpora pro soubory PDB z balíčků v projektech xproj
* Podpora pro iOS a akce sestavení pro Android v elementu contentFiles
* Podpora rozhraní framework monikerů netstandard a netstandardapp

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Výrazné zlepšení výkonu zejména na kartách instalace, aktualizace a konsolidaci
* Nainstalovaný a karty aktualizace jsou teď seřazené podle abecedy
* Přidat tlačítko pro aktualizaci, která umožňuje vyhledávání aktualizovat

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Balíčky odkazuje `project.json` , které mají plovoucí verze nebude aktualizovat při každém sestavení. Místo toho bude aktualizovat jenom v případě, že vynutit obnovení, vyčistit, znovu vytvořit nebo upravit `project.json`.
* nuget.org úložišť zdroje jsou již vynutit do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.
* NuGet už obnoví balíčky ve sdílených projektech ani zapíše soubor zámku.
* Jsme vylepšili selhání sítě a opakujte zpracování pro servery nedostupné nebo pomalé reakce.
* Vylepšené chování klávesnice a myši v Uživatelském rozhraní Správce balíčků Visual Studio.
* Nyní podporujeme nejnovější `project.json` schéma v DNX.

## <a name="known-issues"></a>Známé problémy

Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)