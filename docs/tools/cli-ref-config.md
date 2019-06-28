---
title: Rozhraní příkazového řádku NuGet config
description: Referenční informace pro příkaz config nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426073"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="b1775-103">příkaz config (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="b1775-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="b1775-104">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="b1775-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="b1775-105">Získá nebo nastaví NuGet konfigurační hodnoty.</span><span class="sxs-lookup"><span data-stu-id="b1775-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="b1775-106">Další využití, naleznete v tématu [konfigurace běžných NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b1775-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="b1775-107">Podrobnosti o povolené názvy klíčů najdete [odkaz na soubor NuGet config](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="b1775-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="b1775-108">Použití</span><span class="sxs-lookup"><span data-stu-id="b1775-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="b1775-109">kde `<name>` a `<value>` zadejte pár klíč hodnota v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="b1775-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="b1775-110">Podle potřeby můžete zadat libovolný počet párů.</span><span class="sxs-lookup"><span data-stu-id="b1775-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="b1775-111">Pokud chcete odebrat hodnotu, zadejte název a `=` přihlašování, ale žádná hodnota.</span><span class="sxs-lookup"><span data-stu-id="b1775-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="b1775-112">Povolené názvy klíčů, najdete v článku [odkaz na soubor NuGet config](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="b1775-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="b1775-113">Ve Správci NuGet 3.4 + `<value>` můžete použít [proměnné prostředí](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b1775-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="b1775-114">Možnosti</span><span class="sxs-lookup"><span data-stu-id="b1775-114">Options</span></span>

| <span data-ttu-id="b1775-115">Možnost</span><span class="sxs-lookup"><span data-stu-id="b1775-115">Option</span></span> | <span data-ttu-id="b1775-116">Popis</span><span class="sxs-lookup"><span data-stu-id="b1775-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1775-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="b1775-117">AsPath</span></span> | <span data-ttu-id="b1775-118">Vrátí hodnotu konfigurace jako cestu, ignoruje při `-Set` se používá.</span><span class="sxs-lookup"><span data-stu-id="b1775-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="b1775-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b1775-119">ConfigFile</span></span> | <span data-ttu-id="b1775-120">Konfigurační soubor NuGet upravit.</span><span class="sxs-lookup"><span data-stu-id="b1775-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="b1775-121">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="b1775-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b1775-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b1775-122">ForceEnglishOutput</span></span> | <span data-ttu-id="b1775-123">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="b1775-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b1775-124">Help</span><span class="sxs-lookup"><span data-stu-id="b1775-124">Help</span></span> | <span data-ttu-id="b1775-125">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="b1775-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="b1775-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b1775-126">NonInteractive</span></span> | <span data-ttu-id="b1775-127">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="b1775-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b1775-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b1775-128">Verbosity</span></span> | <span data-ttu-id="b1775-129">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="b1775-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b1775-130">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b1775-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="b1775-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="b1775-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
