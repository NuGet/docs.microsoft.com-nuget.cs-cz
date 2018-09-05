---
title: Rozhraní příkazového řádku NuGet přidat – příkaz
description: Příkaz Přidat odkaz nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545831"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="0bce6-103">Příkaz add (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0bce6-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="0bce6-104">**Platí pro**: balíček publikování &bullet; **podporované verze**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="0bce6-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="0bce6-105">Přidá zadaný balíček ke zdroji balíčku jiným protokolem než HTTP (složka nebo cesta UNC) v hierarchickém rozložení, ve které jsou vytvořeny složky pro číslo ID a verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="0bce6-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="0bce6-106">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0bce6-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="0bce6-107">Při obnovení nebo aktualizaci na zdroji balíčku, hierarchickém rozložení poskytuje výrazně vyšší výkon.</span><span class="sxs-lookup"><span data-stu-id="0bce6-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="0bce6-108">Chcete-li rozbalit všechny soubory v balíčku pro cílový zdroj balíčků, použijte `-Expand` přepnout.</span><span class="sxs-lookup"><span data-stu-id="0bce6-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="0bce6-109">To obvykle za následek další podsložky, které jsou uvedené v cíli, jako například `tools` a `lib`.</span><span class="sxs-lookup"><span data-stu-id="0bce6-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="0bce6-110">Použití</span><span class="sxs-lookup"><span data-stu-id="0bce6-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="0bce6-111">kde `<packagePath>` je cesta k balíčku, který chcete přidat, a `<sourcePath>` Určuje zdroj balíčků založená na složku, do kterého se přidá balíček.</span><span class="sxs-lookup"><span data-stu-id="0bce6-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="0bce6-112">Zdroje HTTP nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="0bce6-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="0bce6-113">Možnosti</span><span class="sxs-lookup"><span data-stu-id="0bce6-113">Options</span></span>

| <span data-ttu-id="0bce6-114">Možnost</span><span class="sxs-lookup"><span data-stu-id="0bce6-114">Option</span></span> | <span data-ttu-id="0bce6-115">Popis</span><span class="sxs-lookup"><span data-stu-id="0bce6-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0bce6-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0bce6-116">ConfigFile</span></span> | <span data-ttu-id="0bce6-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="0bce6-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0bce6-118">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="0bce6-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0bce6-119">Rozbalte položku</span><span class="sxs-lookup"><span data-stu-id="0bce6-119">Expand</span></span> | <span data-ttu-id="0bce6-120">Přidá všechny soubory v balíčku ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="0bce6-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="0bce6-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0bce6-121">ForceEnglishOutput</span></span> | <span data-ttu-id="0bce6-122">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="0bce6-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0bce6-123">Nápověda</span><span class="sxs-lookup"><span data-stu-id="0bce6-123">Help</span></span> | <span data-ttu-id="0bce6-124">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="0bce6-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="0bce6-125">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="0bce6-125">NonInteractive</span></span> | <span data-ttu-id="0bce6-126">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="0bce6-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0bce6-127">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="0bce6-127">Verbosity</span></span> | <span data-ttu-id="0bce6-128">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="0bce6-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0bce6-129">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0bce6-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0bce6-130">Příklady</span><span class="sxs-lookup"><span data-stu-id="0bce6-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
