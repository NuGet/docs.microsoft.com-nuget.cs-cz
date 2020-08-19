---
title: NuGet CLI – příkaz místních hodnot
description: Reference pro příkaz nuget.exe Locals
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623055"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="ba4ac-103">Locals – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ba4ac-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="ba4ac-104">**Platí pro:** &bullet; **podporované verze balíčku:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="ba4ac-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="ba4ac-105">Vymaže nebo vypíše místní prostředky NuGet, například složku *HTTP-cache*, *Global-Packages* a Temp.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="ba4ac-106">`locals`Příkaz lze také použít k zobrazení seznamu těchto umístění.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="ba4ac-107">Další informace najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ba4ac-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ba4ac-108">Využití</span><span class="sxs-lookup"><span data-stu-id="ba4ac-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="ba4ac-109">kde `<folder>` je jedna z `all` , `http-cache` , `packages-cache` *(3,5 a starší)*, `global-packages` , `temp` *(3.4 +)* a `plugins-cache` *(4.8 +)*.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="ba4ac-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="ba4ac-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="ba4ac-111">Vymaže určenou složku.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ba4ac-112">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="ba4ac-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ba4ac-113">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ba4ac-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ba4ac-114">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ba4ac-115">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="ba4ac-116">Vypíše umístění zadané složky nebo umístění všech složek při použití se *všemi*.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ba4ac-117">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="ba4ac-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ba4ac-118">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ba4ac-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="ba4ac-119">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="ba4ac-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ba4ac-120">Příklady</span><span class="sxs-lookup"><span data-stu-id="ba4ac-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="ba4ac-121">Další příklady najdete v tématu [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ba4ac-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
