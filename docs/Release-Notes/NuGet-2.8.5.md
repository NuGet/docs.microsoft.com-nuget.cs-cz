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
# <a name="nuget-285-release-notes"></a><span data-ttu-id="98e6d-104">Poznámky k verzi NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="98e6d-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="98e6d-105">[Poznámky k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 přílohy poznámky k verzi](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="98e6d-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="98e6d-106">NuGet 2.8.5 byla vydána 30. března 2015.</span><span class="sxs-lookup"><span data-stu-id="98e6d-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="98e6d-107">Je to méně závažné aktualizace na našem 2.8.3 VSIX s některými cílí opravy.</span><span class="sxs-lookup"><span data-stu-id="98e6d-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="98e6d-108">V této verzi byla přidána podpora pro dialogové okno Správce balíčků NuGet [DNX cílový Framework Monikery](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="98e6d-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="98e6d-109">Tyto nové monikery framework, které jsou podporovány patří:</span><span class="sxs-lookup"><span data-stu-id="98e6d-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="98e6d-110">**core50** – "base" cíle Přezdívka framework (TFM), který je kompatibilní s CLR jádra.</span><span class="sxs-lookup"><span data-stu-id="98e6d-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="98e6d-111">**dnx452** – A TFM konkrétní na základě DNX aplikací pomocí úplné 4.5.2 verzi rozhraní framework</span><span class="sxs-lookup"><span data-stu-id="98e6d-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="98e6d-112">**dnx46** – A TFM konkrétní na základě DNX aplikací pomocí úplného 4.6 verzi rozhraní framework</span><span class="sxs-lookup"><span data-stu-id="98e6d-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="98e6d-113">**dnxcore50** – A TFM konkrétní na základě DNX aplikace pomocí verze 5.0 základní rozhraní</span><span class="sxs-lookup"><span data-stu-id="98e6d-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="98e6d-114">Jeden chyba byla opravena této prevented balíčky z instalace do projektů FSharp správně:</span><span class="sxs-lookup"><span data-stu-id="98e6d-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="98e6d-115">https://nuget.CodePlex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="98e6d-115">https://nuget.codeplex.com/workitem/4400</span></span>