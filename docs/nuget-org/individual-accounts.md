---
title: Jednotlivé účty
description: Pro publikování balíčků se vyžadují jednotlivé acccounts na NuGet.org.
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c88b88015bd6d5bae4789765126c0a3dec527e24
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419848"
---
# <a name="individual-accounts"></a><span data-ttu-id="4bad8-103">Jednotlivé účty</span><span class="sxs-lookup"><span data-stu-id="4bad8-103">Individual accounts</span></span>

<span data-ttu-id="4bad8-104">Abyste mohli publikovat a spravovat balíčky na NuGet.org, musíte vytvořit jednotlivý účet.</span><span class="sxs-lookup"><span data-stu-id="4bad8-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="4bad8-105">Jednotlivé účty vs. účty organizace</span><span class="sxs-lookup"><span data-stu-id="4bad8-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="4bad8-106">Váš jednotlivý uživatelský účet je vaší identitou v NuGet.org a může být členem libovolného počtu organizací.</span><span class="sxs-lookup"><span data-stu-id="4bad8-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="4bad8-107">Balíček může patřit k účtu organizace, jako by mohl patřit k individuálnímu účtu.</span><span class="sxs-lookup"><span data-stu-id="4bad8-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="4bad8-108">Uživatelé balíčku nevidí žádný rozdíl mezi jednotlivými účty nebo účtem organizace: obě se zobrazí jako balíčky `owners`.</span><span class="sxs-lookup"><span data-stu-id="4bad8-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="4bad8-109">Účet organizace má jako členy jeden nebo více jednotlivých účtů.</span><span class="sxs-lookup"><span data-stu-id="4bad8-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="4bad8-110">Tito členové mohou spravovat sadu balíčků a přitom zachovat jedinou identitu pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="4bad8-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="4bad8-111">Přidat nový jednotlivý účet</span><span class="sxs-lookup"><span data-stu-id="4bad8-111">Add a new individual account</span></span>

<span data-ttu-id="4bad8-112">Pokud chcete vytvořit účet NuGet.org, musíte mít osobní účet Microsoft (MSA) nebo účet Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="4bad8-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="4bad8-113">Pokud žádný nemáte, můžete si ho [vytvořit](https://signup.live.com) .</span><span class="sxs-lookup"><span data-stu-id="4bad8-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="4bad8-114">Pokud máte účet MSA nebo AAD, postupujte podle následujících kroků.</span><span class="sxs-lookup"><span data-stu-id="4bad8-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="4bad8-115">Přejít na [přihlašovací stránku NuGet.org](https://www.nuget.org/users/account/LogOn)</span><span class="sxs-lookup"><span data-stu-id="4bad8-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="4bad8-116">Klikněte na tlačítko **Přihlásit se účtem Microsoft** .</span><span class="sxs-lookup"><span data-stu-id="4bad8-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="4bad8-117">Zadejte účet Microsoft nebo Azure Active Directory podrobnosti účtu.</span><span class="sxs-lookup"><span data-stu-id="4bad8-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="4bad8-118">Kliknutím na **Ano** přijměte oprávnění k aplikaci *NuGet.org* .</span><span class="sxs-lookup"><span data-stu-id="4bad8-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Udělení oprávnění NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="4bad8-120">Budete přesměrováni na *NuGet.org*a požádáni, abyste zaregistrovali uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="4bad8-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="4bad8-121">Do vstupního pole zadejte uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="4bad8-121">Specify the username in the input box.</span></span> <span data-ttu-id="4bad8-122">Všimněte si, **že uživatelské jméno** rozlišuje velká a malá písmena a nelze je změnit nebo přejmenovat později.</span><span class="sxs-lookup"><span data-stu-id="4bad8-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Zadat uživatelské jméno na NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="4bad8-124">Klikněte na tlačítko **Registrovat** .</span><span class="sxs-lookup"><span data-stu-id="4bad8-124">Click the **Register** button.</span></span>

<span data-ttu-id="4bad8-125">Teď máte účet NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4bad8-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="4bad8-126">Správu účtů můžete provádět na stránce [Nastavení účtu](https://www.nuget.org/account) .</span><span class="sxs-lookup"><span data-stu-id="4bad8-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="4bad8-127">Povolit dvojúrovňové ověřování (2FA)</span><span class="sxs-lookup"><span data-stu-id="4bad8-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="4bad8-128">Chcete-li lépe chránit svůj účet, povolte dvojúrovňové ověřování (doporučeno).</span><span class="sxs-lookup"><span data-stu-id="4bad8-128">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="4bad8-129">Když se přihlásíte k účtu, otevřete svůj profil a v části **přihlašovací účet**vyberte **Povolit** .</span><span class="sxs-lookup"><span data-stu-id="4bad8-129">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Povolit 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="4bad8-131">Zobrazí se zpráva s informacemi o tom, že při příštím přihlášení k *NuGet.org*budete požádáni o další přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="4bad8-131">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="4bad8-132">Pokud chcete ověřování dokončit, odhlaste se a znovu se přihlaste.</span><span class="sxs-lookup"><span data-stu-id="4bad8-132">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="4bad8-133">Když se přihlásíte, vyberte jako druhou formu ověřování buď text, nebo e-mail.</span><span class="sxs-lookup"><span data-stu-id="4bad8-133">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="4bad8-134">Ověřte telefonní číslo nebo e-mailovou adresu, která je už přidružená k vašemu účet Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4bad8-134">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="4bad8-135">Pro svůj účet možná budete muset zadat nové telefonní číslo nebo e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="4bad8-135">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="4bad8-136">Pokud ano, zadejte požadované informace podle pokynů a klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="4bad8-136">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Povolit 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="4bad8-138">Ověřte svoje zařízení nebo e-mailový účet a zadejte kód, který jste právě odeslali.</span><span class="sxs-lookup"><span data-stu-id="4bad8-138">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Povolit 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="4bad8-140">Dokončete dvojúrovňové ověřování podle všech dalších pokynů.</span><span class="sxs-lookup"><span data-stu-id="4bad8-140">Follow any additional instructions to complete Two-factor authentication.</span></span>
