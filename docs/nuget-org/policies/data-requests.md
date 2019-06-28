---
title: Požadavky na Data uživatelů
description: Zásady žádosti o export dat uživatele a odstranit
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427512"
---
# <a name="user-data-requests"></a><span data-ttu-id="80a90-103">Požadavky na Data uživatelů</span><span class="sxs-lookup"><span data-stu-id="80a90-103">User Data Requests</span></span>

<span data-ttu-id="80a90-104">nuget.org uživatelé mohli odesílat žádosti o odstranění informace a informace o žádosti o export prostřednictvím [nuget.org](https://www.nuget.org). Oba typy jsou odeslány ve formě podporu požadavků a jsou spustit správci nuget.org do 30 dní.</span><span class="sxs-lookup"><span data-stu-id="80a90-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="80a90-105">Následující data uživatele jsou přímo přístupné prostřednictvím nuget.org:</span><span class="sxs-lookup"><span data-stu-id="80a90-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="80a90-106">Účet související data, jako jsou e-mailovou adresu, účet pro přihlášení, profilový obrázek a nastavení e-mailových oznámení</span><span class="sxs-lookup"><span data-stu-id="80a90-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="80a90-107">Klíče vlastní rozhraní API</span><span class="sxs-lookup"><span data-stu-id="80a90-107">Owned API Keys</span></span>
* <span data-ttu-id="80a90-108">Seznam balíčků vlastněná podnikem</span><span class="sxs-lookup"><span data-stu-id="80a90-108">List of owned packages</span></span>

<span data-ttu-id="80a90-109">Tato data není součástí data exportovaná prostřednictvím žádosti o podporu.</span><span class="sxs-lookup"><span data-stu-id="80a90-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="80a90-110">Identifikace zákaznická data</span><span class="sxs-lookup"><span data-stu-id="80a90-110">Identifying customer data</span></span>

<span data-ttu-id="80a90-111">Zákaznická data je možné identifikovat jako nuget.org názvy uživatelských účtů.</span><span class="sxs-lookup"><span data-stu-id="80a90-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="80a90-112">Odstraňuje se zákaznická data</span><span class="sxs-lookup"><span data-stu-id="80a90-112">Deleting customer data</span></span>

<span data-ttu-id="80a90-113">Žádost o odstranění uživatele data z webu nuget.org:</span><span class="sxs-lookup"><span data-stu-id="80a90-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="80a90-114">Uživatel musí přihlásit k [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="80a90-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="80a90-115">Uživatel, musíte odeslat žádost pro svůj účet odstranit [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="80a90-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="80a90-116">Uživatelé, kteří jsou výhradní vlastníci balíčky můžou najít novým vlastníkům před chce mít jeho účet odstraněn.</span><span class="sxs-lookup"><span data-stu-id="80a90-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="80a90-117">Pokud nepřevezme vlastnictví balíčku, je balíček NuGet neuvedené v seznamu a v důsledku toho už nejsou k dispozici ve vyhledávacích dotazů v sadě Visual Studio nebo na webu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="80a90-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="80a90-118">Před odstraněním účtu, správce nuget.org pracovat uživatele o nalezení novým vlastníkům pro balíčky, které vlastní.</span><span class="sxs-lookup"><span data-stu-id="80a90-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="80a90-119">Účet akce odstranění dokončení správcem nuget.org do 30 dní od data požadavku.</span><span class="sxs-lookup"><span data-stu-id="80a90-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="80a90-120">Při odstraňování účtu všechna data uživatele se odebere ze systému nuget.org a budou provedeny následující akce:</span><span class="sxs-lookup"><span data-stu-id="80a90-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="80a90-121">Odstraněný účet stane odregistrovat s nuget.org</span><span class="sxs-lookup"><span data-stu-id="80a90-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="80a90-122">Všechny vlastněné, že klíče rozhraní API se odstraní.</span><span class="sxs-lookup"><span data-stu-id="80a90-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="80a90-123">Všechny rezervované obory názvů jsou všeobecně dostupné</span><span class="sxs-lookup"><span data-stu-id="80a90-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="80a90-124">Odeberou se všechny vlastnictví balíčku</span><span class="sxs-lookup"><span data-stu-id="80a90-124">Any package ownership are removed</span></span>

<span data-ttu-id="80a90-125">Vlastní balíčky jsou *není* odstraněn.</span><span class="sxs-lookup"><span data-stu-id="80a90-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="80a90-126">I když neuvedené ve výsledcích hledání, zůstaly dostupné prostřednictvím obnovení balíčků pro projekty, které jsou na nich závislé.</span><span class="sxs-lookup"><span data-stu-id="80a90-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="80a90-127">Export zákaznických dat</span><span class="sxs-lookup"><span data-stu-id="80a90-127">Exporting customer data</span></span>

<span data-ttu-id="80a90-128">Po přihlášení na nuget.org, uživatel může odeslat žádost o export prostřednictvím [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="80a90-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="80a90-129">Data exportovaná je k dispozici po dobu 48 hodin na uživatele ke stažení prostřednictvím objektu Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="80a90-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="80a90-130">Po 48 hodinách přístup vyprší a uživatel musí odeslat novou žádost o export, podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="80a90-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="80a90-131">Exportovaná data zahrnují:</span><span class="sxs-lookup"><span data-stu-id="80a90-131">The exported data includes:</span></span>

* <span data-ttu-id="80a90-132">Žádostí o podporu uživatele</span><span class="sxs-lookup"><span data-stu-id="80a90-132">The user's support requests</span></span>
* <span data-ttu-id="80a90-133">Akce uživatele (publikování balíčku, vytvořte účet) jako trvalý v protokolech auditu</span><span class="sxs-lookup"><span data-stu-id="80a90-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="80a90-134">Žádné informace o uživateli jako trvalý v protokolech služby IIS</span><span class="sxs-lookup"><span data-stu-id="80a90-134">Any user information as persisted in the IIS logs</span></span>
