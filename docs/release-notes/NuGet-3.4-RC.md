---
title: Poznámky k verzi pro NuGet 3,4 – RC
description: Poznámky k verzi pro NuGet 3,4 RC, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780239"
---
# <a name="nuget-34-rc-release-notes"></a>Poznámky k verzi pro NuGet 3,4 – RC

Zpráva k [vydání verze](../release-notes/nuget-3.3.md)  |  NuGet 3,3 Zpráva k [vydání verze NuGet 3,4](../release-notes/nuget-3.4.md)

NuGet 3,4 – RC byla vydána 3. března 2016 společně se sadou Visual Studio 2015 Update 2 RC a byla sestavena s několika principy v mozky:

* Podpora pro různé platformy
* Vylepšení výkonu
* Vylepšení dílčího uživatelského rozhraní

V této verzi RC jsou k dispozici následující funkce s vyšším plánovaným vydáním pro 3,4 finální verzi.

## <a name="new-features"></a>Nové funkce

* Klienti NuGet teď podporují kódování obsahu gzip z úložišť.
* Podpora soubory PDB z balíčků v projektech xproj
* Podpora pro akce sestavení pro iOS a Android v elementu contentFiles
* Podpora pro monikery rozhraní netstandard a netstandardapp

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Významná vylepšení výkonu, zejména na kartách nainstalované, aktualizace a konsolidace
* Nainstalované a aktualizované karty jsou nyní seřazené abecedně.
* Přidání tlačítka aktualizovat, které umožňuje aktualizovat hledání

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Balíčky, na které se odkazuje v `project.json` plovoucí verzi, se v každém sestavení neaktualizují. Místo toho se aktualizují pouze v případě, že je vynuceno obnovení, vyčištění, opětovné sestavení nebo změna `project.json` .
* zdroje úložiště nuget.org již nejsou vynuceny do konfigurace projektu, když použijete uživatelské rozhraní konfigurace NuGet.
* NuGet už neobnovuje balíčky ve sdílených projektech ani nezapisuje soubor zámku.
* Vylepšili jsme selhání sítě a zpracování opakování pro nedosažitelné nebo pomalé servery.
* Vylepšení chování klávesnice a myši jsou vylepšena v uživatelském rozhraní Správce balíčků sady Visual Studio.
* Nyní podporujeme nejnovější `project.json` schéma v DNX.

## <a name="known-issues"></a>Známé problémy

Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)