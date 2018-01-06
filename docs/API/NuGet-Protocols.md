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
ms.openlocfilehash: 0bc71795d120256b9eb14ca64141f0b69f01e620
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="7c49c-103">Protokoly nuget.org</span><span class="sxs-lookup"><span data-stu-id="7c49c-103">nuget.org Protocols</span></span>

<span data-ttu-id="7c49c-104">Pro interakci s nuget.org, klienti musí postupovat podle určité protokoly.</span><span class="sxs-lookup"><span data-stu-id="7c49c-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="7c49c-105">Protože tyto protokoly uchovávat vyvíjejí, klienti musí identifikovat verzi protokolu, které používají při volání metody konkrétní nuget.org rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7c49c-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="7c49c-106">To umožňuje nuget.org zavádět změny způsobem pevné pro původní klienty.</span><span class="sxs-lookup"><span data-stu-id="7c49c-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="7c49c-107">Rozhraní API popsané na této stránce jsou specifické pro nuget.org a neexistuje žádný očekávání pro jiné implementace NuGet serveru zavádět tato rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7c49c-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="7c49c-108">Informace o rozhraní API NuGet široce implementována v ekosystému NuGet najdete v tématu [přehled rozhraní API](overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c49c-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="7c49c-109">Toto téma uvádí různé protokoly jako a pokud by byly předány existence.</span><span class="sxs-lookup"><span data-stu-id="7c49c-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="7c49c-110">Verze protokolu NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="7c49c-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="7c49c-111">4.1.0 protokol Určuje použití klíče ověření rozsahu pro interakci s služby než nuget.org se ověřit balíček proti nuget.org účtu.</span><span class="sxs-lookup"><span data-stu-id="7c49c-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="7c49c-112">Všimněte si, že `4.1.0` verze číslo je neprůhledný řetězec, ale se stane, se shoduje s první verzi oficiální klienta NuGet podporovaným tento protokol.</span><span class="sxs-lookup"><span data-stu-id="7c49c-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="7c49c-113">Ověření zajistí, že rozhraní API klíče vytvořené uživatelem se používají pouze s nuget.org a tímto ověřování nebo ověřování z službu třetí strany se zpracovává prostřednictvím jednorázové použití klíče ověření rozsahu.</span><span class="sxs-lookup"><span data-stu-id="7c49c-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="7c49c-114">Tyto klíče ověřte oboru slouží k ověření, že balíček patří do určitého uživatele (účet) v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7c49c-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="7c49c-115">Požadavek klienta</span><span class="sxs-lookup"><span data-stu-id="7c49c-115">Client requirement</span></span>

<span data-ttu-id="7c49c-116">Klienti jsou potřeba předat následující hlavičku při provádění volání rozhraní API **nabízené** balíčků nuget.org:</span><span class="sxs-lookup"><span data-stu-id="7c49c-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="7c49c-117">Všimněte si, že `X-NuGet-Client-Version` záhlaví má podobnou sémantiku, ale je vyhrazen pouze používat oficiální klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="7c49c-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="7c49c-118">Třetí strany klienti měli používat `X-NuGet-Protocol-Version` hlavičku a hodnotu.</span><span class="sxs-lookup"><span data-stu-id="7c49c-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="7c49c-119">**Nabízené** samotný protokol je popsána v dokumentaci k [ `PackagePublish` prostředků](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7c49c-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="7c49c-120">Pokud klient komunikuje s externích služeb a potřebuje k ověření, zda balíček patří do určitého uživatele (účet), měl by se používat protokol následující a používat klíče ověřte oboru a není klíče rozhraní API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7c49c-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="7c49c-121">Žádost o oboru ověřte klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="7c49c-121">API to request a verify-scope key</span></span>

<span data-ttu-id="7c49c-122">Toto rozhraní API slouží k získání klíče ověřte oboru pro autora nuget.org se ověřit balíček vlastníkem mu.</span><span class="sxs-lookup"><span data-stu-id="7c49c-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="7c49c-123">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="7c49c-123">Request parameters</span></span>

<span data-ttu-id="7c49c-124">Název</span><span class="sxs-lookup"><span data-stu-id="7c49c-124">Name</span></span>           | <span data-ttu-id="7c49c-125">V</span><span class="sxs-lookup"><span data-stu-id="7c49c-125">In</span></span>     | <span data-ttu-id="7c49c-126">Typ</span><span class="sxs-lookup"><span data-stu-id="7c49c-126">Type</span></span>   | <span data-ttu-id="7c49c-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="7c49c-127">Required</span></span> | <span data-ttu-id="7c49c-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7c49c-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="7c49c-129">ID</span><span class="sxs-lookup"><span data-stu-id="7c49c-129">ID</span></span>             | <span data-ttu-id="7c49c-130">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7c49c-130">URL</span></span>    | <span data-ttu-id="7c49c-131">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7c49c-131">string</span></span> | <span data-ttu-id="7c49c-132">Ano</span><span class="sxs-lookup"><span data-stu-id="7c49c-132">yes</span></span>      | <span data-ttu-id="7c49c-133">Balíček identidier, pro které je požadováno ověřte, zda klíč oboru</span><span class="sxs-lookup"><span data-stu-id="7c49c-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="7c49c-134">VERZE</span><span class="sxs-lookup"><span data-stu-id="7c49c-134">VERSION</span></span>        | <span data-ttu-id="7c49c-135">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7c49c-135">URL</span></span>    | <span data-ttu-id="7c49c-136">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7c49c-136">string</span></span> | <span data-ttu-id="7c49c-137">Ne</span><span class="sxs-lookup"><span data-stu-id="7c49c-137">no</span></span>       | <span data-ttu-id="7c49c-138">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="7c49c-138">The package version</span></span>
<span data-ttu-id="7c49c-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7c49c-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7c49c-140">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="7c49c-140">Header</span></span> | <span data-ttu-id="7c49c-141">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7c49c-141">string</span></span> | <span data-ttu-id="7c49c-142">Ano</span><span class="sxs-lookup"><span data-stu-id="7c49c-142">yes</span></span>      | <span data-ttu-id="7c49c-143">Třeba `X-NuGet-ApiKey: {USER_API_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7c49c-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="7c49c-144">Odpověď</span><span class="sxs-lookup"><span data-stu-id="7c49c-144">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="7c49c-145">Rozhraní API a ověřte klíč oboru ověřte</span><span class="sxs-lookup"><span data-stu-id="7c49c-145">API to verify the verify scope key</span></span>

<span data-ttu-id="7c49c-146">Toto rozhraní API slouží k ověření oboru ověřte, zda klíč pro vlastníkem nuget.org autora balíčku.</span><span class="sxs-lookup"><span data-stu-id="7c49c-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="7c49c-147">Parametry žádosti</span><span class="sxs-lookup"><span data-stu-id="7c49c-147">Request parameters</span></span>

<span data-ttu-id="7c49c-148">Název</span><span class="sxs-lookup"><span data-stu-id="7c49c-148">Name</span></span>           | <span data-ttu-id="7c49c-149">V</span><span class="sxs-lookup"><span data-stu-id="7c49c-149">In</span></span>     | <span data-ttu-id="7c49c-150">Typ</span><span class="sxs-lookup"><span data-stu-id="7c49c-150">Type</span></span>   | <span data-ttu-id="7c49c-151">Požadováno</span><span class="sxs-lookup"><span data-stu-id="7c49c-151">Required</span></span> | <span data-ttu-id="7c49c-152">Poznámky</span><span class="sxs-lookup"><span data-stu-id="7c49c-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="7c49c-153">ID</span><span class="sxs-lookup"><span data-stu-id="7c49c-153">ID</span></span>             | <span data-ttu-id="7c49c-154">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7c49c-154">URL</span></span>    | <span data-ttu-id="7c49c-155">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7c49c-155">string</span></span> | <span data-ttu-id="7c49c-156">Ano</span><span class="sxs-lookup"><span data-stu-id="7c49c-156">yes</span></span>      | <span data-ttu-id="7c49c-157">Identifikátor balíčku, jehož klíč oboru ověřte, zda je požadováno</span><span class="sxs-lookup"><span data-stu-id="7c49c-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="7c49c-158">VERZE</span><span class="sxs-lookup"><span data-stu-id="7c49c-158">VERSION</span></span>        | <span data-ttu-id="7c49c-159">Adresa URL</span><span class="sxs-lookup"><span data-stu-id="7c49c-159">URL</span></span>    | <span data-ttu-id="7c49c-160">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7c49c-160">string</span></span> | <span data-ttu-id="7c49c-161">Ne</span><span class="sxs-lookup"><span data-stu-id="7c49c-161">no</span></span>       | <span data-ttu-id="7c49c-162">Verze balíčku</span><span class="sxs-lookup"><span data-stu-id="7c49c-162">The package version</span></span>
<span data-ttu-id="7c49c-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="7c49c-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="7c49c-164">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="7c49c-164">Header</span></span> | <span data-ttu-id="7c49c-165">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="7c49c-165">string</span></span> | <span data-ttu-id="7c49c-166">Ano</span><span class="sxs-lookup"><span data-stu-id="7c49c-166">yes</span></span>      | <span data-ttu-id="7c49c-167">Třeba `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.</span><span class="sxs-lookup"><span data-stu-id="7c49c-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="7c49c-168">Tento klíč oboru rozhraní API ověřte platnost vyprší v čase za den nebo při prvním použití, cokoliv nastane dříve.</span><span class="sxs-lookup"><span data-stu-id="7c49c-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="7c49c-169">Odpověď</span><span class="sxs-lookup"><span data-stu-id="7c49c-169">Response</span></span>

<span data-ttu-id="7c49c-170">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="7c49c-170">Status Code</span></span> | <span data-ttu-id="7c49c-171">Význam</span><span class="sxs-lookup"><span data-stu-id="7c49c-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="7c49c-172">200</span><span class="sxs-lookup"><span data-stu-id="7c49c-172">200</span></span>         | <span data-ttu-id="7c49c-173">Klíč rozhraní API je platný</span><span class="sxs-lookup"><span data-stu-id="7c49c-173">The API key is valid</span></span>
<span data-ttu-id="7c49c-174">403</span><span class="sxs-lookup"><span data-stu-id="7c49c-174">403</span></span>         | <span data-ttu-id="7c49c-175">Klíč rozhraní API je neplatný nebo není autorizovaný k nabízení pro balíček</span><span class="sxs-lookup"><span data-stu-id="7c49c-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="7c49c-176">404</span><span class="sxs-lookup"><span data-stu-id="7c49c-176">404</span></span>         | <span data-ttu-id="7c49c-177">Balíček odkazuje `ID` a `VERSION` (volitelné) neexistuje</span><span class="sxs-lookup"><span data-stu-id="7c49c-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
