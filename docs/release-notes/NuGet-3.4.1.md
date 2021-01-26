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
# <a name="nuget-341-release-notes"></a><span data-ttu-id="74aab-103">Poznámky k verzi NuGet 3.4.1</span><span class="sxs-lookup"><span data-stu-id="74aab-103">NuGet 3.4.1 Release Notes</span></span>

<span data-ttu-id="74aab-104">Zpráva k [vydání verze](../release-notes/nuget-3.4.md)  |  NuGet 3,4 [Poznámky k verzi NuGet 3.4.2](../release-notes/nuget-3.4.2.md)</span><span class="sxs-lookup"><span data-stu-id="74aab-104">[NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md) | [NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md)</span></span>

<span data-ttu-id="74aab-105">3.4.1 NuGet byl vydán 30. března 2016 ve stejnou dobu jako vydání sady Visual Studio 2015 Update 2 a Visual Studio 15 Preview, které řeší několik problémů, které byly zjištěny ve verzi 3,4.</span><span class="sxs-lookup"><span data-stu-id="74aab-105">NuGet 3.4.1 was released March 30, 2016 at the same time as the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release to address several issues that were identified in the 3.4 release.</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="74aab-106">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="74aab-106">Updates and Improvements</span></span>

* <span data-ttu-id="74aab-107">Byl opraven problém, který zabránil procházení balíčků z uživatelského rozhraní sady Visual Studio s minimální instalací sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74aab-107">Corrected an issue that prevented browsing packages from the Visual Studio UI with a minimum Visual Studio install</span></span>
* <span data-ttu-id="74aab-108">Byl opraven problém s umístěním sady Visual Studio. `lucene.net.dll`</span><span class="sxs-lookup"><span data-stu-id="74aab-108">Corrected an issue with Visual Studio locating `lucene.net.dll`</span></span>
* <span data-ttu-id="74aab-109">Po instalaci nebo aktualizaci rozšíření NuGet by se všechny zdroje neměly považovat za výchozí zdroj úložiště.</span><span class="sxs-lookup"><span data-stu-id="74aab-109">All sources should not be the default repository source after a NuGet extension install or update.</span></span>  <span data-ttu-id="74aab-110">K této funkci se můžete rozhodnout z nastavení konfigurace.</span><span class="sxs-lookup"><span data-stu-id="74aab-110">You can opt-in to this feature from the configuration settings.</span></span>

<span data-ttu-id="74aab-111">Pořád sledujeme problémy v našem seznamu problémů GitHubu, které najdete na adrese: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="74aab-111">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>