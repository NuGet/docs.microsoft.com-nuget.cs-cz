---
title: NuGet CLI – příkaz specifikace
description: Odkaz na příkaz nuget.exe spec
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622561"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="44698-103">Spec – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="44698-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="44698-104">**Platí pro:** vytváření balíčků &bullet; **podporuje verze:** vše</span><span class="sxs-lookup"><span data-stu-id="44698-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="44698-105">Vygeneruje `.nuspec` soubor pro nový balíček.</span><span class="sxs-lookup"><span data-stu-id="44698-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="44698-106">Pokud se spustí ve stejné složce jako soubor projektu ( `.csproj` , `.vbproj` , `.fsproj` ), `spec` vytvoří soubor s tokeny `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="44698-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="44698-107">Další informace najdete v tématu [Vytvoření balíčku](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="44698-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="44698-108">Využití</span><span class="sxs-lookup"><span data-stu-id="44698-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="44698-109">kde `<packageID>` je volitelný identifikátor balíčku, který se uloží do `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="44698-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="44698-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="44698-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="44698-111">Určuje cestu k sestavení, které se má použít pro metadata.</span><span class="sxs-lookup"><span data-stu-id="44698-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="44698-112">Přepíše všechny existující `.nuspec` soubory.</span><span class="sxs-lookup"><span data-stu-id="44698-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="44698-113">*(3.5 +)* Vynutí spuštění nuget.exe s využitím neutrální jazykové verze založené na angličtině.</span><span class="sxs-lookup"><span data-stu-id="44698-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="44698-114">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="44698-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="44698-115">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="44698-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="44698-116">Určuje množství podrobností zobrazených ve výstupu: `normal` (výchozí), `quiet` nebo `detailed` .</span><span class="sxs-lookup"><span data-stu-id="44698-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="44698-117">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="44698-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="44698-118">Příklady</span><span class="sxs-lookup"><span data-stu-id="44698-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
