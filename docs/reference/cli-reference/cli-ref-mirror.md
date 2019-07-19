---
title: NuGet – příkaz zrcadlení CLI
description: Referenční informace o příkazu NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328303"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="70ba5-103">Příkaz mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="70ba5-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="70ba5-104">**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** zastaralé za 3.2 +</span><span class="sxs-lookup"><span data-stu-id="70ba5-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="70ba5-105">Zrcadlí balíček a jeho závislosti ze zadaných zdrojových úložišť do cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="70ba5-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="70ba5-106">Pokud chcete tento příkaz pro verze NuGet povolit před 3,2, [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)vyberte nejnovější stabilní verzi, Stáhněte si `NuGet.ServerExtensions.dll` a `Nuget-Signed.exe` na místní disk a přejmenujte `Nuget-Signed.exe` na `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="70ba5-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="70ba5-107">Použití</span><span class="sxs-lookup"><span data-stu-id="70ba5-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="70ba5-108">kde `<packageID>` je balíček k zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který vypisuje balíčky pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="70ba5-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="70ba5-109">Určuje zdrojové úložiště a `<publishUrlTarget>` Určuje cílové úložiště. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="70ba5-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="70ba5-110">Pokud vaše cílové úložiště `https://machine/repo` používá službu [NuGet. Server](../../hosting-packages/nuget-server.md), bude seznam a adresy URL `https://machine/repo/nuget` nabízených oznámení a `https://machine/repo/api/v2/package`v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="70ba5-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="70ba5-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="70ba5-111">Options</span></span>

| <span data-ttu-id="70ba5-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="70ba5-112">Option</span></span> | <span data-ttu-id="70ba5-113">Popis</span><span class="sxs-lookup"><span data-stu-id="70ba5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="70ba5-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="70ba5-114">ApiKey</span></span> | <span data-ttu-id="70ba5-115">Klíč rozhraní API pro cílové úložiště</span><span class="sxs-lookup"><span data-stu-id="70ba5-115">The API key for the target repository.</span></span> <span data-ttu-id="70ba5-116">Pokud není k dispozici, použije se ten zadaný v konfiguračním souboru (`%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="70ba5-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="70ba5-117">Help</span><span class="sxs-lookup"><span data-stu-id="70ba5-117">Help</span></span> | <span data-ttu-id="70ba5-118">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="70ba5-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="70ba5-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="70ba5-119">NoCache</span></span> | <span data-ttu-id="70ba5-120">Zabraňuje balíčku NuGet v použití balíčků v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="70ba5-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="70ba5-121">Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="70ba5-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="70ba5-122">NoOp</span><span class="sxs-lookup"><span data-stu-id="70ba5-122">Noop</span></span> | <span data-ttu-id="70ba5-123">Protokoluje, co se provede, ale akce neprovádí. předpokládá úspěch pro operace push.</span><span class="sxs-lookup"><span data-stu-id="70ba5-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="70ba5-124">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="70ba5-124">PreRelease</span></span> | <span data-ttu-id="70ba5-125">Zahrnuje předběžné verze balíčků v operaci zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="70ba5-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="70ba5-126">Source</span><span class="sxs-lookup"><span data-stu-id="70ba5-126">Source</span></span> | <span data-ttu-id="70ba5-127">Seznam zdrojů balíčku pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="70ba5-127">A list of package sources to mirror.</span></span> <span data-ttu-id="70ba5-128">Pokud nejsou zadány žádné zdroje, budou použity ty, které jsou definovány v konfiguračním souboru (viz ApiKey výše). výchozí nastavení je nuget.org, pokud není zadáno.</span><span class="sxs-lookup"><span data-stu-id="70ba5-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="70ba5-129">časový limit</span><span class="sxs-lookup"><span data-stu-id="70ba5-129">Timeout</span></span> | <span data-ttu-id="70ba5-130">Určuje časový limit pro doručování na server v sekundách.</span><span class="sxs-lookup"><span data-stu-id="70ba5-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="70ba5-131">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="70ba5-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="70ba5-132">Version</span><span class="sxs-lookup"><span data-stu-id="70ba5-132">Version</span></span> | <span data-ttu-id="70ba5-133">Verze balíčku, který se má nainstalovat</span><span class="sxs-lookup"><span data-stu-id="70ba5-133">The version of the package to install.</span></span> <span data-ttu-id="70ba5-134">Pokud parametr není zadán, je zrcadlena nejnovější verze.</span><span class="sxs-lookup"><span data-stu-id="70ba5-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="70ba5-135">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="70ba5-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="70ba5-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="70ba5-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
