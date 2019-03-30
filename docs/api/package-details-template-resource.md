---
title: Sbalit podrobnosti o adresu URL šablony NuGet rozhraní API
description: Šablona adresy URL podrobnosti balíčku umožňuje klientům zobrazovat v jejich uživatelského rozhraní webového odkaz na další podrobnosti o balíčku
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638086"
---
# <a name="package-details-url-template"></a><span data-ttu-id="41e8e-103">Šablona adresy URL podrobnosti balíčku</span><span class="sxs-lookup"><span data-stu-id="41e8e-103">Package details URL template</span></span>

<span data-ttu-id="41e8e-104">Je možné pro klienta sestavit adresu URL, která je možné uživatele zobrazíte další podrobnosti balíčku ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="41e8e-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="41e8e-105">To je užitečné, pokud chce zobrazit další informace o balíčku, který se nemusí vejde v rámci oboru co klientská aplikace NuGet zobrazuje zdroje balíčku.</span><span class="sxs-lookup"><span data-stu-id="41e8e-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="41e8e-106">Je použit k sestavení tuto adresu URL prostředku `PackageDetailsUriTemplate` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="41e8e-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="41e8e-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="41e8e-107">Versioning</span></span>

<span data-ttu-id="41e8e-108">Následující `@type` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="41e8e-108">The following `@type` values are used:</span></span>

<span data-ttu-id="41e8e-109">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="41e8e-109">@type value</span></span>                     | <span data-ttu-id="41e8e-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="41e8e-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="41e8e-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="41e8e-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="41e8e-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="41e8e-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="41e8e-113">Adresa URL šablony</span><span class="sxs-lookup"><span data-stu-id="41e8e-113">URL template</span></span>

<span data-ttu-id="41e8e-114">Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="41e8e-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="41e8e-115">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="41e8e-115">HTTP methods</span></span>

<span data-ttu-id="41e8e-116">I když klient není určen tak, aby adresa URL balíčku podrobnosti žádosti jménem uživatele, by měly podporovat webové stránky `GET` metoda umožňující kliknutí na adresu URL snadno otevřít ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="41e8e-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="41e8e-117">Vytvořit adresu URL</span><span class="sxs-lookup"><span data-stu-id="41e8e-117">Construct the URL</span></span>

<span data-ttu-id="41e8e-118">Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL pro přístup k webovým rozhraním.</span><span class="sxs-lookup"><span data-stu-id="41e8e-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="41e8e-119">Implementace klienta pro uživatele, kterým otevřete webový prohlížeč na adresu URL a další informace o balíčku zobrazeno tento konstruovaný adresy URL (nebo prokliknutelný odkaz).</span><span class="sxs-lookup"><span data-stu-id="41e8e-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="41e8e-120">Obsah stránky s podrobnostmi balíčku je určeno implementaci serveru.</span><span class="sxs-lookup"><span data-stu-id="41e8e-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="41e8e-121">Adresa URL musí být absolutní adresu URL a schéma (protokolu) musí být HTTPS.</span><span class="sxs-lookup"><span data-stu-id="41e8e-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="41e8e-122">Hodnota `@id` ve službě index je řetězec adresy URL obsahující některý z následujících tokeny zástupný symbol:</span><span class="sxs-lookup"><span data-stu-id="41e8e-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="41e8e-123">Adresa URL zástupné symboly</span><span class="sxs-lookup"><span data-stu-id="41e8e-123">URL placeholders</span></span>

<span data-ttu-id="41e8e-124">Název</span><span class="sxs-lookup"><span data-stu-id="41e8e-124">Name</span></span>        | <span data-ttu-id="41e8e-125">Type</span><span class="sxs-lookup"><span data-stu-id="41e8e-125">Type</span></span>    | <span data-ttu-id="41e8e-126">Požadováno</span><span class="sxs-lookup"><span data-stu-id="41e8e-126">Required</span></span> | <span data-ttu-id="41e8e-127">Poznámky</span><span class="sxs-lookup"><span data-stu-id="41e8e-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="41e8e-128">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="41e8e-128">string</span></span>  | <span data-ttu-id="41e8e-129">Ne</span><span class="sxs-lookup"><span data-stu-id="41e8e-129">no</span></span>       | <span data-ttu-id="41e8e-130">ID balíčku získat podrobnosti pro</span><span class="sxs-lookup"><span data-stu-id="41e8e-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="41e8e-131">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="41e8e-131">string</span></span>  | <span data-ttu-id="41e8e-132">Ne</span><span class="sxs-lookup"><span data-stu-id="41e8e-132">no</span></span>       | <span data-ttu-id="41e8e-133">Verze balíčku získat podrobnosti pro</span><span class="sxs-lookup"><span data-stu-id="41e8e-133">The package version to get details for</span></span>

<span data-ttu-id="41e8e-134">Server by měl přijmout `{id}` a `{version}` hodnoty všechny velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="41e8e-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="41e8e-135">Kromě toho by neměl být citlivé na tom, jestli je verze serveru [normalizované](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="41e8e-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="41e8e-136">Jinými slovy, by měla přijímat server také přijímat nenormalizovaný verze.</span><span class="sxs-lookup"><span data-stu-id="41e8e-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="41e8e-137">Například šablona podrobnosti balíčku nuget.org vypadá například takto:</span><span class="sxs-lookup"><span data-stu-id="41e8e-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="41e8e-138">Pokud implementace klienta zobrazí odkaz na podrobné informace balíčku pro NuGet.Versioning 4.3.0, to by vytvořit následující adresu URL a poskytují uživateli:</span><span class="sxs-lookup"><span data-stu-id="41e8e-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
