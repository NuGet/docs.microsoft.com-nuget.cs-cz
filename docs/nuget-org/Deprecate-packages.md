---
title: Zastaralé balíčky na nuget.org
description: Podrobný popis procesu zastaralých balíčků a způsobu, jakým klienti tyto informace zobrazují
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096887"
---
# <a name="deprecating-packages"></a>Zastaralé balíčky

Pokud už balíček neuchováváte, nebo pokud chcete, aby se příjemci balíčku mohli přesunout na jiný balíček, můžete ho zařadit do zastaralého. 

Vyřazení balíčku se **liší od** odbalení balíčku, jak je vysvětleno níže:
* Odhlášení balíčku brání jeho zjištění, protože je ve výsledcích hledání skryté. 
* Když zařadíte **balíček,** umožníte stávajícím příjemcům balíčku zjistit, jestli mají nainstalované nebo používané ve svých projektech. Také jim umožňuje zjistit důvod vyřazení a alternativní doporučený balíček, který jste určili (Vydavatel balíčku). Zastaralost balíčku neodstraní balíček. 

Jako vydavatel se můžete rozhodnout, jak odpisovat, tak i jako zastaralé balíčky.

## <a name="deprecation-workflow"></a>Pracovní postup vyřazení
1. Pokud chcete balíček zařadit **, klikněte**na **Spravovat balíčky** a vyberte vyřazení:

    ![Možnost přejít na nepoužívaného balíčku](media/deprecation-select-option.png)

2. Vyberte verzi, kterou chcete vyřadit jako nevybranou. Pokud chcete vyřadit všechny verze, zvolte možnost **Vybrat všechny verze** .

    ![Vybrat verze balíčku k vyřazení](media/deprecation-select-version.png)

3. Vyberte důvod pro vyřazení. Pokud se balíček již neuchovává, vyberte možnost **starší verze** . Pokud má konkrétní verze kritickou chybu, vyberte možnost **má kritické chyby** . Z jakéhokoli jiného důvodu vyberte **jiný**. Pro vlastníky můžete vždy zadat alternativní doporučený balíček (a verzi) a vlastní zprávu. 

    ![Vyberte důvody alternativního balíčku doporučení a vlastní zpráva.](media/deprecation-save.png)

> [!Note]
> Vlastní zpráva se zobrazuje jenom na nuget.org, ale ne z klientů. V současné době klienti, jako je `dotnet.exe` a správce balíčků NuGet, nezobrazují vlastní zprávu.

## <a name="client-experience-for-deprecated-packages"></a>Prostředí klienta pro zastaralé balíčky
Jakmile je balíček zastaralý, jeho příjemci se o tom dozví v následujících způsobech (v závislosti na použitém klientovi).

### <a name="visual-studio"></a>Visual Studio 
*K dispozici počínaje verzí Visual Studio 2019 16,3*

Sada Visual Studio upozorňuje na použití zastaralého balíčku na kartě `Installed`. Zobrazí se upozornění pro balíček a informace o jeho zastaralosti (včetně důvodu, že byl zastaralý a místo toho alternativního balíčku, pokud je k dispozici).

   ![Zastaralé balíčky na kartě nainstalované sady Visual Studio Správce balíčků](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet. exe
*K dispozici od .NET SDK 3,0*

Pokud používáte dotnet. exe, můžete spustit příkaz `dotnet list package --deprecated` ve složce řešení nebo projektu a získat tak seznam zastaralých balíčků spolu s informacemi o vyřazení:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
