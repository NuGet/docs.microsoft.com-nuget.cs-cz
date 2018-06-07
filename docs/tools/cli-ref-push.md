---
title: Příkaz nabízené NuGet rozhraní příkazového řádku
description: Referenční dokumentace pro příkaz nabízené nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817188"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="dcb3f-103">příkaz nabízené (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dcb3f-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="dcb3f-104">**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny; 4.1.0+ požadované pro nuget.org</span><span class="sxs-lookup"><span data-stu-id="dcb3f-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="dcb3f-105">Pro uložení balíčků do nuget.org je nutné použít nuget.exe v4.1.0 +, která implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="dcb3f-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="dcb3f-106">Nabízených oznámení balíček ke zdroji balíčku a vydává je.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="dcb3f-107">NuGet výchozí konfiguraci se získávají načtením `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), pak načítání všechny `Nuget.Config` nebo `.nuget\Nuget.Config` soubory z kořenové složky jednotky počáteční a koncovou v aktuálním adresáři (viz [konfigurace Chování NuGet](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="dcb3f-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="dcb3f-108">Použití</span><span class="sxs-lookup"><span data-stu-id="dcb3f-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="dcb3f-109">kde `<packagePath>` identifikuje balíček k replikaci na server.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="dcb3f-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="dcb3f-110">Options</span></span>

| <span data-ttu-id="dcb3f-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="dcb3f-111">Option</span></span> | <span data-ttu-id="dcb3f-112">Popis</span><span class="sxs-lookup"><span data-stu-id="dcb3f-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dcb3f-113">apiKey</span><span class="sxs-lookup"><span data-stu-id="dcb3f-113">ApiKey</span></span> | <span data-ttu-id="dcb3f-114">Klíč rozhraní API pro cílové úložiště.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-114">The API key for the target repository.</span></span> <span data-ttu-id="dcb3f-115">Pokud není přítomný, použije se verze zadaná v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="dcb3f-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dcb3f-116">ConfigFile</span></span> | <span data-ttu-id="dcb3f-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dcb3f-118">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="dcb3f-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="dcb3f-119">DisableBuffering</span></span> | <span data-ttu-id="dcb3f-120">Zakáže ukládání do vyrovnávací paměti při nabízení do serveru http (s), aby se snížila paměti.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="dcb3f-121">Upozornění: Pokud tato možnost se používá, nemusí fungovat integrované ověřování systému Windows.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="dcb3f-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dcb3f-122">ForceEnglishOutput</span></span> | <span data-ttu-id="dcb3f-123">*(3.5 +)*  Vynutí nuget.exe ke spuštění pomocí invariantní, na základě angličtina jazykové verze.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dcb3f-124">Nápověda</span><span class="sxs-lookup"><span data-stu-id="dcb3f-124">Help</span></span> | <span data-ttu-id="dcb3f-125">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="dcb3f-126">Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="dcb3f-126">NonInteractive</span></span> | <span data-ttu-id="dcb3f-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dcb3f-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="dcb3f-128">NoSymbols</span></span> | <span data-ttu-id="dcb3f-129">*(3.5 +)*  Pokud balíčku symbolů existuje, nebude instaluje na server symbol.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="dcb3f-130">Zdroj</span><span class="sxs-lookup"><span data-stu-id="dcb3f-130">Source</span></span> | <span data-ttu-id="dcb3f-131">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-131">Specifies the server URL.</span></span> <span data-ttu-id="dcb3f-132">NuGet identifikuje UNC nebo místní složky zdroje a jednoduše zkopíruje soubor existuje místo vkládání pomocí protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="dcb3f-133">Od verze NuGet 3.4.2, to je taky povinný parametr. Pokud `NuGet.Config` Určuje soubor *DefaultPushSource* hodnotu (najdete v části [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="dcb3f-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="dcb3f-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="dcb3f-134">SymbolSource</span></span> | <span data-ttu-id="dcb3f-135">*(3.5 +)*  Určuje adresu URL serveru symbol; nuget.smbsrc.net se používá při nabízení do nuget.org</span><span class="sxs-lookup"><span data-stu-id="dcb3f-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="dcb3f-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="dcb3f-136">SymbolApiKey</span></span> | <span data-ttu-id="dcb3f-137">*(3.5 +)*  Určuje klíč rozhraní API pro zadat adresu URL v `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="dcb3f-138">Časový limit</span><span class="sxs-lookup"><span data-stu-id="dcb3f-138">Timeout</span></span> | <span data-ttu-id="dcb3f-139">Určuje časový limit v sekundách pro vkládání na server.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="dcb3f-140">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="dcb3f-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="dcb3f-141">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="dcb3f-141">Verbosity</span></span> | <span data-ttu-id="dcb3f-142">Určuje množství podrobností, které jsou zobrazené ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="dcb3f-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="dcb3f-143">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dcb3f-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dcb3f-144">Příklady</span><span class="sxs-lookup"><span data-stu-id="dcb3f-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
