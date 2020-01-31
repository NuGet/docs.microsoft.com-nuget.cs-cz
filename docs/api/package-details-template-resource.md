---
title: Šablona adresy URL s podrobnostmi balíčku, API NuGet
description: Šablona adresa URL podrobností balíčku umožňuje klientům zobrazit v uživatelském rozhraní webový odkaz na další podrobnosti balíčku.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812932"
---
# <a name="package-details-url-template"></a><span data-ttu-id="49dfb-103">Šablona adresy URL s podrobnostmi balíčku</span><span class="sxs-lookup"><span data-stu-id="49dfb-103">Package details URL template</span></span>

<span data-ttu-id="49dfb-104">Je možné, že klient vytvoří adresu URL, kterou může uživatel použít k zobrazení dalších podrobností o balíčku ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="49dfb-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="49dfb-105">To je užitečné, když zdroj balíčku chce zobrazit další informace o balíčku, který se nemusí vejít do rozsahu, který se zobrazí v klientské aplikaci NuGet.</span><span class="sxs-lookup"><span data-stu-id="49dfb-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="49dfb-106">Prostředek použitý k vytvoření této adresy URL je prostředek `PackageDetailsUriTemplate`, který se našel v [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="49dfb-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="49dfb-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="49dfb-107">Versioning</span></span>

<span data-ttu-id="49dfb-108">Použijí se následující hodnoty `@type`:</span><span class="sxs-lookup"><span data-stu-id="49dfb-108">The following `@type` values are used:</span></span>

<span data-ttu-id="49dfb-109">hodnota @type</span><span class="sxs-lookup"><span data-stu-id="49dfb-109">@type value</span></span>                     | <span data-ttu-id="49dfb-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="49dfb-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="49dfb-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="49dfb-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="49dfb-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="49dfb-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="49dfb-113">Šablona adresy URL</span><span class="sxs-lookup"><span data-stu-id="49dfb-113">URL template</span></span>

<span data-ttu-id="49dfb-114">Adresa URL následujícího rozhraní API je hodnota vlastnosti `@id` přidružená k jedné z výše uvedených `@type` hodnot prostředku.</span><span class="sxs-lookup"><span data-stu-id="49dfb-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="49dfb-115">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="49dfb-115">HTTP methods</span></span>

<span data-ttu-id="49dfb-116">I když klient nemá v úmyslu vytvářet požadavky na adresu URL podrobností balíčku jménem uživatele, měla by webová stránka podporovat metodu `GET`, aby bylo možné snadno otevřít otevřenou adresu URL ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="49dfb-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="49dfb-117">Vytvoření adresy URL</span><span class="sxs-lookup"><span data-stu-id="49dfb-117">Construct the URL</span></span>

<span data-ttu-id="49dfb-118">Vzhledem k známému ID a verzi balíčku může implementace klienta vytvořit adresu URL používanou pro přístup k webovému rozhraní.</span><span class="sxs-lookup"><span data-stu-id="49dfb-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="49dfb-119">Implementace klienta by měla zobrazit tuto vytvořenou adresu URL (nebo odkaz na odkaz) pro uživatele, který jim umožní otevřít webový prohlížeč na adresu URL a získat další informace o balíčku.</span><span class="sxs-lookup"><span data-stu-id="49dfb-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="49dfb-120">Obsah stránky s podrobnostmi balíčku je určený implementací serveru.</span><span class="sxs-lookup"><span data-stu-id="49dfb-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="49dfb-121">Adresa URL musí být absolutní adresa URL a schéma (protokol) musí být HTTPS.</span><span class="sxs-lookup"><span data-stu-id="49dfb-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="49dfb-122">Hodnota `@id` v indexu služby je řetězec adresy URL obsahující následující zástupné tokeny:</span><span class="sxs-lookup"><span data-stu-id="49dfb-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="49dfb-123">Zástupné symboly adresy URL</span><span class="sxs-lookup"><span data-stu-id="49dfb-123">URL placeholders</span></span>

<span data-ttu-id="49dfb-124">Name</span><span class="sxs-lookup"><span data-stu-id="49dfb-124">Name</span></span>        | <span data-ttu-id="49dfb-125">Type</span><span class="sxs-lookup"><span data-stu-id="49dfb-125">Type</span></span>    | <span data-ttu-id="49dfb-126">Požadováno</span><span class="sxs-lookup"><span data-stu-id="49dfb-126">Required</span></span> | <span data-ttu-id="49dfb-127">Poznámky</span><span class="sxs-lookup"><span data-stu-id="49dfb-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="49dfb-128">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="49dfb-128">string</span></span>  | <span data-ttu-id="49dfb-129">Ne</span><span class="sxs-lookup"><span data-stu-id="49dfb-129">no</span></span>       | <span data-ttu-id="49dfb-130">ID balíčku, pro který se mají získat podrobnosti</span><span class="sxs-lookup"><span data-stu-id="49dfb-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="49dfb-131">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="49dfb-131">string</span></span>  | <span data-ttu-id="49dfb-132">Ne</span><span class="sxs-lookup"><span data-stu-id="49dfb-132">no</span></span>       | <span data-ttu-id="49dfb-133">Verze balíčku, pro který se mají získat podrobnosti</span><span class="sxs-lookup"><span data-stu-id="49dfb-133">The package version to get details for</span></span>

<span data-ttu-id="49dfb-134">Server by měl přijmout `{id}` a `{version}` hodnoty s libovolným písmenem.</span><span class="sxs-lookup"><span data-stu-id="49dfb-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="49dfb-135">Kromě toho by neměl být server citlivý na to, jestli je verze [normalizovaná](../concepts/package-versioning.md#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="49dfb-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="49dfb-136">Jinými slovy, server by měl přijímat také nenormalizované verze.</span><span class="sxs-lookup"><span data-stu-id="49dfb-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="49dfb-137">Například šablona s podrobnostmi balíčku NuGet. org vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="49dfb-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="49dfb-138">Pokud implementace klienta potřebuje zobrazit odkaz na podrobnosti balíčku pro NuGet. 4.3.0 správy verzí, vytvoří následující adresu URL a poskytne jí uživateli:</span><span class="sxs-lookup"><span data-stu-id="49dfb-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
