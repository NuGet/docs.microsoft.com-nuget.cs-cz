---
title: NuGet – příkaz zrcadlení CLI
description: Referenční informace o příkazu NuGet. exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959715"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="9c8bf-103">Příkaz mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9c8bf-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="9c8bf-104">**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** zastaralé za 3.2 +</span><span class="sxs-lookup"><span data-stu-id="9c8bf-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="9c8bf-105">Zrcadlí balíček a jeho závislosti ze zadaných zdrojových úložišť do cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="9c8bf-106">Soubory NuGet. ServerExtensions. dll a NuGet-Signed. exe, které dříve podporovaly tento příkaz v NuGet 2. x (přejmenováním NuGet-Signed. exe na NuGet. exe), už nejsou k dispozici ke stažení.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="9c8bf-107">Pokud chcete použít příkaz podobný tomuto, vyzkoušejte [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="9c8bf-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="9c8bf-108">Použití</span><span class="sxs-lookup"><span data-stu-id="9c8bf-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="9c8bf-109">kde `<packageID>` je balíček k zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který vypisuje balíčky pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="9c8bf-110">Určuje zdrojové úložiště a `<publishUrlTarget>` Určuje cílové úložiště. `<listUrlTarget>`</span><span class="sxs-lookup"><span data-stu-id="9c8bf-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="9c8bf-111">Pokud vaše cílové úložiště `https://machine/repo` používá službu [NuGet. Server](../../hosting-packages/nuget-server.md), bude seznam a adresy URL `https://machine/repo/nuget` nabízených oznámení a `https://machine/repo/api/v2/package`v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="9c8bf-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="9c8bf-112">Options</span></span>

| <span data-ttu-id="9c8bf-113">Možnost</span><span class="sxs-lookup"><span data-stu-id="9c8bf-113">Option</span></span> | <span data-ttu-id="9c8bf-114">Popis</span><span class="sxs-lookup"><span data-stu-id="9c8bf-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c8bf-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="9c8bf-115">ApiKey</span></span> | <span data-ttu-id="9c8bf-116">Klíč rozhraní API pro cílové úložiště</span><span class="sxs-lookup"><span data-stu-id="9c8bf-116">The API key for the target repository.</span></span> <span data-ttu-id="9c8bf-117">Pokud není k dispozici, použije se ten zadaný v konfiguračním souboru (`%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="9c8bf-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="9c8bf-118">Help</span><span class="sxs-lookup"><span data-stu-id="9c8bf-118">Help</span></span> | <span data-ttu-id="9c8bf-119">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="9c8bf-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="9c8bf-120">NoCache</span></span> | <span data-ttu-id="9c8bf-121">Zabraňuje balíčku NuGet v použití balíčků v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="9c8bf-122">Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9c8bf-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="9c8bf-123">NoOp</span><span class="sxs-lookup"><span data-stu-id="9c8bf-123">Noop</span></span> | <span data-ttu-id="9c8bf-124">Protokoluje, co se provede, ale akce neprovádí. předpokládá úspěch pro operace push.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="9c8bf-125">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="9c8bf-125">PreRelease</span></span> | <span data-ttu-id="9c8bf-126">Zahrnuje předběžné verze balíčků v operaci zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="9c8bf-127">Source</span><span class="sxs-lookup"><span data-stu-id="9c8bf-127">Source</span></span> | <span data-ttu-id="9c8bf-128">Seznam zdrojů balíčku pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-128">A list of package sources to mirror.</span></span> <span data-ttu-id="9c8bf-129">Pokud nejsou zadány žádné zdroje, budou použity ty, které jsou definovány v konfiguračním souboru (viz ApiKey výše). výchozí nastavení je nuget.org, pokud není zadáno.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="9c8bf-130">časový limit</span><span class="sxs-lookup"><span data-stu-id="9c8bf-130">Timeout</span></span> | <span data-ttu-id="9c8bf-131">Určuje časový limit pro doručování na server v sekundách.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="9c8bf-132">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="9c8bf-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="9c8bf-133">Version</span><span class="sxs-lookup"><span data-stu-id="9c8bf-133">Version</span></span> | <span data-ttu-id="9c8bf-134">Verze balíčku, který se má nainstalovat</span><span class="sxs-lookup"><span data-stu-id="9c8bf-134">The version of the package to install.</span></span> <span data-ttu-id="9c8bf-135">Pokud parametr není zadán, je zrcadlena nejnovější verze.</span><span class="sxs-lookup"><span data-stu-id="9c8bf-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="9c8bf-136">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="9c8bf-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9c8bf-137">Příklady</span><span class="sxs-lookup"><span data-stu-id="9c8bf-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
