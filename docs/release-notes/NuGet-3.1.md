---
title: Zpráva k vydání verze NuGet 3,1
description: Poznámky k verzi pro NuGet 3,1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776535"
---
# <a name="nuget-31-release-notes"></a>Zpráva k vydání verze NuGet 3,1

Zpráva k [vydání verze](../release-notes/nuget-3.0.0.md)  |  NuGet 3,0 [Poznámky k verzi NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

Balíčky NuGet 3,1 byly vydány 27. července 2015 jako rozšíření Univerzální platforma Windows SDK pro sadu Visual Studio 2015. Tuto verzi jsme dodali pomocí sady Windows Platform SDK, aby prostředí pro vývoj systému Windows mohlo využít výhod sady NuGet pro více platforem, kterou jste dříve spustili. Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.

Doporučujeme vývojářům, kteří mají přístup k aktualizaci galerie sady Visual Studio, k nejnovější verzi, která je k dispozici, protože vždy publikujete aktualizace s opravami chyb a novými funkcemi.

## <a name="nuget-visual-studio-extension"></a>Rozšíření sady Visual Studio NuGet

Problémy a funkce v této verzi jsou označené na GitHubu s celkovým [milníkem "3,1 RTM UWP pro přenosnou podporu"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  . v této verzi jsme uzavřeli 67 3,1 problémy.

### <a name="new-features"></a>Nové funkce

* `project.json` Podpora pro Windows UWP a ASP.NET 5
* Instalace přenosného balíčku

Popis a definice těchto funkcí najdete jinde v dokumentaci.

### <a name="deprecated"></a>Zastaralé

Pro Visual Studio 2015 již nejsou k dispozici následující funkce:

* Balíčky na úrovni řešení již nelze instalovat.

Následující funkce již nejsou k dispozici pro Visual Studio 2015 a projekty, které používají `project.json` specifikaci.

* `install.ps1` a `uninstall.ps1` – tyto skripty se během instalace, obnovení, aktualizace a odinstalace balíčku budou ignorovat
* Transformace konfigurace budou ignorovány.
* Obsah se přenese, ale nezkopíruje do projektu.
    * Tým pracuje na opětovné implementaci této funkce, a to po diskuzi a postupu na: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Známé problémy

V této verzi se dodávalo několik známých problémů.

* Instalace verze 3,1 s Windows 10 SDK se bude downgradovat na všechny verze rozšíření NuGet, které se dřív nainstalovaly.

## <a name="nuget-command-line"></a>Příkazový řádek NuGet

Spustitelný soubor příkazového řádku NuGet byl aktualizován a přesunut do nového distribuovatelnýho umístění, aby bylo možné nadále zpřístupnit historické verze nuget.exe.  Verzi 3,1 beta nuget.exe pro Windows si můžete stáhnout v: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Nové Distribuovatelný umístění se nachází na hostiteli dist.nuget.org se strukturou složek, která následuje po této šabloně:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Nové funkce

* nuget.exe může obnovit a nainstalovat balíčky do projektů, které používají `project.json` soubor.
* nuget.exe se může připojit k protokolu NuGet v3 a využívat ho v těchto umístěních: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Známé problémy ##

1.    Nelze provést balíček proti `project.json` souboru – [928](https://github.com/NuGet/Home/issues/928)
2.    Není podporováno v mono- [1059](https://github.com/NuGet/Home/issues/1059)
3.    Není lokalizováno- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    Není podepsáno, stejně jako stávající http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
