---
title: Poznámky k verzi NuGet 2.8.5
description: Poznámky k verzi pro včetně NuGet 2.8.5 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a>Poznámky k verzi NuGet 2.8.5

[Poznámky k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 přílohy poznámky k verzi](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 byla vydána 30. března 2015. Je to méně závažné aktualizace na našem 2.8.3 VSIX s některými cílí opravy.

V této verzi byla přidána podpora pro dialogové okno Správce balíčků NuGet [DNX cílový Framework Monikery](https://github.com/aspnet/dnx).  Tyto nové monikery framework, které jsou podporovány patří:

* **core50** – "base" cíle Přezdívka framework (TFM), který je kompatibilní s CLR jádra.
* **dnx452** – A TFM konkrétní na základě DNX aplikací pomocí úplné 4.5.2 verzi rozhraní framework
* **dnx46** – A TFM konkrétní na základě DNX aplikací pomocí úplného 4.6 verzi rozhraní framework
* **dnxcore50** – A TFM konkrétní na základě DNX aplikace pomocí verze 5.0 základní rozhraní

Jeden chyba byla opravena této prevented balíčky z instalace do projektů FSharp správně:

https://nuget.codeplex.com/workitem/4400