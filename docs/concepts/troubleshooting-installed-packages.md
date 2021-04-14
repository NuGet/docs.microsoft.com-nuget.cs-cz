---
title: Řešení potíží s nainstalovanými balíčky
description: Jak zjistit, který zdroj balíčku se použil pro jednotlivé balíčky
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387554"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="55da2-103">Řešení potíží s nainstalovanými balíčky</span><span class="sxs-lookup"><span data-stu-id="55da2-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="55da2-104">Někdy je možné, že budete chtít ověřit, ze kterého zdroje byl konkrétní balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="55da2-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="55da2-105">Tady je několik způsobů, jak můžete kontrolu provést.</span><span class="sxs-lookup"><span data-stu-id="55da2-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="55da2-106">Některé zdroje balíčků podporují koncept známý jako nadřazené zdroje.</span><span class="sxs-lookup"><span data-stu-id="55da2-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="55da2-107">Například [Azure Artifacts nadřazené zdroje](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="55da2-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="55da2-108">Klienti NuGet neznají, jestli balíček pochází z nadřazeného zdroje.</span><span class="sxs-lookup"><span data-stu-id="55da2-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="55da2-109">Proto jakékoli protokolování zdroje balíčku zobrazí seznam nakonfigurovaného zdroje, nikoli nadřazeného zdroje.</span><span class="sxs-lookup"><span data-stu-id="55da2-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="55da2-110">`.nupkg.metadata` soubor ve složce globálních balíčků</span><span class="sxs-lookup"><span data-stu-id="55da2-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="55da2-111">Při extrakci balíčku do složky *Global-Packages* `.nupkg.metadata` se zapíše soubor.</span><span class="sxs-lookup"><span data-stu-id="55da2-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="55da2-112">Od 5.9.0 NuGet přidá NuGet zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="55da2-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="55da2-113">Níže najdete informace o mapování verzí NuGet na verze sady Visual Studio nebo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="55da2-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="55da2-114">Například:</span><span class="sxs-lookup"><span data-stu-id="55da2-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="55da2-115">Pokud má složka *globálních balíčků* extrahovány balíčky před upgradováním na novější verzi nástrojů, které mají NuGet 5.9.0, bude `.nupkg.metadata` soubor verze 1 a nebude obsahovat zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="55da2-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="55da2-116">Můžete [Vymazat globální složku *balíčků*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) , abyste zajistili, že všechny balíčky budou obsahovat zdroj balíčku.</span><span class="sxs-lookup"><span data-stu-id="55da2-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="55da2-117">NuGet zapisuje `.nupkg.metadata` soubor pouze do složky *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="55da2-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="55da2-118">Projekty používající `packages.config` použití složky balíčků řešení, která nevytváří `.nupkg.metadata` soubor.</span><span class="sxs-lookup"><span data-stu-id="55da2-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="55da2-119">Nainstalovaná zpráva protokolu balíčku</span><span class="sxs-lookup"><span data-stu-id="55da2-119">Installed package log message</span></span>

<span data-ttu-id="55da2-120">Od 5.9.0 NuGet vyprodukuje výstup NuGet zdroj balíčku ve zprávě o obnovení, která informuje o instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="55da2-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="55da2-121">Například:</span><span class="sxs-lookup"><span data-stu-id="55da2-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="55da2-122">Tato zpráva je ve výstupu normální/informativní podrobností.</span><span class="sxs-lookup"><span data-stu-id="55da2-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="55da2-123">Visual Studio a `dotnet` CLI jsou ve výchozím nastavení na minimální úroveň podrobností, takže tato zpráva se ve výchozím nastavení nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="55da2-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="55da2-124">Nástroje rozhraní příkazového `msbuild` řádku a jsou `nuget` ve výchozím nastavení podrobností normální, takže se tato zpráva bude zobrazovat ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="55da2-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="55da2-125">Zpráva protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="55da2-125">HTTP log message</span></span>

<span data-ttu-id="55da2-126">Pokud balíček není místně dostupný, buď ve složce *Global-Packages* , v záložní složce, nebo v místním zdroji souborů, NuGet ho stáhne z libovolného nakonfigurovaného zdroje balíčku přes HTTP.</span><span class="sxs-lookup"><span data-stu-id="55da2-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="55da2-127">Požadavky HTTP a odpovědi jsou protokolovány v normální úrovni podrobností a měli byste vidět pouze jeden požadavek a odpověď na verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="55da2-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="55da2-128">Například:</span><span class="sxs-lookup"><span data-stu-id="55da2-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="55da2-129">Pokud byly soubory nedávno staženy, mohou být načteny z *mezipaměti protokolu HTTP* NuGet.</span><span class="sxs-lookup"><span data-stu-id="55da2-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="55da2-130">Formát adresy URL se může lišit pro různé implementace HTTP serveru NuGet a to, jestli implementuje protokol NuGet v2 nebo V3 HTTP.</span><span class="sxs-lookup"><span data-stu-id="55da2-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="55da2-131">Pokud `nuget.config` má definováno více zdrojů HTTP, zobrazí se pro každý soubor balíčku více požadavků `index.json` , jeden pro každý zdroj.</span><span class="sxs-lookup"><span data-stu-id="55da2-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="55da2-132">Pro každou verzi balíčku bude ale k dispozici pouze jedno `nupkg` stažení.</span><span class="sxs-lookup"><span data-stu-id="55da2-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="55da2-133">Zpráva protokolu podpisu balíčku</span><span class="sxs-lookup"><span data-stu-id="55da2-133">Package signature log message</span></span>

<span data-ttu-id="55da2-134">Pokud je stažený balíček podepsán, NuGet ověří podpis a zaprotokoluje následující zprávu podrobnou podrobnostem:</span><span class="sxs-lookup"><span data-stu-id="55da2-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="55da2-135">Tato zpráva bude hlášena, zda byl balíček stažen ze zdroje balíčku HTTP nebo zkopírován z místního zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="55da2-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="55da2-136">Pokud je balíček už dostupný ve složce *Global-Packages* nebo v záložní složce, nebude se jednat o výstup.</span><span class="sxs-lookup"><span data-stu-id="55da2-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="55da2-137">Z důvodu [odebrání vztahu důvěryhodnosti NuGet CA pro certifikační autoritu](https://github.com/dotnet/announcements/issues/180) se u některých platforem v některých verzích NuGet a .NET SDK zakázalo podepsané ověření balíčku.</span><span class="sxs-lookup"><span data-stu-id="55da2-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="55da2-138">Proto můžou mít stejné balíčky `PackageSignatureVerificationLog` protokoly, nebo můžou chybět protokoly v závislosti na tom, na které platformě se má obnovení spouštět a jakou verzi rozhraní .NET nebo NuGet používáte.</span><span class="sxs-lookup"><span data-stu-id="55da2-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="55da2-139">Mapa verze NuGet</span><span class="sxs-lookup"><span data-stu-id="55da2-139">NuGet Version Map</span></span>

<span data-ttu-id="55da2-140">Následující verze NuGet mají důležité změny týkající se protokolování zdroje balíčků:</span><span class="sxs-lookup"><span data-stu-id="55da2-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="55da2-141">Verze NuGet</span><span class="sxs-lookup"><span data-stu-id="55da2-141">NuGet Version</span></span>|<span data-ttu-id="55da2-142">Verze sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="55da2-142">Visual Studio Version</span></span>|<span data-ttu-id="55da2-143">Verze sady .NET SDK</span><span class="sxs-lookup"><span data-stu-id="55da2-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="55da2-144">5.9.0 NuGet</span><span class="sxs-lookup"><span data-stu-id="55da2-144">NuGet 5.9.0</span></span>|<span data-ttu-id="55da2-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="55da2-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="55da2-146">5.0.200 SADY SDK PRO .NET 5</span><span class="sxs-lookup"><span data-stu-id="55da2-146">.NET 5 SDK 5.0.200</span></span>|
