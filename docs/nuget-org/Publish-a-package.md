---
title: Jak publikovat balíček NuGet
description: Podrobné pokyny pro publikování balíčku NuGet v nuget.org nebo privátních informačních kanálech a o tom, jak spravovat vlastnictví balíčku v nuget.org.
author: JonDouglas
ms.author: jodou
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 05a16d8bf609d727aba3ddbc42959a3deb97b24b
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901912"
---
# <a name="publishing-packages"></a><span data-ttu-id="de87e-103">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="de87e-103">Publishing packages</span></span>

<span data-ttu-id="de87e-104">Jakmile vytvoříte balíček a máte `.nupkg` soubor v ruce, je to jednoduchý proces, který ho zpřístupní ostatním vývojářům, a to veřejně nebo soukromě:</span><span class="sxs-lookup"><span data-stu-id="de87e-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="de87e-105">Veřejné balíčky jsou zpřístupněny všem vývojářům globálně prostřednictvím [NuGet.org](https://www.nuget.org/packages/manage/upload) , jak je popsáno v tomto článku (vyžaduje NuGet 4.1.0 +).</span><span class="sxs-lookup"><span data-stu-id="de87e-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="de87e-106">Soukromé balíčky jsou k dispozici pouze pro tým nebo organizaci, a to jejich hostováním buď sdílené složky, privátního serveru NuGet, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)nebo úložiště třetí strany, jako je například Myget, ProGet, Nexus úložiště a Artifactory.</span><span class="sxs-lookup"><span data-stu-id="de87e-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="de87e-107">Další podrobnosti najdete v tématu [Přehled hostujících balíčků](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="de87e-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="de87e-108">Tento článek popisuje publikování na nuget.org. informace o publikování do Azure Artifacts najdete v tématu [Správa balíčků](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="de87e-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="de87e-109">Publikovat na nuget.org</span><span class="sxs-lookup"><span data-stu-id="de87e-109">Publish to nuget.org</span></span>

<span data-ttu-id="de87e-110">V případě nuget.org se musíte přihlásit pomocí účet Microsoft, se kterým budete požádáni o registraci účtu v nuget.org.</span><span class="sxs-lookup"><span data-stu-id="de87e-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org.</span></span>

![Přihlašovací umístění NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="de87e-112">Dále můžete balíček nahrát prostřednictvím webového portálu nuget.org, vložit ho do nuget.org z příkazového řádku (vyžaduje `nuget.exe` 4.1.0 +) nebo publikovat jako součást procesu CI/CD prostřednictvím Azure DevOps Services, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="de87e-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="de87e-113">Webový portál: použijte kartu nahrát balíček v nuget.org</span><span class="sxs-lookup"><span data-stu-id="de87e-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="de87e-114">V horní nabídce nuget.org vyberte **nahrát** a vyhledejte umístění balíčku.</span><span class="sxs-lookup"><span data-stu-id="de87e-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Nahrání balíčku na nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="de87e-116">nuget.org obsahuje informace o tom, jestli je k dispozici název balíčku.</span><span class="sxs-lookup"><span data-stu-id="de87e-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="de87e-117">Pokud není, změňte identifikátor balíčku v projektu, znovu sestavte a opakujte nahrávání.</span><span class="sxs-lookup"><span data-stu-id="de87e-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="de87e-118">Pokud je název balíčku k dispozici, nuget.org otevře oddíl **ověření** , ve kterém můžete zkontrolovat metadata z manifestu balíčku.</span><span class="sxs-lookup"><span data-stu-id="de87e-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="de87e-119">Pokud jste do balíčku zahrnuli [soubor Readme](/docs/nuget-org/package-readme-on-nuget-org.md) , podívejte se do verze Preview a ujistěte se, že se veškerý obsah vykreslí správně.</span><span class="sxs-lookup"><span data-stu-id="de87e-119">If you included a [readme file](/docs/nuget-org/package-readme-on-nuget-org.md) in your package, check out the preview to ensure all content is being rendered properly.</span></span> <span data-ttu-id="de87e-120">Chcete-li změnit jakoukoli metadata, upravit projekt (soubor projektu nebo `.nuspec` soubor), znovu sestavit, znovu vytvořit balíček a znovu nahrávat.</span><span class="sxs-lookup"><span data-stu-id="de87e-120">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

2. <span data-ttu-id="de87e-121">Až budou všechny informace připravené, vyberte tlačítko **Odeslat** .</span><span class="sxs-lookup"><span data-stu-id="de87e-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="de87e-122">Příkazový řádek</span><span class="sxs-lookup"><span data-stu-id="de87e-122">Command line</span></span>

<span data-ttu-id="de87e-123">Pokud chcete nabízet balíčky do nuget.org, budete nejdřív potřebovat klíč rozhraní API, který se vytvoří v nuget.org. Musíte použít buď dotnet.exe (.NET Core), nebo nuget.exe v 4.1.0 nebo novějším, které implementují požadované protokoly NuGet.</span><span class="sxs-lookup"><span data-stu-id="de87e-123">To push packages to nuget.org, you first need an API key, which is created on nuget.org. You must use either dotnet.exe (.NET Core), or nuget.exe v4.1.0 or above, which implement the required NuGet protocols.</span></span>
<span data-ttu-id="de87e-124">Další informace najdete v tématu protokoly [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads)a [NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="de87e-124">For more information, see [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads), and [NuGet protocols](../api/nuget-protocols.md).</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="de87e-125">Vytvoření klíčů rozhraní API</span><span class="sxs-lookup"><span data-stu-id="de87e-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="de87e-126">Publikování pomocí příkazu dotnet NuGet push</span><span class="sxs-lookup"><span data-stu-id="de87e-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="de87e-127">Publikování s nabízeným oznámením NuGet</span><span class="sxs-lookup"><span data-stu-id="de87e-127">Publish with nuget push</span></span>

1. <span data-ttu-id="de87e-128">Na příkazovém řádku spusťte následující příkaz, kterým nahradíte `<your_API_key>` klíč získaný z NuGet.org:</span><span class="sxs-lookup"><span data-stu-id="de87e-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="de87e-129">Tento příkaz uloží klíč rozhraní API do konfigurace NuGet, takže tento krok nebudete muset opakovat na stejném počítači.</span><span class="sxs-lookup"><span data-stu-id="de87e-129">This command stores your API key in your NuGet configuration so that you don't need to repeat this step again on the same computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="de87e-130">Klíč rozhraní API se nepoužívá pro ověřování pomocí privátního informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="de87e-130">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="de87e-131">Pro správu přihlašovacích údajů pro ověřování ve zdroji použijte [ `nuget sources` příkaz](../reference/cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="de87e-131">Refer to [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
    > <span data-ttu-id="de87e-132">Klíče rozhraní API lze získat z jednotlivých serverů NuGet.</span><span class="sxs-lookup"><span data-stu-id="de87e-132">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="de87e-133">Informace o vytvoření a manange APIKeys pro nuget.org najdete v tématu [vytvoření klíčů rozhraní API](#create-api-keys).</span><span class="sxs-lookup"><span data-stu-id="de87e-133">To create and manange APIKeys for nuget.org refer to [Create API keys](#create-api-keys).</span></span>

1. <span data-ttu-id="de87e-134">Nahrajte balíček do galerie NuGet pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="de87e-134">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="de87e-135">Publikovat podepsané balíčky</span><span class="sxs-lookup"><span data-stu-id="de87e-135">Publish signed packages</span></span>

<span data-ttu-id="de87e-136">Chcete-li odeslat podepsané balíčky, je třeba nejprve [zaregistrovat certifikát](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) použitý k podepsání balíčků.</span><span class="sxs-lookup"><span data-stu-id="de87e-136">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="de87e-137">nuget.org odmítne balíčky, které nesplňují [požadavky na podepsaný balíček](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="de87e-137">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="de87e-138">Ověření a indexování balíčku</span><span class="sxs-lookup"><span data-stu-id="de87e-138">Package validation and indexing</span></span>

<span data-ttu-id="de87e-139">Balíčky vložené do nuget.org prošly několika ověřeními, jako jsou například kontroly virů.</span><span class="sxs-lookup"><span data-stu-id="de87e-139">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="de87e-140">(Všechny balíčky na nuget.org se pravidelně hledají.)</span><span class="sxs-lookup"><span data-stu-id="de87e-140">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="de87e-141">Po úspěšném provedení všech kontrol balíčku může chvíli trvat, než se bude indexovat a zobrazit ve výsledcích hledání.</span><span class="sxs-lookup"><span data-stu-id="de87e-141">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="de87e-142">Po dokončení indexování obdržíte e-mail s potvrzením, že balíček byl úspěšně publikován.</span><span class="sxs-lookup"><span data-stu-id="de87e-142">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="de87e-143">Pokud balíček neuspěje při ověření, aktualizuje se stránka s podrobnostmi balíčku, aby se zobrazila přidružená chyba, a obdržíte také e-mail s upozorněním.</span><span class="sxs-lookup"><span data-stu-id="de87e-143">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="de87e-144">Ověření a indexování balíčku obvykle trvá 15 minut.</span><span class="sxs-lookup"><span data-stu-id="de87e-144">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="de87e-145">Pokud publikování balíčku trvá déle, než se čekalo, navštivte [status.NuGet.org](https://status.nuget.org/) a ověřte, jestli NuGet.org má nějaké přerušení.</span><span class="sxs-lookup"><span data-stu-id="de87e-145">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="de87e-146">Pokud jsou všechny systémy funkční a balíček se do jedné hodiny nepublikoval úspěšně, přihlaste se k nuget.org a kontaktujte nás pomocí odkazu na podporu kontaktů na stránce balíček.</span><span class="sxs-lookup"><span data-stu-id="de87e-146">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="de87e-147">Pokud chcete zobrazit stav balíčku, vyberte **Spravovat balíčky** pod názvem svého účtu v NuGet.org. Po dokončení ověření se zobrazí potvrzovací e-mail.</span><span class="sxs-lookup"><span data-stu-id="de87e-147">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="de87e-148">Všimněte si, že může chvíli trvat, než se váš balíček naindexuje a zobrazí ve výsledcích hledání, kde ho můžou najít jiní uživatelé. v takovém případě se na stránce balíčku zobrazí následující zpráva:</span><span class="sxs-lookup"><span data-stu-id="de87e-148">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Zpráva oznamující, že balíček ještě není publikovaný](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="de87e-150">Azure DevOps Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="de87e-150">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="de87e-151">Pokud zadáte balíčky do nuget.org pomocí Azure DevOps Services jako součást procesu kontinuální integrace nebo nasazení, musíte `nuget.exe` v úlohách NuGet použít 4,1 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="de87e-151">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="de87e-152">Podrobnosti najdete v [části použití nejnovější sady NuGet v sestavení](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="de87e-152">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="de87e-153">Správa vlastníků balíčků na nuget.org</span><span class="sxs-lookup"><span data-stu-id="de87e-153">Managing package owners on nuget.org</span></span>

<span data-ttu-id="de87e-154">I když každý soubor balíčku NuGet `.nuspec` definuje autory balíčku, galerie NuGet.org nepoužívá tato metadata k definování vlastnictví.</span><span class="sxs-lookup"><span data-stu-id="de87e-154">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="de87e-155">Místo toho nuget.org přiřadí počáteční vlastnictví osobě, která balíček zveřejňuje.</span><span class="sxs-lookup"><span data-stu-id="de87e-155">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="de87e-156">Toto je buď přihlášený uživatel, který balíček odeslal prostřednictvím uživatelského rozhraní nuget.org, nebo uživatele, jejichž klíč rozhraní API se použil s `nuget SetApiKey` nebo `nuget push` .</span><span class="sxs-lookup"><span data-stu-id="de87e-156">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="de87e-157">Všichni vlastníci balíčku mají úplná oprávnění pro balíček, včetně přidávání a odebírání jiných vlastníků a publikování aktualizací.</span><span class="sxs-lookup"><span data-stu-id="de87e-157">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="de87e-158">Chcete-li změnit vlastnictví balíčku, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="de87e-158">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="de87e-159">Přihlaste se k nuget.org pomocí účtu, který je aktuálním vlastníkem balíčku.</span><span class="sxs-lookup"><span data-stu-id="de87e-159">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="de87e-160">Vyberte název účtu, vyberte **Spravovat balíčky** a rozbalte **publikované balíčky**.</span><span class="sxs-lookup"><span data-stu-id="de87e-160">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="de87e-161">Vyberte balíček, který chcete spravovat, a pak na pravé straně vyberte **Spravovat vlastníky**.</span><span class="sxs-lookup"><span data-stu-id="de87e-161">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="de87e-162">Tady máte několik možností:</span><span class="sxs-lookup"><span data-stu-id="de87e-162">From here you have several options:</span></span>

1. <span data-ttu-id="de87e-163">Odeberte všechny vlastníka uvedené v části **aktuální vlastníci**.</span><span class="sxs-lookup"><span data-stu-id="de87e-163">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="de87e-164">Přidejte vlastníka do části **Přidat vlastníka** zadáním jeho uživatelského jména, zprávy a výběru možnosti **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="de87e-164">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="de87e-165">Tato akce pošle e-mailem tomuto novému spoluvlastníkovi odkaz s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="de87e-165">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="de87e-166">Po potvrzení tato osoba má úplná oprávnění k přidávání a odebírání vlastníků.</span><span class="sxs-lookup"><span data-stu-id="de87e-166">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="de87e-167">(Až do potvrzení, část **aktuální vlastníci** indikuje, že se čeká na schválení pro tuto osobu.)</span><span class="sxs-lookup"><span data-stu-id="de87e-167">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="de87e-168">Pokud chcete přenést vlastnictví (jako při změně vlastnictví nebo balíčku, který se publikoval v nesprávném účtu), přidejte nového vlastníka a jakmile se potvrdí vlastnictví, můžou vás ze seznamu odebrat.</span><span class="sxs-lookup"><span data-stu-id="de87e-168">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="de87e-169">Pokud chcete přiřadit vlastnictví společnosti nebo skupiny, vytvořte účet nuget.org pomocí e-mailového aliasu předaného příslušnému členovi týmu.</span><span class="sxs-lookup"><span data-stu-id="de87e-169">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="de87e-170">Například různé balíčky Microsoft ASP.NET jsou spoluvlastněny účty [Microsoft](https://nuget.org/profiles/microsoft) a [ASPNET](https://nuget.org/profiles/aspnet) , které jednoduše odkazují na tyto aliasy.</span><span class="sxs-lookup"><span data-stu-id="de87e-170">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](https://nuget.org/profiles/microsoft) and [aspnet](https://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="de87e-171">Obnovování vlastnictví balíčku</span><span class="sxs-lookup"><span data-stu-id="de87e-171">Recovering package ownership</span></span>

<span data-ttu-id="de87e-172">V některých případech nemusí mít daný balíček aktivního vlastníka.</span><span class="sxs-lookup"><span data-stu-id="de87e-172">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="de87e-173">Původní vlastník například mohl přijít o společnost, která vytvořila balíček, nuget.org přihlašovací údaje nebo předchozí chyby v galerii opustili bez vlastníka balíčku.</span><span class="sxs-lookup"><span data-stu-id="de87e-173">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="de87e-174">Pokud jste vlastníkem balíčku rightful a potřebujete znovu získat vlastnictví, použijte [kontaktní formulář](https://www.nuget.org/policies/Contact) v NuGet.org a vysvětlete svou situaci týmu NuGet.</span><span class="sxs-lookup"><span data-stu-id="de87e-174">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="de87e-175">Pak budeme postupovat podle tohoto procesu a ověřit vlastnictví balíčku, včetně pokusu o vyhledání existujícího vlastníka prostřednictvím adresy URL projektu, Twitteru, e-mailu nebo jiného prostředku balíčku.</span><span class="sxs-lookup"><span data-stu-id="de87e-175">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="de87e-176">Pokud se ale všechny ostatní selžou, můžeme vám poslat nové pozvánky, abychom se stali vlastníkem.</span><span class="sxs-lookup"><span data-stu-id="de87e-176">But if all else fails, we can send you a new invite to become an owner.</span></span>
