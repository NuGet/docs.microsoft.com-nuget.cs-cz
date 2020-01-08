---
title: Zpráva k vydání verze NuGet 5,4
description: Poznámky k verzi pro NuGet 5,4, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384108"
---
# <a name="nuget-54-release-notes"></a>Zpráva k vydání verze NuGet 5,4

Prostředky pro distribuci NuGet:

| Verze NuGet | K dispozici ve verzi sady Visual Studio| K dispozici v sadě .NET SDK|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019 verze 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core

## <a name="summary-whats-new-in-54"></a>Shrnutí: Novinky v 5,4

* Rychlejší načítání řešení – režie při spouštění kódu NuGet během prvního načtení řešení se snížila prostřednictvím částečného Ngen, aby se snížily náklady na JIT [#6007](https://github.com/NuGet/Home/issues/6007)

* Nová pomocná funkce – seznam ID a verzí balíčků získáte tak, že získáte pravděpodobná balíčky nejvyšší úrovně. - [#8316](https://github.com/NuGet/Home/issues/8316)

* Nová akce [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) pro instalaci a konfiguraci NuGet. exe na [akcích GitHubu](https://github.com/features/actions). - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>Chyby opravené v této verzi

**Štěnic**

* Modul plug-in: časová přesnost protokolování je vypnutá v systému Linux/Mac – [#8747](https://github.com/NuGet/Home/issues/8747)

* Likvidace modulu plug-in může někdy vyvolat a selhat celou operaci. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Zastavit zobrazování duplicitních verzí v seznamu povolených a blokovaných verzí v PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)

* Soubor zámku není správně vygenerován – řazení rozhraní by nemělo mít vliv na obnovení pomocí lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)

* LockFile se nezdařila pro projekty se sadou <RuntimeIdentifiers> nastavenou v sadě SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)

* Ověřování podpisů teď bude správně odmítat podpisy s časovými razítky, které mají 2 hodnoty pod stejným identifikátorem OID- [#8629](https://github.com/NuGet/Home/issues/8629)

* Aktualizace seznamu licencí – [#8544](https://github.com/NuGet/Home/issues/8544)

**Chcete odeslat obecnou**

* Připojování diagnostických souborů do IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[Seznam všech problémů opravených v této verzi – 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
