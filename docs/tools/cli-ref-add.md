---
title: Rozhraní příkazového řádku NuGet přidat – příkaz
description: Referenční dokumentace pro nuget.exe přidat – příkaz
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817607"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="3ef6e-103">Příkaz add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3ef6e-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="3ef6e-104">**Platí pro**: balíček publikování &bullet; **podporované verze**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="3ef6e-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="3ef6e-105">Přidá zadaný balíček zdroj balíčku jiným protokolem než HTTP (složka nebo cesta UNC) v hierarchickém rozložení, ve kterém se vytvoří složky pro číslo ID a verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="3ef6e-106">Příklad:</span><span class="sxs-lookup"><span data-stu-id="3ef6e-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="3ef6e-107">Při obnovení nebo aktualizaci na zdroji balíčku, hierarchickém rozložení poskytuje výrazně lepší výkon.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="3ef6e-108">Všechny soubory v balíčku rozšířit do cílového zdroje balíčku, použít `-Expand` přepínače.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="3ef6e-109">To obvykle vede k další podsložky zobrazovaných v cílovém umístění, jako například `tools` a `lib`.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="3ef6e-110">Použití</span><span class="sxs-lookup"><span data-stu-id="3ef6e-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="3ef6e-111">kde `<packagePath>` je název cesty k balíčku, který chcete přidat, a `<sourcePath>` určuje zdroji na základě složky balíčku, do které budou přidány balíčku.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="3ef6e-112">Zdroje protokolu HTTP nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="3ef6e-113">Možnosti</span><span class="sxs-lookup"><span data-stu-id="3ef6e-113">Options</span></span>

| <span data-ttu-id="3ef6e-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="3ef6e-114">Option</span></span> | <span data-ttu-id="3ef6e-115">Popis</span><span class="sxs-lookup"><span data-stu-id="3ef6e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ef6e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3ef6e-116">ConfigFile</span></span> | <span data-ttu-id="3ef6e-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3ef6e-118">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3ef6e-119">Rozbalte položku</span><span class="sxs-lookup"><span data-stu-id="3ef6e-119">Expand</span></span> | <span data-ttu-id="3ef6e-120">Přidá všechny soubory v balíčku ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="3ef6e-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3ef6e-121">ForceEnglishOutput</span></span> | <span data-ttu-id="3ef6e-122">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3ef6e-123">Nápověda</span><span class="sxs-lookup"><span data-stu-id="3ef6e-123">Help</span></span> | <span data-ttu-id="3ef6e-124">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="3ef6e-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="3ef6e-125">NonInteractive</span></span> | <span data-ttu-id="3ef6e-126">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3ef6e-127">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="3ef6e-127">Verbosity</span></span> | <span data-ttu-id="3ef6e-128">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="3ef6e-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3ef6e-129">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3ef6e-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3ef6e-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="3ef6e-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
