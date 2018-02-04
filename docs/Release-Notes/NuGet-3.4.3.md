---
title: "Poznámky k verzi NuGet 3.4.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně NuGet 3.4.3 – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.4.3 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a>Poznámky k verzi NuGet 3.4.3

[Poznámky k verzi NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 poznámky k verzi](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 byla vydána 22. dubna 2016 vyřešit několik problémů, které byly zjištěny v 3.4 a následných vydáních.

Si můžete stáhnout VSIX i nuget.exe [zde](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Vylepšení spolehlivosti Visual Studio. Vyřešili jsme některé problémy v NuGet, která způsobila, že dojde k chybě v sadě Visual Studio.

## <a name="fixes"></a>Opravy

* Opravit některé problémy s ověřením s heslem chráněné privátním nuget informačních kanálů.
* Byl opraven problém týkající se nepodařilo obnovit PCL společnosti z `project.json` s moduly runtime zadán.
* Někteří zákazníci byly spuštěny do občasné chyby při instalaci balíčků. Teď to byl opraven v této verzi.
* Byl opraven problém způsobující selhání obnovení v jazyce C + +/ CLI projekty s `project.json`.
* Některé balíčky (např ModernHttpClient) kde nebude rozbalené správně při použití nuget mono. Teď to byl opraven v této verzi.

Úplný seznam oprav a vylepšení v této verzi najdete seznam problémů [zde](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).