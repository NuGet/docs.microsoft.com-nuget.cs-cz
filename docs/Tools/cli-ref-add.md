---
title: Příkaz Přidat NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro nuget.exe přidat – příkaz
keywords: Přidat odkaz nuget, přidat balíček – příkaz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 48e093cbae2cecb1652e17a9b26920107aa8aef7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="462a5-104">Přidat – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="462a5-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="462a5-105">**Platí pro**: balíček publikování &bullet; **podporované verze**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="462a5-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="462a5-106">Přidá zadaný balíček zdroj balíčku jiným protokolem než HTTP (složka nebo cesta UNC) v hierarchickém rozložení, ve kterém se vytvoří složky pro číslo ID a verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="462a5-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="462a5-107">Příklad:</span><span class="sxs-lookup"><span data-stu-id="462a5-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="462a5-108">Při obnovení nebo aktualizaci na zdroji balíčku, hierarchickém rozložení poskytuje výrazně lepší výkon.</span><span class="sxs-lookup"><span data-stu-id="462a5-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="462a5-109">Všechny soubory v balíčku rozšířit do cílového zdroje balíčku, použít `-Expand` přepínače.</span><span class="sxs-lookup"><span data-stu-id="462a5-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="462a5-110">To obvykle vede k další podsložky zobrazovaných v cílovém umístění, jako například `tools` a `lib`.</span><span class="sxs-lookup"><span data-stu-id="462a5-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="462a5-111">Použití</span><span class="sxs-lookup"><span data-stu-id="462a5-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="462a5-112">kde `<packagePath>` je název cesty k balíčku, který chcete přidat, a `<sourcePath>` určuje zdroji na základě složky balíčku, do které budou přidány balíčku.</span><span class="sxs-lookup"><span data-stu-id="462a5-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="462a5-113">Zdroje protokolu HTTP nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="462a5-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="462a5-114">Možnosti</span><span class="sxs-lookup"><span data-stu-id="462a5-114">Options</span></span>

| <span data-ttu-id="462a5-115">Možnost</span><span class="sxs-lookup"><span data-stu-id="462a5-115">Option</span></span> | <span data-ttu-id="462a5-116">Popis</span><span class="sxs-lookup"><span data-stu-id="462a5-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="462a5-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="462a5-117">ConfigFile</span></span> | <span data-ttu-id="462a5-118">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="462a5-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="462a5-119">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="462a5-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="462a5-120">Rozbalte položku</span><span class="sxs-lookup"><span data-stu-id="462a5-120">Expand</span></span> | <span data-ttu-id="462a5-121">Přidá všechny soubory v balíčku ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="462a5-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="462a5-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="462a5-122">ForceEnglishOutput</span></span> | <span data-ttu-id="462a5-123">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="462a5-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="462a5-124">Nápověda</span><span class="sxs-lookup"><span data-stu-id="462a5-124">Help</span></span> | <span data-ttu-id="462a5-125">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="462a5-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="462a5-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="462a5-126">NonInteractive</span></span> | <span data-ttu-id="462a5-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="462a5-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="462a5-128">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="462a5-128">Verbosity</span></span> | <span data-ttu-id="462a5-129">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="462a5-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="462a5-130">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="462a5-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="462a5-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="462a5-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
