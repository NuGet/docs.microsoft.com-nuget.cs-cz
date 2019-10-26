---
title: Sada SDK klienta NuGet
description: Rozhraní API se vyvíjí a ještě není dokumentováno, ale příklady jsou k dispozici na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924608"
---
# <a name="nuget-client-sdk"></a>Sada SDK klienta NuGet

*Sada SDK klienta NuGet* odkazuje na skupinu balíčků NuGet, které se nacentrují do [NuGet. Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.](https://www.nuget.org/packages/NuGet.Packaging)Package a [NuGet. Protocol](https://www.nuget.org/packages/NuGet.Protocol). Tyto balíčky nahrazují předchozí knihovnu [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/) .

> [!Note]
>  Dokumentaci k protokolu serveru NuGet najdete v tématu [rozhraní API serveru NuGet](~/api/overview.md).

## <a name="source-code"></a>Zdrojový kód

Zdrojový kód se zveřejňuje na GitHubu v projektu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Dokumentace třetích stran

Příklady a dokumentaci k některému z rozhraní API najdete v následujících řadách blogu: Dave Glick, Published 2016:

- [Zkoumání knihoven NuGet v3, část 1: Úvod a koncepty](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Zkoumání knihoven NuGet v3, část 2: hledání balíčků](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Zkoumání knihoven NuGet v3, část 3: Instalace balíčků](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Tyto blogové příspěvky byly vypsány krátce po vydání verze **3.4.3** balíčků klientské sady SDK NuGet.
> Novější verze balíčků můžou být nekompatibilní s informacemi v blogových příspěvcích.

Martin Björkström obsahoval následující příspěvek blogu do série blogu Dave Glick, kde zavádí jiný přístup k používání klientské sady SDK NuGet pro instalaci balíčků NuGet:

- [Přenávštěva knihoven NuGet V3](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
