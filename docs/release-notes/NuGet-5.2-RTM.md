---
title: Poznámky k verzi NuGet 5,2 RTM
description: Poznámky k verzi pro NuGet 5,2, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776210"
---
# <a name="nuget-52-release-notes"></a>Zpráva k vydání verze NuGet 5,2

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**5.2.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core 

<sup>2</sup> . K dispozici jako volitelná instalace se sadou Visual Studio 2019 s úlohou .NET Core

## <a name="summary-whats-new-in-52"></a>Shrnutí: Novinky v 5,2

* Opravili jsme kritickou chybu, která způsobila občasné selhání operací NuGet z důvodu potíží s cestou na platformě Linux & Mac – [#7341](https://github.com/NuGet/Home/issues/7341)

* Vylepšená rychlost odezvy uživatelského rozhraní při procházení balíčků pomocí uživatelského rozhraní Správce balíčků NuGet v aplikaci Visual Studio, obzvláště pro pomalé zdroje – [#8039](https://github.com/NuGet/Home/issues/8039)

* Tuny oprav spolehlivosti pro soubor zámku ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) a ověřovací modul plug-in ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Štěnic**

* Výkon: konzola správce balíčků: aktualizace uživatelského rozhraní na základě pole se seznamem výchozí projekt s hodnotou – [#8235](https://github.com/NuGet/Home/issues/8235)

* Výkon: vylepšení výkonu v uživatelském rozhraní PM – [#8039](https://github.com/NuGet/Home/issues/8039)

* Výkon: zpoždění uživatelského rozhraní při čtení výchozího projektu v PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf: [vsfeedback] karta aktualizace NuGet se zablokuje pro zdroj místního balíčku [#6470](https://github.com/NuGet/Home/issues/6470)

* Moduly plug-in: NuGet počká plný časový limit handshake, pokud se nepovede modul plug-in spustit nebo ukončí [#8300](https://github.com/NuGet/Home/issues/8300) .

* Moduly plug-in: vylepšení diagnostiky selhání spuštění modulu plug-in – [#8271](https://github.com/NuGet/Home/issues/8271)

* Moduly plug-in: potíže se zjišťováním nuget.exe vestavěných modulů plug-in – [#8269](https://github.com/NuGet/Home/issues/8269)

* Moduly plug-in: soubor Cache není nikdy čten – [#8210](https://github.com/NuGet/Home/issues/8210)

* Moduly plug-in: úloha byla zrušena. chyby s modulem plug-in ověřování při obnovení – [#8198](https://github.com/NuGet/Home/issues/8198)

* Nezjistitelná mezipaměť modulů plug-in na platformách Linux – [#7845](https://github.com/NuGet/Home/issues/7845)

* LockFile: s ATF má nepravdivé NU1004 z důvodu chybné kontroly rovnosti cílového rozhraní [#8187](https://github.com/NuGet/Home/issues/8187)

* LockFile: příznak obnovení uzamčeného režimu se nerespektuje, pokud je soubor zámku prázdný nebo je poškozený – [#8160](https://github.com/NuGet/Home/issues/8160)

* LockFile: nepoužívá se nemalá písmena projektů s názvy vlastních sestavení v balíčcích soubor zámku- [#8114](https://github.com/NuGet/Home/issues/8114)

* LockFile: vytvořit odkaz na projekt v případě souboru zámku malými písmeny – [#7840](https://github.com/NuGet/Home/issues/7840)

* Obnovení: při instalaci úmyslně podepsaného balíčku dojde k několika neúspěšným pokusům o instalaci (s opakovaným výstupem) – [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: Nepodařilo se deserializovat možnosti uživatele řešení po aktualizaci NuGet – [#8166](https://github.com/NuGet/Home/issues/8166)

* dotnet-list-Package v projektu UnitTest vrátí chybu – [#8154](https://github.com/NuGet/Home/issues/8154)

* Vytvořit skupinu balíčků NuGet pro instalační program VS – oprava některých problémů s instalací VSIX – [#8033](https://github.com/NuGet/Home/issues/8033)

* GeneratePackageOnBuild by neměl nastavovat Build. - [#7801](https://github.com/NuGet/Home/issues/7801)

* Nová možnost "-SymbolPackageFormat snupkg" vygeneruje chybu, pokud soubor. nuspec obsahuje explicitní element odkazu na sestavení- [#7638](https://github.com/NuGet/Home/issues/7638)

* NuGet. TARGETS (498; 5): Chyba: nepovedlo se najít část cesty/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341) .

**DCR**

* Přidání vlastnosti MSBuild, která indikuje, že je PackageDownload podporovaný – [#8106](https://github.com/NuGet/Home/issues/8106)

* FrameworkReference potlačí tok závislostí prostřednictvím FrameworkReference. PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Mechanismus pro dodávání runtime.jsů mimo balíček – [#7351](https://github.com/NuGet/Home/issues/7351)

**[Seznam všech problémů opravených v této verzi – 5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


