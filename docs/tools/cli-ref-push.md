---
title: Rozhraní příkazového řádku NuGet nabízených oznámení
description: Referenční informace pro nuget.exe příkazu push
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b4f73e2b816d8a93e123d6de83ad0a15fbb24d18
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425930"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="70214-103">příkazu push (rozhraní příkazového řádku NuGet)</span><span class="sxs-lookup"><span data-stu-id="70214-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="70214-104">**Platí pro:** balíček publikování &bullet; **podporované verze:** všechny; 4.1.0+ vyžadované pro nuget.org</span><span class="sxs-lookup"><span data-stu-id="70214-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="70214-105">Vložit balíčky nuget.org je nutné použít nuget.exe verze 4.1.0 +, která implementuje požadované [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="70214-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="70214-106">Odešle balíček ke zdroji balíčku a publikuje ji.</span><span class="sxs-lookup"><span data-stu-id="70214-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="70214-107">NuGet výchozí konfigurace se získá načítání `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), pak načítání všechny `Nuget.Config` nebo `.nuget\Nuget.Config` souborů od kořenové jednotky a končící na aktuální adresář (naleznete v tématu [běžné NuGet konfigurace](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="70214-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="70214-108">Použití</span><span class="sxs-lookup"><span data-stu-id="70214-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="70214-109">kde `<packagePath>` identifikuje balíček nainstalovat do serveru.</span><span class="sxs-lookup"><span data-stu-id="70214-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="70214-110">Možnosti</span><span class="sxs-lookup"><span data-stu-id="70214-110">Options</span></span>

| <span data-ttu-id="70214-111">Možnost</span><span class="sxs-lookup"><span data-stu-id="70214-111">Option</span></span> | <span data-ttu-id="70214-112">Popis</span><span class="sxs-lookup"><span data-stu-id="70214-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="70214-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="70214-113">ApiKey</span></span> | <span data-ttu-id="70214-114">Klíč rozhraní API pro cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="70214-114">The API key for the target repository.</span></span> <span data-ttu-id="70214-115">Pokud není k dispozici, použije se verze zadaná v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="70214-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="70214-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="70214-116">ConfigFile</span></span> | <span data-ttu-id="70214-117">Konfigurační soubor NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="70214-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="70214-118">Pokud není zadán, `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) se používá.</span><span class="sxs-lookup"><span data-stu-id="70214-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="70214-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="70214-119">DisableBuffering</span></span> | <span data-ttu-id="70214-120">Zakáže ukládání do vyrovnávací paměti při odesílání na server http (s) ke snížení využití paměti.</span><span class="sxs-lookup"><span data-stu-id="70214-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="70214-121">Upozornění: když tuto možnost použít, nemusí fungovat integrované ověřování Windows.</span><span class="sxs-lookup"><span data-stu-id="70214-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="70214-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="70214-122">ForceEnglishOutput</span></span> | <span data-ttu-id="70214-123">*(3.5 +)*  Vynutí nuget.exe pro spuštění pomocí neutrální, základem je angličtina jazyková verze.</span><span class="sxs-lookup"><span data-stu-id="70214-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="70214-124">Help</span><span class="sxs-lookup"><span data-stu-id="70214-124">Help</span></span> | <span data-ttu-id="70214-125">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="70214-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="70214-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="70214-126">NonInteractive</span></span> | <span data-ttu-id="70214-127">Potlačí vyzve k zadání uživatele o vstup ani potvrzení.</span><span class="sxs-lookup"><span data-stu-id="70214-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="70214-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="70214-128">NoSymbols</span></span> | <span data-ttu-id="70214-129">*(3.5 +)*  Pokud balíček symbolů existuje, neodešle se na server symbolů.</span><span class="sxs-lookup"><span data-stu-id="70214-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="70214-130">Source</span><span class="sxs-lookup"><span data-stu-id="70214-130">Source</span></span> | <span data-ttu-id="70214-131">Určuje adresu URL serveru.</span><span class="sxs-lookup"><span data-stu-id="70214-131">Specifies the server URL.</span></span> <span data-ttu-id="70214-132">Určuje název UNC nebo místní složku zdroje a jednoduše zkopíruje soubor existuje místo doručením (push) pomocí protokolu HTTP NuGet.</span><span class="sxs-lookup"><span data-stu-id="70214-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="70214-133">Také, počínaje NuGet 3.4.2, je to povinný parametr Pokud `NuGet.Config` Určuje soubor *DefaultPushSource* hodnotu (naleznete v tématu [konfigurace NuGet chování](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="70214-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="70214-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="70214-134">SkipDuplicate</span></span> | <span data-ttu-id="70214-135">*(5.1 +)*  Pokud balíček a verzí již existuje, jeho přeskočit a pokračovat další balíček nabízeného oznámení, pokud existuje.</span><span class="sxs-lookup"><span data-stu-id="70214-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="70214-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="70214-136">SymbolSource</span></span> | <span data-ttu-id="70214-137">*(3.5 +)*  Určuje adresu URL serveru symbolů; při odesílání do nuget.org se použije nuget.smbsrc.net</span><span class="sxs-lookup"><span data-stu-id="70214-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="70214-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="70214-138">SymbolApiKey</span></span> | <span data-ttu-id="70214-139">*(3.5 +)*  Určuje klíč rozhraní API pro adresu URL zadané v `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="70214-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="70214-140">časový limit</span><span class="sxs-lookup"><span data-stu-id="70214-140">Timeout</span></span> | <span data-ttu-id="70214-141">Určuje časový limit v sekundách pro odesílání na server.</span><span class="sxs-lookup"><span data-stu-id="70214-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="70214-142">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="70214-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="70214-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="70214-143">Verbosity</span></span> | <span data-ttu-id="70214-144">Určuje množství podrobností, na které se zobrazí ve výstupu: *normální*, *quiet*, *podrobné*.</span><span class="sxs-lookup"><span data-stu-id="70214-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="70214-145">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="70214-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="70214-146">Příklady</span><span class="sxs-lookup"><span data-stu-id="70214-146">Examples</span></span>

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
