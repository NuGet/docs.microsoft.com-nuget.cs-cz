---
title: Sada SDK pro klienta NuGet
description: Rozhraní API se rozvíjející a ještě zdokumentovaných, ale příklady jsou k dispozici na blogu Dave Glick.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324679"
---
# <a name="nuget-client-sdk"></a>Sada SDK pro klienta NuGet

> [!Note]
> Neměl by se zaměňovat s [NuGet *webové* rozhraní API](https://docs.microsoft.com/en-us/nuget/api/overview)

*NuGet klientské sady SDK* odkazuje na skupinu soustředí na knihovny .NET [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), a [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). Tyto balíčky nahradit dříve [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) knihovny.

Pracujeme na s stabilní plochy, která může dokumentujeme brzy.

## <a name="source-code"></a>Zdrojový kód

Zdrojový kód se publikoval na Githubu v projektu [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Dokumentace ke službě třetí strany

Příklady a dokumentaci pro některé z rozhraní API najdete v následujících seriálech blogu podle Dave Glick, publikování 2016:

- [Zkoumání v3 knihovny NuGet, část 1: Úvod a koncepty](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Zkoumání v3 knihovny NuGet, část 2: Vyhledávání balíčků](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Zkoumání v3 knihovny NuGet, část 3: Instalace balíčků](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Příspěvky na blogu byly napsány krátce po **3.4.3** verzi Nugetu, byly vydané balíčky sady SDK klienta.
> Novější verze balíčků možná není kompatibilní s informacemi v blogových příspěvků.

Martin Björkström nebyla zpracování blogovém příspěvku k Dave Glick blogovou sérii, kde mu představuje jiný přístup na pomocí klientské sady SDK NuGet pro instalaci balíčků NuGet:

- [Byste nepřešli znovu na v3 knihovny NuGet](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
