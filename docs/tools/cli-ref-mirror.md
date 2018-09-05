---
title: Rozhraní příkazového řádku NuGet zrcadlový svazek
description: Referenční informace pro příkaz zrcadlení nuget.exe
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550203"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="9b748-103">Příkaz mirror (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9b748-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="9b748-104">**Platí pro:** balíček publikování &bullet; **podporované verze:** přestala nabízet v 3.2 +</span><span class="sxs-lookup"><span data-stu-id="9b748-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="9b748-105">Odráží balíček a jeho závislosti z úložišť zadaného zdroje do cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="9b748-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="9b748-106">Pokud chcete povolit tento příkaz pro verze NuGet před 3.2, přejděte na [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)vyberte nejnovější stabilní verzi, stáhněte si `NuGet.ServerExtensions.dll` a `Nuget-Signed.exe` na místní disk a přejmenování `Nuget-Signed.exe` k `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="9b748-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="9b748-107">Použití</span><span class="sxs-lookup"><span data-stu-id="9b748-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="9b748-108">kde `<packageID>` je balíček pro zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který uvádí balíčky pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="9b748-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="9b748-109">`<listUrlTarget>` Určuje úložiště zdrojového kódu a `<publishUrlTarget>` určuje cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="9b748-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="9b748-110">Pokud je vaše cílové úložiště na `https://machine/repo` , na kterém běží [NuGet.Server](../hosting-packages/nuget-server.md), budou adresy URL seznamu a push `https://machine/repo/nuget` a `https://machine/repo/api/v2/package`v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="9b748-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="9b748-111">Možnosti</span><span class="sxs-lookup"><span data-stu-id="9b748-111">Options</span></span>

| <span data-ttu-id="9b748-112">Možnost</span><span class="sxs-lookup"><span data-stu-id="9b748-112">Option</span></span> | <span data-ttu-id="9b748-113">Popis</span><span class="sxs-lookup"><span data-stu-id="9b748-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9b748-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="9b748-114">ApiKey</span></span> | <span data-ttu-id="9b748-115">Klíč rozhraní API pro cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="9b748-115">The API key for the target repository.</span></span> <span data-ttu-id="9b748-116">Pokud není k dispozici, je uvedeno v konfiguračním souboru se používá (`%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="9b748-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="9b748-117">Nápověda</span><span class="sxs-lookup"><span data-stu-id="9b748-117">Help</span></span> | <span data-ttu-id="9b748-118">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="9b748-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="9b748-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="9b748-119">NoCache</span></span> | <span data-ttu-id="9b748-120">Brání použití mezipaměti balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="9b748-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="9b748-121">Zobrazit [Správa globálních balíčků a složek mezipaměti](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9b748-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="9b748-122">NoOp</span><span class="sxs-lookup"><span data-stu-id="9b748-122">Noop</span></span> | <span data-ttu-id="9b748-123">Protokoly, co by se dělalo, ale neprovede akce; předpokládá úspěchu operací push.</span><span class="sxs-lookup"><span data-stu-id="9b748-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="9b748-124">Platnost předběžné verze</span><span class="sxs-lookup"><span data-stu-id="9b748-124">PreRelease</span></span> | <span data-ttu-id="9b748-125">Obsahuje předběžné verze balíčků v zrcadlení operace.</span><span class="sxs-lookup"><span data-stu-id="9b748-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="9b748-126">Zdroj</span><span class="sxs-lookup"><span data-stu-id="9b748-126">Source</span></span> | <span data-ttu-id="9b748-127">Seznam zdrojů balíčků pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="9b748-127">A list of package sources to mirror.</span></span> <span data-ttu-id="9b748-128">Pokud nejsou zadány žádné zdroje, těm, které jsou definovány v konfiguračním souboru (viz ApiKey výše) se používají, použije výchozí hodnotu nuget.org, pokud nejsou zadány žádné.</span><span class="sxs-lookup"><span data-stu-id="9b748-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="9b748-129">časový limit</span><span class="sxs-lookup"><span data-stu-id="9b748-129">Timeout</span></span> | <span data-ttu-id="9b748-130">Určuje časový limit v sekundách pro odesílání na server.</span><span class="sxs-lookup"><span data-stu-id="9b748-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="9b748-131">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="9b748-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="9b748-132">Version</span><span class="sxs-lookup"><span data-stu-id="9b748-132">Version</span></span> | <span data-ttu-id="9b748-133">Verze balíčku k instalaci.</span><span class="sxs-lookup"><span data-stu-id="9b748-133">The version of the package to install.</span></span> <span data-ttu-id="9b748-134">Pokud není zadán, je zrcadlena na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="9b748-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="9b748-135">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9b748-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9b748-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="9b748-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
