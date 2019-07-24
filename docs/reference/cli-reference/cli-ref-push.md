---
title: Příkaz NuGet CLI push
description: Referenční informace o příkazu NuGet. exe push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328291"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="4a48e-103">Push – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4a48e-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="4a48e-104">**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** All; 4.1.0 + Required for NuGet.org</span><span class="sxs-lookup"><span data-stu-id="4a48e-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="4a48e-105">Pokud chcete nabízet balíčky do nuget.org, musíte použít NuGet. exe v 4.1.0 +, který implementuje požadované [protokoly NuGet](../../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="4a48e-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="4a48e-106">Vloží balíček do zdroje balíčku a publikuje ho.</span><span class="sxs-lookup"><span data-stu-id="4a48e-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="4a48e-107">Výchozí konfigurace NuGet se získá načtením `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a následným načtením všech `Nuget.Config` `.nuget\Nuget.Config` souborů, které začínají z kořene jednotky a končí v aktuálním adresáři (viz [Common NuGet Konfigurace](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="4a48e-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="4a48e-108">Použití</span><span class="sxs-lookup"><span data-stu-id="4a48e-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="4a48e-109">kde `<packagePath>` identifikuje balíček, který se má vložit na server.</span><span class="sxs-lookup"><span data-stu-id="4a48e-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="4a48e-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="4a48e-110">Options</span></span>

| <span data-ttu-id="4a48e-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="4a48e-111">Option</span></span> | <span data-ttu-id="4a48e-112">Popis</span><span class="sxs-lookup"><span data-stu-id="4a48e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4a48e-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="4a48e-113">ApiKey</span></span> | <span data-ttu-id="4a48e-114">Klíč rozhraní API pro cílové úložiště</span><span class="sxs-lookup"><span data-stu-id="4a48e-114">The API key for the target repository.</span></span> <span data-ttu-id="4a48e-115">Pokud není k dispozici, použije se ten, který je zadaný v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="4a48e-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="4a48e-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="4a48e-116">ConfigFile</span></span> | <span data-ttu-id="4a48e-117">Konfigurační soubor NuGet, který se má použít</span><span class="sxs-lookup"><span data-stu-id="4a48e-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4a48e-118">Pokud není zadaný, `%AppData%\NuGet\NuGet.Config` použije se (Windows `~/.nuget/NuGet/NuGet.Config` ) nebo (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="4a48e-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="4a48e-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="4a48e-119">DisableBuffering</span></span> | <span data-ttu-id="4a48e-120">Zakáže ukládání do vyrovnávací paměti při odesílání na server HTTP (s), aby se snížilo využití paměti.</span><span class="sxs-lookup"><span data-stu-id="4a48e-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="4a48e-121">Upozornění: při použití této možnosti nemusí fungovat integrované ověřování systému Windows.</span><span class="sxs-lookup"><span data-stu-id="4a48e-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="4a48e-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4a48e-122">ForceEnglishOutput</span></span> | <span data-ttu-id="4a48e-123">*(3.5 +)* Vynutí, aby soubor NuGet. exe běžel pomocí neutrální jazykové verze určené pro angličtinu.</span><span class="sxs-lookup"><span data-stu-id="4a48e-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4a48e-124">Help</span><span class="sxs-lookup"><span data-stu-id="4a48e-124">Help</span></span> | <span data-ttu-id="4a48e-125">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="4a48e-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="4a48e-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4a48e-126">NonInteractive</span></span> | <span data-ttu-id="4a48e-127">Potlačí výzvy pro vstup uživatele nebo potvrzení.</span><span class="sxs-lookup"><span data-stu-id="4a48e-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4a48e-128">Symboly symbolů</span><span class="sxs-lookup"><span data-stu-id="4a48e-128">NoSymbols</span></span> | <span data-ttu-id="4a48e-129">*(3.5 +)* Pokud balíček symbolů existuje, nebude vložen na server symbolů.</span><span class="sxs-lookup"><span data-stu-id="4a48e-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="4a48e-130">Source</span><span class="sxs-lookup"><span data-stu-id="4a48e-130">Source</span></span> | <span data-ttu-id="4a48e-131">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="4a48e-131">Specifies the server URL.</span></span> <span data-ttu-id="4a48e-132">NuGet identifikuje zdroj v konvenci UNC nebo místní složky a jednoduše zkopíruje soubor místo vložení pomocí protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="4a48e-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="4a48e-133">Kromě toho, počínaje NuGet 3.4.2, se jedná o povinný parametr, pokud `NuGet.Config` soubor neurčuje hodnotu *DefaultPushSource* (viz [Konfigurace chování NuGet](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="4a48e-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="4a48e-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="4a48e-134">SkipDuplicate</span></span> | <span data-ttu-id="4a48e-135">*(5.1 +)* Pokud balíček a verze již existují, přeskočte je a pokračujte dalším balíčkem v nabízené kopii, pokud nějaká existuje.</span><span class="sxs-lookup"><span data-stu-id="4a48e-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="4a48e-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="4a48e-136">SymbolSource</span></span> | <span data-ttu-id="4a48e-137">*(3.5 +)* Určuje adresu URL serveru symbolů; nuget.smbsrc.net se používá při vkládání do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4a48e-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="4a48e-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="4a48e-138">SymbolApiKey</span></span> | <span data-ttu-id="4a48e-139">*(3.5 +)* Určuje klíč rozhraní API pro adresu URL určenou v `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="4a48e-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="4a48e-140">časový limit</span><span class="sxs-lookup"><span data-stu-id="4a48e-140">Timeout</span></span> | <span data-ttu-id="4a48e-141">Určuje časový limit pro doručování na server v sekundách.</span><span class="sxs-lookup"><span data-stu-id="4a48e-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="4a48e-142">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="4a48e-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="4a48e-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="4a48e-143">Verbosity</span></span> | <span data-ttu-id="4a48e-144">Určuje množství podrobností zobrazených ve výstupu: *normální*, tiché a *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="4a48e-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4a48e-145">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="4a48e-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4a48e-146">Příklady</span><span class="sxs-lookup"><span data-stu-id="4a48e-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
