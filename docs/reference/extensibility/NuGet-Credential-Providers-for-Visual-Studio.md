---
title: Poskytovatelé přihlašovacích údajů NuGetu pro Visual Studio
description: Poskytovatelé přihlašovacích údajů NuGet ověřují pomocí kanálů implementaci rozhraní IVsCredentialProvider v rozšíření sady Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f324f1e27e0d718571525152fcf16b55b900dbaa
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777762"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="d029e-103">Ověřování informačních kanálů v aplikaci Visual Studio s poskytovateli přihlašovacích údajů NuGet</span><span class="sxs-lookup"><span data-stu-id="d029e-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="d029e-104">Rozšíření NuGet pro Visual Studio Extensions 3.6 + podporuje poskytovatele přihlašovacích údajů, což umožňuje, aby NuGet fungoval s ověřenými informačními kanály.</span><span class="sxs-lookup"><span data-stu-id="d029e-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="d029e-105">Po instalaci poskytovatele pověření NuGet pro Visual Studio rozšíření NuGet sady Visual Studio automaticky získá a obnoví přihlašovací údaje pro ověřené informační kanály podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="d029e-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="d029e-106">Ukázkovou implementaci najdete v [ukázce VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="d029e-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="d029e-107">V sadě Visual Studio NuGet používá interní, `VsCredentialProviderImporter` který také hledá poskytovatele přihlašovacích údajů modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="d029e-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="d029e-108">Tito zprostředkovatelé přihlašovacích údajů modulu plug-in musí být zjistitelní jako export MEF typu `IVsCredentialProvider` .</span><span class="sxs-lookup"><span data-stu-id="d029e-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="d029e-109">Počínaje verzí 4,8 + NuGet v aplikaci Visual Studio je také podporováno nové moduly plug-in pro ověřování různých platforem, ale nejedná se o doporučený postup z hlediska výkonu.</span><span class="sxs-lookup"><span data-stu-id="d029e-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="d029e-110">Zprostředkovatelé pověření NuGet pro Visual Studio musí být nainstalováni jako běžné rozšíření sady Visual Studio a budou potřebovat [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="d029e-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="d029e-111">Zprostředkovatelé pověření NuGet pro Visual Studio fungují pouze v aplikaci Visual Studio (ne v dotnet restore nebo nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="d029e-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="d029e-112">Pro poskytovatele přihlašovacích údajů s nuget.exe si přečtěte téma [nuget.exe poskytovatelé přihlašovacích údajů](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="d029e-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="d029e-113">Pro poskytovatele přihlašovacích údajů v dotnet a MSBuild si přečtěte modul [Plug-in pro různé platformy](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="d029e-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="d029e-114">Vytvoření poskytovatele pověření NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d029e-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="d029e-115">Rozšíření NuGet pro Visual Studio Extension 3.6 + implementuje interní CredentialService, který se používá k získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="d029e-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="d029e-116">CredentialService má seznam integrovaných poskytovatelů přihlašovacích údajů a modulů plug-in.</span><span class="sxs-lookup"><span data-stu-id="d029e-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="d029e-117">Každý poskytovatel se vyzkouší sekvenčně, dokud nebudou získány přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="d029e-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="d029e-118">Během získávání přihlašovacích údajů se služba přihlašovacích údajů pokusí poskytovatele přihlašovacích údajů vyzkoušet v následujícím pořadí a zastavuje se hned po získání přihlašovacích údajů:</span><span class="sxs-lookup"><span data-stu-id="d029e-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="d029e-119">Přihlašovací údaje se načítají z konfiguračních souborů NuGet (pomocí předdefinovaných `SettingsCredentialProvider` ).</span><span class="sxs-lookup"><span data-stu-id="d029e-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="d029e-120">Pokud je zdroj balíčku v Visual Studio Team Services, `VisualStudioAccountProvider` bude použit.</span><span class="sxs-lookup"><span data-stu-id="d029e-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="d029e-121">Všichni ostatní poskytovatelé přihlašovacích údajů sady Visual Studio budou zkoušet postupně.</span><span class="sxs-lookup"><span data-stu-id="d029e-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="d029e-122">Zkuste použít všechna poskytovatele přihlašovacích údajů pro různé platformy NuGet postupně.</span><span class="sxs-lookup"><span data-stu-id="d029e-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="d029e-123">Pokud se zatím nezískaly žádné přihlašovací údaje, zobrazí se uživateli výzva k zadání přihlašovacích údajů v dialogovém okně standardní základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="d029e-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="d029e-124">Implementace IVsCredentialProvider. GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="d029e-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="d029e-125">Chcete-li vytvořit poskytovatele pověření NuGet pro Visual Studio, vytvořte rozšíření sady Visual Studio, které zveřejňuje veřejný export MEF implementující `IVsCredentialProvider` typ a dodržuje níže uvedené principy.</span><span class="sxs-lookup"><span data-stu-id="d029e-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="d029e-126">Ukázkovou implementaci najdete v [ukázce VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="d029e-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="d029e-127">Každý poskytovatel pověření NuGet pro Visual Studio musí:</span><span class="sxs-lookup"><span data-stu-id="d029e-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="d029e-128">Před zahájením získání přihlašovacích údajů určete, jestli může poskytnout přihlašovací údaje pro cílový identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="d029e-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="d029e-129">Pokud zprostředkovatel nemůže zadat přihlašovací údaje pro cílový zdroj, pak by měl vrátit `null` .</span><span class="sxs-lookup"><span data-stu-id="d029e-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="d029e-130">Pokud zprostředkovatel zpracovává požadavky pro cílový identifikátor URI, ale nemůže zadat přihlašovací údaje, měla by být vyvolána výjimka.</span><span class="sxs-lookup"><span data-stu-id="d029e-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="d029e-131">Vlastní zprostředkovatel pověření NuGet pro Visual Studio musí implementovat `IVsCredentialProvider` rozhraní dostupné v [balíčku NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="d029e-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="d029e-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="d029e-132">GetCredentialAsync</span></span>

| <span data-ttu-id="d029e-133">Vstupní parametr</span><span class="sxs-lookup"><span data-stu-id="d029e-133">Input Parameter</span></span> |<span data-ttu-id="d029e-134">Popis</span><span class="sxs-lookup"><span data-stu-id="d029e-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="d029e-135">Identifikátor URI URI</span><span class="sxs-lookup"><span data-stu-id="d029e-135">Uri uri</span></span> | <span data-ttu-id="d029e-136">Identifikátor URI zdroje balíčku, pro který se vyžadují přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="d029e-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="d029e-137">Proxy IWebProxy</span><span class="sxs-lookup"><span data-stu-id="d029e-137">IWebProxy proxy</span></span> | <span data-ttu-id="d029e-138">Webový proxy server, který se má použít při komunikaci v síti.</span><span class="sxs-lookup"><span data-stu-id="d029e-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="d029e-139">Hodnota null, pokud není nakonfigurováno ověřování proxy serverem.</span><span class="sxs-lookup"><span data-stu-id="d029e-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="d029e-140">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="d029e-140">bool isProxyRequest</span></span> | <span data-ttu-id="d029e-141">Hodnota true, pokud má tento požadavek získat přihlašovací údaje pro ověření proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="d029e-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="d029e-142">Pokud implementace není platná pro získání přihlašovacích údajů proxy serveru, měla by být vrácena hodnota null.</span><span class="sxs-lookup"><span data-stu-id="d029e-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="d029e-143">logická akce</span><span class="sxs-lookup"><span data-stu-id="d029e-143">bool isRetry</span></span> | <span data-ttu-id="d029e-144">True, pokud se pro tento identifikátor URI dřív požadovaly přihlašovací údaje, ale zadané přihlašovací údaje nepovolovaly autorizovaný přístup.</span><span class="sxs-lookup"><span data-stu-id="d029e-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="d029e-145">bool neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="d029e-145">bool nonInteractive</span></span> | <span data-ttu-id="d029e-146">Pokud je hodnota true, poskytovatel pověření musí potlačit všechny výzvy uživatelů a místo toho použít výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="d029e-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="d029e-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="d029e-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="d029e-148">Tento token zrušení by měl být zkontrolován, aby bylo možné zjistit, zda operace požadující přihlašovací údaje byla zrušena.</span><span class="sxs-lookup"><span data-stu-id="d029e-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="d029e-149">**Návratová hodnota**: objekt přihlašovacích údajů implementující [ `System.Net.ICredentials` rozhraní](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="d029e-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
