---
title: Poznámky k verzi 3.0 RC2 NuGet
description: Poznámky k verzi pro NuGet 3.0 RC2 včetně známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819881"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="57bc9-103">Poznámky k verzi 3.0 RC2 NuGet</span><span class="sxs-lookup"><span data-stu-id="57bc9-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="57bc9-104">[Poznámky k verzi RC NuGet 3.0](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 poznámky k verzi](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="57bc9-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="57bc9-105">NuGet 3.0 RC2 byl vydán na 3. června 2015 jako o předběžné verzi k dispozici v galerii rozšíření sady Visual Studio 2015 a [webu Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="57bc9-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="57bc9-106">Tato verze obsahuje několik důležitých oprav chyb a vylepšení výkonu, které jsme popisovač byly důležité k verzi před dokončené verze sady Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="57bc9-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="57bc9-107">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="57bc9-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="57bc9-108">Celkem, jsme uzavřeny 158 problémů v tomto vydání, a můžete zkontrolovat [úplný seznam problémů na Githubu](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="57bc9-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="57bc9-109">Souhrn nejvyšší vyřešení problémů</span><span class="sxs-lookup"><span data-stu-id="57bc9-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="57bc9-110">Aktualizace časté sítě volá při aktualizuje okno Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="57bc9-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="57bc9-111">Odložené scroll při zobrazení změna na instalaci v Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="57bc9-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="57bc9-112">Volání sítě by měl být spouštěn na vlákna na pozadí</span><span class="sxs-lookup"><span data-stu-id="57bc9-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="57bc9-113">Přidat zaškrtávací políčko "Nezobrazovat okno náhledu.</span><span class="sxs-lookup"><span data-stu-id="57bc9-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="57bc9-114">Omezení ke snížení využití procesoru přidané procesů</span><span class="sxs-lookup"><span data-stu-id="57bc9-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="57bc9-115">Vylepšené zpracování reference knihovny tříd portable</span><span class="sxs-lookup"><span data-stu-id="57bc9-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="57bc9-116">Služba pro automatické dokončování se malá a velká písmena</span><span class="sxs-lookup"><span data-stu-id="57bc9-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="57bc9-117">Aktualizace znovu zavést pověření základního ověřování</span><span class="sxs-lookup"><span data-stu-id="57bc9-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="57bc9-118">Chyba vylepšené protokolování</span><span class="sxs-lookup"><span data-stu-id="57bc9-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="57bc9-119">Vylepšené prostředí powershell chybové zprávy při volání metody balíčku aktualizace</span><span class="sxs-lookup"><span data-stu-id="57bc9-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="57bc9-120">Stáhněte si to [aktualizace pro rozšíření NuGet](https://nuget.codeplex.com/releases/view/615507) na webu Codeplex a prosím dohlížet na [náš blog](http://blog.nuget.org) další průběh a hlášení pro NuGet 3.0!</span><span class="sxs-lookup"><span data-stu-id="57bc9-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>