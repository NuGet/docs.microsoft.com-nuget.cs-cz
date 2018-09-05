---
title: Zpráva k vydání verze NuGet 3.4.3
description: Zpráva k vydání verze pro NuGet 3.4.3 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549162"
---
# <a name="nuget-343-release-notes"></a>Zpráva k vydání verze NuGet 3.4.3

[Zpráva k vydání verze NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [zpráva k vydání verze NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 vydané 22. dubna 2016 několik problémů, které jste identifikovali v verze 3.4 a dalších.

Si můžete stáhnout VSIX i nuget.exe [tady](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Vylepšení spolehlivosti pro Visual Studio. Vyřešili jsme některé problémy v NuGet, který způsobil selhání v sadě Visual Studio.

## <a name="fixes"></a>Opravy

* Opravili jsme některé problémy s ověřením s heslem privátního nuget informačních kanálů.
* Opravili jsme problém týkající se nepovedlo obnovit PCL společnosti z `project.json` s moduly runtime zadán.
* Zákazníci, kteří spustili do občasné chyby při instalaci balíčků. Tato chyba byla opravena nyní v této verzi.
* Opravili jsme problém, který způsobil selhání obnovení v jazyce C + +/ CLI projekty s `project.json`.
* Některé balíčky (např. ModernHttpClient) Pokud nebude odblokujte správně při použití nuget mono. Tato chyba byla opravena nyní v této verzi.

Pro úplný seznam oprav chyb a vylepšení v této verzi, projděte si seznam problémů [tady](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).