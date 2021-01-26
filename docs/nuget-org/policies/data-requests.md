---
title: Požadavky na data uživatelů
description: Zásady pro vyžádání exportu a odstraňování uživatelských dat
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775726"
---
# <a name="user-data-requests"></a><span data-ttu-id="28aaf-103">Požadavky na data uživatelů</span><span class="sxs-lookup"><span data-stu-id="28aaf-103">User Data Requests</span></span>

<span data-ttu-id="28aaf-104">nuget.org uživatelé mohou odesílat žádosti o odstranění informací a žádosti o export informací prostřednictvím [NuGet.org](https://www.nuget.org). Oba typy jsou odesílány ve formě žádostí o podporu a správci nuget.org do 30 dnů.</span><span class="sxs-lookup"><span data-stu-id="28aaf-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="28aaf-105">Tato data uživatelů jsou přímo přístupná prostřednictvím nuget.org:</span><span class="sxs-lookup"><span data-stu-id="28aaf-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="28aaf-106">Data týkající se účtu, jako je e-mailová adresa, účet přihlášení, profilový obrázek a nastavení e-mailových oznámení</span><span class="sxs-lookup"><span data-stu-id="28aaf-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="28aaf-107">Vlastní klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="28aaf-107">Owned API Keys</span></span>
* <span data-ttu-id="28aaf-108">Seznam vlastněných balíčků</span><span class="sxs-lookup"><span data-stu-id="28aaf-108">List of owned packages</span></span>

<span data-ttu-id="28aaf-109">Tato data nejsou obsažena v datech exportovaných prostřednictvím žádosti o podporu.</span><span class="sxs-lookup"><span data-stu-id="28aaf-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="28aaf-110">Identifikace zákaznických dat</span><span class="sxs-lookup"><span data-stu-id="28aaf-110">Identifying customer data</span></span>

<span data-ttu-id="28aaf-111">Zákaznická data se dají identifikovat jako názvy uživatelských účtů nuget.org.</span><span class="sxs-lookup"><span data-stu-id="28aaf-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="28aaf-112">Odstraňují se zákaznická data</span><span class="sxs-lookup"><span data-stu-id="28aaf-112">Deleting customer data</span></span>

<span data-ttu-id="28aaf-113">Požadavek na odstranění uživatelských dat z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="28aaf-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="28aaf-114">Uživatel se musí přihlásit k [NuGet.org](https://www.nuget.org) .</span><span class="sxs-lookup"><span data-stu-id="28aaf-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="28aaf-115">Uživatel musí odeslat žádost o odstranění účtu [NuGet.org/Account/Delete](https://www.nuget.org/account/delete) .</span><span class="sxs-lookup"><span data-stu-id="28aaf-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="28aaf-116">Uživatelům, kteří jsou jedinými vlastníky balíčků, doporučujeme najít nové vlastníky a teprve potom požádat o odstranění svého účtu.</span><span class="sxs-lookup"><span data-stu-id="28aaf-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="28aaf-117">Pokud vlastnictví balíčku není předáno, balíček NuGet není v seznamu k dispozici a v důsledku toho již není k dispozici ve vyhledávacích dotazech v sadě Visual Studio nebo na webu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="28aaf-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="28aaf-118">Před odstraněním účtu můžou správci nuget.org pracovat s uživatelem, aby našli nové vlastníky pro balíčky, které vlastní.</span><span class="sxs-lookup"><span data-stu-id="28aaf-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="28aaf-119">Akci odstranění účtu dokončí správce nuget.org do 30 dnů od data žádosti.</span><span class="sxs-lookup"><span data-stu-id="28aaf-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="28aaf-120">Při odstranění účtu se všechna data uživatele odeberou ze systému nuget.org a provedou se následující akce:</span><span class="sxs-lookup"><span data-stu-id="28aaf-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="28aaf-121">Odstraněné účty se neregistrují u nuget.org.</span><span class="sxs-lookup"><span data-stu-id="28aaf-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="28aaf-122">Odstraní se všechny vlastněné klíče rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="28aaf-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="28aaf-123">Všechny rezervované obory názvů jsou vydané.</span><span class="sxs-lookup"><span data-stu-id="28aaf-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="28aaf-124">Odstraní se všechna vlastnictví balíčku.</span><span class="sxs-lookup"><span data-stu-id="28aaf-124">Any package ownership are removed</span></span>

<span data-ttu-id="28aaf-125">Vlastněné *balíčky se neodstraňují* .</span><span class="sxs-lookup"><span data-stu-id="28aaf-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="28aaf-126">I když není seznam z výsledků hledání dostupný, zůstávají k dispozici prostřednictvím obnovení balíčků na projektech, které jsou na nich závislé.</span><span class="sxs-lookup"><span data-stu-id="28aaf-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="28aaf-127">Export zákaznických dat</span><span class="sxs-lookup"><span data-stu-id="28aaf-127">Exporting customer data</span></span>

<span data-ttu-id="28aaf-128">Po přihlášení do nuget.org může uživatel odeslat žádost o export prostřednictvím [NuGet.org/policies/Contact](https://www.nuget.org/policies/Contact) .</span><span class="sxs-lookup"><span data-stu-id="28aaf-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="28aaf-129">Exportovaná data jsou k dispozici po dobu 48 hodin uživateli ke stažení prostřednictvím objektu blob Azure.</span><span class="sxs-lookup"><span data-stu-id="28aaf-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="28aaf-130">Po 48 hodinách vyprší platnost přístupu a uživatel musí podle potřeby Odeslat novou žádost o export.</span><span class="sxs-lookup"><span data-stu-id="28aaf-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="28aaf-131">Exportovaná data zahrnují:</span><span class="sxs-lookup"><span data-stu-id="28aaf-131">The exported data includes:</span></span>

* <span data-ttu-id="28aaf-132">Žádosti o podporu pro uživatele</span><span class="sxs-lookup"><span data-stu-id="28aaf-132">The user's support requests</span></span>
* <span data-ttu-id="28aaf-133">Akce uživatele (publikovat balíček, vytvořit účet) jako trvalé v protokolech auditu</span><span class="sxs-lookup"><span data-stu-id="28aaf-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="28aaf-134">Všechny informace o uživatelích jako trvalé v protokolech služby IIS</span><span class="sxs-lookup"><span data-stu-id="28aaf-134">Any user information as persisted in the IIS logs</span></span>
