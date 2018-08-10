---
title: Ohlásit nevhodné chování adresy URL šablony NuGet rozhraní API
description: Šablona adresy URL sestavy zneužití umožňuje klientům zobrazit odkaz kliknete v jejich uživatelského rozhraní.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020437"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="c6688-103">Šablona adresy URL sestavy urážlivého příspěvku</span><span class="sxs-lookup"><span data-stu-id="c6688-103">Report abuse URL template</span></span>

<span data-ttu-id="c6688-104">Je možné sestavit adresu URL, kterého uživatel k oznámení zneužití o konkrétní balíček klienta.</span><span class="sxs-lookup"><span data-stu-id="c6688-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="c6688-105">To je užitečné, pokud zdroj balíčku chce umožněte všechny klienta (i 3. stran) delegovat zneužití sestavy ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="c6688-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="c6688-106">Je použit k sestavení tuto adresu URL prostředku `ReportAbuseUriTemplate` prostředek se nenašel v [index služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="c6688-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c6688-107">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="c6688-107">Versioning</span></span>

<span data-ttu-id="c6688-108">Následující `@type` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="c6688-108">The following `@type` values are used:</span></span>

<span data-ttu-id="c6688-109">@type Hodnota</span><span class="sxs-lookup"><span data-stu-id="c6688-109">@type value</span></span>                       | <span data-ttu-id="c6688-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c6688-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="c6688-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="c6688-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="c6688-112">Počáteční verze</span><span class="sxs-lookup"><span data-stu-id="c6688-112">The initial release</span></span>
<span data-ttu-id="c6688-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="c6688-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="c6688-114">Alias `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="c6688-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="c6688-115">Adresa URL šablony</span><span class="sxs-lookup"><span data-stu-id="c6688-115">URL template</span></span>

<span data-ttu-id="c6688-116">Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost přiřazené k některému z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="c6688-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c6688-117">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="c6688-117">HTTP methods</span></span>

<span data-ttu-id="c6688-118">I když klient není určena adresa URL sestavy zneužití provádět požadavky jménem uživatele, by měly podporovat webové stránky `GET` metoda umožňující kliknutí na adresu URL snadno otevřít ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="c6688-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="c6688-119">Vytvořit adresu URL</span><span class="sxs-lookup"><span data-stu-id="c6688-119">Construct the URL</span></span>

<span data-ttu-id="c6688-120">Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL pro přístup k webovým rozhraním.</span><span class="sxs-lookup"><span data-stu-id="c6688-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="c6688-121">Implementace klienta pro uživatele, kterým otevřete webový prohlížeč na adresu URL a proveďte všechny nezbytné zneužití sestavy zobrazeno tento konstruovaný adresy URL (nebo prokliknutelný odkaz).</span><span class="sxs-lookup"><span data-stu-id="c6688-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="c6688-122">Implementace formuláře zneužití sestavy je určeno implementaci serveru.</span><span class="sxs-lookup"><span data-stu-id="c6688-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="c6688-123">Hodnota `@id` je řetězec adresy URL obsahující některý z následujících tokeny zástupný symbol:</span><span class="sxs-lookup"><span data-stu-id="c6688-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="c6688-124">Adresa URL zástupné symboly</span><span class="sxs-lookup"><span data-stu-id="c6688-124">URL placeholders</span></span>

<span data-ttu-id="c6688-125">Název</span><span class="sxs-lookup"><span data-stu-id="c6688-125">Name</span></span>        | <span data-ttu-id="c6688-126">Typ</span><span class="sxs-lookup"><span data-stu-id="c6688-126">Type</span></span>    | <span data-ttu-id="c6688-127">Požadováno</span><span class="sxs-lookup"><span data-stu-id="c6688-127">Required</span></span> | <span data-ttu-id="c6688-128">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c6688-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="c6688-129">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="c6688-129">string</span></span>  | <span data-ttu-id="c6688-130">Ne</span><span class="sxs-lookup"><span data-stu-id="c6688-130">no</span></span>       | <span data-ttu-id="c6688-131">ID balíčku, který chcete ohlásit příspěvek jako urážlivý</span><span class="sxs-lookup"><span data-stu-id="c6688-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="c6688-132">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="c6688-132">string</span></span>  | <span data-ttu-id="c6688-133">Ne</span><span class="sxs-lookup"><span data-stu-id="c6688-133">no</span></span>       | <span data-ttu-id="c6688-134">Verze balíčku k oznámení zneužití pro</span><span class="sxs-lookup"><span data-stu-id="c6688-134">The package version to report abuse for</span></span>

<span data-ttu-id="c6688-135">`{id}` a `{version}` hodnoty interpretovány implementací serveru musí být malá a velká písmena a nikoli citlivá, jestli je normalizovány na verzi.</span><span class="sxs-lookup"><span data-stu-id="c6688-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="c6688-136">Například šablona zneužití nuget.org sestavy vypadá například takto:</span><span class="sxs-lookup"><span data-stu-id="c6688-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="c6688-137">Pokud implementace klienta potřebuje k zobrazení odkazu do formuláře zneužití sestavy pro NuGet.Versioning 4.3.0, ho by vytvořit následující adresu URL a poskytují uživateli:</span><span class="sxs-lookup"><span data-stu-id="c6688-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
