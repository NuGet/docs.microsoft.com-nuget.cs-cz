---
title: Specifikace příkaz NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz specifikace nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68d661030ce7bcff7d7a3a1c96c07e149ad4ffea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="11cd1-103">Specifikace příkazu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="11cd1-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="11cd1-104">**Platí pro:** balíček vytvoření &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="11cd1-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="11cd1-105">Generuje `.nuspec` soubor pro nový balíček.</span><span class="sxs-lookup"><span data-stu-id="11cd1-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="11cd1-106">Pokud ve stejné složce jako soubor projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` vytvoří tokenizovaná `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="11cd1-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="11cd1-107">Další informace najdete v tématu [vytváření balíčku](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="11cd1-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="11cd1-108">Použití</span><span class="sxs-lookup"><span data-stu-id="11cd1-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="11cd1-109">kde `<packageID>` je identifikátor volitelné balíček uložit v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="11cd1-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="11cd1-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="11cd1-110">Options</span></span>

| <span data-ttu-id="11cd1-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="11cd1-111">Option</span></span> | <span data-ttu-id="11cd1-112">Popis</span><span class="sxs-lookup"><span data-stu-id="11cd1-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="11cd1-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="11cd1-113">AssemblyPath</span></span> | <span data-ttu-id="11cd1-114">Určuje cestu k sestavení, které má používat pro metadata.</span><span class="sxs-lookup"><span data-stu-id="11cd1-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="11cd1-115">Platnost</span><span class="sxs-lookup"><span data-stu-id="11cd1-115">Force</span></span> | <span data-ttu-id="11cd1-116">Přepíše všechny existující `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="11cd1-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="11cd1-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="11cd1-117">ForceEnglishOutput</span></span> | <span data-ttu-id="11cd1-118">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="11cd1-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="11cd1-119">Nápověda</span><span class="sxs-lookup"><span data-stu-id="11cd1-119">Help</span></span> | <span data-ttu-id="11cd1-120">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="11cd1-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="11cd1-121">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="11cd1-121">NonInteractive</span></span> | <span data-ttu-id="11cd1-122">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="11cd1-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="11cd1-123">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="11cd1-123">Verbosity</span></span> | <span data-ttu-id="11cd1-124">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="11cd1-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="11cd1-125">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="11cd1-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="11cd1-126">Příklady</span><span class="sxs-lookup"><span data-stu-id="11cd1-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
