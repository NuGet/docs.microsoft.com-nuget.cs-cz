---
title: Poznámky k verzi NuGet 2.8.5
description: Poznámky k verzi pro NuGet 2.8.5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780361"
---
# <a name="nuget-285-release-notes"></a>Poznámky k verzi NuGet 2.8.5

Poznámky k verzi [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Poznámky k verzi NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

2.8.5 NuGet byl vydán 30. března 2015. Jedná se o menší aktualizaci našeho 2.8.3 VSIX s některými cílenými opravami.

V této verzi se přidala podpora pro správce balíčků NuGet pro [monikery cílového rozhraní DNX](https://github.com/aspnet/dnx).  Mezi tyto nové monikery rozhraní, které se podporují, patří:

* **core50** – moniker "Base" Target Framework (TFM), který je kompatibilní s jádrem CLR.
* **dnx452** – TFM specificky pro aplikace založené na DNX, které používají plnou verzi 4.5.2 rozhraní .NET Framework
* **dnx46** – TFM specificky pro aplikace založené na DNX s využitím plné verze 4,6 rozhraní Framework
* **dnxcore50** – TFM specificky pro aplikace založené na DNX, které používají základní verzi rozhraní 5,0.

Byla opravena jedna chyba, která zabránila správné instalaci balíčků do projektů FSharp:

https://nuget.codeplex.com/workitem/4400