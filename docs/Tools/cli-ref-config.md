---
title: "Příkaz config NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a50295ff-8be9-47d9-a260-822e899334cb
description: "Referenční dokumentace pro příkaz nuget.exe konfigurace"
keywords: "referenční dokumentace týkající se konfigurace nuget, příkazu config"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 12a8b51dd11b9bc3a496e02e869cdeb95e67b9e3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="5d4cf-104">příkaz config (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5d4cf-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="5d4cf-105">**Platí pro:** všechny &bullet; **podporované verze**: všechny</span><span class="sxs-lookup"><span data-stu-id="5d4cf-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="5d4cf-106">Získá nebo nastaví hodnoty konfigurace NuGet.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="5d4cf-107">Další využití, najdete v části [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="5d4cf-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="5d4cf-108">Podrobnosti na povolené názvy klíčů najdete [odkaz na soubor konfigurace NuGet](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="5d4cf-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5d4cf-109">Použití</span><span class="sxs-lookup"><span data-stu-id="5d4cf-109">Usage</span></span>

```
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="5d4cf-110">kde `<name>` a `<value>` zadejte pár klíč hodnota v konfiguraci nastavit.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="5d4cf-111">Podle potřeby můžete zadat libovolný počet párů.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="5d4cf-112">Odebrat hodnotu, zadejte název a `=` přihlášení, ale žádná hodnota.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="5d4cf-113">V NuGet 3.4 + `<value>` můžete použít [proměnné prostředí](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="5d4cf-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="5d4cf-114">Možnosti</span><span class="sxs-lookup"><span data-stu-id="5d4cf-114">Options</span></span>

| <span data-ttu-id="5d4cf-115">Možnost</span><span class="sxs-lookup"><span data-stu-id="5d4cf-115">Option</span></span> | <span data-ttu-id="5d4cf-116">Popis</span><span class="sxs-lookup"><span data-stu-id="5d4cf-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d4cf-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="5d4cf-117">AsPath</span></span> | <span data-ttu-id="5d4cf-118">Vrátí hodnotu konfigurace jako cesta, ignorovat při `-Set` se používá.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="5d4cf-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5d4cf-119">ConfigFile</span></span> | <span data-ttu-id="5d4cf-120">*(2.5 +)*  NuGet konfiguračním souboru chcete upravit.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-120">*(2.5+)* The NuGet configuration file to modify.</span></span> <span data-ttu-id="5d4cf-121">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="5d4cf-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5d4cf-122">ForceEnglishOutput</span></span> | <span data-ttu-id="5d4cf-123">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5d4cf-124">Nápověda</span><span class="sxs-lookup"><span data-stu-id="5d4cf-124">Help</span></span> | <span data-ttu-id="5d4cf-125">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="5d4cf-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="5d4cf-126">NonInteractive</span></span> | <span data-ttu-id="5d4cf-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5d4cf-128">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="5d4cf-128">Verbosity</span></span> | <span data-ttu-id="5d4cf-129">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="5d4cf-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="5d4cf-130">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5d4cf-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="5d4cf-131">Příklady</span><span class="sxs-lookup"><span data-stu-id="5d4cf-131">Examples</span></span>

```
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
