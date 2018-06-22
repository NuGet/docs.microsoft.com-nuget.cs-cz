---
title: Poznámky k verzi NuGet 3.4.1
description: Poznámky k verzi pro NuGet 3.4.1 včetně – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d492afc59fe2f9237aaf54dca56e09f9148a0dcf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819242"
---
# <a name="nuget-341-release-notes"></a><span data-ttu-id="5fa5f-103">Poznámky k verzi NuGet 3.4.1</span><span class="sxs-lookup"><span data-stu-id="5fa5f-103">NuGet 3.4.1 Release Notes</span></span>

<span data-ttu-id="5fa5f-104">[Poznámky k verzi NuGet 3.4](../release-notes/nuget-3.4.md) | [NuGet 3.4.2 poznámky k verzi](../release-notes/nuget-3.4.2.md)</span><span class="sxs-lookup"><span data-stu-id="5fa5f-104">[NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md) | [NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md)</span></span>

<span data-ttu-id="5fa5f-105">NuGet 3.4.1 byla vydána 30. března 2016 ve stejnou dobu jako Visual Studio 2015 Update 2 a Visual Studio 15 Preview vydání vyřešit několik problémů, které byly zjištěny v 3,4 verzi.</span><span class="sxs-lookup"><span data-stu-id="5fa5f-105">NuGet 3.4.1 was released March 30, 2016 at the same time as the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release to address several issues that were identified in the 3.4 release.</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="5fa5f-106">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="5fa5f-106">Updates and Improvements</span></span>

* <span data-ttu-id="5fa5f-107">Opravené chyby, která zabránila procházení balíčky z rozhraní Visual Studio s minimální instalací sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5fa5f-107">Corrected an issue that prevented browsing packages from the Visual Studio UI with a minimum Visual Studio install</span></span>
* <span data-ttu-id="5fa5f-108">Vyřešen problém s umístěním Visual Studio `lucene.net.dll`</span><span class="sxs-lookup"><span data-stu-id="5fa5f-108">Corrected an issue with Visual Studio locating `lucene.net.dll`</span></span>
* <span data-ttu-id="5fa5f-109">Všechny zdroje nesmí být výchozí zdroj úložiště, po instalaci rozšíření NuGet nebo aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="5fa5f-109">All sources should not be the default repository source after a NuGet extension install or update.</span></span>  <span data-ttu-id="5fa5f-110">Vám může výslovný souhlas k této funkci z nastavení konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5fa5f-110">You can opt-in to this feature from the configuration settings.</span></span>

<span data-ttu-id="5fa5f-111">Abychom mohli pokračovat ke sledování problémů na našich seznamu Githubu problémy, které najdete na: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="5fa5f-111">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>