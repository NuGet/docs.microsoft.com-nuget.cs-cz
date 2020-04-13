---
title: Jednotlivé účty - NuGet.org
description: Jednotlivé počty na NuGet.org jsou povinny publikovat balíky
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429015"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="680ef-103">Jednotlivé účty na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="680ef-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="680ef-104">Chcete-li publikovat a spravovat balíčky v NuGet.org, musíte vytvořit individuální účet.</span><span class="sxs-lookup"><span data-stu-id="680ef-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="680ef-105">Jednotlivé účty a účty organizace</span><span class="sxs-lookup"><span data-stu-id="680ef-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="680ef-106">Váš individuální (uživatelský) účet je vaše identita na NuGet.org a může být členem libovolného počtu organizací.</span><span class="sxs-lookup"><span data-stu-id="680ef-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="680ef-107">Balíček může patřit k účtu organizace, stejně jako může patřit k individuálnímu účtu.</span><span class="sxs-lookup"><span data-stu-id="680ef-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="680ef-108">Spotřebitelé balíčků nevidí žádný rozdíl mezi individuálním účtem nebo účtem organizace: oba se zobrazují jako balíček `owners`.</span><span class="sxs-lookup"><span data-stu-id="680ef-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="680ef-109">Účet organizace má jeden nebo více individuálních účtů jako své členy.</span><span class="sxs-lookup"><span data-stu-id="680ef-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="680ef-110">Tito členové mohou spravovat sadu balíčků při zachování jedné identity pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="680ef-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="680ef-111">Přidání nového individuálního účtu</span><span class="sxs-lookup"><span data-stu-id="680ef-111">Add a new individual account</span></span>

<span data-ttu-id="680ef-112">Chcete-li vytvořit účet NuGet.org, musíte mít osobní účet Microsoft (MSA) nebo účet Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="680ef-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="680ef-113">Pokud ho nemáte, můžete ho [vytvořit.](https://signup.live.com)</span><span class="sxs-lookup"><span data-stu-id="680ef-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="680ef-114">Pokud máte účet MSA nebo AAD, postupujte podle následujících kroků.</span><span class="sxs-lookup"><span data-stu-id="680ef-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="680ef-115">Přejděte na [přihlašovací stránku NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="680ef-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="680ef-116">Klikněte na **Tlačítko Přihlásit se pomocí Microsoftu.**</span><span class="sxs-lookup"><span data-stu-id="680ef-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="680ef-117">Zadejte podrobnosti o účtu Microsoft nebo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="680ef-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="680ef-118">Chcete-li přijmout oprávnění k NuGet.org *aplikaci,* klepněte na tlačítko **Ano.**</span><span class="sxs-lookup"><span data-stu-id="680ef-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Udělení oprávnění k NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="680ef-120">Budete přesměrováni na *nuget.org*a budete požádáni o registraci uživatelského jména.</span><span class="sxs-lookup"><span data-stu-id="680ef-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="680ef-121">Zadejte uživatelské jméno do vstupního pole.</span><span class="sxs-lookup"><span data-stu-id="680ef-121">Specify the username in the input box.</span></span> <span data-ttu-id="680ef-122">Upozorňujeme, že uživatelské jméno **rozlišuje** malá a velká písmena a nelze jej později změnit ani přejmenovat.</span><span class="sxs-lookup"><span data-stu-id="680ef-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Zadání uživatelského jména v NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="680ef-124">Klepněte na tlačítko **Registrovat.**</span><span class="sxs-lookup"><span data-stu-id="680ef-124">Click the **Register** button.</span></span>

<span data-ttu-id="680ef-125">Nyní máte účet NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="680ef-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="680ef-126">Správu účtu můžete provádět na stránce [nastavení účtu.](https://www.nuget.org/account)</span><span class="sxs-lookup"><span data-stu-id="680ef-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="680ef-127">Povolit dvoufaktorové ověřování (2FA)</span><span class="sxs-lookup"><span data-stu-id="680ef-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="680ef-128">Dvoufaktorové ověřování neboli 2FA je další vrstva zabezpečení používaná při přihlašování k webům nebo aplikacím.</span><span class="sxs-lookup"><span data-stu-id="680ef-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="680ef-129">S 2FA se musíte přihlásit pomocí svého účtu Microsoft (MSA) a poskytnout jinou formu ověřování, kterou znáte nebo k němu máte přístup pouze vy.</span><span class="sxs-lookup"><span data-stu-id="680ef-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="680ef-130">Chcete-li lépe chránit svůj účet, povolte dvoufaktorové ověřování (doporučeno).</span><span class="sxs-lookup"><span data-stu-id="680ef-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="680ef-131">Když se přihlásíte ke svému účtu, otevřete si profil a v části **Přihlašovací účet**zvolte **Povolit** .</span><span class="sxs-lookup"><span data-stu-id="680ef-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Povolit 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="680ef-133">Zobrazí se zpráva s oznámením, že při příštím přihlášení k *nuget.org*budete požádáni o další pověření.</span><span class="sxs-lookup"><span data-stu-id="680ef-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="680ef-134">Chcete-li ověření dokončit, odhlaste se a znovu se přihlaste.</span><span class="sxs-lookup"><span data-stu-id="680ef-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="680ef-135">Při přihlášení zvolte jako druhou formu ověřování text nebo e-mail.</span><span class="sxs-lookup"><span data-stu-id="680ef-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="680ef-136">Ověřte telefonní číslo nebo e-mail, který je již přidružen k vašemu účtu Microsoft.</span><span class="sxs-lookup"><span data-stu-id="680ef-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="680ef-137">Možná budete muset zadat nové telefonní číslo nebo e-mail pro svůj účet.</span><span class="sxs-lookup"><span data-stu-id="680ef-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="680ef-138">Pokud ano, zadejte požadované informace podle pokynů a klepněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="680ef-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Povolit 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="680ef-140">Zkontrolujte zařízení nebo e-mailový účet a zadejte kód, který vám byl právě odeslán.</span><span class="sxs-lookup"><span data-stu-id="680ef-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Povolit 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="680ef-142">Dokončete dvoufaktorové ověřování podle pokynů.</span><span class="sxs-lookup"><span data-stu-id="680ef-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="680ef-143">Povolení 2FA pro váš účet NuGet.org nemá vliv na nastavení ověřování pro jiné účty nebo služby, které mohou být propojeny s účtem Microsoft, který používáte k přihlášení k NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="680ef-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="680ef-144">Odstranění NuGet.org účtu</span><span class="sxs-lookup"><span data-stu-id="680ef-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="680ef-145">Nápovědu k dalším úkolům souvisejícím s účtem, jako je například odstranění NuGet.org účtu, naleznete [v tématu správa účtu NuGet.org](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="680ef-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
