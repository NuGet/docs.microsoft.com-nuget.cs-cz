---
title: nuget.org protokoly
description: Vývoj nuget.orgch protokolů pro interakci s klienty NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773968"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="279e7-103">Protokoly nuget.org</span><span class="sxs-lookup"><span data-stu-id="279e7-103">nuget.org protocols</span></span>

<span data-ttu-id="279e7-104">Aby mohli klienti pracovat s nuget.org, musí dodržovat určité protokoly.</span><span class="sxs-lookup"><span data-stu-id="279e7-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="279e7-105">Vzhledem k tomu, že tyto protokoly neustále vyvíjejí vývoj, musí klienti určit verzi protokolu, kterou používají při volání specifických rozhraní nuget.org API.</span><span class="sxs-lookup"><span data-stu-id="279e7-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="279e7-106">To umožňuje nuget.org začlenit změny nevhodným způsobem pro staré klienty.</span><span class="sxs-lookup"><span data-stu-id="279e7-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="279e7-107">Rozhraní API dokumentované na této stránce jsou specifická pro nuget.org a neočekávají se pro zavedení těchto rozhraní API jinými implementacemi serveru NuGet.</span><span class="sxs-lookup"><span data-stu-id="279e7-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="279e7-108">Informace o rozhraní NuGet API implementovaném v celém ekosystému NuGet najdete v tématu [Přehled rozhraní API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="279e7-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="279e7-109">V tomto tématu je uveden seznam různých protokolů, které jsou a kdy existují.</span><span class="sxs-lookup"><span data-stu-id="279e7-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="279e7-110">Verze protokolu NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="279e7-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="279e7-111">Protokol 4.1.0 určuje použití klíčů ověření a rozsahu pro interakci s jinými službami, než je nuget.org, k ověření balíčku proti účtu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="279e7-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="279e7-112">Všimněte si, že `4.1.0` číslo verze je neprůhledný řetězec, ale v případě, že se shoduje s první verzí oficiálního klienta NuGet, který tento protokol podporuje.</span><span class="sxs-lookup"><span data-stu-id="279e7-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="279e7-113">Ověřování zajišťuje, aby se uživatelsky vytvořené klíče rozhraní API používaly jenom s nuget.org a aby se jiné ověřování nebo ověřování od služby třetí strany zpracovalo pomocí klíčů pro ověření platnosti.</span><span class="sxs-lookup"><span data-stu-id="279e7-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="279e7-114">Tyto klíče ověření a rozsahu se dají použít k ověření, že balíček patří ke konkrétnímu uživateli (účtu) v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="279e7-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="279e7-115">Požadavek klienta</span><span class="sxs-lookup"><span data-stu-id="279e7-115">Client requirement</span></span>

<span data-ttu-id="279e7-116">Při volání rozhraní API k **nabízení** balíčků do NuGet.org musí klienti předat následující hlavičku:</span><span class="sxs-lookup"><span data-stu-id="279e7-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="279e7-117">Všimněte si, že `X-NuGet-Client-Version` Hlavička má podobnou sémantiku, ale je vyhrazena jenom pro oficiálního klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="279e7-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="279e7-118">Klienti třetích stran by měli používat `X-NuGet-Protocol-Version` hlavičku a hodnotu.</span><span class="sxs-lookup"><span data-stu-id="279e7-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="279e7-119">Samotný protokol **push** je popsaný v dokumentaci k [ `PackagePublish` prostředku](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="279e7-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="279e7-120">Pokud klient komunikuje s externími službami a potřebuje ověřit, jestli balíček patří konkrétnímu uživateli (účtu), měl by použít následující protokol a použít klíče rozhraní API pro ověření a nikoli klíče rozhraní API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="279e7-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="279e7-121">Rozhraní API pro vyžádání klíče pro kontrolu rozsahu</span><span class="sxs-lookup"><span data-stu-id="279e7-121">API to request a verify-scope key</span></span>

<span data-ttu-id="279e7-122">Toto rozhraní API slouží k získání klíče ověřovacího oboru pro autora nuget.org k ověření balíčku, jehož vlastníkem je.</span><span class="sxs-lookup"><span data-stu-id="279e7-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="279e7-123">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="279e7-123">Request parameters</span></span>

<span data-ttu-id="279e7-124">Name</span><span class="sxs-lookup"><span data-stu-id="279e7-124">Name</span></span>           | <span data-ttu-id="279e7-125">V</span><span class="sxs-lookup"><span data-stu-id="279e7-125">In</span></span>     | <span data-ttu-id="279e7-126">Typ</span><span class="sxs-lookup"><span data-stu-id="279e7-126">Type</span></span>   | <span data-ttu-id="279e7-127">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="279e7-127">Required</span></span> | <span data-ttu-id="279e7-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="279e7-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="279e7-129">ID</span><span class="sxs-lookup"><span data-stu-id="279e7-129">ID</span></span>             | <span data-ttu-id="279e7-130">URL</span><span class="sxs-lookup"><span data-stu-id="279e7-130">URL</span></span>    | <span data-ttu-id="279e7-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="279e7-131">string</span></span> | <span data-ttu-id="279e7-132">ano</span><span class="sxs-lookup"><span data-stu-id="279e7-132">yes</span></span>      | <span data-ttu-id="279e7-133">Identidier balíčku, pro který se požaduje klíč ověření</span><span class="sxs-lookup"><span data-stu-id="279e7-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="279e7-134">VERZE</span><span class="sxs-lookup"><span data-stu-id="279e7-134">VERSION</span></span>        | <span data-ttu-id="279e7-135">URL</span><span class="sxs-lookup"><span data-stu-id="279e7-135">URL</span></span>    | <span data-ttu-id="279e7-136">řetězec</span><span class="sxs-lookup"><span data-stu-id="279e7-136">string</span></span> | <span data-ttu-id="279e7-137">ne</span><span class="sxs-lookup"><span data-stu-id="279e7-137">no</span></span>       | <span data-ttu-id="279e7-138">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="279e7-138">The package version</span></span>
<span data-ttu-id="279e7-139">X-NuGet – ApiKey</span><span class="sxs-lookup"><span data-stu-id="279e7-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="279e7-140">Hlavička</span><span class="sxs-lookup"><span data-stu-id="279e7-140">Header</span></span> | <span data-ttu-id="279e7-141">řetězec</span><span class="sxs-lookup"><span data-stu-id="279e7-141">string</span></span> | <span data-ttu-id="279e7-142">ano</span><span class="sxs-lookup"><span data-stu-id="279e7-142">yes</span></span>      | <span data-ttu-id="279e7-143">Například `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="279e7-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="279e7-144">Odpověď</span><span class="sxs-lookup"><span data-stu-id="279e7-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="279e7-145">Rozhraní API pro ověření klíče oboru ověřování</span><span class="sxs-lookup"><span data-stu-id="279e7-145">API to verify the verify scope key</span></span>

<span data-ttu-id="279e7-146">Toto rozhraní API se používá k ověření klíče ověřovacího oboru pro balíček vlastněné autorem nuget.org.</span><span class="sxs-lookup"><span data-stu-id="279e7-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="279e7-147">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="279e7-147">Request parameters</span></span>

<span data-ttu-id="279e7-148">Name</span><span class="sxs-lookup"><span data-stu-id="279e7-148">Name</span></span>           | <span data-ttu-id="279e7-149">V</span><span class="sxs-lookup"><span data-stu-id="279e7-149">In</span></span>     | <span data-ttu-id="279e7-150">Typ</span><span class="sxs-lookup"><span data-stu-id="279e7-150">Type</span></span>   | <span data-ttu-id="279e7-151">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="279e7-151">Required</span></span> | <span data-ttu-id="279e7-152">Poznámky</span><span class="sxs-lookup"><span data-stu-id="279e7-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="279e7-153">ID</span><span class="sxs-lookup"><span data-stu-id="279e7-153">ID</span></span>             | <span data-ttu-id="279e7-154">URL</span><span class="sxs-lookup"><span data-stu-id="279e7-154">URL</span></span>    | <span data-ttu-id="279e7-155">řetězec</span><span class="sxs-lookup"><span data-stu-id="279e7-155">string</span></span> | <span data-ttu-id="279e7-156">ano</span><span class="sxs-lookup"><span data-stu-id="279e7-156">yes</span></span>      | <span data-ttu-id="279e7-157">Identifikátor balíčku, pro který se požaduje klíč ověření</span><span class="sxs-lookup"><span data-stu-id="279e7-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="279e7-158">VERZE</span><span class="sxs-lookup"><span data-stu-id="279e7-158">VERSION</span></span>        | <span data-ttu-id="279e7-159">URL</span><span class="sxs-lookup"><span data-stu-id="279e7-159">URL</span></span>    | <span data-ttu-id="279e7-160">řetězec</span><span class="sxs-lookup"><span data-stu-id="279e7-160">string</span></span> | <span data-ttu-id="279e7-161">ne</span><span class="sxs-lookup"><span data-stu-id="279e7-161">no</span></span>       | <span data-ttu-id="279e7-162">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="279e7-162">The package version</span></span>
<span data-ttu-id="279e7-163">X-NuGet – ApiKey</span><span class="sxs-lookup"><span data-stu-id="279e7-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="279e7-164">Hlavička</span><span class="sxs-lookup"><span data-stu-id="279e7-164">Header</span></span> | <span data-ttu-id="279e7-165">řetězec</span><span class="sxs-lookup"><span data-stu-id="279e7-165">string</span></span> | <span data-ttu-id="279e7-166">ano</span><span class="sxs-lookup"><span data-stu-id="279e7-166">yes</span></span>      | <span data-ttu-id="279e7-167">Například `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="279e7-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="279e7-168">Tento klíč rozhraní API oboru rozhraní API vyprší během dne nebo při prvním použití, podle toho, co nastane dřív.</span><span class="sxs-lookup"><span data-stu-id="279e7-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="279e7-169">Odpověď</span><span class="sxs-lookup"><span data-stu-id="279e7-169">Response</span></span>

<span data-ttu-id="279e7-170">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="279e7-170">Status Code</span></span> | <span data-ttu-id="279e7-171">Význam</span><span class="sxs-lookup"><span data-stu-id="279e7-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="279e7-172">200</span><span class="sxs-lookup"><span data-stu-id="279e7-172">200</span></span>         | <span data-ttu-id="279e7-173">Klíč rozhraní API je platný.</span><span class="sxs-lookup"><span data-stu-id="279e7-173">The API key is valid</span></span>
<span data-ttu-id="279e7-174">403</span><span class="sxs-lookup"><span data-stu-id="279e7-174">403</span></span>         | <span data-ttu-id="279e7-175">Klíč rozhraní API je neplatný nebo nemá oprávnění k vložení do balíčku.</span><span class="sxs-lookup"><span data-stu-id="279e7-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="279e7-176">404</span><span class="sxs-lookup"><span data-stu-id="279e7-176">404</span></span>         | <span data-ttu-id="279e7-177">Balíček, na který odkazuje `ID` a `VERSION` (volitelné), neexistuje.</span><span class="sxs-lookup"><span data-stu-id="279e7-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
