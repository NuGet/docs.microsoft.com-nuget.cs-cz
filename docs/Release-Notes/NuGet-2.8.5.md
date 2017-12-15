---
title: "Poznámky k verzi NuGet 2.8.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Poznámky k verzi pro včetně NuGet 2.8.5 – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 2.8.5 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
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

https://nuget.CodePlex.com/workitem/4400