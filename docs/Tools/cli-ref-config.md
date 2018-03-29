---
title: Příkaz config NuGet rozhraní příkazového řádku | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenční dokumentace pro příkaz nuget.exe konfigurace
keywords: referenční dokumentace týkající se konfigurace nuget, příkazu config
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e3d08f210bd56fcb8eb701fc9b241a3ab45998ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="8cfd9-104">příkaz config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8cfd9-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="8cfd9-105">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="8cfd9-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="8cfd9-106">Získá nebo nastaví hodnoty konfigurace NuGet.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="8cfd9-107">Další využití, najdete v části [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="8cfd9-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="8cfd9-108">Podrobnosti na povolené názvy klíčů najdete [odkaz na soubor konfigurace NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8cfd9-108">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8cfd9-109">Použití</span><span class="sxs-lookup"><span data-stu-id="8cfd9-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="8cfd9-110">kde `<name>` a `<value>` zadejte pár klíč hodnota v konfiguraci nastavit.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="8cfd9-111">Podle potřeby můžete zadat libovolný počet párů.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="8cfd9-112">Odebrat hodnotu, zadejte název a `=` přihlášení, ale žádná hodnota.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="8cfd9-113">Povolené názvy klíčů najdete v článku [odkaz na soubor konfigurace NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="8cfd9-113">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="8cfd9-114">V NuGet 3.4 + `<value>` můžete použít [proměnné prostředí](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="8cfd9-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="8cfd9-115">Možnosti</span><span class="sxs-lookup"><span data-stu-id="8cfd9-115">Options</span></span>

| <span data-ttu-id="8cfd9-116">Možnost</span><span class="sxs-lookup"><span data-stu-id="8cfd9-116">Option</span></span> | <span data-ttu-id="8cfd9-117">Popis</span><span class="sxs-lookup"><span data-stu-id="8cfd9-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8cfd9-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="8cfd9-118">AsPath</span></span> | <span data-ttu-id="8cfd9-119">Vrátí hodnotu konfigurace jako cesta, ignorovat při `-Set` se používá.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="8cfd9-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8cfd9-120">ConfigFile</span></span> | <span data-ttu-id="8cfd9-121">Konfigurační soubor NuGet chcete upravit.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="8cfd9-122">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="8cfd9-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8cfd9-123">ForceEnglishOutput</span></span> | <span data-ttu-id="8cfd9-124">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8cfd9-125">Nápověda</span><span class="sxs-lookup"><span data-stu-id="8cfd9-125">Help</span></span> | <span data-ttu-id="8cfd9-126">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="8cfd9-127">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="8cfd9-127">NonInteractive</span></span> | <span data-ttu-id="8cfd9-128">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8cfd9-129">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="8cfd9-129">Verbosity</span></span> | <span data-ttu-id="8cfd9-130">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="8cfd9-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8cfd9-131">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8cfd9-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="8cfd9-132">Příklady</span><span class="sxs-lookup"><span data-stu-id="8cfd9-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
