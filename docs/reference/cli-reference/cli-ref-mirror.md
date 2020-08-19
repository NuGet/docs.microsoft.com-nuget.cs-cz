---
title: NuGet – příkaz zrcadlení CLI
description: Referenční informace pro příkaz nuget.exe Mirror
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622964"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="fd7c1-103">zrcadlení – příkaz (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fd7c1-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="fd7c1-104">**Platí pro:** publikování &bullet; **podporovaných verzí balíčku:** zastaralé za 3.2 +</span><span class="sxs-lookup"><span data-stu-id="fd7c1-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="fd7c1-105">Zrcadlí balíček a jeho závislosti ze zadaných zdrojových úložišť do cílového úložiště.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="fd7c1-106">NuGet.ServerExtensions.dll a NuGet-Signed.exe, které dříve podporovaly tento příkaz v NuGet 2. x (přejmenováním NuGet-Signed.exe na nuget.exe), již nejsou k dispozici ke stažení.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="fd7c1-107">Pokud chcete použít příkaz podobný tomuto, vyzkoušejte [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="fd7c1-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="fd7c1-108">Využití</span><span class="sxs-lookup"><span data-stu-id="fd7c1-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="fd7c1-109">kde `<packageID>` je balíček k zrcadlení, nebo `<configFilePath>` identifikuje `packages.config` soubor, který vypisuje balíčky pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="fd7c1-110">`<listUrlTarget>`Určuje zdrojové úložiště a `<publishUrlTarget>` Určuje cílové úložiště.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="fd7c1-111">Pokud vaše cílové úložiště používá `https://machine/repo` službu [NuGet. Server](../../hosting-packages/nuget-server.md), bude seznam a adresy URL nabízených oznámení a v `https://machine/repo/nuget` `https://machine/repo/api/v2/package` uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="fd7c1-112">Možnosti</span><span class="sxs-lookup"><span data-stu-id="fd7c1-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="fd7c1-113">Klíč rozhraní API pro cílové úložiště</span><span class="sxs-lookup"><span data-stu-id="fd7c1-113">The API key for the target repository.</span></span> <span data-ttu-id="fd7c1-114">Pokud není k dispozici, použije se ten zadaný v konfiguračním souboru ( `%AppData%\NuGet\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="fd7c1-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="fd7c1-115">Zobrazí informace o nápovědě k příkazu.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="fd7c1-116">Zabraňuje balíčku NuGet v použití balíčků v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="fd7c1-117">Viz [Správa globálních balíčků a složek mezipaměti](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fd7c1-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="fd7c1-118">Protokoluje, co se provede, ale akce neprovádí. předpokládá úspěch pro operace push.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="fd7c1-119">Zahrnuje předběžné verze balíčků v operaci zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="fd7c1-120">Seznam zdrojů balíčku pro zrcadlení.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-120">A list of package sources to mirror.</span></span> <span data-ttu-id="fd7c1-121">Pokud nejsou zadány žádné zdroje, budou použity ty, které jsou definovány v konfiguračním souboru (viz ApiKey výše). výchozí nastavení je nuget.org, pokud není zadáno.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="fd7c1-122">Určuje časový limit pro doručování na server v sekundách.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="fd7c1-123">Výchozí hodnota je 300 sekund (5 minut).</span><span class="sxs-lookup"><span data-stu-id="fd7c1-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="fd7c1-124">Verze balíčku, který se má nainstalovat</span><span class="sxs-lookup"><span data-stu-id="fd7c1-124">The version of the package to install.</span></span> <span data-ttu-id="fd7c1-125">Pokud parametr není zadán, je zrcadlena nejnovější verze.</span><span class="sxs-lookup"><span data-stu-id="fd7c1-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="fd7c1-126">Podívejte se také na [proměnné prostředí](cli-ref-environment-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="fd7c1-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fd7c1-127">Příklady</span><span class="sxs-lookup"><span data-stu-id="fd7c1-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
