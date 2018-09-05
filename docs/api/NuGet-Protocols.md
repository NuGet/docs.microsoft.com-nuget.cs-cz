---
title: Protokoly nuget.org
description: Rozvíjející protokoly nuget.org k interakci s klienty NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547270"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="14062-103">protokoly nuget.org</span><span class="sxs-lookup"><span data-stu-id="14062-103">nuget.org protocols</span></span>

<span data-ttu-id="14062-104">K interakci s nuget.org, klienti musí použít některé protokoly.</span><span class="sxs-lookup"><span data-stu-id="14062-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="14062-105">Protože tyto protokoly umožní mít vznikající, musí klienti určují verzi protokolu, které používají při volání konkrétní nuget.org rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="14062-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="14062-106">To umožňuje nuget.org zavedení změn způsobem pevné pro staré klienty.</span><span class="sxs-lookup"><span data-stu-id="14062-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="14062-107">Rozhraní API popsané na této stránce jsou specifické pro nuget.org a neexistuje žádná očekávání pro jiné implementace NuGet server k zavedení těchto rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="14062-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="14062-108">Informace o rozhraní API NuGet široce implementované v ekosystému NuGet, najdete v článku [přehled rozhraní API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="14062-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="14062-109">Toto téma obsahuje seznam různých protokolů jako a pokud by byly předány existence.</span><span class="sxs-lookup"><span data-stu-id="14062-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="14062-110">NuGet protocol verze 4.1.0</span><span class="sxs-lookup"><span data-stu-id="14062-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="14062-111">4.1.0 protokol Určuje použití klíče ověření rozsahu pro interakci s jinými službami než nuget.org se ověřit balíček proti účtu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="14062-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="14062-112">Všimněte si, že `4.1.0` verze číslo, které je neprůhledný řetězec, ale se stane se shoduje s první verzi oficiální klienta NuGet, který nepodporuje tento protokol.</span><span class="sxs-lookup"><span data-stu-id="14062-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="14062-113">Ověření zajistí, že klíče rozhraní API vytvořené uživatelem se používají pouze s nuget.org a tohoto ověření nebo ověřovací služby třetích stran probíhá prostřednictvím funkce klíče ověření oboru jedno použití.</span><span class="sxs-lookup"><span data-stu-id="14062-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="14062-114">Tyto klíče ověření oboru slouží k ověření, že balíček patří do určitého uživatele (účet) na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="14062-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="14062-115">Požadavek klienta</span><span class="sxs-lookup"><span data-stu-id="14062-115">Client requirement</span></span>

<span data-ttu-id="14062-116">Klientů je potřeba předat následující záhlaví při provádění volání rozhraní API **nabízených** balíčků na nuget.org:</span><span class="sxs-lookup"><span data-stu-id="14062-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="14062-117">Všimněte si, `X-NuGet-Client-Version` má podobnou sémantiku jako záhlaví, ale je vyhrazen pouze použije oficiální klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="14062-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="14062-118">Třetí strany klienti měli používat `X-NuGet-Protocol-Version` hlavičku a hodnotu.</span><span class="sxs-lookup"><span data-stu-id="14062-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="14062-119">**Nabízených** samotný protokol je popsán v dokumentaci k [ `PackagePublish` prostředků](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="14062-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="14062-120">Pokud klient komunikuje s externími službami a je potřeba ověřit, jestli balíček patří do určitého uživatele (účet), měl by používat následující protokol a ověřte, zda rozsah klíčů a ne klíče rozhraní API z webu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="14062-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="14062-121">Rozhraní API pro požádat o klíč ověřte, zda rozsah</span><span class="sxs-lookup"><span data-stu-id="14062-121">API to request a verify-scope key</span></span>

<span data-ttu-id="14062-122">Toto rozhraní API slouží k získání klíče ověřte obor autora nuget.org se ověřit balíček vlastněné neúčtuje.</span><span class="sxs-lookup"><span data-stu-id="14062-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="14062-123">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="14062-123">Request parameters</span></span>

<span data-ttu-id="14062-124">Název</span><span class="sxs-lookup"><span data-stu-id="14062-124">Name</span></span>           | <span data-ttu-id="14062-125">V</span><span class="sxs-lookup"><span data-stu-id="14062-125">In</span></span>     | <span data-ttu-id="14062-126">Typ</span><span class="sxs-lookup"><span data-stu-id="14062-126">Type</span></span>   | <span data-ttu-id="14062-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="14062-127">Required</span></span> | <span data-ttu-id="14062-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="14062-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="14062-129">ID</span><span class="sxs-lookup"><span data-stu-id="14062-129">ID</span></span>             | <span data-ttu-id="14062-130">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="14062-130">URL</span></span>    | <span data-ttu-id="14062-131">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="14062-131">string</span></span> | <span data-ttu-id="14062-132">Ano</span><span class="sxs-lookup"><span data-stu-id="14062-132">yes</span></span>      | <span data-ttu-id="14062-133">Balíček identidier, pro kterou je požadována klíč oboru ověřte</span><span class="sxs-lookup"><span data-stu-id="14062-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="14062-134">VERZE</span><span class="sxs-lookup"><span data-stu-id="14062-134">VERSION</span></span>        | <span data-ttu-id="14062-135">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="14062-135">URL</span></span>    | <span data-ttu-id="14062-136">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="14062-136">string</span></span> | <span data-ttu-id="14062-137">Ne</span><span class="sxs-lookup"><span data-stu-id="14062-137">no</span></span>       | <span data-ttu-id="14062-138">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="14062-138">The package version</span></span>
<span data-ttu-id="14062-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="14062-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="14062-140">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="14062-140">Header</span></span> | <span data-ttu-id="14062-141">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="14062-141">string</span></span> | <span data-ttu-id="14062-142">Ano</span><span class="sxs-lookup"><span data-stu-id="14062-142">yes</span></span>      | <span data-ttu-id="14062-143">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="14062-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="14062-144">Odpověď</span><span class="sxs-lookup"><span data-stu-id="14062-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="14062-145">Rozhraní API pro ověření klíče ověřte, zda rozsah</span><span class="sxs-lookup"><span data-stu-id="14062-145">API to verify the verify scope key</span></span>

<span data-ttu-id="14062-146">Toto rozhraní API slouží k ověření ověřte, zda rozsah klíč pro vlastní nuget.org Autor balíčku.</span><span class="sxs-lookup"><span data-stu-id="14062-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="14062-147">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="14062-147">Request parameters</span></span>

<span data-ttu-id="14062-148">Název</span><span class="sxs-lookup"><span data-stu-id="14062-148">Name</span></span>           | <span data-ttu-id="14062-149">V</span><span class="sxs-lookup"><span data-stu-id="14062-149">In</span></span>     | <span data-ttu-id="14062-150">Typ</span><span class="sxs-lookup"><span data-stu-id="14062-150">Type</span></span>   | <span data-ttu-id="14062-151">Požadováno</span><span class="sxs-lookup"><span data-stu-id="14062-151">Required</span></span> | <span data-ttu-id="14062-152">Poznámky</span><span class="sxs-lookup"><span data-stu-id="14062-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="14062-153">ID</span><span class="sxs-lookup"><span data-stu-id="14062-153">ID</span></span>             | <span data-ttu-id="14062-154">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="14062-154">URL</span></span>    | <span data-ttu-id="14062-155">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="14062-155">string</span></span> | <span data-ttu-id="14062-156">Ano</span><span class="sxs-lookup"><span data-stu-id="14062-156">yes</span></span>      | <span data-ttu-id="14062-157">Identifikátor balíčku, pro kterou je požadována klíč oboru ověřte</span><span class="sxs-lookup"><span data-stu-id="14062-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="14062-158">VERZE</span><span class="sxs-lookup"><span data-stu-id="14062-158">VERSION</span></span>        | <span data-ttu-id="14062-159">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="14062-159">URL</span></span>    | <span data-ttu-id="14062-160">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="14062-160">string</span></span> | <span data-ttu-id="14062-161">Ne</span><span class="sxs-lookup"><span data-stu-id="14062-161">no</span></span>       | <span data-ttu-id="14062-162">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="14062-162">The package version</span></span>
<span data-ttu-id="14062-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="14062-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="14062-164">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="14062-164">Header</span></span> | <span data-ttu-id="14062-165">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="14062-165">string</span></span> | <span data-ttu-id="14062-166">Ano</span><span class="sxs-lookup"><span data-stu-id="14062-166">yes</span></span>      | <span data-ttu-id="14062-167">Třeba `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="14062-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="14062-168">Tento klíč rozhraní API oboru ověřte, zda vypršení platnosti v čase za den nebo při prvním použití podle toho, co nastane dříve.</span><span class="sxs-lookup"><span data-stu-id="14062-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="14062-169">Odpověď</span><span class="sxs-lookup"><span data-stu-id="14062-169">Response</span></span>

<span data-ttu-id="14062-170">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="14062-170">Status Code</span></span> | <span data-ttu-id="14062-171">Význam</span><span class="sxs-lookup"><span data-stu-id="14062-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="14062-172">200</span><span class="sxs-lookup"><span data-stu-id="14062-172">200</span></span>         | <span data-ttu-id="14062-173">Klíč rozhraní API je platný</span><span class="sxs-lookup"><span data-stu-id="14062-173">The API key is valid</span></span>
<span data-ttu-id="14062-174">403</span><span class="sxs-lookup"><span data-stu-id="14062-174">403</span></span>         | <span data-ttu-id="14062-175">Klíč rozhraní API je neplatný nebo není povoleno push pro balíček</span><span class="sxs-lookup"><span data-stu-id="14062-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="14062-176">404</span><span class="sxs-lookup"><span data-stu-id="14062-176">404</span></span>         | <span data-ttu-id="14062-177">Balíček odkazuje `ID` a `VERSION` (volitelné) neexistuje</span><span class="sxs-lookup"><span data-stu-id="14062-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
