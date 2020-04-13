---
title: Vaše organizace na NuGet.org
description: Organizace na NuGet.org vám pomohou spravovat balíčky publikované podle skupiny nebo v týmovém prostředí společnosti.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427539"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="c1ec6-103">Vaše organizace na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="c1ec6-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="c1ec6-104">Organizace umožňují firmám a projektům s otevřeným zdrojovým kódem spolupracovat na balíčcích pomocí jediné NuGet.org identity.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="c1ec6-105">Pro příjemce balíčku účet organizace se zobrazí stejně jako existující uživatelský účet na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="c1ec6-106">Účty organizace vs. jednotlivé účty</span><span class="sxs-lookup"><span data-stu-id="c1ec6-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="c1ec6-107">Účet organizace má jeden nebo více individuálních (uživatelských) účtů jako svých členů.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="c1ec6-108">Tito členové mohou spravovat sadu balíčků při zachování jedné identity pro vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="c1ec6-109">Váš individuální účet je vaší identitou na NuGet.org a může být členem libovolného počtu organizací.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="c1ec6-110">Balíček může patřit k účtu organizace, stejně jako může patřit k individuálnímu účtu.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="c1ec6-111">Spotřebitelé balíčků nevidí žádný rozdíl mezi individuálním účtem nebo účtem organizace: oba se zobrazují jako balíček `owners`.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="c1ec6-112">Přidání nové organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-112">Adding a new organization</span></span>

<span data-ttu-id="c1ec6-113">Chcete-li přidat novou organizaci, vyberte svůj účet v NuGet.org a pak vyberte příkaz **nabídky Spravovat organizace...**</span><span class="sxs-lookup"><span data-stu-id="c1ec6-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Možnost nabídky v NuGet.org pro manažerské organizace](media/org-manage-option.png)

<span data-ttu-id="c1ec6-115">Na další stránce vyberte tlačítko **Přidat novou organizaci:**</span><span class="sxs-lookup"><span data-stu-id="c1ec6-115">On the next page, select the **Add new organization** button:</span></span>

![Tlačítko pro vytvoření nové organizace v NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="c1ec6-117">Na další stránce zadejte název organizace a e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="c1ec6-118">Vzhledem k tomu, že účty organizace sdílejí stejný obor názvů jako uživatelské účty, musí se název organizace lišit od všech ostatních existujících účtů organizace nebo uživatelů.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="c1ec6-119">E-mailová adresa musí být také jedinečná ve všech účtech.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-119">The email address must also be unique across all accounts.</span></span>

![Přidání nové stránky organizace na NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="c1ec6-121">Po vytvoření účtu organizace jste správcem a můžete odeslat balíčky pro organizaci a přidat členy organizace.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="c1ec6-122">Transformace existujícího účtu na organizaci</span><span class="sxs-lookup"><span data-stu-id="c1ec6-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="c1ec6-123">Převod účtu je nevratný: nelze přeměnit organizaci zpět na uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="c1ec6-124">Pokud spravujete balíčky jako tým pomocí jednoho uživatelského účtu a chcete tento účet převést do organizace, použijte možnost **Transformovat svůj účet na organizaci** na stránce Spravovat **organizace:**</span><span class="sxs-lookup"><span data-stu-id="c1ec6-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Možnost NuGet.org transformovat existující účet na organizaci](media/org-transform-option.png)

<span data-ttu-id="c1ec6-126">Na další stránce zadejte jiný uživatelský účet, který chcete přiřadit jako správce organizace, a pak vyberte **Transformovat**.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Zadávání informací o transformaci uživatelského účtu do organizace](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="c1ec6-128">Správa členů organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-128">Managing organization members</span></span>

<span data-ttu-id="c1ec6-129">Jako správce organizace můžete přidávat členy zadáním *NuGet.org uživatelského účtu*každého člena ; e-mailové adresy nelze použít.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="c1ec6-130">Potom označíte každého člena jako spolupracovníka nebo správce pomocí následujících oprávnění:</span><span class="sxs-lookup"><span data-stu-id="c1ec6-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="c1ec6-131">Oprávnění</span><span class="sxs-lookup"><span data-stu-id="c1ec6-131">Permission</span></span> | <span data-ttu-id="c1ec6-132">Spolupracovník</span><span class="sxs-lookup"><span data-stu-id="c1ec6-132">Collaborator</span></span> | <span data-ttu-id="c1ec6-133">Správce</span><span class="sxs-lookup"><span data-stu-id="c1ec6-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1ec6-134">Správa balíčků organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-134">Manage the organization's packages</span></span><br/><span data-ttu-id="c1ec6-135">(odeslat nové balíčky, aktualizovat nebo zrušit seznam existujících balíčků)</span><span class="sxs-lookup"><span data-stu-id="c1ec6-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="c1ec6-136">Ano</span><span class="sxs-lookup"><span data-stu-id="c1ec6-136">Yes</span></span> | <span data-ttu-id="c1ec6-137">Ano</span><span class="sxs-lookup"><span data-stu-id="c1ec6-137">Yes</span></span> |
| <span data-ttu-id="c1ec6-138">Změna metadat organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-138">Change organization metadata</span></span><br/><span data-ttu-id="c1ec6-139">(e-mailová adresa, nastavení oznámení)</span><span class="sxs-lookup"><span data-stu-id="c1ec6-139">(email address, notification settings)</span></span> | <span data-ttu-id="c1ec6-140">Ne</span><span class="sxs-lookup"><span data-stu-id="c1ec6-140">No</span></span> | <span data-ttu-id="c1ec6-141">Ano</span><span class="sxs-lookup"><span data-stu-id="c1ec6-141">Yes</span></span> |
| <span data-ttu-id="c1ec6-142">Správa členů organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-142">Manage organization members</span></span> | <span data-ttu-id="c1ec6-143">Ne</span><span class="sxs-lookup"><span data-stu-id="c1ec6-143">No</span></span> | <span data-ttu-id="c1ec6-144">Ano</span><span class="sxs-lookup"><span data-stu-id="c1ec6-144">Yes</span></span> |
| <span data-ttu-id="c1ec6-145">Žádost nebo jednat na základě žádostí o spoluvlastnictví pro organizační balíčky</span><span class="sxs-lookup"><span data-stu-id="c1ec6-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="c1ec6-146">Ne</span><span class="sxs-lookup"><span data-stu-id="c1ec6-146">No</span></span> | <span data-ttu-id="c1ec6-147">Ano</span><span class="sxs-lookup"><span data-stu-id="c1ec6-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="c1ec6-148">Správa balíčků</span><span class="sxs-lookup"><span data-stu-id="c1ec6-148">Managing packages</span></span>

<span data-ttu-id="c1ec6-149">Můžete zobrazit všechny balíčky ve vašem účtu a všechny organizace, jejichž jste členem na stránce [Spravovat balíčky.](https://www.nuget.org/account/Packages)</span><span class="sxs-lookup"><span data-stu-id="c1ec6-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="c1ec6-150">Chcete-li zobrazit balíčky specifické pro váš účet nebo konkrétní organizaci, použijte filtr účtů v pravém horním rohu stránky.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Správa balíčků pomocí filtru účtu](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="c1ec6-152">Přenos balíčků do organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-152">Transferring packages to an organization</span></span>
<span data-ttu-id="c1ec6-153">Pokud chcete převést některé balíčky do nově vytvořené organizace, můžete tak učinit tak, že požádáte účet organizace, abyste spoluvlastnili balíček a poté se odebrali jako vlastník.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="c1ec6-154">Pokud jste správcem organizace, není nutné k přijetí vlastnictví žádné potvrzení.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="c1ec6-155">Pokud jste však spolupracovník, přidání organizace jako vlastníka vyžaduje, aby jeden ze správců převzal vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="c1ec6-156">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="c1ec6-156">Publishing packages</span></span>

<span data-ttu-id="c1ec6-157">Publikujete balíčky do organizace, jako je publikování balíčků do uživatelského účtu: přímým `nuget push` nahráním balíčku do NuGet.org nebo odesláním balíčku prostřednictvím příkazů příkazu příkazu příkazu příkazu nebo `dotnet nuget push` CLI.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="c1ec6-158">Nahrávání balíčků</span><span class="sxs-lookup"><span data-stu-id="c1ec6-158">Uploading packages</span></span>

<span data-ttu-id="c1ec6-159">Když přímo nahrajete nový balíček na stránku [NuGet.org Upload,](https://www.nuget.org/packages/manage/upload) přiřadíte vlastníka balíčku k uživatelskému nebo organizačnímu účtu :</span><span class="sxs-lookup"><span data-stu-id="c1ec6-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Možnost Nahrát balíček s možností účtu](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="c1ec6-161">Použití klíčů rozhraní API</span><span class="sxs-lookup"><span data-stu-id="c1ec6-161">Using API keys</span></span>

<span data-ttu-id="c1ec6-162">Chcete-li protlačit `nuget push` `dotnet nuget push` balíček prostřednictvím příkazů příkazového příkazu nebo příkazového příkazu, musíte získat klíč rozhraní API, který tyto příkazy potřebují.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="c1ec6-163">Podrobnosti naleznete [v tématu Publikování balíčku](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="c1ec6-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="c1ec6-164">Při vytváření nového klíče rozhraní API vyberte příslušnou organizaci v rozevíracím seznamu **Vlastník balíčku.**</span><span class="sxs-lookup"><span data-stu-id="c1ec6-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="c1ec6-165">Jakýkoli klíč rozhraní API, který vytvoříte, se vztahuje pouze na vybranou organizaci:</span><span class="sxs-lookup"><span data-stu-id="c1ec6-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Klíč rozhraní API s možností účtu](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="c1ec6-167">Odebrání organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-167">Removing an organization</span></span>

<span data-ttu-id="c1ec6-168">Jako uživatel můžete odebrat sami sebe z organizace výběrem tlačítka **X** zobrazeného členstvím v organizaci:</span><span class="sxs-lookup"><span data-stu-id="c1ec6-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Odebrání uživatelského účtu z organizace](media/org-remove-self-option.png)

<span data-ttu-id="c1ec6-170">Správci mohou odebrat libovolného člena organizace, včetně jiných správců.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="c1ec6-171">Pokud jste jediným správcem organizace, nemůžete se odebrat sami, pokud jako správce nepřidáte jiného člena.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="c1ec6-172">Odstranění účtu organizace</span><span class="sxs-lookup"><span data-stu-id="c1ec6-172">Deleting an organization account</span></span>

<span data-ttu-id="c1ec6-173">Účet organizace můžete odstranit kliknutím na tlačítko **Odstranit** zobrazené na stránce organizace.</span><span class="sxs-lookup"><span data-stu-id="c1ec6-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Odstranění organizace](media/org-delete-option.png)

<span data-ttu-id="c1ec6-175">Chcete-li organizaci odstranit, musíte ji potvrdit kliknutím na tlačítko Odstranit potvrzení **organizace.**</span><span class="sxs-lookup"><span data-stu-id="c1ec6-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
