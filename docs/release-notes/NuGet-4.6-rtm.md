---
title: Zpráva k vydání verze NuGet 4.6 RTM
description: Zpráva k vydání verze pro NuGet 4.6.0 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 3c71d05144aa2b92b916d4ebf319c5a4e321581f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549841"
---
# <a name="nuget-46-rtm-release-notes"></a>Zpráva k vydání verze NuGet 4.6 RTM

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) součástí [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Souhrn: Novinky v této verzi

* Přidali jsme podporu pro [podepisování balíčků](../create-packages/sign-a-package.md).
* Visual Studio 2017 a nuget.exe nyní ověří integritu balíčků před instalací, obnovují se balíčky pro [podepsaných balíčků](../reference/signed-packages-reference.md).
* Vylepšili jsme výkon postupné obnovení.

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET Standard 2.0 pomocí rozhraní .NET Framework a NuGet 

.NET standard a jeho nástroje je navržená tak, že projekty cílené na rozhraní .NET Framework 4.6.1 může spotřebovat balíčky NuGet & projekty cílené na .NET Standard 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře plánu pro účely řešení a alternativní řešení můžete nasadit s dnešní stavu nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Nejzávažnější chyby opravené v této verzi

**Opravy výkonu**

* Nezapisujte soubory prostředků, pokud není žádná změna - [#6491](https://github.com/NuGet/Home/issues/6491)
* Obnovení způsobí, že další MSBuild hodnocení při TFM podřízené projekty se neshodují s nadřazenou projektu – [#6311](https://github.com/NuGet/Home/issues/6311)
* Zlepšení výkonu obnovení NoOp optimalizací závislost grafu specifikace vytvoření - [#6252](https://github.com/NuGet/Home/issues/6252)

**Chyby**

* Metodou push do místní složky opustí nupkg uzamčen - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementace modulu plug-in NuGet: několik problémů - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - odebrat dotaz volání služby od inicializace MEF v VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)
* Výjimky pro hlášení chyb zrušit úlohy stahování balíčku - [#6096](https://github.com/NuGet/Home/issues/6096)
* Nahradí NuGet.exe '+' s '% 2B' v sestavení názvu - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn + F1 nepřijímá na stránku odbornou pomoc pro PM uživatelského rozhraní a konzolu - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet zapíše absolutní cesty do souborů projektu za specifických podmínek - [#5888](https://github.com/NuGet/Home/issues/5888)
* Oprava regrese 4.3 - zástupné symboly $product$ a $AssemblyGuid$ není nahrazena v contentfile prostřednictvím transformací – [#5880](https://github.com/NuGet/Home/issues/5880)
* DotNet restore s chybovými ukončeními více zdrojů - [#5817](https://github.com/NuGet/Home/issues/5817)
* Balíček by se měl znovu vyhodnotit verze projektu k povolení správy verzí git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Zlepšení intenzivně pochopit chyby při instalaci nekompatibilní balíček – [#4555](https://github.com/NuGet/Home/issues/4555)
* Možnost instalace balíčků jako PackageReferences - potřebuje TemplateWizard [#4549](https://github.com/NuGet/Home/issues/4549)
* Soubory balíčku doručit vlastností ignoruje při MSBuild.exe spuštění z mimo příkazový řádek vývojáře - [#4530](https://github.com/NuGet/Home/issues/4530)
* Oprava nízký chybová zpráva při odkazování na standardní knihovny .NET, který se nedá použít k projekci - [#4423](https://github.com/NuGet/Home/issues/4423)
* příkaz DotNet add balíčku selže cílení přenosné profilu balíček s trochu poradit - [#4349](https://github.com/NuGet/Home/issues/4349)
* balíčku DotNet - suffix verze chybí ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Vytváření chyb a selhání VS se šablonou .NET Core – [#3973](https://github.com/NuGet/Home/issues/3973)
* Nepovedlo se načíst index služby pro zdroj https:* - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list - allversions nefunguje - [#3441](https://github.com/NuGet/Home/issues/3441)
* Zavádějící závislost rozlišení chybová zpráva - [#2984](https://github.com/NuGet/Home/issues/2984)
* obnovení nuget.exe nevytvoří .props a .targets soubory pro .msbuildproj (regrese v3.3.0 3.4.4 upgradu) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Zpoždění uživatelského rozhraní při aktualizaci balíčku NuGet s XAML soubor otevřen - [#2878](https://github.com/NuGet/Home/issues/2878)
* Projektu web služby IIS se nezdaří neplatné znaky v cestě - [#2798](https://github.com/NuGet/Home/issues/2798)
* Přidat Nuget. program přestane reagovat na CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Obnovení s packagesavemode - nupkg selže u json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Správce balíčků filtru není k dispozici v sadě Visual Studio výstupní okno pro příkaz restore - [#2704](https://github.com/NuGet/Home/issues/2704)

[Seznam všech problémů, které jsou opravené v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
