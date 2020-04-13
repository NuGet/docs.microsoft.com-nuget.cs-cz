---
title: Spotřebovávající balíky z ověřených informačních kanálů
description: Spotřebovávající balíčky z ověřených informačních kanálů ve všech klientských scénářích NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231789"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="ee45c-103">Spotřebovávající balíky z ověřených informačních kanálů</span><span class="sxs-lookup"><span data-stu-id="ee45c-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="ee45c-104">Kromě nuget.org [veřejný zdroj](https://api.nuget.org/v3/index.json), NuGet klienti mají možnost pracovat s kanály souborů a soukromé http kanály.</span><span class="sxs-lookup"><span data-stu-id="ee45c-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="ee45c-105">Chcete-li ověřit pomocí soukromých http kanály, 2 přístupy jsou:</span><span class="sxs-lookup"><span data-stu-id="ee45c-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="ee45c-106">Přidání pověření do [souboru NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="ee45c-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="ee45c-107">Ověřte pomocí jednoho z mnoha modelů rozšiřitelnosti v závislosti na použitém klientovi.</span><span class="sxs-lookup"><span data-stu-id="ee45c-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="ee45c-108">Rozšiřitelnost ověřování klientů NuGet</span><span class="sxs-lookup"><span data-stu-id="ee45c-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="ee45c-109">Pro různé klienty NuGet soukromého poskytovatele informačního kanálu sám je zodpovědný za ověřování.</span><span class="sxs-lookup"><span data-stu-id="ee45c-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="ee45c-110">Všechny klienty NuGet mají metody rozšiřitelnosti pro podporu tohoto.</span><span class="sxs-lookup"><span data-stu-id="ee45c-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="ee45c-111">Jedná se buď rozšíření sady Visual Studio nebo plugin, který může komunikovat s NuGet načíst pověření.</span><span class="sxs-lookup"><span data-stu-id="ee45c-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="ee45c-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee45c-112">Visual Studio</span></span>

<span data-ttu-id="ee45c-113">V sadě Visual Studio NuGet zveřejňuje rozhraní, které zprostředkovatelé informačního kanálu můžete implementovat a poskytnout svým zákazníkům.</span><span class="sxs-lookup"><span data-stu-id="ee45c-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="ee45c-114">Další podrobnosti naleznete v dokumentaci [k vytvoření zprostředkovatele pověření sady Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="ee45c-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="ee45c-115">K dispozici zprostředkovatelé pověření NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee45c-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="ee45c-116">V sadě Visual Studio je integrovaný poskytovatel přihlašovacích údajů, který podporuje Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="ee45c-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="ee45c-117">Mezi dostupné poskytovatele přihlašovacích údajů modulu plug-in patří:</span><span class="sxs-lookup"><span data-stu-id="ee45c-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="ee45c-118">MyGet zprostředkovatele pověření pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee45c-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="ee45c-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ee45c-119">nuget.exe</span></span>

<span data-ttu-id="ee45c-120">Když `nuget.exe` potřebuje pověření k ověření pomocí informačního kanálu, hledá je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ee45c-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ee45c-121">Vyhledejte pověření `NuGet.config` v souborech.</span><span class="sxs-lookup"><span data-stu-id="ee45c-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="ee45c-122">Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V2</span><span class="sxs-lookup"><span data-stu-id="ee45c-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="ee45c-123">Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V1</span><span class="sxs-lookup"><span data-stu-id="ee45c-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="ee45c-124">NuGet pak vyzve uživatele k zadání pověření na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="ee45c-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="ee45c-125">zprostředkovatelé pověření nuget.exe a V2</span><span class="sxs-lookup"><span data-stu-id="ee45c-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="ee45c-126">Ve `4.8` verzi NuGet definoval nový mechanismus modulu plug-in ověřování, dále jen zprostředkovatelé pověření V2.</span><span class="sxs-lookup"><span data-stu-id="ee45c-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="ee45c-127">Instalace a zjišťování těchto poskytovatelů naleznete [v nugetských zásuvných modulech pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ee45c-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="ee45c-128">zprostředkovatelé pověření nuget.exe a V1</span><span class="sxs-lookup"><span data-stu-id="ee45c-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="ee45c-129">Ve `3.3` verzi NuGet představil první verzi ověřovacích pluginů.</span><span class="sxs-lookup"><span data-stu-id="ee45c-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="ee45c-130">Instalace a zjišťování těchto poskytovatelů naleznete na [nuget.exe zprostředkovatele pověření](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="ee45c-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="ee45c-131">K dispozici zprostředkovatelé pověření pro nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ee45c-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="ee45c-132">[Zprostředkovatelé přihlašovacích údajů Azure DevOps V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) nebo [zprostředkovatel evitorů artefaktů Azure](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="ee45c-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="ee45c-133">S Visual Studio 2017 verze 15.9 a novější, Azure DevOps poskytovatel přihlašovacích údajů je součástí Sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee45c-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="ee45c-134">Pokud `nuget.exe` používá MSBuild z této konkrétní sady nástrojů Sady visual studio, pak plugin bude zjištěna automaticky.</span><span class="sxs-lookup"><span data-stu-id="ee45c-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="ee45c-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="ee45c-135">dotnet.exe</span></span>

<span data-ttu-id="ee45c-136">Když `dotnet.exe` potřebuje pověření k ověření pomocí informačního kanálu, hledá je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ee45c-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ee45c-137">Vyhledejte pověření `NuGet.config` v souborech.</span><span class="sxs-lookup"><span data-stu-id="ee45c-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="ee45c-138">Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V2</span><span class="sxs-lookup"><span data-stu-id="ee45c-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="ee45c-139">Ve `dotnet.exe` výchozím nastavení není interaktivní, takže `--interactive` možná budete muset předat příznak, aby se nástroj blokovat pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="ee45c-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="ee45c-140">Zprostředkovatelé pověření dotnet.exe a V2</span><span class="sxs-lookup"><span data-stu-id="ee45c-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="ee45c-141">Ve `2.2.100` verzi sady SDK definuje nuget mechanismus modulu plug-in ověřování, který funguje ve všech klientech.</span><span class="sxs-lookup"><span data-stu-id="ee45c-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="ee45c-142">Instalace a zjišťování těchto poskytovatelů naleznete [v nugetských zásuvných modulech pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ee45c-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="ee45c-143">Dostupní zprostředkovatelé pověření pro program dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="ee45c-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="ee45c-144">Zprostředkovatel přihlašovacích údajů artefaktů Azure</span><span class="sxs-lookup"><span data-stu-id="ee45c-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="ee45c-145">Soubor MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="ee45c-145">MSBuild.exe</span></span>

<span data-ttu-id="ee45c-146">Když `MSBuild.exe` potřebuje pověření k ověření pomocí informačního kanálu, hledá je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ee45c-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ee45c-147">Hledání přihlašovacích `NuGet.config` údajů v souborech</span><span class="sxs-lookup"><span data-stu-id="ee45c-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="ee45c-148">Použití zprostředkovatelů přihlašovacích údajů modulu plug-in V2</span><span class="sxs-lookup"><span data-stu-id="ee45c-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="ee45c-149">Ve `MSBuild.exe` výchozím nastavení není interaktivní, takže `/p:NuGetInteractive=true` možná budete muset nastavit vlastnost, aby se nástroj blokovat pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="ee45c-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="ee45c-150">Zprostředkovatelé pověření MSBuild.exe a V2</span><span class="sxs-lookup"><span data-stu-id="ee45c-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="ee45c-151">V aktualizaci Visual Studio 2019 Update 9, NuGet definován mechanismus modulu plug-in ověřování, který funguje ve všech klientech.</span><span class="sxs-lookup"><span data-stu-id="ee45c-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="ee45c-152">Instalace a zjišťování těchto poskytovatelů naleznete [v nugetských zásuvných modulech pro různé platformy](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="ee45c-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="ee45c-153">Dostupní zprostředkovatelé pověření pro soubor MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="ee45c-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="ee45c-154">Zprostředkovatel přihlašovacích údajů artefaktů Azure</span><span class="sxs-lookup"><span data-stu-id="ee45c-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="ee45c-155">S Visual Studio 2017 Update 9 a novější, Azure DevOps poskytovatel přihlašovacích údajů je součástí Sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee45c-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="ee45c-156">Nejsou vyžadovány žádné další kroky.</span><span class="sxs-lookup"><span data-stu-id="ee45c-156">No additional steps are required.</span></span>
