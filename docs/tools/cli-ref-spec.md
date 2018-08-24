---
title: Specifikace rozhraní příkazového řádku NuGet
description: Referenční informace pro příkaz specifikace nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794148"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="3d80a-103">Specifikace příkazu (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="3d80a-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="3d80a-104">**Platí pro:** vytvoření balíčku &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="3d80a-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3d80a-105">Generuje `.nuspec` soubor pro nový balíček.</span><span class="sxs-lookup"><span data-stu-id="3d80a-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="3d80a-106">Spuštění ve stejné složce jako soubor projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` vytvoří tokenizovaná `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="3d80a-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="3d80a-107">Další informace najdete v tématu [vytvoření balíčku](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="3d80a-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="3d80a-108">Použití</span><span class="sxs-lookup"><span data-stu-id="3d80a-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="3d80a-109">kde `<packageID>` je volitelný balíček identifikátoru Uložit `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="3d80a-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="3d80a-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="3d80a-110">Options</span></span>

| <span data-ttu-id="3d80a-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="3d80a-111">Option</span></span> | <span data-ttu-id="3d80a-112">Popis</span><span class="sxs-lookup"><span data-stu-id="3d80a-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d80a-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="3d80a-113">AssemblyPath</span></span> | <span data-ttu-id="3d80a-114">Určuje cestu k sestavení, které má používat pro metadata.</span><span class="sxs-lookup"><span data-stu-id="3d80a-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="3d80a-115">Platnost</span><span class="sxs-lookup"><span data-stu-id="3d80a-115">Force</span></span> | <span data-ttu-id="3d80a-116">Přepíše všechny existující `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="3d80a-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="3d80a-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3d80a-117">ForceEnglishOutput</span></span> | <span data-ttu-id="3d80a-118">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="3d80a-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3d80a-119">Nápověda</span><span class="sxs-lookup"><span data-stu-id="3d80a-119">Help</span></span> | <span data-ttu-id="3d80a-120">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="3d80a-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="3d80a-121">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="3d80a-121">NonInteractive</span></span> | <span data-ttu-id="3d80a-122">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="3d80a-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3d80a-123">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="3d80a-123">Verbosity</span></span> | <span data-ttu-id="3d80a-124">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="3d80a-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3d80a-125">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3d80a-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3d80a-126">Příklady</span><span class="sxs-lookup"><span data-stu-id="3d80a-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
