---
title: "Příkaz nabízené NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Referenční dokumentace pro příkaz nabízené nuget.exe"
keywords: "referenční dokumentace nabízené nuget, nabízené příkaz"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="06b7b-104">příkaz nabízené (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="06b7b-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="06b7b-105">**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny; 4.1.0+ požadované pro nuget.org</span><span class="sxs-lookup"><span data-stu-id="06b7b-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="06b7b-106">Pro uložení balíčků do nuget.org je nutné použít nuget.exe v4.1.0 +, která implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="06b7b-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="06b7b-107">Nabízených oznámení balíček ke zdroji balíčku a vydává je.</span><span class="sxs-lookup"><span data-stu-id="06b7b-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="06b7b-108">NuGet výchozí konfiguraci se získávají načtením `%AppData%\NuGet\NuGet.Config`, pak všechny načítání `Nuget.Config` nebo `.nuget\Nuget.Config` soubory z kořenové složky jednotky počáteční a koncovou v aktuálním adresáři (najdete v části [konfigurace chování NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="06b7b-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="06b7b-109">Použití</span><span class="sxs-lookup"><span data-stu-id="06b7b-109">Usage</span></span>

```
nuget push <packagePath> [options]
```

<span data-ttu-id="06b7b-110">kde `<packagePath>` identifikuje balíček k replikaci na server.</span><span class="sxs-lookup"><span data-stu-id="06b7b-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="06b7b-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="06b7b-111">Options</span></span>

| <span data-ttu-id="06b7b-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="06b7b-112">Option</span></span> | <span data-ttu-id="06b7b-113">Popis</span><span class="sxs-lookup"><span data-stu-id="06b7b-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="06b7b-114">apiKey</span><span class="sxs-lookup"><span data-stu-id="06b7b-114">ApiKey</span></span> | <span data-ttu-id="06b7b-115">Klíč rozhraní API pro cílové úložiště.</span><span class="sxs-lookup"><span data-stu-id="06b7b-115">The API key for the target repository.</span></span> <span data-ttu-id="06b7b-116">Pokud není přítomný, ten zadat *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="06b7b-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="06b7b-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="06b7b-117">ConfigFile</span></span> | <span data-ttu-id="06b7b-118">*(2.5 +)*  NuGet konfiguračním souboru použít.</span><span class="sxs-lookup"><span data-stu-id="06b7b-118">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="06b7b-119">Pokud není zadaný, *%AppData%\NuGet\NuGet.Config* se používá.</span><span class="sxs-lookup"><span data-stu-id="06b7b-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="06b7b-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="06b7b-120">DisableBuffering</span></span> | <span data-ttu-id="06b7b-121">Zakáže ukládání do vyrovnávací paměti při nabízení do serveru http (s), aby se snížila paměti.</span><span class="sxs-lookup"><span data-stu-id="06b7b-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="06b7b-122">Upozornění: Pokud tato možnost se používá, nemusí fungovat integrované ověřování systému Windows.</span><span class="sxs-lookup"><span data-stu-id="06b7b-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="06b7b-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="06b7b-123">ForceEnglishOutput</span></span> | <span data-ttu-id="06b7b-124">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="06b7b-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="06b7b-125">Nápověda</span><span class="sxs-lookup"><span data-stu-id="06b7b-125">Help</span></span> | <span data-ttu-id="06b7b-126">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="06b7b-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="06b7b-127">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="06b7b-127">NonInteractive</span></span> | <span data-ttu-id="06b7b-128">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="06b7b-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="06b7b-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="06b7b-129">NoSymbols</span></span> | <span data-ttu-id="06b7b-130">*(3.5 +)*  Pokud balíčku symbolů existuje, nebude instaluje na server symbol.</span><span class="sxs-lookup"><span data-stu-id="06b7b-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="06b7b-131">Zdroj</span><span class="sxs-lookup"><span data-stu-id="06b7b-131">Source</span></span> | <span data-ttu-id="06b7b-132">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="06b7b-132">Specifies the server URL.</span></span> <span data-ttu-id="06b7b-133">U balíčku NuGet 2.5 + bude NuGet identifikovat UNC nebo místní složky zdroje a jednoduše zkopírovat soubor existuje místo vkládání pomocí protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="06b7b-133">With NuGet 2.5+, NuGet will identify a UNC or local folder source and simply copy the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="06b7b-134">Od verze NuGet 3.4.2, to je taky povinný parametr. Pokud `NuGet.Config` Určuje soubor *DefaultPushSource* hodnotu (najdete v části [konfigurace NuGet chování](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="06b7b-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md)).</span></span> |
| <span data-ttu-id="06b7b-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="06b7b-135">SymbolSource</span></span> | <span data-ttu-id="06b7b-136">*(3.5 +)*  Určuje adresu URL serveru symbol; nuget.smbsrc.net se používá při nabízení do nuget.org</span><span class="sxs-lookup"><span data-stu-id="06b7b-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="06b7b-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="06b7b-137">SymbolApiKey</span></span> | <span data-ttu-id="06b7b-138">*(3.5 +)*  Určuje klíč rozhraní API pro zadat adresu URL v `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="06b7b-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="06b7b-139">Časový limit</span><span class="sxs-lookup"><span data-stu-id="06b7b-139">Timeout</span></span> | <span data-ttu-id="06b7b-140">Určuje časový limit v sekundách pro vkládání na server.</span><span class="sxs-lookup"><span data-stu-id="06b7b-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="06b7b-141">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="06b7b-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="06b7b-142">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="06b7b-142">Verbosity</span></span> | <span data-ttu-id="06b7b-143">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné (2.5 +)*.</span><span class="sxs-lookup"><span data-stu-id="06b7b-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="06b7b-144">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="06b7b-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="06b7b-145">Příklady</span><span class="sxs-lookup"><span data-stu-id="06b7b-145">Examples</span></span>

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
