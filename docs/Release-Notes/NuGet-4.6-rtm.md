---
title: Poznámky k verzi RTM NuGet 4.6 | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Poznámky k verzi pro včetně NuGet 4.6.0 – známé problémy, opravy chyb, přidaných funkcí a chcete.
keywords: NuGet 4.6.0 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 004ad16018443292840b00fa88aa78350e371414
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-46-rtm-release-notes"></a>Poznámky k verzi 4.6 RTM NuGet

[Visual Studio 2017 15,6 operací RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) se dodává s [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).

## <a name="summary-whats-new-in-this-release"></a>Souhrn: Novinky v této verzi
* Jsme doplnili podporu pro [podepisování balíčků](https://docs.microsoft.com/en-us/nuget/create-packages/sign-a-package).  
* Visual Studio 2017 a nuget.exe nyní ověří integritu balíčků před instalací, Probíhá obnovení balíčků pro [podepsané balíčky](https://docs.microsoft.com/en-us/nuget/reference/signed-packages-reference).
* Jsme vylepšili výkon následných obnovení.

## <a name="known-issues"></a>Známé problémy
### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problémy s .NET standardní 2.0 pomocí rozhraní .NET Framework & NuGet 

.NET standard & jeho nástrojů je navržené tak, aby projektech zacílených na rozhraní .NET Framework 4.6.1 může využívat balíčky NuGet & projektech zacílených na standardní rozhraní .NET 2.0 nebo dřívější. [Tento dokument](https://github.com/dotnet/standard/issues/481) shrnuje problémy kolem tento scénář, plán pro adresování a alternativní řešení můžete nasadit s je aktuální stav nástrojů.

## <a name="top-issues-fixed-in-this-release"></a>Horní chyby v této verzi

**Opravy výkonu**
* Nemáte zapisovat soubory asset, pokud se nezměnila - [#6491](https://github.com/NuGet/Home/issues/6491)
* Obnovení způsobuje navíc MSBuild hodnocení při podřízené projekty TFM se neshodují s nadřazenou projektu - [#6311](https://github.com/NuGet/Home/issues/6311)
* Zlepšení výkonu nedojde k žádné akci obnovení pomocí optimalizace závislostí graf specifikace vytvoření - [#6252](https://github.com/NuGet/Home/issues/6252)

**Chyby**
* Nabízená do místní složky opustí nupkg uzamčení - [#6325](https://github.com/NuGet/Home/issues/6325)
* Implementace NuGet modulu plug-in: více problémy - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - odebrat dotaz volání služby z inicializace MEF v VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)
* Výjimka pro zpráv o chybách zrušena úloh stažení balíčku - [#6096](https://github.com/NuGet/Home/issues/6096)
* Nahradí NuGet.exe '+' s % 2B v názvu sestavení - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn + F1 nevyžaduje na stránku správnou nápovědu pro PM uživatelského rozhraní a konzoly - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet zapisuje absolutní cesty do souborů projektu v konkrétních případech - [#5888](https://github.com/NuGet/Home/issues/5888)
* Opravte 4.3 regrese - zástupné symboly $product$ a $ $AssemblyGuid není nahrazena v contentfile prostřednictvím transformace - [#5880](https://github.com/NuGet/Home/issues/5880)
* obnovení DotNet s více zdrojů havárií - [#5817](https://github.com/NuGet/Home/issues/5817)
* Pack by měla znovu vyhodnotit verze projektu umožňující správu verzí git - [#4790](https://github.com/NuGet/Home/issues/4790)
* Zlepšení pevného pochopit chyby při instalaci balíčku nekompatibilní - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard potřebuje k instalaci balíčků jako PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)
* Soubory balíčku doručit props se ignorují spustíte MSBuild.exe v mimo příkazový řádek vývojáře - [#4530](https://github.com/NuGet/Home/issues/4530)
* Opravte nízký chybová zpráva při odkazování na standardní knihovny .NET, které se nevztahuje na projektu - [#4423](https://github.com/NuGet/Home/issues/4423)
* Přidat DotNet selže balíčku pro balíček zaměřená na přenosné profil s malým množstvím pokyny - [#4349](https://github.com/NuGet/Home/issues/4349)
* DotNet pack - verze příponu chybí ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)
* Sestavení chyb a VS havárie se šablonou .NET Core - [#3973](https://github.com/NuGet/Home/issues/3973)
* Nelze načíst index služby pro zdroj https:* - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe seznam - allversions nefunguje - [#3441](https://github.com/NuGet/Home/issues/3441)
* Zavádějící závislostí řešení chybová zpráva - [#2984](https://github.com/NuGet/Home/issues/2984)
* obnovení nuget.exe neobsahuje soubory props a .targets pro .msbuildproj (Regrese v v3.3.0 3.4.4 upgrade) - [#2921](https://github.com/NuGet/Home/issues/2921)
* Zpoždění uživatelského rozhraní při aktualizaci balíčku NuGet s XAML souboru open - [#2878](https://github.com/NuGet/Home/issues/2878)
* Projektu webu ze služby IIS se nezdaří s neplatné znaky v cestě - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget přidat zablokování na CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)
* Obnovení s packagesavemode - nupkg selže technologie json.net - [#2706](https://github.com/NuGet/Home/issues/2706)
* Správce balíčků filtru není k dispozici v sadě vs výstup okna pro příkaz restore - [#2704](https://github.com/NuGet/Home/issues/2704)


[Seznam všechny chyby v této verzi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
