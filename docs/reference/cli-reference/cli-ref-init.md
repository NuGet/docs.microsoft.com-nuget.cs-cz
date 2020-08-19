---
title: NuGet – příkaz init CLI
description: Odkaz na příkaz nuget.exe init
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623081"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="6b1f7-103">init – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6b1f7-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="6b1f7-104">**Platí pro:** vytváření balíčků &bullet; **podporuje verze:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="6b1f7-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="6b1f7-105">Zkopíruje všechny balíčky z ploché složky do cílové složky pomocí hierarchického rozložení, jak je popsáno v [příkazu přidat](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="6b1f7-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="6b1f7-106">To znamená, že použití `init` je ekvivalentní s použitím `add` příkazu na každém balíčku ve složce.</span><span class="sxs-lookup"><span data-stu-id="6b1f7-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="6b1f7-107">Stejně jako v nástroji `add` musí být cílem buď místní složka, nebo cesta UNC; Úložiště balíčků HTTP, jako je nuget.org nebo privátní servery, nejsou podporovaná.</span><span class="sxs-lookup"><span data-stu-id="6b1f7-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="6b1f7-108">Využití</span><span class="sxs-lookup"><span data-stu-id="6b1f7-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="6b1f7-109">kde `<source>` je složka obsahující balíčky a `<destination>` je místní složkou nebo cestou UNC, na kterou jsou balíčky zkopírovány.</span><span class="sxs-lookup"><span data-stu-id="6b1f7-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="6b1f7-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="6b1f7-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6b1f7-111">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="6b1f7-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6b1f7-112">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows) nebo `~/.nuget/NuGet/NuGet.Config` nebo `~/.config/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6b1f7-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="6b1f7-113">Přidá všechny soubory v každém balíčku, který je přidán do zdroje balíčku. totéž jako `-Expand` u `add` příkazu.</span><span class="sxs-lookup"><span data-stu-id="6b1f7-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6b1f7-114">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="6b1f7-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6b1f7-115">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="6b1f7-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6b1f7-116">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="6b1f7-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6b1f7-117">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6b1f7-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="6b1f7-118">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="6b1f7-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6b1f7-119">Příklady</span><span class="sxs-lookup"><span data-stu-id="6b1f7-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
