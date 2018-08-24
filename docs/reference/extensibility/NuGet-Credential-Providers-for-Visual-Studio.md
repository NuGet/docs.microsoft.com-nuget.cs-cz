---
title: Poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio
description: Poskytovatelé přihlašovacích údajů Nugetu ověření pomocí informačních kanálů prostřednictvím implementace rozhraní IVsCredentialProvider v rozšíření sady Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793900"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="478a7-103">Ověřování informačních kanálů v sadě Visual Studio prostřednictvím poskytovatelé přihlašovacích údajů Nugetu</span><span class="sxs-lookup"><span data-stu-id="478a7-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="478a7-104">Rozšíření NuGet Visual Studio 3.6 + podporuje poskytovatelé přihlašovacích údajů, které umožňují pracovat s ověřenými informačními kanály balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="478a7-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="478a7-105">Po instalaci poskytovatele přihlašovacích údajů NuGet pro Visual Studio rozšíření NuGet sady Visual Studio automaticky načíst a aktualizovat přihlašovací údaje pro ověřené informační kanály podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="478a7-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="478a7-106">Ukázková implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="478a7-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="478a7-107">Počínaje 4.8 + nová multiplatformní ověřování moduly plug-in také podporuje NuGet v sadě Visual Studio, ale nejsou doporučený postup z důvodů výkonu.</span><span class="sxs-lookup"><span data-stu-id="478a7-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="478a7-108">Poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio musí být nainstalován jako rozšíření sady Visual Studio na regulární a bude vyžadovat [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="478a7-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="478a7-109">Poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio fungují pouze v sadě Visual Studio (ne v dotnet restore nebo nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="478a7-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="478a7-110">Poskytovatelé přihlašovacích údajů s nuget.exe, naleznete v tématu [nuget.exe poskytovatelé přihlašovacích údajů](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="478a7-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="478a7-111">Přihlašovací údaje poskytovatelů v dotnet tak pro msbuild naleznete v tématu [NuGet pro různé platformy modulů plug-in](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="478a7-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="478a7-112">K dispozici poskytovatelé přihlašovacích údajů Nugetu pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="478a7-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="478a7-113">Je integrované rozšíření Visual Studio NuGet poskytovatele přihlašovacích údajů pro podporu služby Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="478a7-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="478a7-114">Rozšíření NuGet sady Visual Studio používá interní `VsCredentialProviderImporter` které rovněž vyhledává poskytovatelé modul plugin přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="478a7-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="478a7-115">Tito poskytovatelé přihlašovacích údajů modul plug-in musí být zjistitelné jako Export rozhraní MEF typu `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="478a7-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="478a7-116">Poskytovatelé přihlašovacích údajů k dispozici modul plug-in patří:</span><span class="sxs-lookup"><span data-stu-id="478a7-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="478a7-117">MyGet Credential Provider for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="478a7-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="478a7-118">Vytvoření poskytovatele přihlašovacích údajů NuGet pro Visual Studio</span><span class="sxs-lookup"><span data-stu-id="478a7-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="478a7-119">Rozšíření NuGet Visual Studio 3.6 + implementuje interní CredentialService, který se používá k získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="478a7-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="478a7-120">CredentialService má seznam zprostředkovatelů integrované a modul plugin přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="478a7-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="478a7-121">Dokud se získat přihlašovací údaje, zkusí se každý poskytovatel postupně.</span><span class="sxs-lookup"><span data-stu-id="478a7-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="478a7-122">Při získání přihlašovacích údajů služba přihlašovacích údajů se pokusí poskytovatelé přihlašovacích údajů v uvedeném pořadí, zastavení, jako jsou přihlašovací údaje získat:</span><span class="sxs-lookup"><span data-stu-id="478a7-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="478a7-123">Přihlašovací údaje se načtou z NuGet konfiguračních souborů (použití předdefinované `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="478a7-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="478a7-124">Pokud je zdroj balíčků ve Visual Studio Team Services, `VisualStudioAccountProvider` se použije.</span><span class="sxs-lookup"><span data-stu-id="478a7-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="478a7-125">Všechny ostatní modulu plug-in Visual Studio poskytovatelé přihlašovacích údajů, vyzkouší se postupně.</span><span class="sxs-lookup"><span data-stu-id="478a7-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="478a7-126">Zkuste použít všechny NuGet pro různé platformy poskytovatelé přihlašovacích údajů postupně.</span><span class="sxs-lookup"><span data-stu-id="478a7-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="478a7-127">Pokud žádné přihlašovací údaje získat, ale uživateli zobrazí výzva k zadání přihlašovacích údajů a dialogové okno Standardní základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="478a7-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="478a7-128">Implementace IVsCredentialProvider.GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="478a7-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="478a7-129">Chcete-li vytvořit poskytovatele přihlašovacích údajů NuGet pro Visual Studio, vytvořit rozšíření aplikace Visual Studio, která zveřejňuje veřejné Export rozhraní MEF implementace `IVsCredentialProvider` zadejte a dodržuje zásady uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="478a7-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="478a7-130">Ukázková implementace lze nalézt v [ukázka VsCredentialProvider](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="478a7-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="478a7-131">Každý poskytovatel přihlašovacích údajů NuGet pro Visual Studio musí:</span><span class="sxs-lookup"><span data-stu-id="478a7-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="478a7-132">Určení, zda může poskytnout přihlašovací údaje pro cílový identifikátor URI před zahájením získání přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="478a7-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="478a7-133">Pokud zprostředkovatele nelze zadat přihlašovací údaje pro cílový zdroj, pak by měl vrátit `null`.</span><span class="sxs-lookup"><span data-stu-id="478a7-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="478a7-134">Pokud poskytovatel zpracovávat požadavky pro cílový identifikátor URI, ale nelze zadat přihlašovací údaje, by měl být vyvolána výjimka.</span><span class="sxs-lookup"><span data-stu-id="478a7-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="478a7-135">Musíte implementovat vlastní poskytovatele přihlašovacích údajů NuGet pro Visual Studio `IVsCredentialProvider` rozhraní, které jsou k dispozici v [NuGet.VisualStudio balíčku](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="478a7-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="478a7-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="478a7-136">GetCredentialAsync</span></span>

| <span data-ttu-id="478a7-137">Vstupní parametr</span><span class="sxs-lookup"><span data-stu-id="478a7-137">Input Parameter</span></span> |<span data-ttu-id="478a7-138">Popis</span><span class="sxs-lookup"><span data-stu-id="478a7-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="478a7-139">Identifikátor uri identifikátor URI</span><span class="sxs-lookup"><span data-stu-id="478a7-139">Uri uri</span></span> | <span data-ttu-id="478a7-140">Zdroje balíčku Uri, pro které jsou požadovány přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="478a7-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="478a7-141">Rozhraní IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="478a7-141">IWebProxy proxy</span></span> | <span data-ttu-id="478a7-142">Webový proxy server při komunikaci v síti.</span><span class="sxs-lookup"><span data-stu-id="478a7-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="478a7-143">Hodnota Null, pokud neexistuje žádné ověřování proxy server nakonfigurovaný.</span><span class="sxs-lookup"><span data-stu-id="478a7-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="478a7-144">BOOL isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="478a7-144">bool isProxyRequest</span></span> | <span data-ttu-id="478a7-145">True, pokud je tento požadavek se získat přihlašovací údaje pro ověření proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="478a7-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="478a7-146">Pokud implementace není platná pro získání přihlašovacích údajů proxy serveru, by měla být vrácena hodnota null.</span><span class="sxs-lookup"><span data-stu-id="478a7-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="478a7-147">BOOL isRetry</span><span class="sxs-lookup"><span data-stu-id="478a7-147">bool isRetry</span></span> | <span data-ttu-id="478a7-148">Hodnota TRUE, pokud pověření byla dříve vyžádána tento identifikátor Uri, ale zadaná pověření nepovolil autorizovaný přístup.</span><span class="sxs-lookup"><span data-stu-id="478a7-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="478a7-149">Neinteraktivní BOOL</span><span class="sxs-lookup"><span data-stu-id="478a7-149">bool nonInteractive</span></span> | <span data-ttu-id="478a7-150">Pokud je hodnota true, musí poskytovatele přihlašovacích údajů potlačit všechny uživatelské výzvy a místo toho použijte výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="478a7-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="478a7-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="478a7-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="478a7-152">Tento token zrušení by měl být zkontrolována k určení, pokud žádost o přihlašovací údaje operace byla zrušena.</span><span class="sxs-lookup"><span data-stu-id="478a7-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="478a7-153">**Návratová hodnota**: implementace objektu přihlašovací údaje [ `System.Net.ICredentials` rozhraní](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="478a7-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
