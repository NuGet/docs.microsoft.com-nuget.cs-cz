---
title: Poznámky k verzi NuGet 3.4.3
description: Poznámky k verzi pro včetně NuGet 3.4.3 – známé problémy, opravy chyb, přidaných funkcí a chcete.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820323"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="31a7b-103">Poznámky k verzi NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="31a7b-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="31a7b-104">[Poznámky k verzi NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 poznámky k verzi](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="31a7b-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="31a7b-105">NuGet 3.4.3 byla vydána 22. dubna 2016 vyřešit několik problémů, které byly zjištěny v 3.4 a následných vydáních.</span><span class="sxs-lookup"><span data-stu-id="31a7b-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="31a7b-106">Si můžete stáhnout VSIX i nuget.exe [zde](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="31a7b-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="31a7b-107">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="31a7b-107">Updates and Improvements</span></span>

* <span data-ttu-id="31a7b-108">Vylepšení spolehlivosti Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31a7b-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="31a7b-109">Vyřešili jsme některé problémy v NuGet, která způsobila, že dojde k chybě v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="31a7b-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="31a7b-110">Opravy</span><span class="sxs-lookup"><span data-stu-id="31a7b-110">Fixes</span></span>

* <span data-ttu-id="31a7b-111">Opravit některé problémy s ověřením s heslem chráněné privátním nuget informačních kanálů.</span><span class="sxs-lookup"><span data-stu-id="31a7b-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="31a7b-112">Byl opraven problém týkající se nepodařilo obnovit PCL společnosti z `project.json` s moduly runtime zadán.</span><span class="sxs-lookup"><span data-stu-id="31a7b-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="31a7b-113">Někteří zákazníci byly spuštěny do občasné chyby při instalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="31a7b-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="31a7b-114">Teď to byl opraven v této verzi.</span><span class="sxs-lookup"><span data-stu-id="31a7b-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="31a7b-115">Byl opraven problém způsobující selhání obnovení v jazyce C + +/ CLI projekty s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="31a7b-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="31a7b-116">Některé balíčky (např ModernHttpClient) kde nebude rozbalené správně při použití nuget mono.</span><span class="sxs-lookup"><span data-stu-id="31a7b-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="31a7b-117">Teď to byl opraven v této verzi.</span><span class="sxs-lookup"><span data-stu-id="31a7b-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="31a7b-118">Úplný seznam oprav a vylepšení v této verzi najdete seznam problémů [zde](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="31a7b-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>