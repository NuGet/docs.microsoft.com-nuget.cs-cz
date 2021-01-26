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
# <a name="nuget-285-release-notes"></a><span data-ttu-id="4e9a6-103">Poznámky k verzi NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="4e9a6-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="4e9a6-104">Poznámky k verzi [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Poznámky k verzi NuGet 2.8.6](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="4e9a6-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="4e9a6-105">2.8.5 NuGet byl vydán 30. března 2015.</span><span class="sxs-lookup"><span data-stu-id="4e9a6-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="4e9a6-106">Jedná se o menší aktualizaci našeho 2.8.3 VSIX s některými cílenými opravami.</span><span class="sxs-lookup"><span data-stu-id="4e9a6-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="4e9a6-107">V této verzi se přidala podpora pro správce balíčků NuGet pro [monikery cílového rozhraní DNX](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="4e9a6-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="4e9a6-108">Mezi tyto nové monikery rozhraní, které se podporují, patří:</span><span class="sxs-lookup"><span data-stu-id="4e9a6-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="4e9a6-109">**core50** – moniker "Base" Target Framework (TFM), který je kompatibilní s jádrem CLR.</span><span class="sxs-lookup"><span data-stu-id="4e9a6-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="4e9a6-110">**dnx452** – TFM specificky pro aplikace založené na DNX, které používají plnou verzi 4.5.2 rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4e9a6-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="4e9a6-111">**dnx46** – TFM specificky pro aplikace založené na DNX s využitím plné verze 4,6 rozhraní Framework</span><span class="sxs-lookup"><span data-stu-id="4e9a6-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="4e9a6-112">**dnxcore50** – TFM specificky pro aplikace založené na DNX, které používají základní verzi rozhraní 5,0.</span><span class="sxs-lookup"><span data-stu-id="4e9a6-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="4e9a6-113">Byla opravena jedna chyba, která zabránila správné instalaci balíčků do projektů FSharp:</span><span class="sxs-lookup"><span data-stu-id="4e9a6-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400