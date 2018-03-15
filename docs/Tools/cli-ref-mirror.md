---
title: "Příkaz zrcadlení NuGet rozhraní příkazového řádku | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenční dokumentace pro příkaz nuget.exe zrcadlení"
keywords: "referenční dokumentace zrcadlení nuget, příkaz zrcadlení"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="35ef1-104">příkaz zrcadlení (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="35ef1-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="35ef1-105">**Platí pro:** balíček publikování &bullet; **podporované verze:** zastaralé v 3.2 +</span><span class="sxs-lookup"><span data-stu-id="35ef1-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="35ef1-106">Odráží balíček a jeho závislosti z zadaná zdrojová úložiště do cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="35ef1-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="35ef1-107">Chcete-li příkaz pro verze NuGet před 3.2, přejděte na [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases)vyberte nejnovější stabilní verze, stáhněte si `NuGet.ServerExtensions.dll` a `Nuget-Signed.exe` na váš místní disk a přejmenování `Nuget-Signed.exe` k `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="35ef1-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="35ef1-108">Použití</span><span class="sxs-lookup"><span data-stu-id="35ef1-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="35ef1-109">kde `<packageID>` je balíček pro zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který obsahuje seznam balíčků pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="35ef1-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="35ef1-110">`<listUrlTarget>` Určuje zdroj úložiště, a `<publishUrlTarget>` Určuje cíl úložiště.</span><span class="sxs-lookup"><span data-stu-id="35ef1-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="35ef1-111">Pokud vaše cílové úložiště na `https://machine/repo` na kterém běží [NuGet.Server](../hosting-packages/nuget-server.md), adresy URL seznamu a nabízených bude `https://machine/repo/nuget` a `https://machine/repo/api/v2/package`, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="35ef1-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="35ef1-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="35ef1-112">Options</span></span>

| <span data-ttu-id="35ef1-113">Možnost</span><span class="sxs-lookup"><span data-stu-id="35ef1-113">Option</span></span> | <span data-ttu-id="35ef1-114">Popis</span><span class="sxs-lookup"><span data-stu-id="35ef1-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="35ef1-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="35ef1-115">ApiKey</span></span> | <span data-ttu-id="35ef1-116">Klíč rozhraní API pro cílové úložiště.</span><span class="sxs-lookup"><span data-stu-id="35ef1-116">The API key for the target repository.</span></span> <span data-ttu-id="35ef1-117">Pokud není přítomný, verze zadaná v konfiguračním souboru se používá (`%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="35ef1-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="35ef1-118">Nápověda</span><span class="sxs-lookup"><span data-stu-id="35ef1-118">Help</span></span> | <span data-ttu-id="35ef1-119">Zobrazí nápovědu pro příkaz.</span><span class="sxs-lookup"><span data-stu-id="35ef1-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="35ef1-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="35ef1-120">NoCache</span></span> | <span data-ttu-id="35ef1-121">NuGet bránit v použití balíčky z mezipaměti místního počítače.</span><span class="sxs-lookup"><span data-stu-id="35ef1-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="35ef1-122">Nedojde k žádné akci</span><span class="sxs-lookup"><span data-stu-id="35ef1-122">Noop</span></span> | <span data-ttu-id="35ef1-123">Protokoly co provádějí, ale neprovádí akce; předpokládá úspěch pro operace push.</span><span class="sxs-lookup"><span data-stu-id="35ef1-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="35ef1-124">Předběžné verze</span><span class="sxs-lookup"><span data-stu-id="35ef1-124">PreRelease</span></span> | <span data-ttu-id="35ef1-125">Obsahuje předběžné verze balíčků v zrcadlení operaci.</span><span class="sxs-lookup"><span data-stu-id="35ef1-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="35ef1-126">Zdroj</span><span class="sxs-lookup"><span data-stu-id="35ef1-126">Source</span></span> | <span data-ttu-id="35ef1-127">Seznam zdrojů balíčku pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="35ef1-127">A list of package sources to mirror.</span></span> <span data-ttu-id="35ef1-128">Pokud nejsou zadány žádné zdroje, těm, které jsou definována v konfiguračním souboru (viz výše ApiKey) se používají, jako výchozí bude použit nuget.org-li zadán žádný.</span><span class="sxs-lookup"><span data-stu-id="35ef1-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="35ef1-129">Časový limit</span><span class="sxs-lookup"><span data-stu-id="35ef1-129">Timeout</span></span> | <span data-ttu-id="35ef1-130">Určuje časový limit v sekundách pro vkládání na server.</span><span class="sxs-lookup"><span data-stu-id="35ef1-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="35ef1-131">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="35ef1-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="35ef1-132">Version</span><span class="sxs-lookup"><span data-stu-id="35ef1-132">Version</span></span> | <span data-ttu-id="35ef1-133">Verze balíčku pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="35ef1-133">The version of the package to install.</span></span> <span data-ttu-id="35ef1-134">Pokud není zadáno, je Zrcadleno na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="35ef1-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="35ef1-135">Viz také [proměnné prostředí](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="35ef1-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="35ef1-136">Příklady</span><span class="sxs-lookup"><span data-stu-id="35ef1-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
