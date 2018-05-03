---
title: Příkaz config NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nuget.exe konfigurace
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="7a4d5-103">příkaz config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7a4d5-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="7a4d5-104">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="7a4d5-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="7a4d5-105">Získá nebo nastaví hodnoty konfigurace NuGet.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="7a4d5-106">Další využití, najdete v části [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7a4d5-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="7a4d5-107">Podrobnosti na povolené názvy klíčů najdete [odkaz na soubor konfigurace NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="7a4d5-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7a4d5-108">Použití</span><span class="sxs-lookup"><span data-stu-id="7a4d5-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="7a4d5-109">kde `<name>` a `<value>` zadejte pár klíč hodnota v konfiguraci nastavit.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="7a4d5-110">Podle potřeby můžete zadat libovolný počet párů.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="7a4d5-111">Odebrat hodnotu, zadejte název a `=` přihlášení, ale žádná hodnota.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="7a4d5-112">Povolené názvy klíčů najdete v článku [odkaz na soubor konfigurace NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="7a4d5-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="7a4d5-113">V NuGet 3.4 + `<value>` můžete použít [proměnné prostředí](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="7a4d5-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="7a4d5-114">Možnosti</span><span class="sxs-lookup"><span data-stu-id="7a4d5-114">Options</span></span>

| <span data-ttu-id="7a4d5-115">Možnost</span><span class="sxs-lookup"><span data-stu-id="7a4d5-115">Option</span></span> | <span data-ttu-id="7a4d5-116">Popis</span><span class="sxs-lookup"><span data-stu-id="7a4d5-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a4d5-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="7a4d5-117">AsPath</span></span> | <span data-ttu-id="7a4d5-118">Vrátí hodnotu konfigurace jako cesta, ignorovat při `-Set` se používá.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="7a4d5-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7a4d5-119">ConfigFile</span></span> | <span data-ttu-id="7a4d5-120">Konfigurační soubor NuGet chcete upravit.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="7a4d5-121">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7a4d5-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7a4d5-122">ForceEnglishOutput</span></span> | <span data-ttu-id="7a4d5-123">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7a4d5-124">Nápověda</span><span class="sxs-lookup"><span data-stu-id="7a4d5-124">Help</span></span> | <span data-ttu-id="7a4d5-125">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="7a4d5-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="7a4d5-126">NonInteractive</span></span> | <span data-ttu-id="7a4d5-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7a4d5-128">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="7a4d5-128">Verbosity</span></span> | <span data-ttu-id="7a4d5-129">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="7a4d5-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7a4d5-130">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7a4d5-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="7a4d5-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="7a4d5-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
