---
title: Poznámky k verzi NuGet 3.4.3
description: Poznámky k verzi pro NuGet 3.4.3, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776470"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="bb741-103">Poznámky k verzi NuGet 3.4.3</span><span class="sxs-lookup"><span data-stu-id="bb741-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="bb741-104">Poznámky k verzi [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Poznámky k verzi NuGet 3.4.4](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="bb741-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="bb741-105">3.4.3 NuGet byl vydán 22. dubna 2016, který řeší několik problémů zjištěných v 3,4 a dalších verzích.</span><span class="sxs-lookup"><span data-stu-id="bb741-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="bb741-106">VSIX i nuget.exe si můžete stáhnout [tady](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="bb741-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="bb741-107">Aktualizace a vylepšení</span><span class="sxs-lookup"><span data-stu-id="bb741-107">Updates and Improvements</span></span>

* <span data-ttu-id="bb741-108">Vylepšená spolehlivost sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb741-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="bb741-109">Opravili jsme některé problémy v NuGet, které způsobily zhroucení v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb741-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="bb741-110">Opravy</span><span class="sxs-lookup"><span data-stu-id="bb741-110">Fixes</span></span>

* <span data-ttu-id="bb741-111">Opravili jsme některé problémy s autorizací s privátními kanály NuGet chráněných heslem.</span><span class="sxs-lookup"><span data-stu-id="bb741-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="bb741-112">Opravili jsme problém s tím, že nemůžete obnovit z `project.json` určených modulů runtime modul PCL.</span><span class="sxs-lookup"><span data-stu-id="bb741-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="bb741-113">Někteří zákazníci narazili na občasné chyby při instalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="bb741-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="bb741-114">Tato verze se teď opravila v této verzi.</span><span class="sxs-lookup"><span data-stu-id="bb741-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="bb741-115">Opravili jsme problém, který způsobil selhání obnovení v projektech C++/CLI pomocí `project.json` .</span><span class="sxs-lookup"><span data-stu-id="bb741-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="bb741-116">Některé balíčky (například ModernHttpClient), kde se při použití NuGet v mono neodesílají správně.</span><span class="sxs-lookup"><span data-stu-id="bb741-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="bb741-117">Tato verze se teď opravila v této verzi.</span><span class="sxs-lookup"><span data-stu-id="bb741-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="bb741-118">Úplný seznam oprav a vylepšení v této [verzi najdete v seznamu problémů.](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="bb741-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>