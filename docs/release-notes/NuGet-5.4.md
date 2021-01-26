---
title: Zpráva k vydání verze NuGet 5,4
description: Poznámky k verzi pro NuGet 5,4, včetně nových funkcí, oprav chyb a chcete odeslat obecnou.
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: dd4c10672db3a65b68f18636105ee55ab09da7ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776184"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="b5f44-103">Zpráva k vydání verze NuGet 5,4</span><span class="sxs-lookup"><span data-stu-id="b5f44-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="b5f44-104">Prostředky pro distribuci NuGet:</span><span class="sxs-lookup"><span data-stu-id="b5f44-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="b5f44-105">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="b5f44-105">NuGet version</span></span> | <span data-ttu-id="b5f44-106">K dispozici ve verzi sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5f44-106">Available in Visual Studio version</span></span>| <span data-ttu-id="b5f44-107">K dispozici v sadě .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b5f44-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="b5f44-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="b5f44-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="b5f44-109">Visual Studio 2019 verze 16,4</span><span class="sxs-lookup"><span data-stu-id="b5f44-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="b5f44-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b5f44-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="b5f44-111"><sup>1</sup> Nainstalováno se sadou Visual Studio 2019 s úlohou .NET Core</span><span class="sxs-lookup"><span data-stu-id="b5f44-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="b5f44-112">Shrnutí: Novinky v 5,4</span><span class="sxs-lookup"><span data-stu-id="b5f44-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="b5f44-113">Rychlejší načítání řešení – režie při spouštění kódu NuGet během prvního načtení řešení se snížila prostřednictvím částečného Ngen, aby se snížily náklady na JIT [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="b5f44-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="b5f44-114">Nová pomocná funkce – seznam ID a verzí balíčků získáte tak, že získáte pravděpodobná balíčky nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="b5f44-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="b5f44-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="b5f44-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="b5f44-116">Nová [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) akce pro instalaci a konfiguraci NuGet.exe na [akcích GitHubu](https://github.com/features/actions).</span><span class="sxs-lookup"><span data-stu-id="b5f44-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="b5f44-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="b5f44-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="b5f44-118">Chyby opravené v této verzi</span><span class="sxs-lookup"><span data-stu-id="b5f44-118">Issues fixed in this release</span></span>

<span data-ttu-id="b5f44-119">**Štěnic**</span><span class="sxs-lookup"><span data-stu-id="b5f44-119">**Bugs**</span></span>

* <span data-ttu-id="b5f44-120">Modul plug-in: časová přesnost protokolování je vypnutá v systému Linux/Mac – [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="b5f44-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="b5f44-121">Likvidace modulu plug-in může někdy vyvolat a selhat celou operaci.</span><span class="sxs-lookup"><span data-stu-id="b5f44-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="b5f44-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="b5f44-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="b5f44-123">Zastavit zobrazování duplicitních verzí v seznamu povolených a blokovaných verzí v PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="b5f44-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="b5f44-124">Soubor zámku není správně vygenerován – řazení rozhraní by nemělo mít vliv na obnovení pomocí lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645)</span><span class="sxs-lookup"><span data-stu-id="b5f44-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="b5f44-125">LockFile se nezdařila pro projekty se <RuntimeIdentifiers> sadou v sadě SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="b5f44-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="b5f44-126">Ověřování podpisů teď bude správně odmítat podpisy s časovými razítky, které mají 2 hodnoty pod stejným identifikátorem OID- [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="b5f44-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="b5f44-127">Aktualizace seznamu licencí – [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="b5f44-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="b5f44-128">**Chcete odeslat obecnou**</span><span class="sxs-lookup"><span data-stu-id="b5f44-128">**DCRs**</span></span>

* <span data-ttu-id="b5f44-129">Připojování diagnostických souborů do IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="b5f44-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="b5f44-130">**[Seznam všech problémů opravených v této verzi – 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="b5f44-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
