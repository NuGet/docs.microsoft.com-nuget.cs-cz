---
title: "Sestavy zneužití URL šablony, NuGet rozhraní API | Microsoft Docs"
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
ms.technology: 
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "Šablona sestavy zneužití URL umožňuje klientům zobrazit odkaz v jejich uživatelského rozhraní."
keywords: "Rozhraní API NuGet oznámení zneužití, rozhraní API NuGet souboru předpisy, šablona adresy URL sestavy NuGet.org"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="0c218-104">Šablona sestavy zneužití adresy URL</span><span class="sxs-lookup"><span data-stu-id="0c218-104">Report Abuse URL Template</span></span>

<span data-ttu-id="0c218-105">Je možné pro klienta sestavit adresu URL, kterého uživatel k oznámení zneužití o určitém balíčku.</span><span class="sxs-lookup"><span data-stu-id="0c218-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="0c218-106">To je užitečné, když chce zdroj balíčku povolit všechny činnosti klienta (i 3. stran) delegovat zneužití sestavy ke zdroji balíčku.</span><span class="sxs-lookup"><span data-stu-id="0c218-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="0c218-107">Je prostředku používaného pro načítání obsahu balíčku `ReportAbuseUriTemplate` v nalezen prostředek [indexu služby](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="0c218-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="0c218-108">Správa verzí</span><span class="sxs-lookup"><span data-stu-id="0c218-108">Versioning</span></span>

<span data-ttu-id="0c218-109">Následující `@type` se používají hodnoty:</span><span class="sxs-lookup"><span data-stu-id="0c218-109">The following `@type` values are used:</span></span>

<span data-ttu-id="0c218-110">@typeHodnota</span><span class="sxs-lookup"><span data-stu-id="0c218-110">@type value</span></span>                       | <span data-ttu-id="0c218-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="0c218-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="0c218-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="0c218-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="0c218-113">Původní verze</span><span class="sxs-lookup"><span data-stu-id="0c218-113">The initial release</span></span>
<span data-ttu-id="0c218-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="0c218-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="0c218-115">Alias`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="0c218-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="0c218-116">Adresa URL šablony</span><span class="sxs-lookup"><span data-stu-id="0c218-116">URL template</span></span>

<span data-ttu-id="0c218-117">Adresa URL pro následující rozhraní API je hodnota `@id` vlastnost spojená s jedním z výše uvedených prostředků `@type` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="0c218-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0c218-118">Metody HTTP</span><span class="sxs-lookup"><span data-stu-id="0c218-118">HTTP methods</span></span>

<span data-ttu-id="0c218-119">I když klient není určen provádět požadavky na adresu URL sestavy zneužití jménem uživatele, musí podporovat webové stránky `GET` metoda umožňující kliknutelnou URL snadno otevřít ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="0c218-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="0c218-120">Vytvořit adresu URL</span><span class="sxs-lookup"><span data-stu-id="0c218-120">Construct the URL</span></span>

<span data-ttu-id="0c218-121">Zadané ID známých balíčku a verzi, implementace klienta můžete vytvořit adresu URL používá pro přístup k webovému rozhraní.</span><span class="sxs-lookup"><span data-stu-id="0c218-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="0c218-122">Implementace klienta by měl zobrazit tento vytvořený adresa URL (nebo prokliknutelný odkaz) uživateli, což jim aby otevřete webový prohlížeč na adresu URL a proveďte všechny nezbytné zneužití sestavy.</span><span class="sxs-lookup"><span data-stu-id="0c218-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="0c218-123">Implementace formuláře pro hlášení zneužití je určen podle implementaci serveru.</span><span class="sxs-lookup"><span data-stu-id="0c218-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="0c218-124">Hodnota `@id` je adresa URL řetězec obsahující všechny následující zástupný symbol tokenů:</span><span class="sxs-lookup"><span data-stu-id="0c218-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="0c218-125">Adresa URL zástupné symboly</span><span class="sxs-lookup"><span data-stu-id="0c218-125">URL placeholders</span></span>

<span data-ttu-id="0c218-126">Název</span><span class="sxs-lookup"><span data-stu-id="0c218-126">Name</span></span>        | <span data-ttu-id="0c218-127">Typ</span><span class="sxs-lookup"><span data-stu-id="0c218-127">Type</span></span>    | <span data-ttu-id="0c218-128">Požadováno</span><span class="sxs-lookup"><span data-stu-id="0c218-128">Required</span></span> | <span data-ttu-id="0c218-129">Poznámky</span><span class="sxs-lookup"><span data-stu-id="0c218-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="0c218-130">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="0c218-130">string</span></span>  | <span data-ttu-id="0c218-131">Ne</span><span class="sxs-lookup"><span data-stu-id="0c218-131">no</span></span>       | <span data-ttu-id="0c218-132">ID balíčku k oznámení zneužití pro</span><span class="sxs-lookup"><span data-stu-id="0c218-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="0c218-133">odkazy řetězců</span><span class="sxs-lookup"><span data-stu-id="0c218-133">string</span></span>  | <span data-ttu-id="0c218-134">Ne</span><span class="sxs-lookup"><span data-stu-id="0c218-134">no</span></span>       | <span data-ttu-id="0c218-135">Verze balíčku k oznámení zneužití pro</span><span class="sxs-lookup"><span data-stu-id="0c218-135">The package version to report abuse for</span></span>

<span data-ttu-id="0c218-136">`{id}` a `{version}` hodnoty interpretovány implementací serveru musí být malá insenstive a zda je verze normalizovány není citlivé.</span><span class="sxs-lookup"><span data-stu-id="0c218-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="0c218-137">Šablona zneužití sestavy nuget.org například vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="0c218-137">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="0c218-138">Pokud implementace klienta potřebuje k zobrazení odkaz na formulář zneužití sestavy NuGet.Versioning 4.3.0, by se vytvořit následující adresu URL a poskytne mu uživateli:</span><span class="sxs-lookup"><span data-stu-id="0c218-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```