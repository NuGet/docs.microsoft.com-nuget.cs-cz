---
title: Poznámky k verzi 3.4 RC NuGet
description: Poznámky k verzi pro NuGet 3.4 RC včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-rc-release-notes"></a>Poznámky k verzi 3.4 RC NuGet

[Poznámky k verzi NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 poznámky k verzi](../release-notes/nuget-3.4.md)

NuGet 3.4-RC byla vydána 3. března 2016 spolu s Visual Studio 2015 Update 2 RC a byl sestaven s několika principů v rozhodnutí:

* Podpora více platforem
* Vylepšení výkonu
* Méně závažné vylepšení uživatelského rozhraní

Následující funkce jsou k dispozici v této RC s více plánované pro 3,4 finální verzi.

## <a name="new-features"></a>Nové funkce

* Klienti NuGet nyní podporují gzip kódování obsahu z úložiště
* Podpora pro soubory PDB z balíčků projektů xproj
* Podpora pro iOS a Android akce v elementu contentFiles sestavení
* Podpora monikerů netstandard a netstandardapp monikery framework

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Významné zlepšení výkonu hlavně na kartách nainstalovaná, aktualizace a konsolidace
* Nainstalovaná a aktualizace karty jsou teď řadí abecedně
* Přidat tlačítko Aktualizovat, která umožňuje vyhledávání nutné aktualizovat

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Balíčky, kterou se odkazuje v `project.json` mají plovoucí verze nebude aktualizovat na každé sestavení. Místo toho bude aktualizovat pouze v případě, že vynutit obnovení, vyčistit, znovu sestavit nebo upravit `project.json`.
* nuget.org úložiště zdrojů již nebude, vynuceně přesunuty do konfigurace projektu při použití konfigurace NuGet uživatelského rozhraní.
* NuGet už obnoví balíčků ve sdílených projektů ani zapisuje do souboru zámku.
* Jsme jste vylepšené selhání sítě a opakujte zpracování pro nedostupné nebo pomalé na reakce serverů.
* Chování klávesnici a myš jsou vylepšení v uživatelském rozhraní Správce balíčků Visual Studio.
* Teď podporujeme nejnovější `project.json` schéma v DNX.

## <a name="known-issues"></a>Známé problémy

Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)