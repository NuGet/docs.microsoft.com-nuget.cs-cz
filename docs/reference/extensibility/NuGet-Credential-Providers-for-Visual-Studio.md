---
title: Poskytovatelé přihlašovacích údajů NuGetu pro Visual Studio
description: Poskytovatelé přihlašovacích údajů NuGet ověřují pomocí kanálů implementaci rozhraní IVsCredentialProvider v rozšíření sady Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 906d07eb22599eb423b00300954ff2601dd33369
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383548"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="542c2-103">Ověřování informačních kanálů v aplikaci Visual Studio s poskytovateli přihlašovacích údajů NuGet</span><span class="sxs-lookup"><span data-stu-id="542c2-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="542c2-104">Rozšíření NuGet pro Visual Studio Extensions 3.6 + podporuje poskytovatele přihlašovacích údajů, což umožňuje, aby NuGet fungoval s ověřenými informačními kanály.</span><span class="sxs-lookup"><span data-stu-id="542c2-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="542c2-105">Po instalaci poskytovatele pověření NuGet pro Visual Studio rozšíření NuGet sady Visual Studio automaticky získá a obnoví přihlašovací údaje pro ověřené informační kanály podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="542c2-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="542c2-106">Ukázkovou implementaci najdete v [ukázce VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="542c2-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="542c2-107">Počínaje verzí 4,8 + NuGet v aplikaci Visual Studio je také podporováno nové moduly plug-in pro ověřování různých platforem, ale nejedná se o doporučený postup z hlediska výkonu.</span><span class="sxs-lookup"><span data-stu-id="542c2-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="542c2-108">Zprostředkovatelé pověření NuGet pro Visual Studio musí být nainstalováni jako běžné rozšíření sady Visual Studio a budou potřebovat [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="542c2-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="542c2-109">Zprostředkovatelé pověření NuGet pro Visual Studio fungují jenom v aplikaci Visual Studio (ne v dotnet restore nebo NuGet. exe).</span><span class="sxs-lookup"><span data-stu-id="542c2-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="542c2-110">Zprostředkovatele přihlašovacích údajů pomocí NuGet. exe najdete v tématu [poskytovatelé přihlašovacích údajů NuGet. exe](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="542c2-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="542c2-111">Pro poskytovatele přihlašovacích údajů v dotnet a MSBuild si přečtěte modul [Plug-in pro různé platformy](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="542c2-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="542c2-112">K dispozici poskytovatelé pověření NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="542c2-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="542c2-113">K dispozici je zprostředkovatel přihlašovacích údajů, který je součástí rozšíření NuGet sady Visual Studio pro podporu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="542c2-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="542c2-114">Rozšíření NuGet pro Visual Studio používá interní `VsCredentialProviderImporter`, který také hledá poskytovatele přihlašovacích údajů modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="542c2-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="542c2-115">Tito zprostředkovatelé přihlašovacích údajů modulu plug-in musí být zjistitelní jako export MEF typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="542c2-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="542c2-116">K dispozici jsou poskytovatelé přihlašovacích údajů pro modul plug-in:</span><span class="sxs-lookup"><span data-stu-id="542c2-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="542c2-117">Poskytovatel pověření MyGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="542c2-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="542c2-118">Vytvoření poskytovatele pověření NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="542c2-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="542c2-119">Rozšíření NuGet pro Visual Studio Extension 3.6 + implementuje interní CredentialService, který se používá k získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="542c2-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="542c2-120">CredentialService má seznam integrovaných poskytovatelů přihlašovacích údajů a modulů plug-in.</span><span class="sxs-lookup"><span data-stu-id="542c2-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="542c2-121">Každý poskytovatel se vyzkouší sekvenčně, dokud nebudou získány přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="542c2-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="542c2-122">Během získávání přihlašovacích údajů se služba přihlašovacích údajů pokusí poskytovatele přihlašovacích údajů vyzkoušet v následujícím pořadí a zastavuje se hned po získání přihlašovacích údajů:</span><span class="sxs-lookup"><span data-stu-id="542c2-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="542c2-123">Přihlašovací údaje se načítají z konfiguračních souborů NuGet (pomocí předdefinovaných `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="542c2-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="542c2-124">Pokud je zdroj balíčku na Visual Studio Team Services, použije se `VisualStudioAccountProvider`.</span><span class="sxs-lookup"><span data-stu-id="542c2-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="542c2-125">Všichni ostatní poskytovatelé přihlašovacích údajů sady Visual Studio budou zkoušet postupně.</span><span class="sxs-lookup"><span data-stu-id="542c2-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="542c2-126">Zkuste použít všechna poskytovatele přihlašovacích údajů pro různé platformy NuGet postupně.</span><span class="sxs-lookup"><span data-stu-id="542c2-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="542c2-127">Pokud se zatím nezískaly žádné přihlašovací údaje, zobrazí se uživateli výzva k zadání přihlašovacích údajů v dialogovém okně standardní základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="542c2-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="542c2-128">Implementace IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="542c2-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="542c2-129">Chcete-li vytvořit poskytovatele pověření NuGet pro Visual Studio, vytvořte rozšíření sady Visual Studio, které zveřejňuje veřejný export MEF implementující `IVsCredentialProvider` typ a dodržuje níže uvedené principy.</span><span class="sxs-lookup"><span data-stu-id="542c2-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="542c2-130">Ukázkovou implementaci najdete v [ukázce VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="542c2-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="542c2-131">Každý poskytovatel pověření NuGet pro Visual Studio musí:</span><span class="sxs-lookup"><span data-stu-id="542c2-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="542c2-132">Před zahájením získání přihlašovacích údajů určete, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="542c2-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="542c2-133">Pokud zprostředkovatel nemůže zadat pověření pro cílový zdroj, pak by měl vrátit `null`.</span><span class="sxs-lookup"><span data-stu-id="542c2-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="542c2-134">Pokud zprostředkovatel zpracovává požadavky pro cílový identifikátor URI, ale nemůže zadat přihlašovací údaje, měla by být vyvolána výjimka.</span><span class="sxs-lookup"><span data-stu-id="542c2-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="542c2-135">Vlastní zprostředkovatel pověření NuGet pro Visual Studio musí implementovat rozhraní `IVsCredentialProvider` dostupné v [balíčku NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="542c2-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="542c2-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="542c2-136">GetCredentialAsync</span></span>

| <span data-ttu-id="542c2-137">Vstupní parametr</span><span class="sxs-lookup"><span data-stu-id="542c2-137">Input Parameter</span></span> |<span data-ttu-id="542c2-138">Popis</span><span class="sxs-lookup"><span data-stu-id="542c2-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="542c2-139">Identifikátor URI URI</span><span class="sxs-lookup"><span data-stu-id="542c2-139">Uri uri</span></span> | <span data-ttu-id="542c2-140">Identifikátor URI zdroje balíčku, pro který se vyžadují přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="542c2-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="542c2-141">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="542c2-141">IWebProxy proxy</span></span> | <span data-ttu-id="542c2-142">Webový proxy server, který se má použít při komunikaci v síti.</span><span class="sxs-lookup"><span data-stu-id="542c2-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="542c2-143">Hodnota null, pokud není nakonfigurováno ověřování proxy serverem.</span><span class="sxs-lookup"><span data-stu-id="542c2-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="542c2-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="542c2-144">bool isProxyRequest</span></span> | <span data-ttu-id="542c2-145">Hodnota true, pokud má tento požadavek získat přihlašovací údaje pro ověření proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="542c2-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="542c2-146">Pokud implementace není platná pro získání přihlašovacích údajů proxy serveru, měla by být vrácena hodnota null.</span><span class="sxs-lookup"><span data-stu-id="542c2-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="542c2-147">logická akce</span><span class="sxs-lookup"><span data-stu-id="542c2-147">bool isRetry</span></span> | <span data-ttu-id="542c2-148">True, pokud se pro tento identifikátor URI dřív požadovaly přihlašovací údaje, ale zadané přihlašovací údaje nepovolovaly autorizovaný přístup.</span><span class="sxs-lookup"><span data-stu-id="542c2-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="542c2-149">bool neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="542c2-149">bool nonInteractive</span></span> | <span data-ttu-id="542c2-150">Pokud je hodnota true, poskytovatel pověření musí potlačit všechny výzvy uživatelů a místo toho použít výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="542c2-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="542c2-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="542c2-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="542c2-152">Tento token zrušení by měl být zkontrolován, aby bylo možné zjistit, zda operace požadující přihlašovací údaje byla zrušena.</span><span class="sxs-lookup"><span data-stu-id="542c2-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="542c2-153">**Návratová hodnota**: objekt přihlašovacích údajů implementuje [rozhraní`System.Net.ICredentials`](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="542c2-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
