---
title: Zpráva k vydání verze NuGet 3.0 RC2
description: Zpráva k vydání verze NuGet 3.0 RC2 včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545818"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="69f01-103">Zpráva k vydání verze NuGet 3.0 RC2</span><span class="sxs-lookup"><span data-stu-id="69f01-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="69f01-104">[Zpráva k vydání verze NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [zpráva k vydání verze NuGet 3.0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="69f01-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="69f01-105">NuGet 3.0 RC2 3. června 2015 byla vydána jako o předběžné verzi dostupný v galerii rozšíření sady Visual Studio 2015 a [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="69f01-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="69f01-106">Tato verze obsahuje řadu oprav chyb a vylepšení výkonu, které jsme popisovač bylo potřeba verzi před dokončení vydání sady Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="69f01-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="69f01-107">Tato verze rozšíření NuGet dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="69f01-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="69f01-108">Celkem, jsme uzavřeli 158 problémů v této verzi a můžete zkontrolovat [úplný seznam všech problémů na Githubu](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="69f01-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="69f01-109">Přehled hlavních problémů vyřešit</span><span class="sxs-lookup"><span data-stu-id="69f01-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="69f01-110">Sítě časté aktualizace se volá, když se aktualizuje okno Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="69f01-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="69f01-111">Zpožděné posuvníku při změně na instalaci zobrazení ve správci balíčků</span><span class="sxs-lookup"><span data-stu-id="69f01-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="69f01-112">Volání sítě by měl běžet na vlákně na pozadí</span><span class="sxs-lookup"><span data-stu-id="69f01-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="69f01-113">Přidá zaškrtávací políčko "Nezobrazovat okno náhledu.</span><span class="sxs-lookup"><span data-stu-id="69f01-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="69f01-114">Přidání procesu omezování ke snížení využití procesoru</span><span class="sxs-lookup"><span data-stu-id="69f01-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="69f01-115">Vylepšené zpracování odkaz na přenosné knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="69f01-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="69f01-116">Automatické dokončování službě se malá a velká písmena</span><span class="sxs-lookup"><span data-stu-id="69f01-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="69f01-117">Aktualizace znovu zavést pověření základního ověřování</span><span class="sxs-lookup"><span data-stu-id="69f01-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="69f01-118">Vylepšené chybové protokolování</span><span class="sxs-lookup"><span data-stu-id="69f01-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="69f01-119">Vylepšené prostředí powershell chybových zpráv při volání metody Update-Package</span><span class="sxs-lookup"><span data-stu-id="69f01-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="69f01-120">Stáhněte si tuto aplikaci [aktualizovat rozšíření NuGet](https://nuget.codeplex.com/releases/view/615507) na webu Codeplex a prosím dohlížet na [náš blog o](http://blog.nuget.org) další průběh a oznámení pro NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="69f01-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>