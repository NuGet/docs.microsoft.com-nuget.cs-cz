---
title: Sestavy zneužití URL šablony, NuGet rozhraní API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Šablona sestavy zneužití URL umožňuje klientům zobrazit odkaz v jejich uživatelského rozhraní.
keywords: Rozhraní API NuGet oznámení zneužití, rozhraní API NuGet souboru předpisy, šablona adresy URL sestavy nuget.org
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ded861e3eaf73e45b8d4bd80b96d54bfeb38e9d6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="e098e-104">Šablona sestavy zneužití adresy URL</span><span class="sxs-lookup"><span data-stu-id="e098e-104">Report abuse URL template</span></span>

<span data-ttu-id="e098e-105">Je možné pro klienta sestavit adresu URL, kterého uživatel k oznámení zneužití o určitém balíčku.</span><span class="sxs-lookup"><span data-stu-id="e098e-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="e098e-106">To je užitečné, když chce zdroj balíčku povolit všechny činnosti klienta (i 3. stran) delegovat zneužití sestavy ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="e098e-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="e098e-107">Je prostředku používaného pro načítání obsahu balíčku `ReportAbuseUriTemplate` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e098e-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e098e-108">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="e098e-108">Versioning</span></span>

<span data-ttu-id="e098e-109">Následující `@type` se používají hodnoty:</span><span class="sxs-lookup"><span data-stu-id="e098e-109">The following `@type` values are used:</span></span>

<span data-ttu-id="e098e-110">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="e098e-110">@type value</span></span>                       | <span data-ttu-id="e098e-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e098e-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="e098e-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="e098e-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="e098e-113">Původní verze</span><span class="sxs-lookup"><span data-stu-id="e098e-113">The initial release</span></span>
<span data-ttu-id="e098e-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="e098e-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="e098e-115">Alias `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="e098e-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="e098e-116">Adresa URL šablony</span><span class="sxs-lookup"><span data-stu-id="e098e-116">URL template</span></span>

<span data-ttu-id="e098e-117">Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e098e-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e098e-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="e098e-118">HTTP methods</span></span>

<span data-ttu-id="e098e-119">I když klient není určen provádět požadavky na adresu URL sestavy zneužití jménem uživatele, musí podporovat webové stránky `GET` metoda umožňující kliknutelnou URL snadno otevřít ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="e098e-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="e098e-120">Vytvořit adresu URL</span><span class="sxs-lookup"><span data-stu-id="e098e-120">Construct the URL</span></span>

<span data-ttu-id="e098e-121">Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL používá pro přístup k webovému rozhraní.</span><span class="sxs-lookup"><span data-stu-id="e098e-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="e098e-122">Implementace klienta by měl zobrazit tento vytvořený adresa URL (nebo prokliknutelný odkaz) uživateli, což jim aby otevřete webový prohlížeč na adresu URL a proveďte všechny nezbytné zneužití sestavy.</span><span class="sxs-lookup"><span data-stu-id="e098e-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="e098e-123">Implementace formuláře pro hlášení zneužití je určen podle implementaci serveru.</span><span class="sxs-lookup"><span data-stu-id="e098e-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="e098e-124">Hodnota `@id` je adresa URL řetězec obsahující všechny následující zástupný symbol tokenů:</span><span class="sxs-lookup"><span data-stu-id="e098e-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="e098e-125">Adresa URL zástupné symboly</span><span class="sxs-lookup"><span data-stu-id="e098e-125">URL placeholders</span></span>

<span data-ttu-id="e098e-126">Název</span><span class="sxs-lookup"><span data-stu-id="e098e-126">Name</span></span>        | <span data-ttu-id="e098e-127">Typ</span><span class="sxs-lookup"><span data-stu-id="e098e-127">Type</span></span>    | <span data-ttu-id="e098e-128">Požadováno</span><span class="sxs-lookup"><span data-stu-id="e098e-128">Required</span></span> | <span data-ttu-id="e098e-129">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e098e-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="e098e-130">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="e098e-130">string</span></span>  | <span data-ttu-id="e098e-131">Ne</span><span class="sxs-lookup"><span data-stu-id="e098e-131">no</span></span>       | <span data-ttu-id="e098e-132">ID balíčku k oznámení zneužití pro</span><span class="sxs-lookup"><span data-stu-id="e098e-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="e098e-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="e098e-133">string</span></span>  | <span data-ttu-id="e098e-134">Ne</span><span class="sxs-lookup"><span data-stu-id="e098e-134">no</span></span>       | <span data-ttu-id="e098e-135">Verze balíčku k oznámení zneužití pro</span><span class="sxs-lookup"><span data-stu-id="e098e-135">The package version to report abuse for</span></span>

<span data-ttu-id="e098e-136">`{id}` a `{version}` hodnoty interpretovány implementací serveru musí být malá a velká písmena a zda je verze normalizovány není citlivé.</span><span class="sxs-lookup"><span data-stu-id="e098e-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="e098e-137">Šablona zneužití sestavy nuget.org například vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="e098e-137">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="e098e-138">Pokud implementace klienta potřebuje k zobrazení odkaz na formulář zneužití sestavy NuGet.Versioning 4.3.0, by se vytvořit následující adresu URL a poskytne mu uživateli:</span><span class="sxs-lookup"><span data-stu-id="e098e-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
