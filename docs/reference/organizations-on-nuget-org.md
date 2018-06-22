---
title: Organizace v nuget.org
description: Organizace v nuget.org pomáhá spravovat balíčky publikovaná podle skupiny nebo v týmu, firemní prostředí.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449575"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="8cc10-103">Organizace v nuget.org</span><span class="sxs-lookup"><span data-stu-id="8cc10-103">Organization on nuget.org</span></span>

<span data-ttu-id="8cc10-104">Organizace povolit podnikům a open source projekty spolupracovat na balíčky pomocí jednoho nuget.org identity.</span><span class="sxs-lookup"><span data-stu-id="8cc10-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="8cc10-105">Pro balíček příjemce zobrazí se stejné jako existující účet uživatele v nuget.org účet organizace.</span><span class="sxs-lookup"><span data-stu-id="8cc10-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="8cc10-106">Uživatelské účty a účty organizace</span><span class="sxs-lookup"><span data-stu-id="8cc10-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="8cc10-107">Váš uživatelský účet je své identity na nuget.org a může být členem skupiny libovolný počet organizace.</span><span class="sxs-lookup"><span data-stu-id="8cc10-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="8cc10-108">Balíček může patřit k účtu organizace jako můžou patřit na uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="8cc10-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="8cc10-109">Balíček příjemci nevidíte žádný rozdíl mezi uživatelský účet nebo účet organizace: obě zobrazí jako balíček `owners`.</span><span class="sxs-lookup"><span data-stu-id="8cc10-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="8cc10-110">Účet organizace obsahuje jeden nebo více uživatelské účty jako členy.</span><span class="sxs-lookup"><span data-stu-id="8cc10-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="8cc10-111">Tito členové můžete spravovat sadu balíčky současně zachovat jedinou identitu pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="8cc10-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="8cc10-112">Přidání nové organizace</span><span class="sxs-lookup"><span data-stu-id="8cc10-112">Adding a new organization</span></span>

<span data-ttu-id="8cc10-113">Chcete-li přidat nové organizace, vyberte svůj účet na nuget.org a poté vyberte **Spravovat organizace...**  příkazu v nabídce:</span><span class="sxs-lookup"><span data-stu-id="8cc10-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Možnost nabídky v nuget.org pro správce organizace](media/org-manage-option.png)

<span data-ttu-id="8cc10-115">Na další stránce, vyberte **přidat nové organizace** tlačítko:</span><span class="sxs-lookup"><span data-stu-id="8cc10-115">On the next page, select the **Add new organization** button:</span></span>

![Tlačítko vytvořte novou organizaci v nuget.org](media/org-add-new-option.png)

<span data-ttu-id="8cc10-117">Na další stránce zadejte jméno a e-mailovou adresu organizace.</span><span class="sxs-lookup"><span data-stu-id="8cc10-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="8cc10-118">Vzhledem k tomu, že účty organizace sdílet stejný obor názvů jako uživatelské účty, název organizace musí být odlišný od jiných stávající organizace nebo uživatelské účty.</span><span class="sxs-lookup"><span data-stu-id="8cc10-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="8cc10-119">E-mailová adresa musí být také jedinečný mezi všechny účty.</span><span class="sxs-lookup"><span data-stu-id="8cc10-119">The email address must also be unique across all accounts.</span></span>

![Přidat novou stránku organizace v nuget.org](media/org-add-new-page.png)

<span data-ttu-id="8cc10-121">Po vytvoření účtu organizace se na správce a můžete odeslat balíčky pro organizaci a přidat členy organizace.</span><span class="sxs-lookup"><span data-stu-id="8cc10-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="8cc10-122">Transformace existující účet organizace</span><span class="sxs-lookup"><span data-stu-id="8cc10-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="8cc10-123">Převod účet je nevratné: nelze transformovat organizaci zpět na uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="8cc10-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="8cc10-124">Pokud jste spravovat balíčky jako tým pomocí jediného uživatelského účtu a chcete převést na organizaci, použijte tento účet **transformace váš účet organizace** možnost **Spravovat organizace** stránky:</span><span class="sxs-lookup"><span data-stu-id="8cc10-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Možnost v nuget.org k transformaci existující účet organizace](media/org-transform-option.png)

<span data-ttu-id="8cc10-126">Na další stránce zadejte jiného uživatelského účtu přiřadit jako správce organizace, a pak vyberte **transformace**.</span><span class="sxs-lookup"><span data-stu-id="8cc10-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Zadávání informací pro transformaci účet uživatele organizaci](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="8cc10-128">Správa organizace členy</span><span class="sxs-lookup"><span data-stu-id="8cc10-128">Managing organization members</span></span>

<span data-ttu-id="8cc10-129">Jako správce organizace, můžete přidat členy tím, že poskytuje každý člen nuget.org *název uživatelského účtu*; e-mailové adresy nelze použít.</span><span class="sxs-lookup"><span data-stu-id="8cc10-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="8cc10-130">Potom můžete označit každého člena jako spolupracovník nebo správce s následujícími oprávněními:</span><span class="sxs-lookup"><span data-stu-id="8cc10-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="8cc10-131">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="8cc10-131">Permission</span></span> | <span data-ttu-id="8cc10-132">Spolupracovníka</span><span class="sxs-lookup"><span data-stu-id="8cc10-132">Collaborator</span></span> | <span data-ttu-id="8cc10-133">Správce</span><span class="sxs-lookup"><span data-stu-id="8cc10-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8cc10-134">Správa balíčků organizace</span><span class="sxs-lookup"><span data-stu-id="8cc10-134">Manage the organization's packages</span></span><br/><span data-ttu-id="8cc10-135">(odeslání nové balíčky, aktualizace nebo unlist existující balíčky)</span><span class="sxs-lookup"><span data-stu-id="8cc10-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="8cc10-136">Ano</span><span class="sxs-lookup"><span data-stu-id="8cc10-136">Yes</span></span> | <span data-ttu-id="8cc10-137">Ano</span><span class="sxs-lookup"><span data-stu-id="8cc10-137">Yes</span></span> |
| <span data-ttu-id="8cc10-138">Změna organizace metadat</span><span class="sxs-lookup"><span data-stu-id="8cc10-138">Change organization metadata</span></span><br/><span data-ttu-id="8cc10-139">(e-mailovou adresu, nastavení oznámení)</span><span class="sxs-lookup"><span data-stu-id="8cc10-139">(email address, notification settings)</span></span> | <span data-ttu-id="8cc10-140">Ne</span><span class="sxs-lookup"><span data-stu-id="8cc10-140">No</span></span> | <span data-ttu-id="8cc10-141">Ano</span><span class="sxs-lookup"><span data-stu-id="8cc10-141">Yes</span></span> |
| <span data-ttu-id="8cc10-142">Spravovat členy organizace</span><span class="sxs-lookup"><span data-stu-id="8cc10-142">Manage organization members</span></span> | <span data-ttu-id="8cc10-143">Ne</span><span class="sxs-lookup"><span data-stu-id="8cc10-143">No</span></span> | <span data-ttu-id="8cc10-144">Ano</span><span class="sxs-lookup"><span data-stu-id="8cc10-144">Yes</span></span> |
| <span data-ttu-id="8cc10-145">Žádosti o nebo provádět akce s co-ownership požadavky organizace balíčky</span><span class="sxs-lookup"><span data-stu-id="8cc10-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="8cc10-146">Ne</span><span class="sxs-lookup"><span data-stu-id="8cc10-146">No</span></span> | <span data-ttu-id="8cc10-147">Ano</span><span class="sxs-lookup"><span data-stu-id="8cc10-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="8cc10-148">Spravovat balíčky</span><span class="sxs-lookup"><span data-stu-id="8cc10-148">Managing packages</span></span>

<span data-ttu-id="8cc10-149">Můžete zobrazit všechny balíčky přes svůj účet a všechny organizace, ve kterých jste členem na [spravovat balíčky](https://www.nuget.org/account/Packages) stránky.</span><span class="sxs-lookup"><span data-stu-id="8cc10-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="8cc10-150">Pokud chcete zobrazit balíčky, které jsou specifické pro váš účet nebo žádné konkrétní organizace, použijte filtr účty v horní pravé části stránky.</span><span class="sxs-lookup"><span data-stu-id="8cc10-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Spravovat balíčky s filtrem účtu](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="8cc10-152">Přenášení balíčky organizaci</span><span class="sxs-lookup"><span data-stu-id="8cc10-152">Transferring packages to an organization</span></span>
<span data-ttu-id="8cc10-153">Pokud chcete některé z vašich balíčků přenést do nově vytvořené organizace, můžete tak učinit vyžádáním účet organizace společně vlastní balíček a odebrání sami jako vlastník.</span><span class="sxs-lookup"><span data-stu-id="8cc10-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="8cc10-154">Pokud jste správce organizace, není třeba tak, aby přijímal vlastnictví bez potvrzení.</span><span class="sxs-lookup"><span data-stu-id="8cc10-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="8cc10-155">Ale pokud jste spolupracovníka, přidání organizace jako vlastníka vyžaduje jednu správců tak, aby přijímal vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="8cc10-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="8cc10-156">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="8cc10-156">Publishing packages</span></span>

<span data-ttu-id="8cc10-157">Publikování balíčků organizaci jako publikovat balíčky na uživatelský účet: přímo nahrávat balíček k nuget.org nebo vynucením balíček `nuget push` nebo `dotnet nuget push` rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="8cc10-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="8cc10-158">Nahrává balíčky</span><span class="sxs-lookup"><span data-stu-id="8cc10-158">Uploading packages</span></span>

<span data-ttu-id="8cc10-159">Pokud jste přímo nahrát nový balíček na [nuget.org nahrávání](https://www.nuget.org/packages/manage/upload) stránky, můžete přiřadit vlastníka balíčku na účet uživatele nebo organizaci:</span><span class="sxs-lookup"><span data-stu-id="8cc10-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Nahrání balíčku s možností účtu](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="8cc10-161">Použití klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="8cc10-161">Using API keys</span></span>

<span data-ttu-id="8cc10-162">Tak, aby nabízel balíček `nuget push` nebo `dotnet nuget push` příkazy rozhraní příkazového řádku, je nutné získat klíč rozhraní API vyžaduje těchto příkazů.</span><span class="sxs-lookup"><span data-stu-id="8cc10-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="8cc10-163">Podrobnosti najdete v tématu [publikování balíčku](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="8cc10-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="8cc10-164">Při vytváření nového klíče rozhraní API, vyberte v příslušné organizace **vlastníka balíčku** rozevírací nabídku.</span><span class="sxs-lookup"><span data-stu-id="8cc10-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="8cc10-165">Všechny klíč rozhraní API, které vytvoříte, se vztahuje pouze na vybrané organizace:</span><span class="sxs-lookup"><span data-stu-id="8cc10-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Klíč rozhraní API s možností účtu](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="8cc10-167">Odebrání organizace</span><span class="sxs-lookup"><span data-stu-id="8cc10-167">Removing an organization</span></span>

<span data-ttu-id="8cc10-168">Jako uživatel, můžete odebrat sami z organizace tak, že vyberete `X` tlačítko zobrazené ve vaší organizaci členství:</span><span class="sxs-lookup"><span data-stu-id="8cc10-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Odebráním účet uživatele organizaci](media/org-remove-self-option.png)

<span data-ttu-id="8cc10-170">Od organizace, včetně jiní správci mohou správci kteréhokoli člena odebrat.</span><span class="sxs-lookup"><span data-stu-id="8cc10-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="8cc10-171">Pokud jste jediným správcem v organizaci, nelze sami odebrat, není-li přidat jiného člena jako správce.</span><span class="sxs-lookup"><span data-stu-id="8cc10-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="8cc10-172">Odstranění účtu organizace</span><span class="sxs-lookup"><span data-stu-id="8cc10-172">Deleting an organization account</span></span>

<span data-ttu-id="8cc10-173">Tato funkce bude brzy k dispozici.</span><span class="sxs-lookup"><span data-stu-id="8cc10-173">This feature is coming soon.</span></span>
