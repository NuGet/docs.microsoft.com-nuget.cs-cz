---
title: Protokoly nuget.org | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "Měnící nuget.org protokoly pro interakci s klienty NuGet."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="88ab1-103">Protokoly nuget.org</span><span class="sxs-lookup"><span data-stu-id="88ab1-103">nuget.org Protocols</span></span>

<span data-ttu-id="88ab1-104">Pro interakci s nuget.org, klienti musí postupovat podle určité protokoly.</span><span class="sxs-lookup"><span data-stu-id="88ab1-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="88ab1-105">Protože tyto protokoly uchovávat vyvíjejí, klienti musí identifikovat verzi protokolu, které používají při volání metody konkrétní nuget.org rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="88ab1-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="88ab1-106">To umožňuje nuget.org zavádět změny způsobem pevné pro původní klienty.</span><span class="sxs-lookup"><span data-stu-id="88ab1-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="88ab1-107">Rozhraní API popsané na této stránce jsou specifické pro nuget.org a neexistuje žádný očekávání pro jiné implementace NuGet serveru zavádět tato rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="88ab1-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="88ab1-108">Informace o rozhraní API NuGet široce implementována v ekosystému NuGet najdete v tématu [přehled rozhraní API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="88ab1-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="88ab1-109">Toto téma uvádí různé protokoly jako a pokud by byly předány existence.</span><span class="sxs-lookup"><span data-stu-id="88ab1-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="88ab1-110">Verze protokolu NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="88ab1-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="88ab1-111">4.1.0 protokol Určuje použití klíče ověření rozsahu pro interakci s služby než nuget.org se ověřit balíček proti nuget.org účtu.</span><span class="sxs-lookup"><span data-stu-id="88ab1-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="88ab1-112">Všimněte si, že `4.1.0` verze číslo je neprůhledný řetězec, ale se stane, se shoduje s první verzi oficiální klienta NuGet podporovaným tento protokol.</span><span class="sxs-lookup"><span data-stu-id="88ab1-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="88ab1-113">Ověření zajistí, že rozhraní API klíče vytvořené uživatelem se používají pouze s nuget.org a tímto ověřování nebo ověřování z službu třetí strany se zpracovává prostřednictvím jednorázové použití klíče ověření rozsahu.</span><span class="sxs-lookup"><span data-stu-id="88ab1-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="88ab1-114">Tyto klíče ověřte oboru slouží k ověření, že balíček patří do určitého uživatele (účet) v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="88ab1-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="88ab1-115">Požadavek klienta</span><span class="sxs-lookup"><span data-stu-id="88ab1-115">Client requirement</span></span>

<span data-ttu-id="88ab1-116">Klienti jsou potřeba předat následující hlavičku při provádění volání rozhraní API **nabízené** balíčků nuget.org:</span><span class="sxs-lookup"><span data-stu-id="88ab1-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="88ab1-117">Všimněte si, že již existující `X-NuGet-Client-Version` záhlaví má stejný účel, ale je nyní zastaralý a by měl být dále používán.</span><span class="sxs-lookup"><span data-stu-id="88ab1-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="88ab1-118">**Nabízené** samotný protokol je popsána v dokumentaci k [ `PackagePublish` prostředků](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="88ab1-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="88ab1-119">Pokud klient komunikuje s externích služeb a potřebuje k ověření, zda balíček patří do určitého uživatele (účet), měl by se používat protokol následující a používat klíče ověřte oboru a není klíče rozhraní API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="88ab1-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="88ab1-120">Žádost o oboru ověřte klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="88ab1-120">API to request a verify-scope key</span></span>

<span data-ttu-id="88ab1-121">Toto rozhraní API slouží k získání klíče ověřte oboru pro autora nuget.org se ověřit balíček vlastníkem mu.</span><span class="sxs-lookup"><span data-stu-id="88ab1-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="88ab1-122">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="88ab1-122">Request parameters</span></span>

<span data-ttu-id="88ab1-123">Název</span><span class="sxs-lookup"><span data-stu-id="88ab1-123">Name</span></span>           | <span data-ttu-id="88ab1-124">V</span><span class="sxs-lookup"><span data-stu-id="88ab1-124">In</span></span>     | <span data-ttu-id="88ab1-125">Typ</span><span class="sxs-lookup"><span data-stu-id="88ab1-125">Type</span></span>   | <span data-ttu-id="88ab1-126">Požadováno</span><span class="sxs-lookup"><span data-stu-id="88ab1-126">Required</span></span> | <span data-ttu-id="88ab1-127">Poznámky</span><span class="sxs-lookup"><span data-stu-id="88ab1-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="88ab1-128">ID</span><span class="sxs-lookup"><span data-stu-id="88ab1-128">ID</span></span>             | <span data-ttu-id="88ab1-129">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="88ab1-129">URL</span></span>    | <span data-ttu-id="88ab1-130">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ab1-130">string</span></span> | <span data-ttu-id="88ab1-131">Ano</span><span class="sxs-lookup"><span data-stu-id="88ab1-131">yes</span></span>      | <span data-ttu-id="88ab1-132">Balíček identidier, pro které je požadováno ověřte, zda klíč oboru</span><span class="sxs-lookup"><span data-stu-id="88ab1-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="88ab1-133">VERZE</span><span class="sxs-lookup"><span data-stu-id="88ab1-133">VERSION</span></span>        | <span data-ttu-id="88ab1-134">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="88ab1-134">URL</span></span>    | <span data-ttu-id="88ab1-135">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ab1-135">string</span></span> | <span data-ttu-id="88ab1-136">Ne</span><span class="sxs-lookup"><span data-stu-id="88ab1-136">no</span></span>       | <span data-ttu-id="88ab1-137">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="88ab1-137">The package version</span></span>
<span data-ttu-id="88ab1-138">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="88ab1-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="88ab1-139">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="88ab1-139">Header</span></span> | <span data-ttu-id="88ab1-140">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ab1-140">string</span></span> | <span data-ttu-id="88ab1-141">Ano</span><span class="sxs-lookup"><span data-stu-id="88ab1-141">yes</span></span>      | <span data-ttu-id="88ab1-142">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="88ab1-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="88ab1-143">Odpověď</span><span class="sxs-lookup"><span data-stu-id="88ab1-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="88ab1-144">Rozhraní API a ověřte klíč oboru ověřte</span><span class="sxs-lookup"><span data-stu-id="88ab1-144">API to verify the verify scope key</span></span>

<span data-ttu-id="88ab1-145">Toto rozhraní API slouží k ověření oboru ověřte, zda klíč pro vlastníkem nuget.org autora balíčku.</span><span class="sxs-lookup"><span data-stu-id="88ab1-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="88ab1-146">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="88ab1-146">Request parameters</span></span>

<span data-ttu-id="88ab1-147">Název</span><span class="sxs-lookup"><span data-stu-id="88ab1-147">Name</span></span>           | <span data-ttu-id="88ab1-148">V</span><span class="sxs-lookup"><span data-stu-id="88ab1-148">In</span></span>     | <span data-ttu-id="88ab1-149">Typ</span><span class="sxs-lookup"><span data-stu-id="88ab1-149">Type</span></span>   | <span data-ttu-id="88ab1-150">Požadováno</span><span class="sxs-lookup"><span data-stu-id="88ab1-150">Required</span></span> | <span data-ttu-id="88ab1-151">Poznámky</span><span class="sxs-lookup"><span data-stu-id="88ab1-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="88ab1-152">ID</span><span class="sxs-lookup"><span data-stu-id="88ab1-152">ID</span></span>             | <span data-ttu-id="88ab1-153">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="88ab1-153">URL</span></span>    | <span data-ttu-id="88ab1-154">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ab1-154">string</span></span> | <span data-ttu-id="88ab1-155">Ano</span><span class="sxs-lookup"><span data-stu-id="88ab1-155">yes</span></span>      | <span data-ttu-id="88ab1-156">Identifikátor balíčku, jehož klíč oboru ověřte, zda je požadováno</span><span class="sxs-lookup"><span data-stu-id="88ab1-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="88ab1-157">VERZE</span><span class="sxs-lookup"><span data-stu-id="88ab1-157">VERSION</span></span>        | <span data-ttu-id="88ab1-158">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="88ab1-158">URL</span></span>    | <span data-ttu-id="88ab1-159">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ab1-159">string</span></span> | <span data-ttu-id="88ab1-160">Ne</span><span class="sxs-lookup"><span data-stu-id="88ab1-160">no</span></span>       | <span data-ttu-id="88ab1-161">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="88ab1-161">The package version</span></span>
<span data-ttu-id="88ab1-162">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="88ab1-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="88ab1-163">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="88ab1-163">Header</span></span> | <span data-ttu-id="88ab1-164">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="88ab1-164">string</span></span> | <span data-ttu-id="88ab1-165">Ano</span><span class="sxs-lookup"><span data-stu-id="88ab1-165">yes</span></span>      | <span data-ttu-id="88ab1-166">Třeba `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="88ab1-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="88ab1-167">Tento klíč oboru rozhraní API ověřte platnost vyprší v čase za den nebo při prvním použití, cokoliv nastane dříve.</span><span class="sxs-lookup"><span data-stu-id="88ab1-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="88ab1-168">Odpověď</span><span class="sxs-lookup"><span data-stu-id="88ab1-168">Response</span></span>

<span data-ttu-id="88ab1-169">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="88ab1-169">Status Code</span></span> | <span data-ttu-id="88ab1-170">Význam</span><span class="sxs-lookup"><span data-stu-id="88ab1-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="88ab1-171">200</span><span class="sxs-lookup"><span data-stu-id="88ab1-171">200</span></span>         | <span data-ttu-id="88ab1-172">Klíč rozhraní API je platný</span><span class="sxs-lookup"><span data-stu-id="88ab1-172">The API key is valid</span></span>
<span data-ttu-id="88ab1-173">403</span><span class="sxs-lookup"><span data-stu-id="88ab1-173">403</span></span>         | <span data-ttu-id="88ab1-174">Klíč rozhraní API je neplatný nebo není autorizovaný k nabízení pro balíček</span><span class="sxs-lookup"><span data-stu-id="88ab1-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="88ab1-175">404</span><span class="sxs-lookup"><span data-stu-id="88ab1-175">404</span></span>         | <span data-ttu-id="88ab1-176">Balíček odkazuje `ID` a `VERSION` (volitelné) neexistuje</span><span class="sxs-lookup"><span data-stu-id="88ab1-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
