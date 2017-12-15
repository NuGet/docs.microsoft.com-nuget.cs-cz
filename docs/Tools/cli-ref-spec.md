---
title: "Specifikace příkaz NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Referenční dokumentace pro příkaz specifikace nuget.exe"
keywords: "Specifikace odkaz nuget, specifikace příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="902e5-104">Specifikace příkazu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="902e5-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="902e5-105">**Platí pro:** balíček vytvoření &bullet; **podporované verze:** všechny</span><span class="sxs-lookup"><span data-stu-id="902e5-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="902e5-106">Generuje `.nuspec` soubor pro nový balíček.</span><span class="sxs-lookup"><span data-stu-id="902e5-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="902e5-107">Pokud ve stejné složce jako soubor projektu (`.csproj`, `.vbproj`, `.fsproj`), `spec` vytvoří tokenizovaná `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="902e5-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="902e5-108">Další informace najdete v tématu [vytváření balíčku](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="902e5-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="902e5-109">Použití</span><span class="sxs-lookup"><span data-stu-id="902e5-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="902e5-110">kde `<packageID>` je identifikátor volitelné balíček uložit v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="902e5-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="902e5-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="902e5-111">Options</span></span>

| <span data-ttu-id="902e5-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="902e5-112">Option</span></span> | <span data-ttu-id="902e5-113">Popis</span><span class="sxs-lookup"><span data-stu-id="902e5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="902e5-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="902e5-114">AssemblyPath</span></span> | <span data-ttu-id="902e5-115">Určuje cestu k sestavení, které má používat pro metadata.</span><span class="sxs-lookup"><span data-stu-id="902e5-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="902e5-116">Platnost</span><span class="sxs-lookup"><span data-stu-id="902e5-116">Force</span></span> | <span data-ttu-id="902e5-117">Přepíše všechny existující `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="902e5-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="902e5-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="902e5-118">ForceEnglishOutput</span></span> | <span data-ttu-id="902e5-119">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="902e5-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="902e5-120">Nápověda</span><span class="sxs-lookup"><span data-stu-id="902e5-120">Help</span></span> | <span data-ttu-id="902e5-121">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="902e5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="902e5-122">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="902e5-122">NonInteractive</span></span> | <span data-ttu-id="902e5-123">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="902e5-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="902e5-124">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="902e5-124">Verbosity</span></span> | <span data-ttu-id="902e5-125">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="902e5-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="902e5-126">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="902e5-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="902e5-127">Příklady</span><span class="sxs-lookup"><span data-stu-id="902e5-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
