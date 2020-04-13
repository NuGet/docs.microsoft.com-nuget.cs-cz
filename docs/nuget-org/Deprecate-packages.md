---
title: Zastaralé balíčky na nuget.org
description: Podrobný popis procesu zavržení balíků a jak klienti tyto informace zobrazují
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096887"
---
# <a name="deprecating-packages"></a>Zastaralé balíčky

Balíček můžete zamezit, pokud již nespravujete balíček nebo pokud chcete povzbudit spotřebitele balíčku, aby se přesunuli na jiný balíček. 

Vyřazení balíčku se liší od **vyřazení balíčku,** jak je vysvětleno níže:
* **Zrušení výpisu** balíčku zabrání jeho zjišťování, protože je skrytý ve výsledcích hledání. 
* **Zastaralá** balíček umožňuje existující příjemci balíčku zjistit, zda mají nainstalován nebo použit y ve svých projektech. Také jim umožní znát důvod vyřazení a alternativní doporučený balíček, jak jste určili (vydavatel balíčku). Zavržení balíček není zrušit seznam balíček. 

Jako vydavatel se můžete rozhodnout zrušit seznam i zapojit meze balíčků.

## <a name="deprecation-workflow"></a>Pracovní postup vyřazení
1. Chcete-li balíček zařadit, přejděte na **Spravovat balíčky** a vyberte **možnost Vyřazení**:

    ![Přejít na možnost zavržení balíčku](media/deprecation-select-option.png)

2. Vyberte verzi, kterou chcete zapřetat. Pokud chcete zařadit všechny verze, zvolte **Vybrat všechny verze** možnost.

    ![Vyberte verze balíčků, které chcete zakácet.](media/deprecation-select-version.png)

3. Zvolte důvod pro vyřazení. Pokud balíček již není udržován, zvolte možnost **Starší verze.** Pokud konkrétní verze má kritickou chybu, zvolte možnost **má kritické chyby.** Z jakéhokoli jiného důvodu vyberte **možnost Jiné**. Vždy můžete zadat alternativní doporučený balíček (a verzi) a vlastní zprávu vlastníkům. 

    ![Výběr důvodů doporučení alternativního balíčku a vlastní zprávy](media/deprecation-save.png)

> [!Note]
> Vlastní zpráva se zobrazí pouze na nuget.org, ale ne od klientů. V současné době `dotnet.exe` klienti jako a NuGet Správce balíčků nezobrazují vlastní zprávu.

## <a name="client-experience-for-deprecated-packages"></a>Zkušenosti s klientem pro zastaralé balíčky
Jakmile balíček byl zastaralá, jeho spotřebitelé jsou upozorněni na to následujícími způsoby (v závislosti na použitém klientem).

### <a name="visual-studio"></a>Visual Studio 
*K dispozici od visual studia 2019 verze 16.3*

Visual Studio varuje o zastaralé balíček použití `Installed` na kartě. Zobrazí upozornění pro balíček a jeho informace o vyřazení (včetně důvodu, že byl zastarala a alternativní balíček použít místo, pokud je k dispozici).

   ![Zastaralé balíčky na kartě nainstalované aplikací Visual Studio správce balíčků](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*K dispozici počínaje sadou .NET SDK 3.0*

Pokud používáte dotnet.exe, můžete `dotnet list package --deprecated` spustit příkaz na řešení nebo složky projektu získat seznam zastaralé balíčky spolu s informacemi vyřazení:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
