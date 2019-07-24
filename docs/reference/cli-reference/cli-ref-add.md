---
title: NuGet CLI – příkaz Add
description: Referenční informace o příkazu NuGet. exe Add
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328360"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="fc712-103">Příkaz add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fc712-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="fc712-104">**Platí pro**: publikování &bullet; **podporovaných verzí**balíčku: 3.3+</span><span class="sxs-lookup"><span data-stu-id="fc712-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="fc712-105">Přidá zadaný balíček do zdroje nepřipojeného balíčku protokolu HTTP (složka nebo cesta UNC) v hierarchickém rozložení, kde jsou vytvářeny složky pro ID a číslo verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="fc712-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="fc712-106">Příklad:</span><span class="sxs-lookup"><span data-stu-id="fc712-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="fc712-107">Při obnovení nebo aktualizaci zdroje balíčku poskytuje hierarchické rozložení významně lepší výkon.</span><span class="sxs-lookup"><span data-stu-id="fc712-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="fc712-108">K rozbalení všech souborů v balíčku do cílového zdroje balíčků použijte `-Expand` přepínač.</span><span class="sxs-lookup"><span data-stu-id="fc712-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="fc712-109">To obvykle vede k tomu, že se v cíli objeví další podsložky `tools` , `lib`například a.</span><span class="sxs-lookup"><span data-stu-id="fc712-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="fc712-110">Použití</span><span class="sxs-lookup"><span data-stu-id="fc712-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="fc712-111">kde `<packagePath>` je cesta k balíčku, který se má přidat, `<sourcePath>` a určuje zdroj balíčku na bázi složky, do kterého se balíček přidá.</span><span class="sxs-lookup"><span data-stu-id="fc712-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="fc712-112">Zdroje HTTP nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="fc712-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="fc712-113">Možnosti</span><span class="sxs-lookup"><span data-stu-id="fc712-113">Options</span></span>

| <span data-ttu-id="fc712-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="fc712-114">Option</span></span> | <span data-ttu-id="fc712-115">Popis</span><span class="sxs-lookup"><span data-stu-id="fc712-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fc712-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fc712-116">ConfigFile</span></span> | <span data-ttu-id="fc712-117">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="fc712-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fc712-118">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fc712-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fc712-119">Expand</span><span class="sxs-lookup"><span data-stu-id="fc712-119">Expand</span></span> | <span data-ttu-id="fc712-120">Přidá všechny soubory v balíčku do zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="fc712-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="fc712-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fc712-121">ForceEnglishOutput</span></span> | <span data-ttu-id="fc712-122">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="fc712-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fc712-123">Help</span><span class="sxs-lookup"><span data-stu-id="fc712-123">Help</span></span> | <span data-ttu-id="fc712-124">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="fc712-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="fc712-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fc712-125">NonInteractive</span></span> | <span data-ttu-id="fc712-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="fc712-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fc712-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="fc712-127">Verbosity</span></span> | <span data-ttu-id="fc712-128">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="fc712-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fc712-129">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="fc712-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fc712-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="fc712-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
