---
title: Samostatné účty
description: Jednotlivé acccounts na NuGet.org je potřeba publikovat balíčky
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427557"
---
# <a name="individual-accounts"></a><span data-ttu-id="8e5b4-103">Samostatné účty</span><span class="sxs-lookup"><span data-stu-id="8e5b4-103">Individual accounts</span></span>

<span data-ttu-id="8e5b4-104">Musíte vytvořit samostatný účet pro publikování a správě balíčků na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="8e5b4-105">Samostatné účty a účty organizace</span><span class="sxs-lookup"><span data-stu-id="8e5b4-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="8e5b4-106">Váš účet osoba (uživatel) je svoji identitu na NuGet.org a může mít libovolný počet organizace.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="8e5b4-107">Balíček může patřit k účtu organizace jako můžou patřit do individuálního účtu.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="8e5b4-108">Balíček příjemci nezobrazuje žádný rozdíl mezi samostatný účet nebo účet organizace: oba se objeví jako balíček `owners`.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="8e5b4-109">Účet organizace má jeden nebo více samostatné účty jako členy.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="8e5b4-110">Tyto členy můžete spravovat sadu balíčků při zachování jedinou identitu pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="8e5b4-111">Přidat nový individuálního účtu</span><span class="sxs-lookup"><span data-stu-id="8e5b4-111">Add a new individual account</span></span>

<span data-ttu-id="8e5b4-112">Pokud chcete vytvořit účet NuGet.org, potřebujete osobní účet Microsoft (MSA) nebo účet Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="8e5b4-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="8e5b4-113">Pokud nemáte, můžete si [vytvořit](https://signup.live.com) jeden.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="8e5b4-114">Pokud již máte účet MSA nebo AAD, postupujte podle následujících kroků.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="8e5b4-115">Přejděte [NuGet.org přihlašovací stránku](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="8e5b4-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="8e5b4-116">Klikněte na **přihlásit se účtem Microsoft** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="8e5b4-117">Zadejte svůj účet Microsoft nebo podrobnosti o účtu služby Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="8e5b4-118">Po klepnutí na **Ano** tak, aby přijímal oprávnění k *NuGet.org* aplikace.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Udělení oprávnění ke NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="8e5b4-120">Budete přesměrováni na *nuget.org*a zobrazí se výzva k registraci uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="8e5b4-121">Zadejte uživatelské jméno do vstupního pole.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-121">Specify the username in the input box.</span></span> <span data-ttu-id="8e5b4-122">Pamatujte, že uživatelské jméno **je** malá a velká citlivé a nelze změnit ani přejmenovat později.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Zadejte uživatelské jméno na NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="8e5b4-124">Klikněte na tlačítko **zaregistrovat** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-124">Click the **Register** button.</span></span>

<span data-ttu-id="8e5b4-125">Teď máte účet NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="8e5b4-126">Správa účtů můžete provádět na [nastavení účtu](https://www.nuget.org/account) stránky.</span><span class="sxs-lookup"><span data-stu-id="8e5b4-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
