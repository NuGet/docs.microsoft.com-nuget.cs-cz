---
title: Poznámky k verzi NuGet 3.4.1
description: Poznámky k verzi pro NuGet 3.4.1, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1e234becd2c92ae64fa0f1ac95b358e9a2fb3207
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776487"
---
# <a name="nuget-341-release-notes"></a>Poznámky k verzi NuGet 3.4.1

Zpráva k [vydání verze](../release-notes/nuget-3.4.md)  |  NuGet 3,4 [Poznámky k verzi NuGet 3.4.2](../release-notes/nuget-3.4.2.md)

3.4.1 NuGet byl vydán 30. března 2016 ve stejnou dobu jako vydání sady Visual Studio 2015 Update 2 a Visual Studio 15 Preview, které řeší několik problémů, které byly zjištěny ve verzi 3,4.

## <a name="updates-and-improvements"></a>Aktualizace a vylepšení

* Byl opraven problém, který zabránil procházení balíčků z uživatelského rozhraní sady Visual Studio s minimální instalací sady Visual Studio.
* Byl opraven problém s umístěním sady Visual Studio. `lucene.net.dll`
* Po instalaci nebo aktualizaci rozšíření NuGet by se všechny zdroje neměly považovat za výchozí zdroj úložiště.  K této funkci se můžete rozhodnout z nastavení konfigurace.

Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)