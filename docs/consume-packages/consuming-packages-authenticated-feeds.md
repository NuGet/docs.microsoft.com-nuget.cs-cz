---
title: Využívání balíčků ze ověřených informačních kanálů
description: Využívání balíčků ze ověřených informačních kanálů ve všech scénářích klientů NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231789"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="bbab8-103">Využívání balíčků ze ověřených informačních kanálů</span><span class="sxs-lookup"><span data-stu-id="bbab8-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="bbab8-104">Kromě [veřejného informačního kanálu](https://api.nuget.org/v3/index.json)NuGet.org mají klienti NuGet možnost pracovat s kanály souborů a soukromými kanály http.</span><span class="sxs-lookup"><span data-stu-id="bbab8-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="bbab8-105">K ověřování pomocí privátních informačních kanálů http jsou k diskaždé dva přístupy:</span><span class="sxs-lookup"><span data-stu-id="bbab8-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="bbab8-106">Přidat pověření do [souboru NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="bbab8-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="bbab8-107">Proveďte ověření pomocí jednoho z mnoha modelů rozšiřitelnosti v závislosti na použitém klientovi.</span><span class="sxs-lookup"><span data-stu-id="bbab8-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="bbab8-108">Rozšiřitelnost ověřování klientů NuGet</span><span class="sxs-lookup"><span data-stu-id="bbab8-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="bbab8-109">U různých klientů NuGet zodpovídá poskytovatel privátního informačního kanálu za ověřování.</span><span class="sxs-lookup"><span data-stu-id="bbab8-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="bbab8-110">Všichni klienti NuGet mají metody rozšíření, které to podporují.</span><span class="sxs-lookup"><span data-stu-id="bbab8-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="bbab8-111">Jsou to buď rozšíření sady Visual Studio, nebo modul plug-in, který může komunikovat s NuGet za účelem načtení přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="bbab8-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="bbab8-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbab8-112">Visual Studio</span></span>

<span data-ttu-id="bbab8-113">V aplikaci Visual Studio NuGet zveřejňuje rozhraní, které poskytovatelé kanálu můžou implementovat a poskytnout svým zákazníkům.</span><span class="sxs-lookup"><span data-stu-id="bbab8-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="bbab8-114">Další podrobnosti najdete v dokumentaci o [tom, jak vytvořit poskytovatele pověření sady Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="bbab8-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="bbab8-115">K dispozici poskytovatelé pověření NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbab8-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="bbab8-116">Do sady Visual Studio je integrovaný poskytovatel přihlašovacích údajů, který podporuje Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="bbab8-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="bbab8-117">K dispozici jsou poskytovatelé přihlašovacích údajů pro modul plug-in:</span><span class="sxs-lookup"><span data-stu-id="bbab8-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="bbab8-118">Poskytovatel pověření MyGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbab8-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="bbab8-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="bbab8-119">nuget.exe</span></span>

<span data-ttu-id="bbab8-120">Když `nuget.exe` potřebuje přihlašovací údaje k ověřování pomocí informačního kanálu, vyhledá je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bbab8-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="bbab8-121">Vyhledejte přihlašovací údaje v `NuGet.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="bbab8-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="bbab8-122">Použít poskytovatele pověření modulu plug-in v2</span><span class="sxs-lookup"><span data-stu-id="bbab8-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="bbab8-123">Použít poskytovatele přihlašovacích údajů modulu plug-in v1</span><span class="sxs-lookup"><span data-stu-id="bbab8-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="bbab8-124">NuGet pak vyzve uživatele k zadání přihlašovacích údajů na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="bbab8-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="bbab8-125">Zprostředkovatelé přihlašovacích údajů NuGet. exe a v2</span><span class="sxs-lookup"><span data-stu-id="bbab8-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="bbab8-126">Ve verzi `4.8` NuGet definovala nový mechanismus ověřovacího modulu plug-in (dále jen jako poskytovatelé přihlašovacích údajů v2).</span><span class="sxs-lookup"><span data-stu-id="bbab8-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="bbab8-127">Pro instalaci a zjišťování těchto zprostředkovatelů se podívejte na [moduly plug-in NuGet pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="bbab8-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="bbab8-128">Zprostředkovatelé přihlašovacích údajů NuGet. exe a v1</span><span class="sxs-lookup"><span data-stu-id="bbab8-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="bbab8-129">Ve verzi `3.3` NuGet představil první verzi modulů plug-in pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="bbab8-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="bbab8-130">Pro instalaci a zjišťování těchto zprostředkovatelů se odkazují na [poskytovatele pověření NuGet. exe.](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="bbab8-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="bbab8-131">K dispozici poskytovatelé přihlašovacích údajů pro NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="bbab8-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="bbab8-132">Poskytovatelé [přihlašovacích údajů služby Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) nebo [Poskytovatel pověření Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="bbab8-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="bbab8-133">V sadě Visual Studio 2017 verze 15,9 a novější je poskytovatel přihlašovacích údajů Azure DevOps zahrnutý v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbab8-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="bbab8-134">Pokud `nuget.exe` používá nástroj MSBuild z konkrétní sady nástrojů sady Visual Studio, bude modul plug-in zjištěn automaticky.</span><span class="sxs-lookup"><span data-stu-id="bbab8-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="bbab8-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="bbab8-135">dotnet.exe</span></span>

<span data-ttu-id="bbab8-136">Když `dotnet.exe` potřebuje přihlašovací údaje k ověřování pomocí informačního kanálu, vyhledá je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bbab8-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="bbab8-137">Vyhledejte přihlašovací údaje v `NuGet.config` soubory.</span><span class="sxs-lookup"><span data-stu-id="bbab8-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="bbab8-138">Použít poskytovatele pověření modulu plug-in v2</span><span class="sxs-lookup"><span data-stu-id="bbab8-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="bbab8-139">Ve výchozím nastavení `dotnet.exe` není interaktivní, takže možná budete muset předat příznak `--interactive` a získat tak nástroj k blokování ověřování.</span><span class="sxs-lookup"><span data-stu-id="bbab8-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="bbab8-140">Zprostředkovatelé přihlašovacích údajů dotnet. exe a v2</span><span class="sxs-lookup"><span data-stu-id="bbab8-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="bbab8-141">Ve verzi `2.2.100` sady SDK sada NuGet definovala mechanismus ověřovacího modulu plug-in, který funguje ve všech klientech.</span><span class="sxs-lookup"><span data-stu-id="bbab8-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="bbab8-142">Pro instalaci a zjišťování těchto zprostředkovatelů se podívejte na [moduly plug-in NuGet pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="bbab8-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="bbab8-143">K dispozici poskytovatelé přihlašovacích údajů pro dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="bbab8-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="bbab8-144">Poskytovatel pověření Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="bbab8-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="bbab8-145">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="bbab8-145">MSBuild.exe</span></span>

<span data-ttu-id="bbab8-146">Když `MSBuild.exe` potřebuje přihlašovací údaje k ověřování pomocí informačního kanálu, vyhledá je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bbab8-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="bbab8-147">Hledat přihlašovací údaje v `NuGet.config` soubory</span><span class="sxs-lookup"><span data-stu-id="bbab8-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="bbab8-148">Použít poskytovatele pověření modulu plug-in v2</span><span class="sxs-lookup"><span data-stu-id="bbab8-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="bbab8-149">Ve výchozím nastavení `MSBuild.exe` není interaktivní, takže možná budete muset nastavit vlastnost `/p:NuGetInteractive=true` a získat tak nástroj k blokování ověřování.</span><span class="sxs-lookup"><span data-stu-id="bbab8-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="bbab8-150">Zprostředkovatelé přihlašovacích údajů pro MSBuild. exe a v2</span><span class="sxs-lookup"><span data-stu-id="bbab8-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="bbab8-151">V sadě Visual Studio 2019 Update 9, NuGet definoval mechanismus ověřovacího modulu plug-in, který funguje ve všech klientech.</span><span class="sxs-lookup"><span data-stu-id="bbab8-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="bbab8-152">Pro instalaci a zjišťování těchto zprostředkovatelů se podívejte na [moduly plug-in NuGet pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="bbab8-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="bbab8-153">K dispozici poskytovatelé přihlašovacích údajů pro MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="bbab8-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="bbab8-154">Poskytovatel pověření Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="bbab8-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="bbab8-155">V sadě Visual Studio 2017 Update 9 a novějších je poskytovatel přihlašovacích údajů Azure DevOps zahrnutý v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbab8-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="bbab8-156">Nejsou nutné žádné další kroky.</span><span class="sxs-lookup"><span data-stu-id="bbab8-156">No additional steps are required.</span></span>
