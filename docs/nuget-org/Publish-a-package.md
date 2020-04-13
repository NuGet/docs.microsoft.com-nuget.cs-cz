---
title: Jak publikovat balíček NuGet
description: Podrobné pokyny pro publikování balíčku NuGet pro nuget.org nebo soukromé informační kanály a jak spravovat vlastnictví balíčku na nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429022"
---
# <a name="publishing-packages"></a><span data-ttu-id="df5e8-103">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="df5e8-103">Publishing packages</span></span>

<span data-ttu-id="df5e8-104">Jakmile vytvoříte balíček a `.nupkg` máte soubor v ruce, je to jednoduchý proces, aby byl k dispozici ostatním vývojářům, a to buď veřejně nebo soukromě:</span><span class="sxs-lookup"><span data-stu-id="df5e8-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="df5e8-105">Veřejné balíčky jsou k dispozici všem vývojářům globálně prostřednictvím [nuget.org](https://www.nuget.org/packages/manage/upload) jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="df5e8-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="df5e8-106">Soukromé balíčky jsou k dispozici pouze pro tým nebo organizaci tím, že je hostuje buď sdílená složka, soukromý nugetový server, [artefakty Azure](https://www.visualstudio.com/docs/package/nuget/publish)nebo úložiště třetích stran, jako je myget, ProGet, Nexus Repository a Artifactory.</span><span class="sxs-lookup"><span data-stu-id="df5e8-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="df5e8-107">Další podrobnosti naleznete v [tématu Přehled hostování balíčků](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="df5e8-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="df5e8-108">Tento článek popisuje publikování na nuget.org; pro publikování na Artefakty Azure, najdete v [tématu Správa balíčků](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="df5e8-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="df5e8-109">Publikovat do nuget.org</span><span class="sxs-lookup"><span data-stu-id="df5e8-109">Publish to nuget.org</span></span>

<span data-ttu-id="df5e8-110">V nuget.org se musíte přihlásit pomocí účtu Microsoft, pomocí kterého budete požádáni o registraci účtu u nuget.org. Můžete se také přihlásit pomocí účtu nuget.org vytvořeného pomocí starších verzí portálu.</span><span class="sxs-lookup"><span data-stu-id="df5e8-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Umístění přihlášení NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="df5e8-112">Dále můžete buď nahrát balíček prostřednictvím webového portálu nuget.org, `nuget.exe` nabízený nuget.org z příkazového řádku (vyžaduje 4.1.0+) nebo publikovat jako součást procesu CI/CD prostřednictvím služby Azure DevOps Services, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="df5e8-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="df5e8-113">Webový portál: Použijte kartu Nahrát balíček na nuget.org</span><span class="sxs-lookup"><span data-stu-id="df5e8-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="df5e8-114">V horní nabídce nuget.org vyberte **Nahrát** a vyhledejte umístění balíčku.</span><span class="sxs-lookup"><span data-stu-id="df5e8-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Nahrání balíčku na nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="df5e8-116">nuget.org vám řekne, zda je k dispozici název balíčku.</span><span class="sxs-lookup"><span data-stu-id="df5e8-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="df5e8-117">Pokud tomu tak není, změňte identifikátor balíčku v projektu, znovu se stavněte a zkuste nahrát znovu.</span><span class="sxs-lookup"><span data-stu-id="df5e8-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="df5e8-118">Pokud je k dispozici název balíčku, otevře nuget.org oddíl **Ověření,** ve kterém můžete zkontrolovat metadata z manifestu balíčku.</span><span class="sxs-lookup"><span data-stu-id="df5e8-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="df5e8-119">Chcete-li změnit libovolné z metadat, upravte `.nuspec` projekt (soubor projektu nebo soubor), znovu vytvořit balíček a znovu nahrát.</span><span class="sxs-lookup"><span data-stu-id="df5e8-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="df5e8-120">V části **Import dokumentace** můžete vložit Markdown, přejděte na dokumenty s adresou URL nebo nahrajte soubor dokumentace.</span><span class="sxs-lookup"><span data-stu-id="df5e8-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="df5e8-121">Až budou všechny informace připravené, vyberte tlačítko **Odeslat.**</span><span class="sxs-lookup"><span data-stu-id="df5e8-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="df5e8-122">Příkazový řádek</span><span class="sxs-lookup"><span data-stu-id="df5e8-122">Command line</span></span>

<span data-ttu-id="df5e8-123">Chcete-li vysunout balíčky nuget.org musíte použít [nuget.exe v4.1.0 nebo vyšší](https://www.nuget.org/downloads), který implementuje požadované [protokoly NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="df5e8-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="df5e8-124">Potřebujete také klíč rozhraní API, který je vytvořen na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="df5e8-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="df5e8-125">Vytvořit klíče rozhraní API</span><span class="sxs-lookup"><span data-stu-id="df5e8-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="df5e8-126">Publikovat pomocí dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="df5e8-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="df5e8-127">Publikovat pomocí nuget push</span><span class="sxs-lookup"><span data-stu-id="df5e8-127">Publish with nuget push</span></span>

1. <span data-ttu-id="df5e8-128">Na příkazovém řádku spusťte `<your_API_key>` následující příkaz, který nahradí klíč získaný z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="df5e8-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="df5e8-129">Tento příkaz ukládá klíč rozhraní API v konfiguraci NuGet, takže není nutné opakovat tento krok znovu ve stejném počítači.</span><span class="sxs-lookup"><span data-stu-id="df5e8-129">This command stores your API key in your NuGet configuration so that you don't need to repeat this step again on the same computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="df5e8-130">Klíč rozhraní API se nepoužívá pro ověřování s privátním zdrojem.</span><span class="sxs-lookup"><span data-stu-id="df5e8-130">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="df5e8-131">Odkazovat [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md) na příkaz pro správu pověření pro ověřování se zdrojem.</span><span class="sxs-lookup"><span data-stu-id="df5e8-131">Refer to [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
    > <span data-ttu-id="df5e8-132">Klíče rozhraní API lze získat z jednotlivých serverů NuGet.</span><span class="sxs-lookup"><span data-stu-id="df5e8-132">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="df5e8-133">Chcete-li vytvořit a manange APIKeys pro nuget.org naleznete [na publish-api-key](../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="df5e8-133">To create and manange APIKeys for nuget.org refer to [publish-api-key](../quickstart/includes/publish-api-key.md)</span></span>

1. <span data-ttu-id="df5e8-134">Převelitím balíčku do Galerie NuGet pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="df5e8-134">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="df5e8-135">Publikování podepsaných balíčků</span><span class="sxs-lookup"><span data-stu-id="df5e8-135">Publish signed packages</span></span>

<span data-ttu-id="df5e8-136">Chcete-li odeslat podepsané balíčky, musíte [nejprve zaregistrovat certifikát](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) použitý k podpisu balíčků.</span><span class="sxs-lookup"><span data-stu-id="df5e8-136">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="df5e8-137">nuget.org odmítne balíčky, které nesplňují [požadavky podepsaného balíčku](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="df5e8-137">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="df5e8-138">Ověření a indexování balíčků</span><span class="sxs-lookup"><span data-stu-id="df5e8-138">Package validation and indexing</span></span>

<span data-ttu-id="df5e8-139">Balíčky, které byly posunuty nuget.org, procházejí několika ověřeními, například kontrolami virů.</span><span class="sxs-lookup"><span data-stu-id="df5e8-139">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="df5e8-140">(Všechny balíčky na nuget.org jsou pravidelně kontrolovány.)</span><span class="sxs-lookup"><span data-stu-id="df5e8-140">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="df5e8-141">Pokud balíček prošel všechny kontroly ověření, může chvíli trvat, než se indexuje a zobrazí se ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="df5e8-141">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="df5e8-142">Po dokončení indexování obdržíte e-mail s potvrzením, že balíček byl úspěšně publikován.</span><span class="sxs-lookup"><span data-stu-id="df5e8-142">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="df5e8-143">Pokud balíček neprojde kontrolou ověření, stránka podrobností balíčku se aktualizuje, aby se zobrazila přidružená chyba, a obdržíte také e-mail s upozorněním na něj.</span><span class="sxs-lookup"><span data-stu-id="df5e8-143">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="df5e8-144">Ověření a indexování balíčku obvykle trvá méně než 15 minut.</span><span class="sxs-lookup"><span data-stu-id="df5e8-144">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="df5e8-145">Pokud publikování balíčku trvá déle, než bylo očekáváno, navštivte [status.nuget.org](https://status.nuget.org/) a zkontrolujte, zda nuget.org dochází k přerušení.</span><span class="sxs-lookup"><span data-stu-id="df5e8-145">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="df5e8-146">Pokud jsou všechny systémy funkční a balíček nebyl úspěšně publikován do hodiny, přihlaste se k nuget.org a kontaktujte nás pomocí odkazu Kontaktujte podporu na stránce balíčku.</span><span class="sxs-lookup"><span data-stu-id="df5e8-146">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="df5e8-147">Pokud chcete zobrazit stav balíčku, vyberte **spravovat balíčky** pod názvem účtu na nuget.org. Po dokončení ověření obdržíte potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="df5e8-147">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="df5e8-148">Všimněte si, že může chvíli trvat, než se váš balíček indexuje a zobrazí se ve výsledcích vyhledávání tam, kde ho mohou najít ostatní, během které se na stránce balíčku zobrazí následující zpráva:</span><span class="sxs-lookup"><span data-stu-id="df5e8-148">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Zpráva označující balíček ještě není publikována](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="df5e8-150">Služby Azure DevOps (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="df5e8-150">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="df5e8-151">Pokud vysáváte balíčky nuget.org pomocí služby Azure DevOps `nuget.exe` Services jako součást procesu průběžné integrace/nasazení, musíte použít 4.1 nebo vyšší v nugetových úlohách.</span><span class="sxs-lookup"><span data-stu-id="df5e8-151">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="df5e8-152">Podrobnosti najdete na [použití nejnovější NuGet ve vašem sestavení](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span><span class="sxs-lookup"><span data-stu-id="df5e8-152">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="df5e8-153">Správa vlastníků balíčků na nuget.org</span><span class="sxs-lookup"><span data-stu-id="df5e8-153">Managing package owners on nuget.org</span></span>

<span data-ttu-id="df5e8-154">Přestože každý `.nuspec` soubor balíčku NuGet definuje autory balíčku, galerie nuget.org nepoužívá tato metadata k definování vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="df5e8-154">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="df5e8-155">Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která publikuje balíček.</span><span class="sxs-lookup"><span data-stu-id="df5e8-155">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="df5e8-156">Toto je buď přihlášený uživatel, který nahrál balíček prostřednictvím uživatelského rozhraní `nuget SetApiKey` nuget.org, nebo uživatelé, jejichž klíč rozhraní API byl použit s nebo `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="df5e8-156">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="df5e8-157">Všichni vlastníci balíčku mají úplná oprávnění pro balíček, včetně přidání a odebrání dalších vlastníků a publikování aktualizací.</span><span class="sxs-lookup"><span data-stu-id="df5e8-157">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="df5e8-158">Chcete-li změnit vlastnictví balíčku, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="df5e8-158">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="df5e8-159">Přihlaste se k nuget.org s účtem, který je aktuálním vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="df5e8-159">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="df5e8-160">Vyberte název účtu, vyberte **Spravovat balíčky**a **rozbalte Položku Publikované balíčky**.</span><span class="sxs-lookup"><span data-stu-id="df5e8-160">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="df5e8-161">Vyberte na balíčku, který chcete spravovat, pak na pravé straně vyberte **Spravovat vlastníky**.</span><span class="sxs-lookup"><span data-stu-id="df5e8-161">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="df5e8-162">Zde máte několik možností:</span><span class="sxs-lookup"><span data-stu-id="df5e8-162">From here you have several options:</span></span>

1. <span data-ttu-id="df5e8-163">Odeberte všechny vlastníky uvedené v části **Aktuální vlastníci**.</span><span class="sxs-lookup"><span data-stu-id="df5e8-163">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="df5e8-164">V části **Přidat vlastníka** přidejte vlastníka zadáním uživatelského jména, zprávy a výběrem možnosti **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="df5e8-164">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="df5e8-165">Tato akce odešle e-mail novému spoluvlastníkovi s potvrzovacím odkazem.</span><span class="sxs-lookup"><span data-stu-id="df5e8-165">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="df5e8-166">Po potvrzení má tato osoba úplná oprávnění k přidávání a odebírá vlastníky.</span><span class="sxs-lookup"><span data-stu-id="df5e8-166">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="df5e8-167">(Dokud nebude potvrzeno, část **Aktuální vlastníci** označuje čekající schválení pro tuto osobu.)</span><span class="sxs-lookup"><span data-stu-id="df5e8-167">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="df5e8-168">Chcete-li převést vlastnictví (jako když bylo vlastnické právo publikováno nebo byl balíček publikován pod nesprávným účtem), přidejte nového vlastníka a po potvrzení vlastnictví vás může ze seznamu odebrat.</span><span class="sxs-lookup"><span data-stu-id="df5e8-168">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="df5e8-169">Chcete-li přiřadit vlastnictví společnosti nebo skupině, vytvořte účet nuget.org pomocí e-mailového aliasu, který je předán příslušným členům týmu.</span><span class="sxs-lookup"><span data-stu-id="df5e8-169">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="df5e8-170">Například různé balíčky Microsoft ASP.NET jsou spoluvlastněny účty [Microsoft](https://nuget.org/profiles/microsoft) a [aspnet,](https://nuget.org/profiles/aspnet) které jednoduše takové aliasy.</span><span class="sxs-lookup"><span data-stu-id="df5e8-170">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](https://nuget.org/profiles/microsoft) and [aspnet](https://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="df5e8-171">Obnovení vlastnictví balíčku</span><span class="sxs-lookup"><span data-stu-id="df5e8-171">Recovering package ownership</span></span>

<span data-ttu-id="df5e8-172">V některých případě balíček nemusí mít aktivního vlastníka.</span><span class="sxs-lookup"><span data-stu-id="df5e8-172">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="df5e8-173">Původní vlastník například opustil společnost, která balíček vyrábí, nuget.org pověření jsou ztraceny nebo dřívější chyby v galerii zanechaly balíček bez vlastníka.</span><span class="sxs-lookup"><span data-stu-id="df5e8-173">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="df5e8-174">Pokud jste právoplatným vlastníkem balíčku a potřebujete znovu získat vlastnictví, použijte [kontaktní formulář](https://www.nuget.org/policies/Contact) na nuget.org vysvětlit vaši situaci týmu NuGet.</span><span class="sxs-lookup"><span data-stu-id="df5e8-174">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="df5e8-175">Poté se řídíme procesem ověření vašeho vlastnictví balíčku, včetně pokusu o nalezení stávajícího vlastníka prostřednictvím adresy URL projektu, Twitteru, e-mailu nebo jiným i jiným způsobem.</span><span class="sxs-lookup"><span data-stu-id="df5e8-175">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="df5e8-176">Ale pokud vše ostatní selže, můžeme vám poslat novou pozvánku, abyste se stali vlastníkem.</span><span class="sxs-lookup"><span data-stu-id="df5e8-176">But if all else fails, we can send you a new invite to become an owner.</span></span>
