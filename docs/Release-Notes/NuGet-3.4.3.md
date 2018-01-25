---
title: "Poznámky k verzi NuGet 3.4.3 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně NuGet 3.4.3 – známé problémy, opravy chyb, přidaných funkcí a chcete."
keywords: "NuGet 3.4.3 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="fdce7-104">Poznámky k verzi NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="fdce7-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="fdce7-105">[Poznámky k verzi NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 poznámky k verzi](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="fdce7-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="fdce7-106">NuGet 3.4.3 byla vydána 22. dubna 2016 vyřešit několik problémů, které byly zjištěny v 3.4 a následných vydáních.</span><span class="sxs-lookup"><span data-stu-id="fdce7-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="fdce7-107">Si můžete stáhnout VSIX i nuget.exe [zde](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="fdce7-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="fdce7-108">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="fdce7-108">Updates and Improvements</span></span>

* <span data-ttu-id="fdce7-109">Vylepšení spolehlivosti Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fdce7-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="fdce7-110">Vyřešili jsme některé problémy v NuGet, která způsobila, že dojde k chybě v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fdce7-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="fdce7-111">Opravy</span><span class="sxs-lookup"><span data-stu-id="fdce7-111">Fixes</span></span>

* <span data-ttu-id="fdce7-112">Opravit některé problémy s ověřením s heslem chráněné privátním nuget informačních kanálů.</span><span class="sxs-lookup"><span data-stu-id="fdce7-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="fdce7-113">Byl opraven problém týkající se nepodařilo obnovit PCL společnosti z `project.json` s moduly runtime zadán.</span><span class="sxs-lookup"><span data-stu-id="fdce7-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="fdce7-114">Někteří zákazníci byly spuštěny do občasné chyby při instalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="fdce7-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="fdce7-115">Teď to byl opraven v této verzi.</span><span class="sxs-lookup"><span data-stu-id="fdce7-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="fdce7-116">Byl opraven problém způsobující selhání obnovení v jazyce C + +/ CLI projekty s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="fdce7-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="fdce7-117">Některé balíčky (např ModernHttpClient) kde nebude rozbalené správně při použití nuget mono.</span><span class="sxs-lookup"><span data-stu-id="fdce7-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="fdce7-118">Teď to byl opraven v této verzi.</span><span class="sxs-lookup"><span data-stu-id="fdce7-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="fdce7-119">Úplný seznam oprav a vylepšení v této verzi najdete seznam problémů [zde](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="fdce7-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>