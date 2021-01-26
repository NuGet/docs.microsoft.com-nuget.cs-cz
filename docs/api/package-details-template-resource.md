---
title: Šablona adresy URL s podrobnostmi balíčku, API NuGet
description: Šablona adresa URL podrobností balíčku umožňuje klientům zobrazit v uživatelském rozhraní webový odkaz na další podrobnosti balíčku.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773942"
---
# <a name="package-details-url-template"></a><span data-ttu-id="5c4f6-103">Šablona adresy URL s podrobnostmi balíčku</span><span class="sxs-lookup"><span data-stu-id="5c4f6-103">Package details URL template</span></span>

<span data-ttu-id="5c4f6-104">Je možné, že klient vytvoří adresu URL, kterou může uživatel použít k zobrazení dalších podrobností o balíčku ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="5c4f6-105">To je užitečné, když zdroj balíčku chce zobrazit další informace o balíčku, který se nemusí vejít do rozsahu, který se zobrazí v klientské aplikaci NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="5c4f6-106">Prostředek použitý k vytvoření této adresy URL je prostředek, který se `PackageDetailsUriTemplate` našel v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5c4f6-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5c4f6-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="5c4f6-107">Versioning</span></span>

<span data-ttu-id="5c4f6-108">Použijí se tyto `@type` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="5c4f6-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5c4f6-109">@type osa</span><span class="sxs-lookup"><span data-stu-id="5c4f6-109">@type value</span></span>                     | <span data-ttu-id="5c4f6-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="5c4f6-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="5c4f6-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="5c4f6-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="5c4f6-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="5c4f6-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="5c4f6-113">Šablona adresy URL</span><span class="sxs-lookup"><span data-stu-id="5c4f6-113">URL template</span></span>

<span data-ttu-id="5c4f6-114">Adresa URL následujícího rozhraní API je hodnota `@id` vlastnosti přidružené k jedné z výše uvedených `@type` hodnot prostředků.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5c4f6-115">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="5c4f6-115">HTTP methods</span></span>

<span data-ttu-id="5c4f6-116">I když klient nemá v úmyslu vytvářet požadavky na adresu URL podrobností balíčku jménem uživatele, měla by tato webová stránka podporovat metodu, aby bylo možné `GET` snadno otevřít otevřenou webovou stránku ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="5c4f6-117">Vytvoření adresy URL</span><span class="sxs-lookup"><span data-stu-id="5c4f6-117">Construct the URL</span></span>

<span data-ttu-id="5c4f6-118">Vzhledem k známému ID a verzi balíčku může implementace klienta vytvořit adresu URL používanou pro přístup k webovému rozhraní.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="5c4f6-119">Implementace klienta by měla zobrazit tuto vytvořenou adresu URL (nebo odkaz na odkaz) pro uživatele, který jim umožní otevřít webový prohlížeč na adresu URL a získat další informace o balíčku.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="5c4f6-120">Obsah stránky s podrobnostmi balíčku je určený implementací serveru.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="5c4f6-121">Adresa URL musí být absolutní adresa URL a schéma (protokol) musí být HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="5c4f6-122">Hodnota `@id` v indexu služby je řetězec adresy URL obsahující kteroukoli z následujících zástupných tokenů:</span><span class="sxs-lookup"><span data-stu-id="5c4f6-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="5c4f6-123">Zástupné symboly adresy URL</span><span class="sxs-lookup"><span data-stu-id="5c4f6-123">URL placeholders</span></span>

<span data-ttu-id="5c4f6-124">Název</span><span class="sxs-lookup"><span data-stu-id="5c4f6-124">Name</span></span>        | <span data-ttu-id="5c4f6-125">Typ</span><span class="sxs-lookup"><span data-stu-id="5c4f6-125">Type</span></span>    | <span data-ttu-id="5c4f6-126">Vyžadováno</span><span class="sxs-lookup"><span data-stu-id="5c4f6-126">Required</span></span> | <span data-ttu-id="5c4f6-127">Poznámky</span><span class="sxs-lookup"><span data-stu-id="5c4f6-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="5c4f6-128">řetězec</span><span class="sxs-lookup"><span data-stu-id="5c4f6-128">string</span></span>  | <span data-ttu-id="5c4f6-129">ne</span><span class="sxs-lookup"><span data-stu-id="5c4f6-129">no</span></span>       | <span data-ttu-id="5c4f6-130">ID balíčku, pro který se mají získat podrobnosti</span><span class="sxs-lookup"><span data-stu-id="5c4f6-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="5c4f6-131">řetězec</span><span class="sxs-lookup"><span data-stu-id="5c4f6-131">string</span></span>  | <span data-ttu-id="5c4f6-132">ne</span><span class="sxs-lookup"><span data-stu-id="5c4f6-132">no</span></span>       | <span data-ttu-id="5c4f6-133">Verze balíčku, pro který se mají získat podrobnosti</span><span class="sxs-lookup"><span data-stu-id="5c4f6-133">The package version to get details for</span></span>

<span data-ttu-id="5c4f6-134">Server by měl přijmout `{id}` `{version}` hodnoty a s libovolnými velkými písmeny.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="5c4f6-135">Kromě toho by neměl být server citlivý na to, jestli je verze [normalizovaná](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="5c4f6-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="5c4f6-136">Jinými slovy, server by měl přijímat také nenormalizované verze.</span><span class="sxs-lookup"><span data-stu-id="5c4f6-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="5c4f6-137">Například šablona s podrobnostmi balíčku NuGet. org vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="5c4f6-137">For example, nuget.org's package details template looks like this:</span></span>

```http
https://www.nuget.org/packages/{id}/{version}
```

<span data-ttu-id="5c4f6-138">Pokud implementace klienta potřebuje zobrazit odkaz na podrobnosti balíčku pro NuGet. 4.3.0 správy verzí, vytvoří následující adresu URL a poskytne jí uživateli:</span><span class="sxs-lookup"><span data-stu-id="5c4f6-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
