---
title: NuGet 4.6 RTM Poznámky k verzi
description: Poznámky k verzi pro NuGet 4.6.0 včetně známých problémů, oprav chyb, přidaných funkcí a řadičů domény.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498686"
---
# <a name="nuget-46-release-notes"></a>NuGet 4.6 Poznámky k verzi

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) přichází s [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-460"></a>Shrnutí: Co je nového v 4.6.0

* Přidali jsme podporu pro [podepisování balíčků](../create-packages/sign-a-package.md).
* Visual Studio 2017 a nuget.exe nyní ověřuje integritu balíčku před instalací a obnovuje balíčky pro [podepsané balíčky](../reference/signed-packages-reference.md).
* Zlepšili jsme výkon po sobě jdoucích obnovení.

## <a name="summary-whats-new-in-463"></a>Shrnutí: Co je nového v 4.6.3

* Oprava zabezpečení: Oprávnění k souborům vytvořeným uvnitř ~/.nuget jsou příliš otevřená [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-464"></a>Shrnutí: Co je nového v 4.6.4

* Oprava zabezpečení: Soubory uvnitř NUPKGs mohou mít relativní cestu nad adresářem NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Známé problémy

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s rozhraním .NET Standard 2.0 s rozhraním .NET Framework & NuGet 

.NET Standard & jeho nástroje byly navrženy tak, že projekty zaměřené na rozhraní .NET Framework 4.6.1 mohou využívat balíčky NuGet & projekty zaměřené na standard .NET Standard 2.0 nebo starší. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tohoto scénáře, plán pro jejich řešení a řešení, která můžete nasadit s dnešním stavem nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Hlavní problémy opravené v této verzi

**Opravy výkonu**

* Nezapisujte soubory datových zdrojů, pokud nedojde k žádné změně - [#6491](https://github.com/NuGet/Home/issues/6491)
* Obnovení způsobí další hodnocení MSBuild, když tfm podřízených projektů neodpovídají nadřazenému projektu – [#6311](https://github.com/NuGet/Home/issues/6311)
* Zlepšete perf obnovení noop optimalizací vytváření specifikací závislostí - [#6252](https://github.com/NuGet/Home/issues/6252)

**Chyby**

* Push do místní složky listy nupkg zamčené - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementace modulu Plug-in NuGet: několik problémů - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - Odebrat volání služby dotazu z inicializace MEF v VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)
* Chyba hlášení výjimky pro zrušenou úlohu stahování balíčku - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe nahradí '+' s '%2B' v názvu sestavení - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 nepřejde na správnou stránku nápovědy pro PM UI a Console - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet zapisuje absolutní cesty do souborů projektu za určitých okolností - [#5888](https://github.com/NuGet/Home/issues/5888)
* Oprava regrese 4.3 - Zástupné symboly $product$ a $AssemblyGuid$ nejsou nahrazeny v contentfile prostřednictvím transformace - [#5880](https://github.com/NuGet/Home/issues/5880)
* dotnet obnovení s více zdrojů pády - [#5817](https://github.com/NuGet/Home/issues/5817)
* Pack by měl přehodnotit verze projektu, aby umožňoval správu verzí git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Zlepšit těžko pochopit chyby při instalaci nekompatibilní balíček - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard potřebuje možnost instalovat balíčky jako PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* Soubory rekvizit dodaných balíky jsou ignorovány, když je msbuild.exe spuštěn mimo příkazový řádek pro vývojáře – [#4530](https://github.com/NuGet/Home/issues/4530)
* Oprava chybové zprávy při odkazování na standardní knihovnu .NET, která není použitelná pro projekt – [#4423](https://github.com/NuGet/Home/issues/4423)
* dotnet přidat balíček selže pro balíček cílení přenosný profil s malou pokyny - [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet pack - přípona verze chybí v ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Chyby sestavení a selhání VS pomocí šablony .NET Core - [#3973](https://github.com/NuGet/Home/issues/3973)
* Nelze načíst index služby pro zdroj https:* - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe list -allversionne nefunguje - [#3441](https://github.com/NuGet/Home/issues/3441)
* Chybová zpráva o řešení závislosti zavádějící - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe restore nevytváří .props a .targets soubory pro .msbuildproj (regrese v v3.3.0-3.4.4 upgrade) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Zpoždění uživatelského rozhraní při aktualizaci balíčku NuGet s otevřeným souborem XAML - [#2878](https://github.com/NuGet/Home/issues/2878)
* Projekt webového serveru ze služby IIS se nezdaří s neplatnými znaky v cestě - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget přidat zablokuje na CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Obnovení s packagesavemode -nupkg selže pro json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Filtr Správce balíčků není k dispozici ve výstupním okně vs pro příkaz obnovení - [#2704](https://github.com/NuGet/Home/issues/2704)

[Seznam všech problémů opravených v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
