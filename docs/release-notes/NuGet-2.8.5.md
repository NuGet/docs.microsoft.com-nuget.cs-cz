---
title: Zpráva k vydání verze NuGet 2.8.5
description: Zpráva k vydání verze pro NuGet 2.8.5 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548622"
---
# <a name="nuget-285-release-notes"></a>Zpráva k vydání verze NuGet 2.8.5

[Poznámky k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [zpráva k vydání verze NuGet 2.8.6 přílohy](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 bylo vydáno 30. března 2015. Je menší aktualizace našich 2.8.3 VSIX s některými cílová opravy.

V této verzi byla přidána podpora pro dialogové okno Správce balíčků NuGet [DNX cílové rozhraní Framework Monikery](https://github.com/aspnet/dnx).  Tyto nové monikery rozhraní framework, které jsou podporovány, patří:

* **core50** - A "základní" cílit na moniker rozhraní (TFM), který je kompatibilní s Core CLR.
* **dnx452** – A TFM specifické pro založených na DNX aplikací pomocí úplné 4.5.2 verzi rozhraní framework
* **dnx46** – A TFM specifické pro založených na DNX aplikace s využitím úplného 4.6 verzi rozhraní framework
* **dnxcore50** – A TFM specifické pro založených na DNX aplikace s využitím 5.0 základní verzi rozhraní framework

Jedna chyba byla opravena této mu balíčky pro instalaci do projektů FSharp správně:

https://nuget.codeplex.com/workitem/4400