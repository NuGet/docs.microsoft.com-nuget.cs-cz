---
title: NuGet 3.4 poznámky
description: Poznámky k verzi pro NuGet 3.4, včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820469"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 poznámky

[Poznámky k verzi 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 poznámky k verzi](../release-notes/nuget-3.4.1.md)

NuGet 3.4 byl vydané 30. března 2016 jako součást sady Visual Studio 2015 Update 2 a Visual Studio 15 Preview verze a byl sestaven s několika principů v rozhodnutí:

* Podpora více platforem
* Vylepšení výkonu
* Méně závažné vylepšení uživatelského rozhraní

Následující funkce byly dříve přidány v RC a byly aktualizovány nebo dokončit 3,4 verzi:

## <a name="new-features"></a>Nové funkce

* Klienti NuGet nyní podporují gzip kódování obsahu z úložiště
* Podpora pro soubory PDB z balíčků projektů xproj
* Podpora pro iOS a Android akce v elementu contentFiles sestavení
* Podpora monikerů netstandard a netstandardapp monikery framework

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Významné zlepšení výkonu hlavně na kartách nainstalovaná, aktualizace a konsolidace
* Je k dispozici s slučování výsledek hledání správné agregovaného zdroje 'všechny zdroje balíčků.
* Nainstalovaná a aktualizace karty jsou teď řadí abecedně
* Přidat tlačítko Aktualizovat, která umožňuje vyhledávání nutné aktualizovat
* Nejnovější sestavení možnosti v horní části seznamu verze

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Balíčky, kterou se odkazuje v `project.json` mají plovoucí verze nebude aktualizovat na každé sestavení. Místo toho bude aktualizovat pouze v případě, že vynutit obnovení, vyčistit, znovu sestavit nebo upravit `project.json`.
* nuget.org úložiště zdrojů již nebude, vynuceně přesunuty do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.
* NuGet už obnoví balíčků ve sdílených projektů ani zapisuje do souboru zámku.
* Jsme jste vylepšené selhání sítě a opakujte zpracování pro nedostupné nebo pomalé na reakce serverů.
* Chování klávesnici a myš jsou vylepšení v uživatelském rozhraní Správce balíčků Visual Studio.
* Teď podporujeme nejnovější `project.json` schéma v DNX.

## <a name="breaking-changes"></a>Nejnovější změny

* Čísla verzí balíčku jsou nyní normalizovány na formát *hlavní*. *méně závažné*. *oprava*-*předprodejní* každé hlavní, malé a opravy se považují za celá čísla a vyřadit všechny úvodní nuly.  Předběžné informace se považuje za řetězec a žádné změny se použijí k němu. Tato čísla se používají v dotazech klienti NuGet a hledání poskytovaný službou nuget.org.  Další podrobnosti naleznete v dokumentaci NuGet v rámci [vydanou verzí](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Známé problémy

* **Problém:** Windows 10 v1511, můžou uživatelé zaznamenat potíže nebo i Visual Studio havárie v prostředí Powershell v sadě Visual Studio v následujících scénářích:
    * Instalace / Odinstalace balíčky, které mají install.ps1 / uninstall.ps1 skriptů
    * Načítání projekty, které mají skript Init.ps1, způsobí (např. EntityFramework)
    * Publikování webového obsahu

* **Alternativní řešení:** zajistěte, aby vaše instalace systému Windows 10 nejnovější použitých, expecially leden 2016 (KB 3124263) nebo novější aktualizace.  Další podrobnosti jsou dostupné na [potíže Githubu #1638](http://github.com/nuget/home/issues/1638)

* **Problém:** Přesměrování protokolu NuGet v2 jsou přerušená.
Vlastní úložiště NuGet, které směrují požadavky na alternativního hostitele, nerespektují požadavky přesměrování.
* **Alternativní řešení:** tento problém obejít, nakonfigurujte identifikátor URI úložiště balíčků tak, aby odkazoval na přesměrované umístění serveru.
Další informace najdete v tématu [Githubu žádost o přijetí změn #387](https://github.com/NuGet/NuGet.Client/pull/387).

Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)