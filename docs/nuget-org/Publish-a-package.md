---
title: Jak publikovat balíček NuGet
description: Podrobné pokyny pro publikování balíčku NuGet na nuget.org nebo privátní kanály a jak spravovat vlastnictví balíčků na nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 6d183100a8319b517347567f34d276e94eb4e15d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427572"
---
# <a name="publishing-packages"></a><span data-ttu-id="90a9e-103">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="90a9e-103">Publishing packages</span></span>

<span data-ttu-id="90a9e-104">Po vytvoření balíčku a mít vaše `.nupkg` soubor spolupráce, je jednoduchý proces, aby byla k dispozici pro jiné vývojáře veřejně nebo soukromě:</span><span class="sxs-lookup"><span data-stu-id="90a9e-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="90a9e-105">Veřejné balíčky jsou k dispozici pro všechny vývojáře globálně až [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="90a9e-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="90a9e-106">Privátní balíčky jsou k dispozici pouze tým nebo organizace, hostováním buď sdílené, privátní server NuGet [Azure artefakty](https://www.visualstudio.com/docs/package/nuget/publish), nebo jiného úložiště, jako je například myget, ProGet, Nexus úložiště a Artifactory.</span><span class="sxs-lookup"><span data-stu-id="90a9e-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="90a9e-107">Další podrobnosti najdete v tématu [hostování balíčků přehled](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="90a9e-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="90a9e-108">Tento článek se týká publikování do nuget.org; publikování artefaktů Azure, najdete v části [správy balíčků](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="90a9e-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="90a9e-109">Publikování na nuget.org</span><span class="sxs-lookup"><span data-stu-id="90a9e-109">Publish to nuget.org</span></span>

<span data-ttu-id="90a9e-110">Pro nuget.org musíte se přihlásit pomocí účtu Microsoft, pomocí kterého budete požádáni o registraci účtu s nuget.org. Také se můžete přihlásit pomocí účtu nuget.org, vytvořena pomocí starší verze portálu.</span><span class="sxs-lookup"><span data-stu-id="90a9e-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet přihlášení umístění](media/publish_NuGetSignIn.png)

<span data-ttu-id="90a9e-112">V dalším kroku můžete buď nahrání balíčku prostřednictvím webového portálu nuget.org, push na nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0+), nebo publikovat jako součást procesu CI/CD DevOps službami Azure, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="90a9e-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="90a9e-113">Webový portál: na kartě nahrání balíčků na nuget.org</span><span class="sxs-lookup"><span data-stu-id="90a9e-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="90a9e-114">Vyberte **nahrát** v horní nabídce nuget.org a přejděte do umístění balíčku.</span><span class="sxs-lookup"><span data-stu-id="90a9e-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Nahrání balíčků na nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="90a9e-116">nuget.org informuje, pokud název balíčku je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="90a9e-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="90a9e-117">Pokud není, změňte identifikátor balíčku v projektu, sestavte znovu a zkuste nahrát znovu.</span><span class="sxs-lookup"><span data-stu-id="90a9e-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="90a9e-118">Pokud název balíčku je k dispozici, se otevře nuget.org **ověřte** oddílu, ve kterém můžete zkontrolovat metadat z manifestu balíčku.</span><span class="sxs-lookup"><span data-stu-id="90a9e-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="90a9e-119">Chcete-li změnit některý z metadat, upravte svůj projekt (soubor projektu nebo `.nuspec` souboru), znovu sestavit, znovu vytvořte balíček a odešlete znovu.</span><span class="sxs-lookup"><span data-stu-id="90a9e-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="90a9e-120">V části **Import dokumentaci** můžete vložit Markdownu, přejděte na svoje dokumenty pomocí adresy URL nebo nahrát soubor dokumentace.</span><span class="sxs-lookup"><span data-stu-id="90a9e-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="90a9e-121">Když je připraven všechny informace, vyberte **odeslat** tlačítko</span><span class="sxs-lookup"><span data-stu-id="90a9e-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="90a9e-122">Příkazový řádek</span><span class="sxs-lookup"><span data-stu-id="90a9e-122">Command line</span></span>

<span data-ttu-id="90a9e-123">Push balíčků na nuget.org je nutné použít [nuget.exe verze 4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [NuGet protokoly](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="90a9e-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="90a9e-124">Budete také potřebovat klíče rozhraní API, která je vytvořena na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="90a9e-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="90a9e-125">Vytvoření klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="90a9e-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="90a9e-126">Publikování pomocí nuget dotnet nasdílení změn</span><span class="sxs-lookup"><span data-stu-id="90a9e-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="90a9e-127">Publikování pomocí nuget nasdílení změn</span><span class="sxs-lookup"><span data-stu-id="90a9e-127">Publish with nuget push</span></span>

1. <span data-ttu-id="90a9e-128">Na příkazovém řádku spusťte následující příkaz a nahraďte `<your_API_key>` pomocí klíče získané z webu nuget.org:</span><span class="sxs-lookup"><span data-stu-id="90a9e-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="90a9e-129">Tento příkaz uloží klíč rozhraní API v konfiguraci Nugetu tak, že potřebujete opakujte tento krok znovu ve stejném počítači.</span><span class="sxs-lookup"><span data-stu-id="90a9e-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="90a9e-130">Nahrání balíčku do Galerie NuGet pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="90a9e-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="90a9e-131">Publikovat podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="90a9e-131">Publish signed packages</span></span>

<span data-ttu-id="90a9e-132">Odeslat podepsaný balíčků, je nutné nejprve [zaregistrovat certifikát](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) používá k podepisování balíčků.</span><span class="sxs-lookup"><span data-stu-id="90a9e-132">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="90a9e-133">nuget.org odmítne balíčky, které splňují není [podepsaný balíček požadavky](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="90a9e-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="90a9e-134">Ověření balíčku a indexování</span><span class="sxs-lookup"><span data-stu-id="90a9e-134">Package validation and indexing</span></span>

<span data-ttu-id="90a9e-135">Balíčky nuget.org do této oblasti podstupovali několik ověření, jako jsou antivirové kontroly.</span><span class="sxs-lookup"><span data-stu-id="90a9e-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="90a9e-136">(Všech balíčků na nuget.org jsou pravidelně kontrolovány.)</span><span class="sxs-lookup"><span data-stu-id="90a9e-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="90a9e-137">Když tento balíček prošel všechny ověřovací kontroly, může trvat nějakou dobu se indexovat a zobrazí ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="90a9e-137">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="90a9e-138">Po dokončení indexování obdržíte e-mail s potvrzením, že byl balíček úspěšně publikovala.</span><span class="sxs-lookup"><span data-stu-id="90a9e-138">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="90a9e-139">Pokud balíček selhání kontroly ověřování, na stránce podrobností balíčku se aktualizuje a zobrazí související chyby a také obdržíte e-mail s upozorněním můžete o něm.</span><span class="sxs-lookup"><span data-stu-id="90a9e-139">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="90a9e-140">Ověření balíčku a indexování obvykle trvá méně než 15 minut.</span><span class="sxs-lookup"><span data-stu-id="90a9e-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="90a9e-141">Pokud o publikování balíčku trvá déle, než se očekávalo, navštivte [status.nuget.org](https://status.nuget.org/) ke kontrole, pokud nuget.org dochází k žádné přerušení.</span><span class="sxs-lookup"><span data-stu-id="90a9e-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="90a9e-142">Pokud jsou všechny systémy provozní a balíčku nebyla úspěšně publikována do jedné hodiny, přihlaste se prosím na nuget.org a kontaktujte nás přes odkaz na podporu se obraťte se na stránce balíček pro.</span><span class="sxs-lookup"><span data-stu-id="90a9e-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="90a9e-143">Pokud chcete zobrazit stav balíčku, vyberte **spravovat balíčky** pod názvem vašeho účtu na nuget.org. Po dokončení ověření obdržíte e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="90a9e-143">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="90a9e-144">Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazí ve výsledcích hledání tam, kde ostatní můžete najít, během této doby se zobrazí následující zpráva na stránce balíček:</span><span class="sxs-lookup"><span data-stu-id="90a9e-144">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Zpráva oznamující, že balíček ještě nebyla publikována.](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="90a9e-146">Služby Azure DevOps (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="90a9e-146">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="90a9e-147">Pokud vložíte balíčků na nuget.org jako součást procesu průběžnou integraci a nasazování pomocí služby Azure DevOps, je nutné použít `nuget.exe` 4.1 nebo vyšší v úlohách NuGet.</span><span class="sxs-lookup"><span data-stu-id="90a9e-147">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="90a9e-148">Podrobnosti najdete na [pomocí nejnovějšího balíčku NuGet ve vašem buildu](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blogu Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="90a9e-148">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="90a9e-149">Správa vlastníků balíčků na nuget.org</span><span class="sxs-lookup"><span data-stu-id="90a9e-149">Managing package owners on nuget.org</span></span>

<span data-ttu-id="90a9e-150">I když každý balíček NuGet `.nuspec` soubor definuje autory balíčku, galerie nuget.org nepoužívá tato metadata k definování vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="90a9e-150">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="90a9e-151">Místo toho nuget.org přiřadí osobě, která publikuje balíček počáteční vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="90a9e-151">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="90a9e-152">Toto je balíček prostřednictvím uživatelského rozhraní nuget.org přihlášeného uživatele nebo uživatele, jehož klíč rozhraní API byla použita s `nuget SetApiKey` nebo `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="90a9e-152">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="90a9e-153">Všechny vlastníky balíčku máte úplná oprávnění pro balíček, včetně přidání a odebrání dalších vlastníků a publikování aktualizací.</span><span class="sxs-lookup"><span data-stu-id="90a9e-153">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="90a9e-154">Chcete-li změnit vlastnictví balíčku, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="90a9e-154">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="90a9e-155">Přihlaste se k nuget.org pomocí účtu, který je aktuálním vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="90a9e-155">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="90a9e-156">Vyberte název svého účtu, vyberte **spravovat balíčky**a rozbalte **publikovat balíčky**.</span><span class="sxs-lookup"><span data-stu-id="90a9e-156">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="90a9e-157">Vyberte balíček, který chcete spravovat a potom na pravé straně vyberte **Spravovat vlastníky**.</span><span class="sxs-lookup"><span data-stu-id="90a9e-157">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="90a9e-158">Zde máte několik možností:</span><span class="sxs-lookup"><span data-stu-id="90a9e-158">From here you have several options:</span></span>

1. <span data-ttu-id="90a9e-159">Odebrat všechny vlastníka uvedený v části **aktuální vlastníky**.</span><span class="sxs-lookup"><span data-stu-id="90a9e-159">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="90a9e-160">Přidat vlastníka pod **přidat vlastníka** zadáním jejich uživatelskému jménu, zprávu, a výběrem **přidat**.</span><span class="sxs-lookup"><span data-stu-id="90a9e-160">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="90a9e-161">Tato akce odešle e-mailu na tuto novou spoluvlastník s odkazem na potvrzení.</span><span class="sxs-lookup"><span data-stu-id="90a9e-161">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="90a9e-162">Po potvrzení, tato osoba má úplná oprávnění k přidání a odebrání vlastníků.</span><span class="sxs-lookup"><span data-stu-id="90a9e-162">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="90a9e-163">(Dokud není potvrzené, **aktuální vlastníky** čekající na schválení pro tuto osobu, která určuje části.)</span><span class="sxs-lookup"><span data-stu-id="90a9e-163">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="90a9e-164">Převést vlastnictví (jako v části k nesprávnému účtu byl při publikování změny vlastnictví nebo balíčku), přidejte nového vlastníka a po jejich ověření, že vlastnictví, můžete odebrat ze seznamu.</span><span class="sxs-lookup"><span data-stu-id="90a9e-164">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="90a9e-165">Přiřazení vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí e-mailový alias, který je předán členům týmu odpovídající.</span><span class="sxs-lookup"><span data-stu-id="90a9e-165">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="90a9e-166">Například různé balíčky Microsoft ASP.NET jsou společné vlastnictví [microsoft](http://nuget.org/profiles/microsoft) a [aspnet](http://nuget.org/profiles/aspnet) účty, které jednoduše tyto aliasy.</span><span class="sxs-lookup"><span data-stu-id="90a9e-166">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="90a9e-167">Obnovení balíčku vlastnictví</span><span class="sxs-lookup"><span data-stu-id="90a9e-167">Recovering package ownership</span></span>

<span data-ttu-id="90a9e-168">Balíček v některých případech nemusí mít aktivní vlastníka.</span><span class="sxs-lookup"><span data-stu-id="90a9e-168">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="90a9e-169">Například původního vlastníka ještě zbývá společnosti, která vytvoří balíček, nuget.org přihlašovací údaje budou ztraceny, nebo předchozí chyby v galerii ponechat ownerless balíček.</span><span class="sxs-lookup"><span data-stu-id="90a9e-169">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="90a9e-170">Pokud jsou právoplatného vlastníka balíčku a potřebujete znovu získat vlastnictví, použijte [kontaktní formulář](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit vaší situaci týmu NuGet.</span><span class="sxs-lookup"><span data-stu-id="90a9e-170">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="90a9e-171">My potom postupujte podle procesu ověřit vlastnictví balíček, včetně pokusu o nalezení stávající vlastník prostřednictvím adresy URL projektu daného balíčku, Twitter, e-mailu nebo jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="90a9e-171">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="90a9e-172">Ale když nic jiného nepomůže, vám můžeme poslat nové pozvánky stát vlastníkem.</span><span class="sxs-lookup"><span data-stu-id="90a9e-172">But if all else fails, we can send you a new invite to become an owner.</span></span>
