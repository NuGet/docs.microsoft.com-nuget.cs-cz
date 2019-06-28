---
title: Vaše organizace na NuGet.org
description: Organizace na NuGet.org vám umožní spravovat balíčky publikovaná podle skupiny nebo týmu, firemní prostředí.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427539"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="0b487-103">Vaše organizace na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0b487-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="0b487-104">Organizacím umožňují podnikům a open source projekty, spolupracovat na balíčky pomocí jediné identity NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0b487-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="0b487-105">Pro spotřebitele balíčku zobrazí se stejná jako existující uživatelský účet na NuGet.org účet organizace.</span><span class="sxs-lookup"><span data-stu-id="0b487-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="0b487-106">Účty organizace a samostatné účty</span><span class="sxs-lookup"><span data-stu-id="0b487-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="0b487-107">Účet organizace má jeden nebo více účtů osoba (uživatel) jako členy.</span><span class="sxs-lookup"><span data-stu-id="0b487-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="0b487-108">Tyto členy můžete spravovat sadu balíčků při zachování jedinou identitu pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="0b487-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="0b487-109">Svého individuálního účtu je svoji identitu na NuGet.org a může mít libovolný počet organizace.</span><span class="sxs-lookup"><span data-stu-id="0b487-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="0b487-110">Balíček může patřit k účtu organizace jako můžou patřit do individuálního účtu.</span><span class="sxs-lookup"><span data-stu-id="0b487-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="0b487-111">Balíček příjemci nezobrazuje žádný rozdíl mezi samostatný účet nebo účet organizace: oba se objeví jako balíček `owners`.</span><span class="sxs-lookup"><span data-stu-id="0b487-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="0b487-112">Přidává se nová organizace</span><span class="sxs-lookup"><span data-stu-id="0b487-112">Adding a new organization</span></span>

<span data-ttu-id="0b487-113">Pokud chcete přidat novou organizaci, vyberte svůj účet na NuGet.org a pak vyberte **Správa organizace...**  příkazu nabídky:</span><span class="sxs-lookup"><span data-stu-id="0b487-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Možnost nabídky na NuGet.org pro správce organizace](media/org-manage-option.png)

<span data-ttu-id="0b487-115">Na další stránce vyberte **přidat novou organizaci** tlačítka:</span><span class="sxs-lookup"><span data-stu-id="0b487-115">On the next page, select the **Add new organization** button:</span></span>

![Pro vytvoření nové organizace na NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="0b487-117">Na další stránce zadejte jméno a e-mailovou adresu organizace.</span><span class="sxs-lookup"><span data-stu-id="0b487-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="0b487-118">Protože účty organizace sdílejí stejný obor názvů jako uživatelské účty, název organizace musí být odlišné od všech existující organizace nebo uživatelské účty.</span><span class="sxs-lookup"><span data-stu-id="0b487-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="0b487-119">E-mailová adresa musí být také jedinečný ve všech účtech.</span><span class="sxs-lookup"><span data-stu-id="0b487-119">The email address must also be unique across all accounts.</span></span>

![Přidejte novou stránku organizace na NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="0b487-121">Po vytvoření účtu organizace, se na správce a můžete odesílat balíčky pro organizaci a přidat členy organizace.</span><span class="sxs-lookup"><span data-stu-id="0b487-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="0b487-122">Transformace existující účet organizace</span><span class="sxs-lookup"><span data-stu-id="0b487-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="0b487-123">Převod účtu je nevratná operace: nelze transformovat organizace zpět na uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="0b487-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="0b487-124">Pokud už správu balíčků v týmu pomocí jediného uživatelského účtu a chcete převést na tento účet organizace, použijte **transformovat váš účet organizace** možnost **Správa organizace** stránky:</span><span class="sxs-lookup"><span data-stu-id="0b487-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Možnost převést existující účet organizace na NuGet.org](media/org-transform-option.png)

<span data-ttu-id="0b487-126">Na další stránce zadejte jiného uživatelského účtu přiřadit jako správce organizace, a pak vyberte **transformace**.</span><span class="sxs-lookup"><span data-stu-id="0b487-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Zadání informací pro transformaci uživatelský účet organizace](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="0b487-128">Správa organizace členy</span><span class="sxs-lookup"><span data-stu-id="0b487-128">Managing organization members</span></span>

<span data-ttu-id="0b487-129">Jako správce organizace, můžete přidat členy tím, že poskytuje každý člen NuGet.org *název uživatelského účtu*; e-mailové adresy nelze použít.</span><span class="sxs-lookup"><span data-stu-id="0b487-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="0b487-130">Pak označit každý člen jako spolupracovník nebo správce s následujícími oprávněními:</span><span class="sxs-lookup"><span data-stu-id="0b487-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="0b487-131">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="0b487-131">Permission</span></span> | <span data-ttu-id="0b487-132">Spolupracovníka</span><span class="sxs-lookup"><span data-stu-id="0b487-132">Collaborator</span></span> | <span data-ttu-id="0b487-133">Správce</span><span class="sxs-lookup"><span data-stu-id="0b487-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b487-134">Správa balíčků pro organizaci</span><span class="sxs-lookup"><span data-stu-id="0b487-134">Manage the organization's packages</span></span><br/><span data-ttu-id="0b487-135">(odeslání nové balíčky, aktualizace nebo vyjmutí ze seznamu existujících balíčků)</span><span class="sxs-lookup"><span data-stu-id="0b487-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="0b487-136">Ano</span><span class="sxs-lookup"><span data-stu-id="0b487-136">Yes</span></span> | <span data-ttu-id="0b487-137">Ano</span><span class="sxs-lookup"><span data-stu-id="0b487-137">Yes</span></span> |
| <span data-ttu-id="0b487-138">Změna organizace metadat</span><span class="sxs-lookup"><span data-stu-id="0b487-138">Change organization metadata</span></span><br/><span data-ttu-id="0b487-139">(e-mailovou adresu, nastavení oznámení)</span><span class="sxs-lookup"><span data-stu-id="0b487-139">(email address, notification settings)</span></span> | <span data-ttu-id="0b487-140">Ne</span><span class="sxs-lookup"><span data-stu-id="0b487-140">No</span></span> | <span data-ttu-id="0b487-141">Ano</span><span class="sxs-lookup"><span data-stu-id="0b487-141">Yes</span></span> |
| <span data-ttu-id="0b487-142">Spravovat členy organizace</span><span class="sxs-lookup"><span data-stu-id="0b487-142">Manage organization members</span></span> | <span data-ttu-id="0b487-143">Ne</span><span class="sxs-lookup"><span data-stu-id="0b487-143">No</span></span> | <span data-ttu-id="0b487-144">Ano</span><span class="sxs-lookup"><span data-stu-id="0b487-144">Yes</span></span> |
| <span data-ttu-id="0b487-145">Požádat o nebo reagovat na požadavky co-ownership pro organizaci balíčky</span><span class="sxs-lookup"><span data-stu-id="0b487-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="0b487-146">Ne</span><span class="sxs-lookup"><span data-stu-id="0b487-146">No</span></span> | <span data-ttu-id="0b487-147">Ano</span><span class="sxs-lookup"><span data-stu-id="0b487-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="0b487-148">Správa balíčků</span><span class="sxs-lookup"><span data-stu-id="0b487-148">Managing packages</span></span>

<span data-ttu-id="0b487-149">Můžete zobrazit všechny balíčky přes svůj účet a všechny organizace, kterých jste členem na [spravovat balíčky](https://www.nuget.org/account/Packages) stránky.</span><span class="sxs-lookup"><span data-stu-id="0b487-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="0b487-150">Chcete-li zobrazit balíčky, které jsou specifické pro váš účet nebo libovolné konkrétní organizaci, použijte filtr účty v horní části stránky.</span><span class="sxs-lookup"><span data-stu-id="0b487-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Správa balíčků s filtrem účtu](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="0b487-152">Přenos balíčků do organizace</span><span class="sxs-lookup"><span data-stu-id="0b487-152">Transferring packages to an organization</span></span>
<span data-ttu-id="0b487-153">Pokud chcete převést některé své balíčky do nově vytvořeného organizace, můžete k tomu vyžádání účet organizace, který chcete spoluvlastní balíček a odebrat sami sebe jako vlastníka.</span><span class="sxs-lookup"><span data-stu-id="0b487-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="0b487-154">Pokud jste správcem organizace, neexistuje žádná potvrzení vyžadovat, abyste přijali vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="0b487-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="0b487-155">Ale pokud spolupracovníka, přidání organizace jako vlastníka vyžaduje jednu z Správci tak, aby přijímal vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="0b487-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="0b487-156">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="0b487-156">Publishing packages</span></span>

<span data-ttu-id="0b487-157">Publikovat balíčky organizace jako publikovat balíčky uživatelský účet: přímo nahráním balíček do NuGet.org nebo vynucením balíček `nuget push` nebo `dotnet nuget push` příkazy rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="0b487-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="0b487-158">Nahrání balíčků</span><span class="sxs-lookup"><span data-stu-id="0b487-158">Uploading packages</span></span>

<span data-ttu-id="0b487-159">Když můžete přímo nahrát nový balíček na [nahrát NuGet.org](https://www.nuget.org/packages/manage/upload) stránce přiřadit vlastníka balíčku k účtu uživatele nebo organizaci:</span><span class="sxs-lookup"><span data-stu-id="0b487-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Nahrání balíčku s možností účtu](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="0b487-161">Pomocí klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="0b487-161">Using API keys</span></span>

<span data-ttu-id="0b487-162">Vložit balíčku `nuget push` nebo `dotnet nuget push` příkazy rozhraní příkazového řádku, je nutné získat klíč rozhraní API vyžaduje těchto příkazů.</span><span class="sxs-lookup"><span data-stu-id="0b487-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="0b487-163">Podrobnosti najdete v tématu [publikování balíčku](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="0b487-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="0b487-164">Při vytváření nového klíče rozhraní API, vyberte příslušné organizaci **vlastníka balíčku** rozevírací seznam.</span><span class="sxs-lookup"><span data-stu-id="0b487-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="0b487-165">Žádné klíče rozhraní API, které vytvoříte se vztahuje pouze na zvoleném organizace:</span><span class="sxs-lookup"><span data-stu-id="0b487-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Klíč rozhraní API s možností účtu](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="0b487-167">Odebrání organizace</span><span class="sxs-lookup"><span data-stu-id="0b487-167">Removing an organization</span></span>

<span data-ttu-id="0b487-168">Jako uživatel, můžete odebrat sami sebe z organizace tak, že vyberete **X** tlačítko zobrazí vaše členství v organizaci:</span><span class="sxs-lookup"><span data-stu-id="0b487-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Odebrání uživatelského účtu z organizace](media/org-remove-self-option.png)

<span data-ttu-id="0b487-170">Správci můžou odeberte všechny členy z organizace, včetně jiných správců.</span><span class="sxs-lookup"><span data-stu-id="0b487-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="0b487-171">Pokud jste jediným správcem organizace, nemůžete se sami odebrat není-li přidat jiného člena jako správce.</span><span class="sxs-lookup"><span data-stu-id="0b487-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="0b487-172">Odstraňuje se účet organizace</span><span class="sxs-lookup"><span data-stu-id="0b487-172">Deleting an organization account</span></span>

<span data-ttu-id="0b487-173">Účet organizace můžete odstranit kliknutím **odstranit** tlačítko zobrazené na stránce vaší organizace.</span><span class="sxs-lookup"><span data-stu-id="0b487-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Odstranit organizaci](media/org-delete-option.png)

<span data-ttu-id="0b487-175">Odstranit organizace, musíte potvrdit ho kliknutím **odstranit organizaci** tlačítko potvrzení.</span><span class="sxs-lookup"><span data-stu-id="0b487-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
