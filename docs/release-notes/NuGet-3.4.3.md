---
title: Zpráva k vydání verze NuGet 3.4.3
description: Zpráva k vydání verze pro NuGet 3.4.3 včetně – známé problémy, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549162"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="3da48-103">Zpráva k vydání verze NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="3da48-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="3da48-104">[Zpráva k vydání verze NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [zpráva k vydání verze NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="3da48-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="3da48-105">NuGet 3.4.3 vydané 22. dubna 2016 několik problémů, které jste identifikovali v verze 3.4 a dalších.</span><span class="sxs-lookup"><span data-stu-id="3da48-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="3da48-106">Si můžete stáhnout VSIX i nuget.exe [tady](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="3da48-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3da48-107">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="3da48-107">Updates and Improvements</span></span>

* <span data-ttu-id="3da48-108">Vylepšení spolehlivosti pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3da48-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="3da48-109">Vyřešili jsme některé problémy v NuGet, který způsobil selhání v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3da48-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="3da48-110">Opravy</span><span class="sxs-lookup"><span data-stu-id="3da48-110">Fixes</span></span>

* <span data-ttu-id="3da48-111">Opravili jsme některé problémy s ověřením s heslem privátního nuget informačních kanálů.</span><span class="sxs-lookup"><span data-stu-id="3da48-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="3da48-112">Opravili jsme problém týkající se nepovedlo obnovit PCL společnosti z `project.json` s moduly runtime zadán.</span><span class="sxs-lookup"><span data-stu-id="3da48-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="3da48-113">Zákazníci, kteří spustili do občasné chyby při instalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="3da48-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="3da48-114">Tato chyba byla opravena nyní v této verzi.</span><span class="sxs-lookup"><span data-stu-id="3da48-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="3da48-115">Opravili jsme problém, který způsobil selhání obnovení v jazyce C + +/ CLI projekty s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="3da48-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="3da48-116">Některé balíčky (např. ModernHttpClient) Pokud nebude odblokujte správně při použití nuget mono.</span><span class="sxs-lookup"><span data-stu-id="3da48-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="3da48-117">Tato chyba byla opravena nyní v této verzi.</span><span class="sxs-lookup"><span data-stu-id="3da48-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="3da48-118">Pro úplný seznam oprav chyb a vylepšení v této verzi, projděte si seznam problémů [tady](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="3da48-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>