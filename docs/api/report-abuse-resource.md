---
title: Šablona pro adresu URL zneužití ze sestavy, NuGet rozhraní API
description: Šablona sestavy zneužití URL umožňuje klientům zobrazit odkaz v jejich uživatelského rozhraní.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818464"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="5beae-103">Šablona sestavy zneužití adresy URL</span><span class="sxs-lookup"><span data-stu-id="5beae-103">Report abuse URL template</span></span>

<span data-ttu-id="5beae-104">Je možné pro klienta sestavit adresu URL, kterého uživatel k oznámení zneužití o určitém balíčku.</span><span class="sxs-lookup"><span data-stu-id="5beae-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="5beae-105">To je užitečné, když chce zdroj balíčku povolit všechny činnosti klienta (i 3. stran) delegovat zneužití sestavy ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="5beae-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="5beae-106">Je prostředku používaného pro načítání obsahu balíčku `ReportAbuseUriTemplate` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="5beae-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5beae-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="5beae-107">Versioning</span></span>

<span data-ttu-id="5beae-108">Následující `@type` se používají hodnoty:</span><span class="sxs-lookup"><span data-stu-id="5beae-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5beae-109">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="5beae-109">@type value</span></span>                       | <span data-ttu-id="5beae-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="5beae-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="5beae-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="5beae-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="5beae-112">Původní verze</span><span class="sxs-lookup"><span data-stu-id="5beae-112">The initial release</span></span>
<span data-ttu-id="5beae-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="5beae-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="5beae-114">Alias `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="5beae-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="5beae-115">Adresa URL šablony</span><span class="sxs-lookup"><span data-stu-id="5beae-115">URL template</span></span>

<span data-ttu-id="5beae-116">Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="5beae-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5beae-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="5beae-117">HTTP methods</span></span>

<span data-ttu-id="5beae-118">I když klient není určen provádět požadavky na adresu URL sestavy zneužití jménem uživatele, musí podporovat webové stránky `GET` metoda umožňující kliknutelnou URL snadno otevřít ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="5beae-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="5beae-119">Vytvořit adresu URL</span><span class="sxs-lookup"><span data-stu-id="5beae-119">Construct the URL</span></span>

<span data-ttu-id="5beae-120">Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL používá pro přístup k webovému rozhraní.</span><span class="sxs-lookup"><span data-stu-id="5beae-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="5beae-121">Implementace klienta by měl zobrazit tento vytvořený adresa URL (nebo prokliknutelný odkaz) uživateli, což jim aby otevřete webový prohlížeč na adresu URL a proveďte všechny nezbytné zneužití sestavy.</span><span class="sxs-lookup"><span data-stu-id="5beae-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="5beae-122">Implementace formuláře pro hlášení zneužití je určen podle implementaci serveru.</span><span class="sxs-lookup"><span data-stu-id="5beae-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="5beae-123">Hodnota `@id` je adresa URL řetězec obsahující všechny následující zástupný symbol tokenů:</span><span class="sxs-lookup"><span data-stu-id="5beae-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="5beae-124">Adresa URL zástupné symboly</span><span class="sxs-lookup"><span data-stu-id="5beae-124">URL placeholders</span></span>

<span data-ttu-id="5beae-125">Název</span><span class="sxs-lookup"><span data-stu-id="5beae-125">Name</span></span>        | <span data-ttu-id="5beae-126">Typ</span><span class="sxs-lookup"><span data-stu-id="5beae-126">Type</span></span>    | <span data-ttu-id="5beae-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="5beae-127">Required</span></span> | <span data-ttu-id="5beae-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="5beae-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="5beae-129">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="5beae-129">string</span></span>  | <span data-ttu-id="5beae-130">Ne</span><span class="sxs-lookup"><span data-stu-id="5beae-130">no</span></span>       | <span data-ttu-id="5beae-131">ID balíčku k oznámení zneužití pro</span><span class="sxs-lookup"><span data-stu-id="5beae-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="5beae-132">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="5beae-132">string</span></span>  | <span data-ttu-id="5beae-133">Ne</span><span class="sxs-lookup"><span data-stu-id="5beae-133">no</span></span>       | <span data-ttu-id="5beae-134">Verze balíčku k oznámení zneužití pro</span><span class="sxs-lookup"><span data-stu-id="5beae-134">The package version to report abuse for</span></span>

<span data-ttu-id="5beae-135">`{id}` a `{version}` hodnoty interpretovány implementací serveru musí být malá a velká písmena a zda je verze normalizovány není citlivé.</span><span class="sxs-lookup"><span data-stu-id="5beae-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="5beae-136">Šablona zneužití sestavy nuget.org například vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="5beae-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="5beae-137">Pokud implementace klienta potřebuje k zobrazení odkaz na formulář zneužití sestavy NuGet.Versioning 4.3.0, by se vytvořit následující adresu URL a poskytne mu uživateli:</span><span class="sxs-lookup"><span data-stu-id="5beae-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
