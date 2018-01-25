---
title: "Postup publikování balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Podrobné pokyny pro publikování balíčku NuGet nuget.org nebo privátní informačních kanálů a jak spravovat vlastnictví balíčku na nuget.org."
keywords: "Publikování balíčku NuGet, publikování balíčku NuGet, vlastnictví balíčku NuGet, publikovat do nuget.org, privátní kanály NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b57845d79c3ba45aa06a934a30d41e6f4d3057e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="06903-104">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="06903-104">Publishing packages</span></span>

<span data-ttu-id="06903-105">Jakmile máte [vytvořil balíček](../create-packages/creating-a-package.md) s `nuget pack`, je jednoduchý proces, aby byl k dispozici pro ostatní vývojáři veřejných nebo soukromých:</span><span class="sxs-lookup"><span data-stu-id="06903-105">Once you have [created a package](../create-packages/creating-a-package.md) with `nuget pack`, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="06903-106">Veřejné balíčky jsou k dispozici pro všechny vývojáře globálně přes [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="06903-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="06903-107">Soukromé balíčky jsou k dispozici pouze tým nebo organizace, hostování je buď sdílenou složku, server privátní NuGet [Visual Studio Team Services balíček Management](https://www.visualstudio.com/docs/package/nuget/publish), nebo jako je například myget ProGet, Nexus úložiště jiných výrobců Úložiště a Artifactory.</span><span class="sxs-lookup"><span data-stu-id="06903-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="06903-108">Další podrobnosti najdete v tématu [hostování přehled balíčky](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="06903-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="06903-109">Toto téma popisuje publikování nuget.org; pro publikování na Visual Studio Team Services, najdete v části [správy balíčků](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="06903-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="06903-110">Publikovat do nuget.org</span><span class="sxs-lookup"><span data-stu-id="06903-110">Publish to nuget.org</span></span>

<span data-ttu-id="06903-111">Pro nuget.org, musíte nejdřív [zaregistrovat bezplatný účet](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) nebo přihlásit, pokud již zaregistrován:</span><span class="sxs-lookup"><span data-stu-id="06903-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![NuGet registrace a přihlášení umístění](media/publish_NuGetSignIn.png)

<span data-ttu-id="06903-113">Dále můžete buď nahrání balíčku přes webový portál nuget.org, nabízená nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0+), nebo publikovat v rámci procesu CI/CD prostřednictvím Visual Studio Team Services, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="06903-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="06903-114">Webový portál: karta odeslat balíček v nuget.org</span><span class="sxs-lookup"><span data-stu-id="06903-114">Web portal: use the Upload Package tab on nuget.org</span></span>

![Nahrání balíčku s Správce balíčků NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="06903-116">Příkazový řádek</span><span class="sxs-lookup"><span data-stu-id="06903-116">Command line</span></span>

> [!Important]
> <span data-ttu-id="06903-117">K nabízení balíčků nuget.org je nutné použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="06903-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="06903-118">Klikněte na jméno uživatele, přejděte na nastavení svého účtu.</span><span class="sxs-lookup"><span data-stu-id="06903-118">Click on your user name to navigate to your account settings.</span></span>
1. <span data-ttu-id="06903-119">V části **klíč rozhraní API**, klikněte na tlačítko **kopírovat do schránky** načíst přístup klíčů budete potřebovat v rozhraní příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="06903-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you'll need in the CLI:</span></span>

    ![Kopírování klíč rozhraní API z nastavení účtu](media/publish_APIKey.png)

1. <span data-ttu-id="06903-121">Na příkazovém řádku spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="06903-121">At a command prompt, run the following command:</span></span>

    ```cli
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="06903-122">To ukládá klíč rozhraní API na počítači, aby nemusí proveďte tento krok opakujte na stejném počítači.</span><span class="sxs-lookup"><span data-stu-id="06903-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

1. <span data-ttu-id="06903-123">Nabízená vašeho balíčku Galerie NuGet pomocí příkazu:</span><span class="sxs-lookup"><span data-stu-id="06903-123">Push your package to NuGet Gallery using the command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="06903-124">Před prováděné veřejný, jsou všechny balíčky nahrán do nuget.org zkontrolovat viry a odmítnuta, pokud nejsou nalezeny žádné viry.</span><span class="sxs-lookup"><span data-stu-id="06903-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="06903-125">Všechny balíčky uvedené v nuget.org také jsou pravidelně kontrolovány.</span><span class="sxs-lookup"><span data-stu-id="06903-125">All packages listed on nuget.org are also scanned periodically.</span></span>

1. <span data-ttu-id="06903-126">Ve vašem účtu na nuget.org, klikněte na tlačítko **spravovat vlastní balíčky** zobrazíte ten, který jste právě publikovaná; také obdržíte e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="06903-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you'll also receive a confirmation email.</span></span> <span data-ttu-id="06903-127">Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazit ve výsledcích hledání, kde je během této doby se zobrazí tato zpráva na stránce balíček můžete najít jiné:</span><span class="sxs-lookup"><span data-stu-id="06903-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you'll see the following message on your package page:</span></span>

    ![Zpráva oznamující, že balíček není ještě indexované](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="06903-129">Ověřování balíčku a indexování</span><span class="sxs-lookup"><span data-stu-id="06903-129">Package validation and indexing</span></span>

<span data-ttu-id="06903-130">Balíčky nabídnutých do NuGet.org podstoupit několik ověření.</span><span class="sxs-lookup"><span data-stu-id="06903-130">Packages pushed to NuGet.org undergo several validations.</span></span> <span data-ttu-id="06903-131">Když balíček uplynutí všechny ověřovací kontroly, může trvat nějakou dobu se indexovat a zobrazí ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="06903-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="06903-132">Po dokončení indexování obdržíte e-mail s potvrzením, že byl balíček úspěšně publikovala.</span><span class="sxs-lookup"><span data-stu-id="06903-132">Once indexing is complete, you'll receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="06903-133">Pokud se balíček nezdaří ověřování pravosti, stránce s podrobnostmi o balíčku se aktualizuje a zobrazí související chybu a také obdržíte e-mail s upozorněním o něm.</span><span class="sxs-lookup"><span data-stu-id="06903-133">If the package fails a validation check, the package details page will update to display the associated error and you'll also receive an email notifying you about it.</span></span>

<span data-ttu-id="06903-134">Ověřování balíčku a indexování obvykle trvá v části 15 minut.</span><span class="sxs-lookup"><span data-stu-id="06903-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="06903-135">Pokud balíček publikování trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud NuGet.org dochází k žádné přerušení.</span><span class="sxs-lookup"><span data-stu-id="06903-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="06903-136">Pokud jsou všechny systémy provozní a balíčku nebyla publikována úspěšně v rámci hodiny, přihlaste se prosím na NuGet.org a kontaktujte nás na stránce balíček pomocí odkazu obraťte se na podporu.</span><span class="sxs-lookup"><span data-stu-id="06903-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to NuGet.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="06903-137">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="06903-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="06903-138">Pokud jste nabízená balíčky nuget.org pomocí Visual Studio Team Services jako součást procesu průběžnou integraci a nasazení, musíte použít `nuget.exe` 4.1 nebo vyšší v úlohách NuGet.</span><span class="sxs-lookup"><span data-stu-id="06903-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="06903-139">Podrobnosti najdete na [pomocí nejnovější NuGet v buildu](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="06903-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="06903-140">Správa vlastníků balíčku v nuget.org</span><span class="sxs-lookup"><span data-stu-id="06903-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="06903-141">I když každý balíček NuGet `.nuspec` soubor definuje autoři balíčku, galerie nuget.org nepoužívá aby metadata k definování vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="06903-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="06903-142">Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která publikuje balíček.</span><span class="sxs-lookup"><span data-stu-id="06903-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="06903-143">Toto je balíček prostřednictvím uživatelského rozhraní nuget.org přihlášeného uživatele nebo uživatele, jehož klíč rozhraní API se použila se `nuget SetApiKey` nebo `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="06903-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="06903-144">Všechny vlastníky balíček mít úplná oprávnění pro daný balíček, včetně přidání a odebrání dalších vlastníci a publikování aktualizací.</span><span class="sxs-lookup"><span data-stu-id="06903-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="06903-145">Chcete-li změnit vlastnictví balíčku, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="06903-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="06903-146">Přihlaste se k nuget.org pomocí účtu, který je vlastníkem aktuální balíčku.</span><span class="sxs-lookup"><span data-stu-id="06903-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="06903-147">Klikněte na své uživatelské jméno, pak na **spravovat vlastní balíčky**, pak na balíčku, kterou chcete spravovat.</span><span class="sxs-lookup"><span data-stu-id="06903-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="06903-148">Klikněte **Spravovat vlastníky** odkaz na levé straně.</span><span class="sxs-lookup"><span data-stu-id="06903-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="06903-149">Zde máte několik možností:</span><span class="sxs-lookup"><span data-stu-id="06903-149">From here you have several options:</span></span>

1. <span data-ttu-id="06903-150">Chcete-li přidat vlastníka, zadejte název účtu jejich NuGet a klikněte na **přidat**.</span><span class="sxs-lookup"><span data-stu-id="06903-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="06903-151">Tím se odešle e-mail do této nové spoluvlastník s odkazem potvrzení.</span><span class="sxs-lookup"><span data-stu-id="06903-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="06903-152">Po potvrzení, tento uživatel má úplná oprávnění k přidání a odebrání vlastníky.</span><span class="sxs-lookup"><span data-stu-id="06903-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="06903-153">(Dokud potvrzen, **Spravovat vlastníky** stránky označuje "čekající na schválení" pro tuto osobu).</span><span class="sxs-lookup"><span data-stu-id="06903-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="06903-154">Odebrat vlastníka, vyberte své jméno na **Spravovat vlastníky** a klikněte na tlačítko **odebrat**.</span><span class="sxs-lookup"><span data-stu-id="06903-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="06903-155">Jednoduše převést vlastnictví (jako když změny vlastnictví nebo balíčku byla publikována v části nesprávný účet), přidejte nový vlastník a po jejich jste potvrzen vlastnictví jejich můžete odebrat ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="06903-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="06903-156">K přiřazení vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí alias e-mailu, který se předají odpovídající jednotlivým členům.</span><span class="sxs-lookup"><span data-stu-id="06903-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="06903-157">Například různé Microsoft ASP.NET balíčky jsou společně vlastněny [microsoft](http://nuget.org/profiles/microsoft) a [aspnet](http://nuget.org/profiles/aspnet) účty, které jednoduše takové aliasy.</span><span class="sxs-lookup"><span data-stu-id="06903-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="06903-158">Obnovení balíčku vlastnictví</span><span class="sxs-lookup"><span data-stu-id="06903-158">Recovering package ownership</span></span>

<span data-ttu-id="06903-159">Balíček v některých případech nemusí mít aktivní vlastníka.</span><span class="sxs-lookup"><span data-stu-id="06903-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="06903-160">Například si původního vlastníka opustili společnost, která vytvoří balíček, nuget.org přihlašovací údaje budou ztraceny nebo dřívější chyby v galerii zbývajících balíček ownerless.</span><span class="sxs-lookup"><span data-stu-id="06903-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="06903-161">Pokud jste jeho oprávněný vlastník balíčku a muset znovu získat vlastnictví, použijte [obraťte se na formuláři](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit, vaší konkrétní situace týmu NuGet.</span><span class="sxs-lookup"><span data-stu-id="06903-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="06903-162">Jsme potom postupujte podle procesu ověřit vlastnictví balíčku, včetně pokusu o nalezení vlastník existující prostřednictvím adresy URL projektu balíčku, Twitter, e-mailu nebo jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="06903-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="06903-163">Ale pokud všechno ostatní selže, může vám můžeme poslat nové pozvání k vlastníka.</span><span class="sxs-lookup"><span data-stu-id="06903-163">But if all else fails, we can send you a new invite to become an owner.</span></span>
