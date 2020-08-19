---
title: NuGet – příkaz help CLI
description: Reference k příkazu nuget.exe Help
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623107"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="8adbe-103">help nebo ?</span><span class="sxs-lookup"><span data-stu-id="8adbe-103">help or ?</span></span> <span data-ttu-id="8adbe-104">– příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8adbe-104">command (NuGet CLI)</span></span>

<span data-ttu-id="8adbe-105">**Platí pro:** všechny &bullet; **podporované verze**: vše</span><span class="sxs-lookup"><span data-stu-id="8adbe-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8adbe-106">Zobrazí obecné informace o nápovědě a nápovědu k určitým příkazům.</span><span class="sxs-lookup"><span data-stu-id="8adbe-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="8adbe-107">Využití</span><span class="sxs-lookup"><span data-stu-id="8adbe-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="8adbe-108">WHERE [příkaz] identifikuje konkrétní příkaz, pro který chcete zobrazit nápovědu.</span><span class="sxs-lookup"><span data-stu-id="8adbe-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="8adbe-109">U některých příkazů Nezapomeňte zadat nejprve *help* , jako je `nuget help install` například, protože v NuGet.org je balíček s názvem "Help". Pokud příkaz přiřadíte, nebudete `nuget install help` mít k příkazu install nápovědu, ale místo toho se nainstaluje balíček s názvem Nápověda.</span><span class="sxs-lookup"><span data-stu-id="8adbe-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="8adbe-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="8adbe-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="8adbe-111">Vytiskne podrobnou nápovědu pro všechny dostupné příkazy. ignoruje se, pokud je zadaný konkrétní příkaz.</span><span class="sxs-lookup"><span data-stu-id="8adbe-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="8adbe-112">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="8adbe-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8adbe-113">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="8adbe-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="8adbe-114">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="8adbe-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8adbe-115">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="8adbe-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="8adbe-116">Při použití s nástrojem tisknout podrobnou podporu ve formátu Markdownu `-All`</span><span class="sxs-lookup"><span data-stu-id="8adbe-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="8adbe-117">V opačném případě ignorována.</span><span class="sxs-lookup"><span data-stu-id="8adbe-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8adbe-118">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="8adbe-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8adbe-119">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="8adbe-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="8adbe-120">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="8adbe-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8adbe-121">Příklady</span><span class="sxs-lookup"><span data-stu-id="8adbe-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
