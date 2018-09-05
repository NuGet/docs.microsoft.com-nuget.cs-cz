---
title: NuGet 3.4 poznámky
description: Zpráva k vydání verze pro NuGet 3.4, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551188"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 poznámky

[Poznámky k verzi 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [zpráva k vydání verze NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 30. března 2016 byla vydána jako součást Visual Studio 2015 Update 2 a Preview verze sady Visual Studio 15 a byl sestaven s několika zásady v mozky:

* Podporu pro různé platformy
* Vylepšení výkonu
* Menší vylepšení uživatelského rozhraní

Následující funkce byly dříve přidány do verze RC a byly aktualizovány nebo dokončení verze 3.4:

## <a name="new-features"></a>Nové funkce

* Klienti NuGet nyní podporují kódování obsahu gzip z úložišť
* Podpora pro soubory PDB z balíčků v projektech xproj
* Podpora pro iOS a akce sestavení pro Android v elementu contentFiles
* Podpora rozhraní framework monikerů netstandard a netstandardapp

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Výrazné zlepšení výkonu zejména na kartách instalace, aktualizace a konsolidaci
* Je k dispozici ke slučování výsledků hledání správné agregovaného zdroje 'všechny zdroje balíčků.
* Nainstalovaný a karty aktualizace jsou teď seřazené podle abecedy
* Přidat tlačítko pro aktualizaci, která umožňuje vyhledávání aktualizovat
* Nejnovější sestavení možnosti v horní části seznamu verze

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Balíčky odkazuje `project.json` , které mají plovoucí verze nebude aktualizovat při každém sestavení. Místo toho bude aktualizovat jenom v případě, že vynutit obnovení, vyčistit, znovu vytvořit nebo upravit `project.json`.
* nuget.org úložišť zdroje jsou již vynutit do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.
* NuGet už obnoví balíčky ve sdílených projektech ani zapíše soubor zámku.
* Jsme vylepšili selhání sítě a opakujte zpracování pro servery nedostupné nebo pomalé reakce.
* Vylepšené chování klávesnice a myši v Uživatelském rozhraní Správce balíčků Visual Studio.
* Nyní podporujeme nejnovější `project.json` schéma v DNX.

## <a name="breaking-changes"></a>Nejnovější změny

* Čísla verzí balíčku jsou nyní normalizovány na formát *hlavní*. *vedlejší*. *oprava*-*předběžnou verzi* všech hlavních, podverze a oprava jsou považovány za celých čísel a vyřadit všechny úvodní nuly.  Informace o předběžnou verzi je považován za řetězcový a žádné změny se použijí k němu. Tyto hodnoty se používají v dotazech klienti NuGet a vyhledávání poskytovaných službou nuget.org.  Další podrobnosti najdete v dokumentaci NuGet v rámci [zkušební verze](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Známé problémy

* **Problém:** Windows 10 v1511, můžou uživatelé zaznamenat potíže nebo dokonce i sady Visual Studio selhání pomocí Powershellu v sadě Visual Studio v následujících scénářích:
    * Instalace / Odinstalace balíčky, které mají install.ps1 / uninstall.ps1 skriptů
    * Načítají se projekty, které mají skriptu init.ps1 (např. EntityFramework)
    * Publikování webového obsahu

* **Alternativní řešení:** zajistěte, aby vaše instalace Windows 10 nejnovějších oprav použít, expecially leden 2016 (KB 3124263) nebo novější aktualizace.  Další podrobnosti jsou dostupné na [problém Githubu #1638](http://github.com/nuget/home/issues/1638)

* **Problém:** Přesměrování protokolu NuGet v2 jsou přerušená.
Vlastní úložiště NuGet, které směrují požadavky na alternativního hostitele, nerespektují požadavky přesměrování.
* **Alternativní řešení:** Pokud chcete tento problém obejít, nakonfigurujte identifikátor URI úložiště balíčků tak, aby odkazoval na přesměrované umístění serveru.
Další informace najdete v tématu [žádosti o přijetí změn Githubu #387](https://github.com/NuGet/NuGet.Client/pull/387).

Pokračujeme v sledování problémů v našem seznamu problémů na Githubu najdete je na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)