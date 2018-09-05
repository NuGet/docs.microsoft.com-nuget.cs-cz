---
title: Poznámky k verzi 1.3 NuGet
description: Zpráva k vydání verze pro NuGet 1.3, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551348"
---
# <a name="nuget-13-release-notes"></a>Poznámky k verzi 1.3 NuGet

[Zpráva k vydání verze NuGet 1.2](../release-notes/nuget-1.2.md) | [zpráva k vydání verze NuGet 1.4](../release-notes/nuget-1.4.md)

NuGet 1.3 byla vydána 25. dubna 2011.

## <a name="new-features"></a>Nové funkce

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Zjednodušené vytváření balíčků s integrací serveru symbolů

Tým NuGet ve spolupráci s lidé na [SymbolSource.org](http://www.symbolsource.org/) nabízí opravdu jednoduchý způsob publikování zdrojů a souboru PDB. spolu s vašeho balíčku. To umožňuje uživatelům balíčku můžete krokovat s vnořením zdroj balíčku v ladicím programu. Další podrobnosti najdete v článku [vytváření a publikování balíčku symbolů](../create-packages/symbol-packages.md) snadný způsob, jak publikovat balíčky NuGet se zdroji. Můžete také sledovat živé ukázku této funkce jako součást balíčku NuGet do hloubky komunikovat na Mix11. Tato funkce je znázorněn plně od 20 minut označte videa.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Příkaz

Tento příkaz umožňuje snadno získat na stránce projektu pro balíček z konzoly Správce balíčků. Poskytuje také možnosti Otevřít adresu URL licence a zneužití stránky sestavy pro balíček.
Syntaxe příkazu je:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` Možnost se používá k vrácení hodnoty zadané adresy URL.

Příklady:

    PM> Open-PackagePage Ninject

Otevře prohlížeč na adrese URL projektu zadané v balíčku Ninject.

    PM> Open-PackagePage Ninject -License

Otevře prohlížeč na adrese URL licence zadané v balíčku Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Otevře prohlížeč na adrese URL u aktuálního zdroje balíčku použitého k oznámení zneužití pro zadaný balíček.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Přiřadí proměnné $url adresu URL licence bez otevření této adresy URL v prohlížeči.

### <a name="performance-improvements"></a>Zvýšení výkonu

NuGet 1.3 přináší spoustu vylepšení výkonu. NuGet 1.3 se vyhnete stahování stejnou verzi balíčku více než jednou zahrnutím mezipaměti místního uživatele. Mezipaměti můžete přistupovat a vymaže přes dialogové okno Nastavení správce balíčků:

![Dialogové okno Možnosti NuGet s nastavení mezipaměti balíčku](./media/nuget-options.png)

Další vylepšení výkonu zahrnují přidání podpory pro kompresi HTTP a vylepšení rychlosti instalaci balíčku sady Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio a nuget.exe používá stejný seznam zdroje balíčků

Před NuGet 1.3 seznam zdroje balíčků, které používají nuget.exe a NuGet Visual Studio Add-In nebyly uloženy na stejném místě. NuGet 1.3 nyní používá stejný seznam na obou místech. Seznam je uložen v `NuGet.Config` a uložené ve složce data aplikací.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe ignoruje soubory a složky, které začínají znakem '.' ve výchozím nastavení

Aby NuGet dobře fungují s systémy správy zdrojového kódu takové Subversion nebo Mercurial nuget.exe ignoruje složky a soubory, které začínají "." znaku při vytváření balíčků. To lze přepsat pomocí dvou nových příznaky:

* __-NoDefaultExcludes__ se používá pro toto nastavení přepsat a zahrnují všechny soubory.
* __-Vyloučení__ se používá k přidání dalších souborů a složek na vyloučit pomocí vzoru. Třeba vyloučit všechny soubory s příponou ".bak.

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Poznámka: vzor není rekurzivní ve výchozím nastavení._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Podpora pro projekty WiX a Micro rozhraní .NET Framework

Díky příspěvky vytvořené komunitou NuGet zahrnuje podporu pro typy projektů WiX, jakož i rozhraní .NET Framework Micro.

## <a name="bug-fixes"></a>Opravy chyb

Úplný seznam oprav chyb, podívejte se prosím [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb za zmínku

* Balíčky se zdrojovým souborem fungovat na obou webech a v projektech webových aplikací.
Pro moduly Websites, zdrojové soubory jsou zkopírovány do `App_Code` složky
