---
title: Postup publikování balíčku NuGet
description: Podrobné pokyny pro publikování balíčku NuGet nuget.org nebo privátní informačních kanálů a jak spravovat vlastnictví balíčku na nuget.org.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a47ff9fa3babf830cdd2de25ac0b92af782b5e7e
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="58842-103">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="58842-103">Publishing packages</span></span>

<span data-ttu-id="58842-104">Po vytvoření balíčku a mít vaše `.nupkg` souboru v ručně, je jednoduchý proces, aby byl k dispozici pro ostatní vývojáři veřejných nebo soukromých:</span><span class="sxs-lookup"><span data-stu-id="58842-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="58842-105">Veřejné balíčky jsou k dispozici pro všechny vývojáře globálně přes [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="58842-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="58842-106">Soukromé balíčky jsou k dispozici pouze tým nebo organizace, hostování je buď sdílenou složku, server privátní NuGet [Visual Studio Team Services balíček Management](https://www.visualstudio.com/docs/package/nuget/publish), nebo jako je například myget ProGet, Nexus úložiště jiných výrobců Úložiště a Artifactory.</span><span class="sxs-lookup"><span data-stu-id="58842-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="58842-107">Další podrobnosti najdete v tématu [hostování přehled balíčky](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="58842-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="58842-108">Tento článek se zabývá publikování nuget.org; pro publikování na Visual Studio Team Services, najdete v části [správy balíčků](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="58842-108">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="58842-109">Publikovat do nuget.org</span><span class="sxs-lookup"><span data-stu-id="58842-109">Publish to nuget.org</span></span>

<span data-ttu-id="58842-110">Pro nuget.org musíte se přihlásit s účtem Microsoft, pomocí kterého budete vyzváni k registraci účet s nuget.org. Také se můžete přihlásit pomocí účet nuget.org vytvořené pomocí starší verze portálu.</span><span class="sxs-lookup"><span data-stu-id="58842-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Místo přihlášení NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="58842-112">Dále můžete buď nahrání balíčku přes webový portál nuget.org, nabízená nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0+), nebo publikovat v rámci procesu CI/CD prostřednictvím Visual Studio Team Services, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="58842-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="58842-113">Webový portál: karta odeslat balíček v nuget.org</span><span class="sxs-lookup"><span data-stu-id="58842-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="58842-114">Vyberte **nahrát** v horní nabídce nuget.org a přejděte do umístění balíčku.</span><span class="sxs-lookup"><span data-stu-id="58842-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Nahrání balíčku v nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="58842-116">nuget.org zjistíte, zda je název balíčku k dispozici.</span><span class="sxs-lookup"><span data-stu-id="58842-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="58842-117">Pokud není, změnit identifikátor balíčku v projektu, znovu sestavit a opakujte odeslání.</span><span class="sxs-lookup"><span data-stu-id="58842-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="58842-118">Pokud je dostupný název balíčku, otevře se nuget.org **ověřte** části, ve kterém můžete zkontrolovat metadata z manifestu balíčku.</span><span class="sxs-lookup"><span data-stu-id="58842-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="58842-119">Chcete-li změnit některé z metadat, upravte projektu (soubor projektu nebo `.nuspec` soubor), znovu vytvořit, znovu vytvořte balíček a odešlete znovu.</span><span class="sxs-lookup"><span data-stu-id="58842-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="58842-120">V části **Import dokumentaci** můžete vložit Markdownu, přejděte na svoje dokumenty s adresou URL nebo odeslat soubor dokumentace.</span><span class="sxs-lookup"><span data-stu-id="58842-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="58842-121">Když je připraven všechny informace, vyberte **odeslání** tlačítko</span><span class="sxs-lookup"><span data-stu-id="58842-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="58842-122">Příkazový řádek</span><span class="sxs-lookup"><span data-stu-id="58842-122">Command line</span></span>

<span data-ttu-id="58842-123">K nabízení balíčků nuget.org je nutné použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadovaná [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="58842-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="58842-124">Musíte také klíč rozhraní API, která je vytvořena na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="58842-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="58842-125">Vytvoření klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="58842-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="58842-126">Publikování pomocí nabízených nuget dotnet.</span><span class="sxs-lookup"><span data-stu-id="58842-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="58842-127">Publikování pomocí nabízených nuget</span><span class="sxs-lookup"><span data-stu-id="58842-127">Publish with nuget push</span></span>

1. <span data-ttu-id="58842-128">Na příkazovém řádku spusťte následující příkaz, nahraďte `<your_API_key>` klíčem získané z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="58842-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="58842-129">Tento příkaz uloží klíč rozhraní API v konfiguraci NuGet tak, aby potřebovat opakujte tento krok opakujte na stejném počítači.</span><span class="sxs-lookup"><span data-stu-id="58842-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="58842-130">Nabízená vašeho balíčku Galerie NuGet pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="58842-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a><span data-ttu-id="58842-131">Ověřování balíčku a indexování</span><span class="sxs-lookup"><span data-stu-id="58842-131">Package validation and indexing</span></span>

<span data-ttu-id="58842-132">Balíčky nabídnutých do nuget.org podstoupit několik ověření, jako jsou antivirové kontroly.</span><span class="sxs-lookup"><span data-stu-id="58842-132">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="58842-133">(Všechny balíčky v nuget.org jsou pravidelně kontrolovány.)</span><span class="sxs-lookup"><span data-stu-id="58842-133">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="58842-134">.</span><span class="sxs-lookup"><span data-stu-id="58842-134">.</span></span> <span data-ttu-id="58842-135">Když balíček uplynutí všechny ověřovací kontroly, může trvat nějakou dobu se indexovat a zobrazí ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="58842-135">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="58842-136">Po dokončení indexování obdržíte e-mail s potvrzením, že byl balíček úspěšně publikovala.</span><span class="sxs-lookup"><span data-stu-id="58842-136">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="58842-137">Pokud se balíček nezdaří ověřování pravosti, stránce s podrobnostmi o balíčku se aktualizuje a zobrazí související chybu a taky dostane e-mail s upozorněním o něm.</span><span class="sxs-lookup"><span data-stu-id="58842-137">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="58842-138">Ověřování balíčku a indexování obvykle trvá v části 15 minut.</span><span class="sxs-lookup"><span data-stu-id="58842-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="58842-139">Pokud balíček publikování trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud nuget.org dochází k žádné přerušení.</span><span class="sxs-lookup"><span data-stu-id="58842-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="58842-140">Pokud jsou všechny systémy provozní a balíčku nebyla publikována úspěšně v rámci hodiny, přihlaste se prosím na nuget.org a kontaktujte nás na stránce balíček pomocí odkazu obraťte se na podporu.</span><span class="sxs-lookup"><span data-stu-id="58842-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="58842-141">Chcete-li zobrazit stav balíčku, vyberte **spravovat balíčky** pod názvem vašeho účtu na nuget.org. Po dokončení ověření obdržíte e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="58842-141">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="58842-142">Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazit ve výsledcích hledání, kde je během této doby zobrazí se následující zpráva na stránce balíček můžete najít jiné:</span><span class="sxs-lookup"><span data-stu-id="58842-142">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Zpráva oznamující, že balíček ještě není publikována.](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="58842-144">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="58842-144">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="58842-145">Pokud jste nabízená balíčky nuget.org pomocí Visual Studio Team Services jako součást procesu průběžnou integraci a nasazení, musíte použít `nuget.exe` 4.1 nebo vyšší v úlohách NuGet.</span><span class="sxs-lookup"><span data-stu-id="58842-145">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="58842-146">Podrobnosti najdete na [pomocí nejnovější NuGet v buildu](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="58842-146">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="58842-147">Správa vlastníků balíčku v nuget.org</span><span class="sxs-lookup"><span data-stu-id="58842-147">Managing package owners on nuget.org</span></span>

<span data-ttu-id="58842-148">I když každý balíček NuGet `.nuspec` soubor definuje autoři balíčku, galerie nuget.org nepoužívá aby metadata k definování vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="58842-148">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="58842-149">Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která publikuje balíček.</span><span class="sxs-lookup"><span data-stu-id="58842-149">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="58842-150">Toto je balíček prostřednictvím uživatelského rozhraní nuget.org přihlášeného uživatele nebo uživatele, jehož klíč rozhraní API se použila se `nuget SetApiKey` nebo `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="58842-150">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="58842-151">Všechny vlastníky balíček mít úplná oprávnění pro daný balíček, včetně přidání a odebrání dalších vlastníci a publikování aktualizací.</span><span class="sxs-lookup"><span data-stu-id="58842-151">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="58842-152">Chcete-li změnit vlastnictví balíčku, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="58842-152">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="58842-153">Přihlaste se k nuget.org pomocí účtu, který je vlastníkem aktuální balíčku.</span><span class="sxs-lookup"><span data-stu-id="58842-153">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="58842-154">Vyberte název účtu, vyberte **spravovat balíčky**a rozbalte **publikované balíčky**.</span><span class="sxs-lookup"><span data-stu-id="58842-154">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="58842-155">Vyberte na balíček, který chcete spravovat a pak na pravé straně vyberte **Spravovat vlastníky**.</span><span class="sxs-lookup"><span data-stu-id="58842-155">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="58842-156">Zde máte několik možností:</span><span class="sxs-lookup"><span data-stu-id="58842-156">From here you have several options:</span></span>

1. <span data-ttu-id="58842-157">Odeberte všechny vlastníka uvedený v seznamu **aktuální vlastníky**.</span><span class="sxs-lookup"><span data-stu-id="58842-157">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="58842-158">Přidat vlastníka pod **přidat vlastníka** zadáním uživatelského jména, zprávu, a výběrem **přidat**.</span><span class="sxs-lookup"><span data-stu-id="58842-158">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="58842-159">Tato akce odešle e-mail na tuto novou spoluvlastník s odkazem potvrzení.</span><span class="sxs-lookup"><span data-stu-id="58842-159">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="58842-160">Po potvrzení, tento uživatel má úplná oprávnění k přidání a odebrání vlastníky.</span><span class="sxs-lookup"><span data-stu-id="58842-160">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="58842-161">(Dokud potvrzen, **aktuální vlastníky** části označuje čekající na schválení pro tuto osobu.)</span><span class="sxs-lookup"><span data-stu-id="58842-161">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="58842-162">Převést vlastnictví (jako když změny vlastnictví nebo balíčku byla publikována v části nesprávný účet), přidejte nový vlastník a po jejich jste potvrzen vlastnictví jejich můžete odebrat ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="58842-162">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="58842-163">K přiřazení vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí alias e-mailu, který se předají odpovídající jednotlivým členům.</span><span class="sxs-lookup"><span data-stu-id="58842-163">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="58842-164">Například různé Microsoft ASP.NET balíčky jsou společně vlastněny [microsoft](http://nuget.org/profiles/microsoft) a [aspnet](http://nuget.org/profiles/aspnet) účty, které jednoduše takové aliasy.</span><span class="sxs-lookup"><span data-stu-id="58842-164">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="58842-165">Obnovení balíčku vlastnictví</span><span class="sxs-lookup"><span data-stu-id="58842-165">Recovering package ownership</span></span>

<span data-ttu-id="58842-166">Balíček v některých případech nemusí mít aktivní vlastníka.</span><span class="sxs-lookup"><span data-stu-id="58842-166">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="58842-167">Například si původního vlastníka opustili společnost, která vytvoří balíček, nuget.org přihlašovací údaje budou ztraceny nebo dřívější chyby v galerii zbývajících balíček ownerless.</span><span class="sxs-lookup"><span data-stu-id="58842-167">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="58842-168">Pokud jste jeho oprávněný vlastník balíčku a muset znovu získat vlastnictví, použijte [obraťte se na formuláři](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit, vaší konkrétní situace týmu NuGet.</span><span class="sxs-lookup"><span data-stu-id="58842-168">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="58842-169">Jsme potom postupujte podle procesu ověřit vlastnictví balíčku, včetně pokusu o nalezení vlastník existující prostřednictvím adresy URL projektu balíčku, Twitter, e-mailu nebo jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="58842-169">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="58842-170">Ale pokud všechno ostatní selže, může vám můžeme poslat nové pozvání k vlastníka.</span><span class="sxs-lookup"><span data-stu-id="58842-170">But if all else fails, we can send you a new invite to become an owner.</span></span>
