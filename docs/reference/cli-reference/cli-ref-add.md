---
title: NuGet CLI – příkaz Add
description: Referenční informace o příkazu nuget.exe Add
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776095"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="42b88-103">Add – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="42b88-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="42b88-104">**Platí pro**: publikování &bullet; **podporovaných verzí** balíčku: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="42b88-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="42b88-105">Přidá zadaný balíček do zdroje nepřipojeného balíčku protokolu HTTP (složka nebo cesta UNC) v hierarchickém rozložení, kde jsou vytvářeny složky pro ID a číslo verze balíčku.</span><span class="sxs-lookup"><span data-stu-id="42b88-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="42b88-106">Například:</span><span class="sxs-lookup"><span data-stu-id="42b88-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="42b88-107">Při obnovení nebo aktualizaci zdroje balíčku poskytuje hierarchické rozložení významně lepší výkon.</span><span class="sxs-lookup"><span data-stu-id="42b88-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="42b88-108">K rozbalení všech souborů v balíčku do cílového zdroje balíčků použijte `-Expand` přepínač.</span><span class="sxs-lookup"><span data-stu-id="42b88-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="42b88-109">To obvykle vede k tomu, že se v cíli objeví další podsložky, například `tools` a `lib` .</span><span class="sxs-lookup"><span data-stu-id="42b88-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="42b88-110">Využití</span><span class="sxs-lookup"><span data-stu-id="42b88-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="42b88-111">kde `<packagePath>` je cesta k balíčku, který se má přidat, a `<sourcePath>` Určuje zdroj balíčku na bázi složky, do kterého se balíček přidá.</span><span class="sxs-lookup"><span data-stu-id="42b88-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="42b88-112">Zdroje HTTP nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="42b88-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="42b88-113">Možnosti</span><span class="sxs-lookup"><span data-stu-id="42b88-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="42b88-114">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="42b88-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="42b88-115">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="42b88-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="42b88-116">Přidá všechny soubory v balíčku do zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="42b88-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="42b88-117">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="42b88-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="42b88-118">Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="42b88-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="42b88-119">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="42b88-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="42b88-120">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="42b88-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="42b88-121">Určuje zdroj balíčku, což je složka nebo sdílená složka UNC, do které se nupkg přidá.</span><span class="sxs-lookup"><span data-stu-id="42b88-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="42b88-122">Zdroje http nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="42b88-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="42b88-123">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="42b88-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="42b88-124">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="42b88-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="42b88-125">Příklady</span><span class="sxs-lookup"><span data-stu-id="42b88-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
