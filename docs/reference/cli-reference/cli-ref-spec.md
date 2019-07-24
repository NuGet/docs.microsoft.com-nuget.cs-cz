---
title: NuGet CLI – příkaz specifikace
description: Referenční informace o příkazu NuGet. exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328273"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="92cf0-103">Spec – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="92cf0-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="92cf0-104">**Platí pro:** vytváření &bullet; balíčků **podporuje verze:** vše</span><span class="sxs-lookup"><span data-stu-id="92cf0-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="92cf0-105">Vygeneruje `.nuspec` soubor pro nový balíček.</span><span class="sxs-lookup"><span data-stu-id="92cf0-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="92cf0-106">Pokud se spustí ve stejné složce jako soubor projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` vytvoří `.nuspec` soubor s tokeny.</span><span class="sxs-lookup"><span data-stu-id="92cf0-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="92cf0-107">Další informace najdete v tématu [Vytvoření balíčku](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="92cf0-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="92cf0-108">Použití</span><span class="sxs-lookup"><span data-stu-id="92cf0-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="92cf0-109">kde `<packageID>` je volitelný identifikátor balíčku, který se uloží `.nuspec` do souboru.</span><span class="sxs-lookup"><span data-stu-id="92cf0-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="92cf0-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="92cf0-110">Options</span></span>

| <span data-ttu-id="92cf0-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="92cf0-111">Option</span></span> | <span data-ttu-id="92cf0-112">Popis</span><span class="sxs-lookup"><span data-stu-id="92cf0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92cf0-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="92cf0-113">AssemblyPath</span></span> | <span data-ttu-id="92cf0-114">Určuje cestu k sestavení, které se má použít pro metadata.</span><span class="sxs-lookup"><span data-stu-id="92cf0-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="92cf0-115">Ode</span><span class="sxs-lookup"><span data-stu-id="92cf0-115">Force</span></span> | <span data-ttu-id="92cf0-116">Přepíše všechny existující `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="92cf0-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="92cf0-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="92cf0-117">ForceEnglishOutput</span></span> | <span data-ttu-id="92cf0-118">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="92cf0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="92cf0-119">Help</span><span class="sxs-lookup"><span data-stu-id="92cf0-119">Help</span></span> | <span data-ttu-id="92cf0-120">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="92cf0-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="92cf0-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="92cf0-121">NonInteractive</span></span> | <span data-ttu-id="92cf0-122">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="92cf0-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="92cf0-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="92cf0-123">Verbosity</span></span> | <span data-ttu-id="92cf0-124">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="92cf0-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="92cf0-125">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="92cf0-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="92cf0-126">Příklady</span><span class="sxs-lookup"><span data-stu-id="92cf0-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
