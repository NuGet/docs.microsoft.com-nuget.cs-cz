---
title: Zpráva k vydání verze NuGet 5,6
description: Poznámky k verzi pro NuGet 5,6, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727819"
---
# <a name="nuget-56-release-notes"></a>Zpráva k vydání verze NuGet 5,6

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core

## <a name="summary-whats-new-in-56"></a>Shrnutí: Novinky v 5,6

* Podporuje předběžné verze balíčků s plovoucími verzemi. `Version="*-*"`, `Version="1.*-*"` a podobného typu float na nejnovější verze, včetně předprodejních verzí, v rámci zadaného rozsahu – [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Chyby:**

* `nuget push *.nupkg`dojde k chybě, pokud snupkg neexistuje – [#8148](https://github.com/NuGet/Home/issues/8148)

* A několik dalších cest kódu, které selžou, závisí na národním prostředí. Použití RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Výkon: specifikace DG pro Neuvolněné projektové scénáře by se neměly zapisovat do obnovení verze Preview- [#8793](https://github.com/NuGet/Home/issues/8793)

* Obnovení: zlepšení výkonu ukládáním specifikací grafu závislostí řešení do mezipaměti – [#9201](https://github.com/NuGet/Home/issues/9201)

* Uživatelské rozhraní PM nefunguje pro projekty stylu sady SDK po instalaci balíčku pomocí konzoly PM – [#9203](https://github.com/NuGet/Home/issues/9203)

* Vložená ikona se nedá zobrazit v uživatelském rozhraní PM s informačním kanálem místního balíčku – v závislosti na zapnutém/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)

* NuGetVersion. TryParseStrict () by měl vrátit hodnotu false, pokud se nepovede analyzovat – [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`nápovědu pro `-source` , by měla navrhovat použití názvu zdroje, nikoli zdrojového URL – [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`Vytvoří chybný výchozí název zdroje balíčku – [#9277](https://github.com/NuGet/Home/issues/9277)

* Čtečka obrazovky neoznamuje hledání... zpráva při přepínání karet – [#9307](https://github.com/NuGet/Home/issues/9307)

* Usnadnění: barva pro výběr – obdélník není dostupná na kartách uživatelského rozhraní PM v tmavém motivu – [#9336](https://github.com/NuGet/Home/issues/9336)

* Nástroj NuGet. exe 5,5 se nemůže obnovit pomocí nástroje MSBuild 14 nebo nižšího [#9458](https://github.com/NuGet/Home/issues/9458)

* V příkazech obnovit zprávy se neprotokolují časy milisekund – [#8977](https://github.com/NuGet/Home/issues/8977)

* Převést IOutputConsole na asynchronní [#9268](https://github.com/NuGet/Home/issues/9268)

* Vyzvednutí verze nástroje MSBuild v některých jazykových kulturách nefunguje správně – [#9322](https://github.com/NuGet/Home/issues/9322)

* Chybějící výchozí formát pro `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Výkon: RestoreOperationLogger má nepotřebnou spřažení vlákna – [#9288](https://github.com/NuGet/Home/issues/9288)

* Automatizované vytváření dokumentů pro `dotnet nuget` příkazy – [#9146](https://github.com/NuGet/Home/issues/9146)

* Výchozí podrobnost by neměla oznamovat NoOp obnovení jednotlivých projektů – [#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`Parametr podpory pro příkaz `NuGet.exe update` podobný příkazu install- [#7694](https://github.com/NuGet/Home/issues/7694)


**Chcete odeslat obecnou**

* Přidat počáteční podporu pro NET 5.0 Target Framework – [#9584](https://github.com/NuGet/Home/issues/9584)

* Seřaďte balíčky podle ID na kartě aktualizace uživatelského rozhraní PM – [#9278](https://github.com/NuGet/Home/issues/9278)


**[Seznam všech problémů opravených v této verzi – 5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
