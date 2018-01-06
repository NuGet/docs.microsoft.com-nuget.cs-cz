---
title: "Poskytovatelé přihlašovacích údajů NuGet pro Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "Poskytovatelé přihlašovacích údajů NuGet ověřit pomocí informačních kanálů implementací rozhraní IVsCredentialProvider v rozšíření sady Visual Studio."
keywords: "Poskytovatelé přihlašovacích údajů NuGet, ověřování pomocí informačního kanálu, ověřování pomocí Galerie rozšíření NuGet sady visual studio"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d7360205387d4813f95560018e2ac68f71f5603
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="15444-104">Ověřování informační kanály v sadě Visual Studio s poskytovatelé přihlašovacích údajů NuGet</span><span class="sxs-lookup"><span data-stu-id="15444-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="15444-105">Rozšíření NuGet Visual Studio 3.6 + podporuje poskytovatelé přihlašovacích údajů, které umožňují NuGet pro práci s ověřené kanály.</span><span class="sxs-lookup"><span data-stu-id="15444-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="15444-106">Po instalaci poskytovatele přihlašovacích údajů NuGet pro Visual Studio rozšíření NuGet sady Visual Studio automaticky získat a aktualizujte přihlašovací údaje pro ověřený kanály podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="15444-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="15444-107">Ukázka implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="15444-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="15444-108">Poskytovatelé přihlašovacích údajů NuGet pro Visual Studio musí být nainstalován jako regulární rozšíření sady Visual Studio a bude vyžadovat [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (aktuálně ve verzi preview) nebo novější.</span><span class="sxs-lookup"><span data-stu-id="15444-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="15444-109">Poskytovatelé přihlašovacích údajů NuGet pro Visual Studio fungovat pouze v sadě Visual Studio (ne ve dotnet obnovení nebo nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="15444-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="15444-110">Poskytovatelé přihlašovacích údajů s nuget.exe, najdete v části [nuget.exe poskytovatelé přihlašovacích údajů](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="15444-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="15444-111">K dispozici poskytovatelé přihlašovacích údajů NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15444-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="15444-112">Není součástí rozšíření Visual Studio NuGet poskytovatele přihlašovacích údajů pro podporu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="15444-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="15444-113">Rozšíření NuGet Visual Studio používá interní `VsCredentialProviderImporter` které také hledá poskytovatelé přihlašovacích údajů modulu plug-in.</span><span class="sxs-lookup"><span data-stu-id="15444-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="15444-114">Tyto přihlašovací údaje modul plug-in zprostředkovatele musí být zjistitelný jako Export rozhraní MEF typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="15444-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="15444-115">Poskytovatelé přihlašovacích údajů k dispozici modul plug-in patří:</span><span class="sxs-lookup"><span data-stu-id="15444-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="15444-116">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="15444-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="15444-117">Vytvoření zprostředkovatele pověření NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="15444-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="15444-118">Rozšíření NuGet Visual Studio 3.6 + implementuje interní CredentialService, který slouží k získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="15444-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="15444-119">CredentialService má seznam zprostředkovatelů předdefinované a modul plugin přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="15444-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="15444-120">Dokud se získal přihlašovací údaje, zkusí se každý poskytovatel postupně.</span><span class="sxs-lookup"><span data-stu-id="15444-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="15444-121">Během získávání přihlašovacích údajů službu přihlašovacích údajů se pokusí poskytovatelé přihlašovacích údajů v uvedeném pořadí, zastavení, jakmile jsou získat přihlašovací údaje:</span><span class="sxs-lookup"><span data-stu-id="15444-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="15444-122">Přihlašovací údaje budou načtena z NuGet konfigurační soubory (pomocí integrovaných `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="15444-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="15444-123">Pokud je zdroj balíčku na Visual Studio Team Services, `VisualStudioAccountProvider` se použije.</span><span class="sxs-lookup"><span data-stu-id="15444-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="15444-124">Všichni ostatní poskytovatelé přihlašovacích údajů modulu plug-in vyzkouší se postupně.</span><span class="sxs-lookup"><span data-stu-id="15444-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="15444-125">Pokud bylo získáno žádné přihlašovací údaje ještě uživatel vyzve k zadání pověření v dialogu standardní základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="15444-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="15444-126">Implementace IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="15444-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="15444-127">Chcete-li vytvořit poskytovatele přihlašovacích údajů NuGet pro Visual Studio, vytvořte rozšíření Visual Studio, který zveřejňuje veřejné Export rozhraní MEF implementace `IVsCredentialProvider` typ a dodržuje zásady uvedených níže.</span><span class="sxs-lookup"><span data-stu-id="15444-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="15444-128">Ukázka implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="15444-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="15444-129">Musí být každý poskytovatel pověření NuGet pro Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="15444-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="15444-130">Určí, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="15444-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="15444-131">Pokud zprostředkovatele nelze zadat přihlašovací údaje pro cílové zdroj, pak by měla vrátit `null`.</span><span class="sxs-lookup"><span data-stu-id="15444-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="15444-132">Pokud zprostředkovatel zpracovávat požadavky pro cílový identifikátor URI, ale nelze zadat přihlašovací údaje, by měl být vyvolána výjimka.</span><span class="sxs-lookup"><span data-stu-id="15444-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="15444-133">Vlastní poskytovatel pověření NuGet pro Visual Studio musí implementovat `IVsCredentialProvider` rozhraní, které jsou k dispozici v [NuGet.VisualStudio balíček](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="15444-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="15444-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="15444-134">GetCredentialAsync</span></span>

| <span data-ttu-id="15444-135">Vstupní parametr</span><span class="sxs-lookup"><span data-stu-id="15444-135">Input Parameter</span></span> |<span data-ttu-id="15444-136">Popis</span><span class="sxs-lookup"><span data-stu-id="15444-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="15444-137">Identifikátor URI uri</span><span class="sxs-lookup"><span data-stu-id="15444-137">Uri uri</span></span> | <span data-ttu-id="15444-138">Zdroj balíčku Uri, pro které se vyžadují přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="15444-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="15444-139">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="15444-139">IWebProxy proxy</span></span> | <span data-ttu-id="15444-140">Webový proxy server pro použití při komunikaci v síti.</span><span class="sxs-lookup"><span data-stu-id="15444-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="15444-141">Hodnota Null, pokud neexistuje žádné ověření proxy serverem, který je nakonfigurovaný.</span><span class="sxs-lookup"><span data-stu-id="15444-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="15444-142">BOOL isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="15444-142">bool isProxyRequest</span></span> | <span data-ttu-id="15444-143">Hodnota TRUE, pokud tento požadavek je získat pověření pro ověření proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="15444-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="15444-144">Pokud implementace není platná pro získání přihlašovacích údajů proxy, by měl vrátit hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="15444-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="15444-145">BOOL isRetry</span><span class="sxs-lookup"><span data-stu-id="15444-145">bool isRetry</span></span> | <span data-ttu-id="15444-146">Hodnota TRUE, pokud se přihlašovací údaje byly dříve požadované pro tento identifikátor Uri, ale zadaná pověření neumožňuje autorizovaný přístup.</span><span class="sxs-lookup"><span data-stu-id="15444-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="15444-147">Neinteraktivní BOOL</span><span class="sxs-lookup"><span data-stu-id="15444-147">bool nonInteractive</span></span> | <span data-ttu-id="15444-148">V případě hodnoty true musí poskytovatel pověření potlačit všechny uživatelské výzvy a místo toho použít výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="15444-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="15444-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="15444-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="15444-150">Tento token zrušení kontroly k určení, pokud operace s požadavkem na pověření byla zrušena.</span><span class="sxs-lookup"><span data-stu-id="15444-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="15444-151">**Návratová hodnota**: implementace objektu přihlašovací údaje [ `System.Net.ICredentials` rozhraní](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="15444-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
