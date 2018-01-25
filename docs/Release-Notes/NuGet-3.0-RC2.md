---
title: "Poznámky k verzi RC2 NuGet 3.0 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro NuGet 3.0 RC2 včetně známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.0 RC2 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="6d628-104">Poznámky k verzi 3.0 RC2 NuGet</span><span class="sxs-lookup"><span data-stu-id="6d628-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="6d628-105">[Poznámky k verzi RC NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 poznámky k verzi](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="6d628-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="6d628-106">NuGet 3.0 RC2 byl vydán na 3. června 2015 jako o předběžné verzi k dispozici v galerii rozšíření sady Visual Studio 2015 a [webu Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="6d628-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="6d628-107">Tato verze obsahuje několik důležitých oprav chyb a vylepšení výkonu, které jsme popisovač byly důležité k verzi před dokončené verze sady Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6d628-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="6d628-108">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6d628-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="6d628-109">Celkem, jsme uzavřeny 158 problémů v tomto vydání, a můžete zkontrolovat [úplný seznam problémů na Githubu](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="6d628-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="6d628-110">Souhrn nejvyšší vyřešení problémů</span><span class="sxs-lookup"><span data-stu-id="6d628-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="6d628-111">Aktualizace časté sítě volá při aktualizuje okno Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="6d628-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="6d628-112">Odložené scroll při zobrazení změna na instalaci v Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="6d628-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="6d628-113">Volání sítě by měl být spouštěn na vlákna na pozadí</span><span class="sxs-lookup"><span data-stu-id="6d628-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="6d628-114">Přidat zaškrtávací políčko "Nezobrazovat okno náhledu.</span><span class="sxs-lookup"><span data-stu-id="6d628-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="6d628-115">Omezení ke snížení využití procesoru přidané procesů</span><span class="sxs-lookup"><span data-stu-id="6d628-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="6d628-116">Vylepšené zpracování reference knihovny tříd portable</span><span class="sxs-lookup"><span data-stu-id="6d628-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="6d628-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="6d628-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="6d628-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="6d628-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="6d628-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="6d628-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="6d628-120">Služba pro automatické dokončování se malá a velká písmena</span><span class="sxs-lookup"><span data-stu-id="6d628-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="6d628-121">Aktualizace znovu zavést pověření základního ověřování</span><span class="sxs-lookup"><span data-stu-id="6d628-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="6d628-122">Chyba vylepšené protokolování</span><span class="sxs-lookup"><span data-stu-id="6d628-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="6d628-123">Vylepšené prostředí powershell chybové zprávy při volání metody balíčku aktualizace</span><span class="sxs-lookup"><span data-stu-id="6d628-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="6d628-124">Stáhněte si to [aktualizace pro rozšíření NuGet](https://nuget.codeplex.com/releases/view/615507) na webu Codeplex a prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a hlášení pro NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="6d628-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>