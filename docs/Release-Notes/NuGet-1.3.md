---
title: "Poznámky k verzi NuGet 1.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.3 NuGet."
keywords: "NuGet 1.3 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-13-release-notes"></a>1.3 poznámky NuGet

[Poznámky k verzi NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4 poznámky k verzi](../release-notes/nuget-1.4.md)

NuGet 1.3 byla vydána 25 Duben 2011.

## <a name="new-features"></a>Nové funkce

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Zjednodušená vytvoření balíčku s integrací serveru – symbol

Týmem NuGet ve spolupráci s zaměstnance na [SymbolSource.org](http://www.symbolsource.org/) nabízet skutečně jednoduchý způsob publikování zdrojů a na PDB společně s vašeho balíčku. To umožňuje příjemci vašeho balíčku na krok do zdroje balíčku v ladicím programu. Další informace najdete v [vytváření a publikování balíčku Symbol](../create-packages/symbol-packages.md) snadný způsob, jak publikovat balíčky NuGet se zdroji. Můžete také shlédnout této funkce jako součást NuGet podrobněji za provozu ukázkový komunikovat v Mix11. Tato funkce je plně ukázán začínající na 20 minut označit videa.

### <a name="open-packagepage-command"></a>`Open-PackagePage`Příkaz

Tento příkaz lze snadno získat na stránku projektu pro balíček z konzoly Správce balíčků. Obsahuje také možnosti otevřete adresu URL licence a zneužití stránka sestavy pro daný balíček.
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

NuGet 1.3 představuje mnoho vylepšení výkonu. NuGet 1.3 zabraňuje stahování stejnou verzi balíčku vícekrát zahrnutím mezipaměti místní jednotlivé uživatele. Mezipaměti můžete získat přístup a vymazat prostřednictvím dialogu Nastavení správce balíčků:

![Dialogové okno Možnosti NuGet s nastavení mezipaměti balíčku](./media/nuget-options.png)

Další vylepšení výkonu zahrnují přidání podpory pro komprese protokolu HTTP a vylepšení rychlosti instalace balíčku Visual Studia.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio a nuget.exe používá stejný seznam zdroje balíčků

Před NuGet 1.3 nebyly uloženy seznam slouží jako nuget.exe a NuGet Visual Studio Add-In zdroje balíčku na stejném místě. NuGet 1.3 teď používá stejný seznam na obou místech. Seznam je uložen v `NuGet.Config` a uložen ve složce data aplikací.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe ignoruje soubory a složky, které začínají s '.' ve výchozím nastavení

Aby bylo možné NuGet tyto Subversion a Mercurial funkce fungují dobře u zdrojových systémů řízení, nuget.exe ignoruje složek a souborů, které začínají '.' znak při vytváření balíčků. To lze přepsat pomocí dva nové příznaky:

* __-NoDefaultExcludes__ se používá pro toto nastavení přepsat a zahrnují všechny soubory.
* __-Vyloučit__ se používá k přidání další soubory a složky, které chcete vyloučit pomocí vzoru. Chcete-li například vyloučí všechny soubory s příponou souboru '.bak.

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Poznámka: vzoru není rekurzivní ve výchozím nastavení._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Podpora pro projekty WiX a malých rozhraní .NET Framework

Díky komunitní příspěvky NuGet zahrnuje podporu pro typy projektů WiX, jakož i rozhraní .NET Framework Micro.

## <a name="bug-fixes"></a>Opravy chyb

Úplný seznam oprav chyb, zobrazte [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Opravy chyb vhodné poznamenat

* Balíčky s zdrojové soubory fungovat v obou webů a projekty webových aplikací.
Pro weby, zdrojové soubory jsou kopírovány do `App_Code` složky
