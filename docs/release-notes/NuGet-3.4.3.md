---
title: Poznámky k verzi NuGet 3.4.3
description: Poznámky k verzi pro včetně NuGet 3.4.3 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820323"
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