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
# <a name="nuget-285-release-notes"></a><span data-ttu-id="d8f90-103">Zpráva k vydání verze NuGet 2.8.5</span><span class="sxs-lookup"><span data-stu-id="d8f90-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="d8f90-104">[Poznámky k verzi NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [zpráva k vydání verze NuGet 2.8.6 přílohy](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="d8f90-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="d8f90-105">NuGet 2.8.5 bylo vydáno 30. března 2015.</span><span class="sxs-lookup"><span data-stu-id="d8f90-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="d8f90-106">Je menší aktualizace našich 2.8.3 VSIX s některými cílová opravy.</span><span class="sxs-lookup"><span data-stu-id="d8f90-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="d8f90-107">V této verzi byla přidána podpora pro dialogové okno Správce balíčků NuGet [DNX cílové rozhraní Framework Monikery](https://github.com/aspnet/dnx).</span><span class="sxs-lookup"><span data-stu-id="d8f90-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="d8f90-108">Tyto nové monikery rozhraní framework, které jsou podporovány, patří:</span><span class="sxs-lookup"><span data-stu-id="d8f90-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="d8f90-109">**core50** - A "základní" cílit na moniker rozhraní (TFM), který je kompatibilní s Core CLR.</span><span class="sxs-lookup"><span data-stu-id="d8f90-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="d8f90-110">**dnx452** – A TFM specifické pro založených na DNX aplikací pomocí úplné 4.5.2 verzi rozhraní framework</span><span class="sxs-lookup"><span data-stu-id="d8f90-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="d8f90-111">**dnx46** – A TFM specifické pro založených na DNX aplikace s využitím úplného 4.6 verzi rozhraní framework</span><span class="sxs-lookup"><span data-stu-id="d8f90-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="d8f90-112">**dnxcore50** – A TFM specifické pro založených na DNX aplikace s využitím 5.0 základní verzi rozhraní framework</span><span class="sxs-lookup"><span data-stu-id="d8f90-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="d8f90-113">Jedna chyba byla opravena této mu balíčky pro instalaci do projektů FSharp správně:</span><span class="sxs-lookup"><span data-stu-id="d8f90-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400