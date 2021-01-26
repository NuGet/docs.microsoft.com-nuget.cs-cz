---
title: Poznámky k verzi NuGet 3,0 RC2
description: Poznámky k verzi pro NuGet 3,0 RC2 včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780278"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="98083-103">Poznámky k verzi NuGet 3,0 RC2</span><span class="sxs-lookup"><span data-stu-id="98083-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="98083-104">Poznámky k verzi [NuGet 3,0 RC](../release-notes/nuget-3.0-RC.md)  |  Zpráva k [vydání verze NuGet 3,0](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="98083-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="98083-105">NuGet 3,0 RC2 byla vydána 3. června 2015 jako dočasná verze, která je k dispozici v galerii rozšíření sady Visual Studio 2015 a [CodePlex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="98083-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="98083-106">Tato verze obsahuje řadu důležitých oprav chyb a vylepšení výkonu, které jsme zjistili, že byly důležité k vydání před dokončením sady Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="98083-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="98083-107">Tato verze rozšíření NuGet je dostupná jenom pro Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="98083-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="98083-108">V této verzi jsme uzavřeli 158 problémů a můžete si prohlédnout [úplný seznam problémů na GitHubu](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="98083-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="98083-109">Shrnutí nejdůležitějších vyřešených problémů</span><span class="sxs-lookup"><span data-stu-id="98083-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="98083-110">Častá volání síťové aktualizace po aktualizaci okna Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="98083-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="98083-111">Zpožděný posun při změně na nainstalované zobrazení ve Správci balíčků</span><span class="sxs-lookup"><span data-stu-id="98083-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="98083-112">Síťová volání by se měla spustit ve vlákně na pozadí.</span><span class="sxs-lookup"><span data-stu-id="98083-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="98083-113">Přidáno zaškrtávací políčko nezobrazit Náhled okna</span><span class="sxs-lookup"><span data-stu-id="98083-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="98083-114">Přidání omezení procesů pro snížení využití procesoru</span><span class="sxs-lookup"><span data-stu-id="98083-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="98083-115">Vylepšené zpracování odkazů na přenositelné knihovny tříd</span><span class="sxs-lookup"><span data-stu-id="98083-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="98083-116">Služba automatického dokončování rozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="98083-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="98083-117">Aktualizace pro znovu zavedení přihlašovacích údajů základního ověřování</span><span class="sxs-lookup"><span data-stu-id="98083-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="98083-118">Vylepšené protokolování chyb</span><span class="sxs-lookup"><span data-stu-id="98083-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="98083-119">Vylepšené chybové zprávy PowerShellu při volání rutiny Update-Package</span><span class="sxs-lookup"><span data-stu-id="98083-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="98083-120">Stáhněte si tuto [aktualizaci do rozšíření NuGet](https://nuget.codeplex.com/releases/view/615507) z webu CodePlex a podívejte se na [náš blog](http://blog.nuget.org) , abyste mohli další postup a oznámení pro NuGet 3,0!</span><span class="sxs-lookup"><span data-stu-id="98083-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>