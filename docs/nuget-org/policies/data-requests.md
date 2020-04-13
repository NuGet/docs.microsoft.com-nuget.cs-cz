---
title: Požadavky na uživatelská data
description: Zásady pro vyžádání exportu a odstranění uživatelských dat
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427512"
---
# <a name="user-data-requests"></a><span data-ttu-id="e327b-103">Požadavky na uživatelská data</span><span class="sxs-lookup"><span data-stu-id="e327b-103">User Data Requests</span></span>

<span data-ttu-id="e327b-104">nuget.org uživatelé mohou odesílat žádosti o odstranění informací a žádosti o export informací prostřednictvím [nuget.org](https://www.nuget.org). Oba typy jsou odeslány ve formě žádostí o podporu a jsou provedeny správci nuget.org do 30 dnů.</span><span class="sxs-lookup"><span data-stu-id="e327b-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="e327b-105">Následující uživatelská data jsou přímo přístupná prostřednictvím nuget.org:</span><span class="sxs-lookup"><span data-stu-id="e327b-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="e327b-106">Údaje související s účtem, jako je e-mailová adresa, přihlašovací účet, profilový obrázek a nastavení e-mailových oznámení</span><span class="sxs-lookup"><span data-stu-id="e327b-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="e327b-107">Vlastněné klíče ROZHRANÍ API</span><span class="sxs-lookup"><span data-stu-id="e327b-107">Owned API Keys</span></span>
* <span data-ttu-id="e327b-108">Seznam vlastněných balíčků</span><span class="sxs-lookup"><span data-stu-id="e327b-108">List of owned packages</span></span>

<span data-ttu-id="e327b-109">Tato data nejsou zahrnuta v datech exportovaných prostřednictvím žádosti o podporu.</span><span class="sxs-lookup"><span data-stu-id="e327b-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="e327b-110">Identifikace údajů o zákaznících</span><span class="sxs-lookup"><span data-stu-id="e327b-110">Identifying customer data</span></span>

<span data-ttu-id="e327b-111">Údaje o zákaznících lze identifikovat jako nuget.org názvy uživatelských účtů.</span><span class="sxs-lookup"><span data-stu-id="e327b-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="e327b-112">Odstranění dat zákazníků</span><span class="sxs-lookup"><span data-stu-id="e327b-112">Deleting customer data</span></span>

<span data-ttu-id="e327b-113">Chcete-li požádat o odstranění uživatelských dat z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="e327b-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="e327b-114">Uživatel se musí přihlásit k [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="e327b-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="e327b-115">Uživatel musí odeslat žádost o odstranění svého účtu [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="e327b-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="e327b-116">Uživatelům, kteří jsou výhradními vlastníky balíčků, doporučujeme najít nové vlastníky, než požádají o odstranění svého účtu.</span><span class="sxs-lookup"><span data-stu-id="e327b-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="e327b-117">Pokud vlastnictví balíčku není převedena, balíček NuGet je neuvedena a v důsledku toho již není k dispozici ve vyhledávacích dotazech v sadě Visual Studio nebo na webu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e327b-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="e327b-118">Před odstraněním účtu nuget.org správci spolupracují s uživatelem na hledání nových vlastníků pro balíčky, které vlastní.</span><span class="sxs-lookup"><span data-stu-id="e327b-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="e327b-119">Akci odstranění účtu dokončí správce nuget.org do 30 dnů od data žádosti.</span><span class="sxs-lookup"><span data-stu-id="e327b-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="e327b-120">Po odstranění účtu budou všechna data uživatele odebrána ze systému nuget.org a budou podniknuty následující akce:</span><span class="sxs-lookup"><span data-stu-id="e327b-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="e327b-121">Odstraněný účet se stane neregistrovaným u nuget.org</span><span class="sxs-lookup"><span data-stu-id="e327b-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="e327b-122">Všechny vlastněné klíče ROZHRANÍ API jsou odstraněny.</span><span class="sxs-lookup"><span data-stu-id="e327b-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="e327b-123">Všechny vyhrazené obory názvů jsou uvolněny.</span><span class="sxs-lookup"><span data-stu-id="e327b-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="e327b-124">Jakékoli vlastnictví balíčku bude odebráno.</span><span class="sxs-lookup"><span data-stu-id="e327b-124">Any package ownership are removed</span></span>

<span data-ttu-id="e327b-125">Vlastněné balíčky *nejsou* odstraněny.</span><span class="sxs-lookup"><span data-stu-id="e327b-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="e327b-126">Přestože nejsou uvedeny z výsledků hledání, zůstávají k dispozici prostřednictvím obnovení balíčku pro projekty, které jsou na nich závislé.</span><span class="sxs-lookup"><span data-stu-id="e327b-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="e327b-127">Export dat zákazníků</span><span class="sxs-lookup"><span data-stu-id="e327b-127">Exporting customer data</span></span>

<span data-ttu-id="e327b-128">Po přihlášení k nuget.org může uživatel odeslat žádost o export prostřednictvím [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="e327b-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="e327b-129">Exportovaná data jsou k dispozici pro 48 hodin pro uživatele ke stažení prostřednictvím objektu blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e327b-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="e327b-130">Po 48 hodinách vyprší platnost přístupu a uživatel musí podle potřeby odeslat novou žádost o export.</span><span class="sxs-lookup"><span data-stu-id="e327b-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="e327b-131">Exportovaná data zahrnují:</span><span class="sxs-lookup"><span data-stu-id="e327b-131">The exported data includes:</span></span>

* <span data-ttu-id="e327b-132">Požadavky uživatele na podporu</span><span class="sxs-lookup"><span data-stu-id="e327b-132">The user's support requests</span></span>
* <span data-ttu-id="e327b-133">Akce uživatele (publikovat balíček, vytvořit účet) jako trvalé v protokolech auditu</span><span class="sxs-lookup"><span data-stu-id="e327b-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="e327b-134">Všechny informace o uživateli jako trvalé v protokolech iis</span><span class="sxs-lookup"><span data-stu-id="e327b-134">Any user information as persisted in the IIS logs</span></span>
