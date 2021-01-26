---
title: Poznámky k verzi NuGet 3.4.3
description: Poznámky k verzi pro NuGet 3.4.3, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776470"
---
# <a name="nuget-343-release-notes"></a>Poznámky k verzi NuGet 3.4.3

Poznámky k verzi [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Poznámky k verzi NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

3.4.3 NuGet byl vydán 22. dubna 2016, který řeší několik problémů zjištěných v 3,4 a dalších verzích.

VSIX i nuget.exe si můžete stáhnout [tady](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Vylepšená spolehlivost sady Visual Studio. Opravili jsme některé problémy v NuGet, které způsobily zhroucení v aplikaci Visual Studio.

## <a name="fixes"></a>Opravy

* Opravili jsme některé problémy s autorizací s privátními kanály NuGet chráněných heslem.
* Opravili jsme problém s tím, že nemůžete obnovit z `project.json` určených modulů runtime modul PCL.
* Někteří zákazníci narazili na občasné chyby při instalaci balíčků. Tato verze se teď opravila v této verzi.
* Opravili jsme problém, který způsobil selhání obnovení v projektech C++/CLI pomocí `project.json` .
* Některé balíčky (například ModernHttpClient), kde se při použití NuGet v mono neodesílají správně. Tato verze se teď opravila v této verzi.

Úplný seznam oprav a vylepšení v této [verzi najdete v seznamu problémů.](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)