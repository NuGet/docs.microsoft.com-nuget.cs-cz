---
title: Zpráva k vydání verze NuGet 1,3
description: Poznámky k verzi pro NuGet 1,3, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777122"
---
# <a name="nuget-13-release-notes"></a>Zpráva k vydání verze NuGet 1,3

Zpráva k [vydání verze](../release-notes/nuget-1.2.md)  |  NuGet 1,2 Zpráva k [vydání verze NuGet 1,4](../release-notes/nuget-1.4.md)

NuGet 1,3 byl vydán 25. dubna 2011.

## <a name="new-features"></a>Nové funkce

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Zjednodušené vytváření balíčků s integrací serveru symbolů

Tým NuGet spolupracuje s lidé na [SymbolSource.org](http://www.symbolsource.org/) , který nabízí opravdu jednoduchý způsob publikování vašich zdrojů a PDB spolu s balíčkem. To umožňuje uživatelům vašeho balíčku krokovat se se zdrojem balíčku v ladicím programu. Další podrobnosti najdete v [tématu Vytvoření a publikování balíčku symbolů](../create-packages/symbol-packages.md) snadný způsob, jak publikovat balíčky NuGet se zdroji. Můžete také sledovat živou ukázku této funkce jako součást NuGet v podrobném hovoru na Mix11. Tato funkce je plně znázorněna na začátku 20 minut videa.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Systému

Tento příkaz usnadňuje zobrazení stránky projektu pro balíček v konzole správce balíčků. Poskytuje taky možnosti pro otevření adresy URL licence a stránky pro zneužití sestav pro daný balíček.
Syntaxe příkazu je:

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

`-PassThru`Možnost slouží k vrácení hodnoty zadané adresy URL.

Příklady:

```
PM> Open-PackagePage Ninject
```

Otevře prohlížeč na adrese URL projektu zadané v balíčku Ninject.

```
PM> Open-PackagePage Ninject -License
```

Otevře prohlížeč na adrese URL licence zadané v balíčku Ninject.

```
PM> Open-PackagePage Ninject -ReportAbuse
```

Otevře prohlížeč na adrese URL v aktuálním zdroji balíčků, který se používá k nahlášení zneužití pro zadaný balíček.

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

Přiřadí adresu URL licence k proměnné, $url, bez otevření adresy URL v prohlížeči.

### <a name="performance-improvements"></a>Zvýšení výkonu

NuGet 1,3 zavádí spoustu vylepšení výkonu. NuGet 1,3 vylučuje stažení stejné verze balíčku několikrát zahrnutím místní mezipaměti pro jednotlivé uživatele. Mezipaměť je k dispozici a vymazána prostřednictvím dialogového okna nastavení správce balíčků:

![Dialogové okno Možnosti NuGet s nastavením mezipaměti pro balíčky](./media/nuget-options.png)

Další vylepšení výkonu zahrnuje přidání podpory pro kompresi HTTP a vylepšení rychlosti instalace balíčku v rámci sady Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Sada Visual Studio a nuget.exe používají stejný seznam zdrojů balíčků

Před NuGet 1,3 se seznam zdrojů balíčků používaných nástrojem nuget.exe a sady NuGet pro Visual Studio Add-In neuložily na stejné místo. NuGet 1,3 teď používá stejný seznam na obou místech. Seznam je uložen v `NuGet.Config` a uložený ve složce sady data.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe ignoruje soubory a složky, které ve výchozím nastavení začínají na.

Aby mohla aplikace NuGet dobře fungovat se systémy správy zdrojového kódu, jako jsou podverze a Mercurial, nuget.exe při vytváření balíčků ignorovat složky a soubory, které začínají znakem ".". To lze přepsat pomocí dvou nových příznaků:

* __-NoDefaultExcludes__ se používá k přepsání tohoto nastavení a zahrnutí všech souborů.
* __– Vyloučení__ se používá k přidání dalších souborů nebo složek, které se mají vyloučit pomocí vzoru. Například pro vyloučení všech souborů s příponou souboru. bak

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Poznámka: vzor není ve výchozím nastavení rekurzivní._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Podpora pro projekty WiX a rozhraní .NET Micro Framework

Díky komunitním příspěvkům zahrnuje NuGet podporu typů projektů WiX i rozhraní .NET Micro Framework.

## <a name="bug-fixes"></a>Opravy chyb

Úplný seznam oprav chyb najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb zaznamenaly

* Balíčky se zdrojovými soubory fungují na webech i v projektech webových aplikací.
Pro websites se zdrojové soubory zkopírují do `App_Code` složky.
