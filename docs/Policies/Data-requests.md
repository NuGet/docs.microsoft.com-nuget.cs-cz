---
title: Požadavky na Data uživatele
description: Exportovat zásady pro požadování uživatelská data a odstranit
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/04/2018
---
# <a name="user-data-requests"></a><span data-ttu-id="549ba-103">Požadavky na Data uživatele</span><span class="sxs-lookup"><span data-stu-id="549ba-103">User Data Requests</span></span>

<span data-ttu-id="549ba-104">nuget.org uživatelé mohli odesílat žádosti o odstranění informace a požadavky na informace o exportu prostřednictvím [nuget.org](https://www.nuget.org). Oba typy jsou odeslány ve formě podporu požadavků a jsou provádět správce nuget.org do 30 dní.</span><span class="sxs-lookup"><span data-stu-id="549ba-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="549ba-105">Následující data uživatele je přímo přístupný prostřednictvím nuget.org:</span><span class="sxs-lookup"><span data-stu-id="549ba-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="549ba-106">Souvisejícím s účtem data, jako jsou e-mailovou adresu, účet pro přihlášení, obrázek profilu a nastavení e-mailových oznámení</span><span class="sxs-lookup"><span data-stu-id="549ba-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="549ba-107">Vlastní rozhraní API klíče</span><span class="sxs-lookup"><span data-stu-id="549ba-107">Owned API Keys</span></span>
* <span data-ttu-id="549ba-108">Seznam balíčky, které vlastní</span><span class="sxs-lookup"><span data-stu-id="549ba-108">List of owned packages</span></span>

<span data-ttu-id="549ba-109">Tato data není součástí daty exportovanými pomocí žádosti o podporu.</span><span class="sxs-lookup"><span data-stu-id="549ba-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="549ba-110">Identifikace data zákazníků</span><span class="sxs-lookup"><span data-stu-id="549ba-110">Identifying customer data</span></span>

<span data-ttu-id="549ba-111">Zákaznická data je možné identifikovat jako nuget.org názvy uživatelských účtů.</span><span class="sxs-lookup"><span data-stu-id="549ba-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="549ba-112">Odstraňování dat zákazníka</span><span class="sxs-lookup"><span data-stu-id="549ba-112">Deleting customer data</span></span>

<span data-ttu-id="549ba-113">Žádost o odstraňuje data uživatele z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="549ba-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="549ba-114">Uživatel musí přihlásit k [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="549ba-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="549ba-115">Uživatel musí odeslat žádost o svůj účet odstranit [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="549ba-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="549ba-116">Uživatelé, kteří jsou jedinou vlastníky balíčků doporučujeme najít nové vlastníky před výzvou tak, aby měl svůj účet odstranit.</span><span class="sxs-lookup"><span data-stu-id="549ba-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="549ba-117">Pokud není přenést vlastnictví balíčku, je balíček NuGet neuvedené a v důsledku toho je již k dispozici v vyhledávací dotazy v sadě Visual Studio nebo na webu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="549ba-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="549ba-118">Před odstraněním účtu, správce nuget.org pracovat s uživatele k vyhledání nové vlastníků pro balíčky, které vlastní.</span><span class="sxs-lookup"><span data-stu-id="549ba-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="549ba-119">Akci odstranění účtu je dokončeno správce nuget.org do 30 dní od data požadavku.</span><span class="sxs-lookup"><span data-stu-id="549ba-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="549ba-120">Po odstranění účtu všechna data uživatele je odebrán ze systému nuget.org a budou provedeny následující akce:</span><span class="sxs-lookup"><span data-stu-id="549ba-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="549ba-121">Odstraněného účtu stane registrace s nuget.org</span><span class="sxs-lookup"><span data-stu-id="549ba-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="549ba-122">Všechny vlastněných že klíče rozhraní API se odstraní.</span><span class="sxs-lookup"><span data-stu-id="549ba-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="549ba-123">Jsou vydávány všechny vyhrazené obory názvů</span><span class="sxs-lookup"><span data-stu-id="549ba-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="549ba-124">Budou odebrány všechny vlastnictví balíčku</span><span class="sxs-lookup"><span data-stu-id="549ba-124">Any package ownership are removed</span></span>

<span data-ttu-id="549ba-125">Vlastní balíčky jsou *není* odstranit.</span><span class="sxs-lookup"><span data-stu-id="549ba-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="549ba-126">Když neuvedené z výsledků hledání, zůstanou k dispozici prostřednictvím balíčku obnovení do projektů, které jsou na nich závislé.</span><span class="sxs-lookup"><span data-stu-id="549ba-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="549ba-127">Export dat zákazníka</span><span class="sxs-lookup"><span data-stu-id="549ba-127">Exporting customer data</span></span>

<span data-ttu-id="549ba-128">Po přihlášení k nuget.org, uživatel může odeslat požadavek export prostřednictvím [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="549ba-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="549ba-129">Data exportovaná je k dispozici pro 48 hodin pro uživatele o stažení prostřednictvím objektu Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="549ba-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="549ba-130">Po 48 hodinách přístup vyprší a uživatel musí odešlete novou žádost exportu, podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="549ba-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="549ba-131">Exportovaná data zahrnuje:</span><span class="sxs-lookup"><span data-stu-id="549ba-131">The exported data includes:</span></span>

* <span data-ttu-id="549ba-132">Požadavky na podporu uživatele</span><span class="sxs-lookup"><span data-stu-id="549ba-132">The user's support requests</span></span>
* <span data-ttu-id="549ba-133">Akce uživatele (publikování balíčku, vytvořte účet) jako trvalý v protokolech auditu</span><span class="sxs-lookup"><span data-stu-id="549ba-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="549ba-134">Všechny informace o uživateli jako trvalý v protokoly služby IIS</span><span class="sxs-lookup"><span data-stu-id="549ba-134">Any user information as persisted in the IIS logs</span></span>
