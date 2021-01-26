---
title: Zpráva k vydání verze NuGet 3,4
description: Poznámky k verzi pro NuGet 3,4, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776415"
---
# <a name="nuget-34-release-notes"></a>Zpráva k vydání verze NuGet 3,4

Poznámky k verzi [pro NuGet 3,4 – RC](../release-notes/nuget-3.4-RC.md)  |  [Poznámky k verzi NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3,4 byl vydán 30. března 2016 jako součást verze Visual Studio 2015 Update 2 a Visual Studio 15 Preview a vytvořila se s několika principy v mozky:

* Podpora pro různé platformy
* Vylepšení výkonu
* Vylepšení dílčího uživatelského rozhraní

Následující funkce byly dříve přidány ve verzi RC a byly aktualizovány nebo dokončeny pro vydání 3,4:

## <a name="new-features"></a>Nové funkce

* Klienti NuGet teď podporují kódování obsahu gzip z úložišť.
* Podpora soubory PDB z balíčků v projektech xproj
* Podpora pro akce sestavení pro iOS a Android v elementu contentFiles
* Podpora pro monikery rozhraní netstandard a netstandardapp

## <a name="new-user-interface-features"></a>Nové funkce uživatelského rozhraní

* Významná vylepšení výkonu, zejména na kartách nainstalované, aktualizace a konsolidace
* Zdroj všech zdrojů balíčků je k dispozici v rámci správného sloučení výsledků hledání.
* Nainstalované a aktualizované karty jsou nyní seřazené abecedně.
* Přidání tlačítka aktualizovat, které umožňuje aktualizovat hledání
* Nejnovější možnosti sestavení v horní části seznamu verzí

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Balíčky, na které se odkazuje v `project.json` plovoucí verzi, se v každém sestavení neaktualizují. Místo toho se aktualizují pouze v případě, že je vynuceno obnovení, vyčištění, opětovné sestavení nebo změna `project.json` .
* zdroje úložiště nuget.org již nejsou vynuceny do konfigurace projektu, když použijete uživatelské rozhraní konfigurace NuGet.
* NuGet už neobnovuje balíčky ve sdílených projektech ani nezapisuje soubor zámku.
* Vylepšili jsme selhání sítě a zpracování opakování pro nedosažitelné nebo pomalé servery.
* Vylepšení chování klávesnice a myši jsou vylepšena v uživatelském rozhraní Správce balíčků sady Visual Studio.
* Nyní podporujeme nejnovější `project.json` schéma v DNX.

## <a name="breaking-changes"></a>Zásadní změny

* Čísla verzí balíčků jsou nyní normalizována na formát *Hlavní*. *vedlejší*. *Oprava* - *Předběžná verze*   Každá z hlavních, vedlejších a oprav je považována za celá čísla a vynechá úvodní nuly.  Předprodejní informace se považují za řetězec a na ni se nevztahují žádné změny. Tato čísla se používají v dotazech klientů NuGet a hledání poskytované službou nuget.org.  Další podrobnosti najdete v dokumentaci NuGet v části [předprodejní verze](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Známé problémy

* **Problém:** Uživatelé v1511 s Windows 10 můžou zaznamenat problémy nebo dokonce chybu sady Visual Studio s prostředím PowerShell v aplikaci Visual Studio v následujících scénářích:
    * Instalace/odinstalace balíčků, které mají skripty install.ps1/uninstall.ps1
    * Načítání projektů, které mají skript init.ps1 (například EntityFramework)
    * Publikování webového obsahu

* **Alternativní řešení:** Ujistěte se, že instalace Windows 10 má nejnovější použité opravy, expecially 2016. ledna (KB 3124263) nebo novější aktualizace.  Další podrobnosti jsou k dispozici v [problému na githubu #1638](http://github.com/nuget/home/issues/1638)

* **Problém:** Přesměrování protokolu NuGet v2 jsou přerušená.
Vlastní úložiště NuGet, které směrují požadavky na alternativního hostitele, nerespektují požadavky přesměrování.
* **Alternativní řešení:**  Pokud chcete tento problém obejít, nakonfigurujte identifikátor URI úložiště balíčků v nastavení tak, aby odkazoval na přesměrované umístění serveru.
Další informace najdete v tématu [žádosti o přijetí změn githubu #387](https://github.com/NuGet/NuGet.Client/pull/387).

Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)