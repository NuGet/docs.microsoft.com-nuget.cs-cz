---
title: "Úvodní příručka o vytváření a publikování balíčku NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Návod kurz týkající se vytváření a publikování balíčku NuGet pomocí rozhraní příkazového řádku nuget.exe a Visual Studio."
keywords: "Vytvoření balíčku NuGet, publikování, balíček NuGet kurzu NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b33344c3b3dd782fc4668d2a1674b9501fadcc03
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="136c9-104">Vytvoření a publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="136c9-104">Create and publish a package</span></span>

<span data-ttu-id="136c9-105">Je jednoduchý proces vytvoření balíčku NuGet z knihovny tříd rozhraní .NET a publikujete ho v nuget.org. Následující kroky vás provedou procesem, pomocí rozhraní NuGet příkazového řádku (CLI) a Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="136c9-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="136c9-106">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="136c9-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="136c9-107">Vytvoření souboru manifestu balíčku příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="136c9-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="136c9-108">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="136c9-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="136c9-109">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="136c9-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="136c9-110">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="136c9-110">Pre-requisites</span></span>

1. <span data-ttu-id="136c9-111">Nainstalujte všechny edice Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="136c9-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="136c9-112">Nainstalujte nástroj příkazového řádku NuGet `nuget.exe`, stáhněte nejnovější verzi `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads)a uložit `.exe` do umístění v CESTĚ.</span><span class="sxs-lookup"><span data-stu-id="136c9-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="136c9-113">Všimněte si, že stahování *je* nástroj sám, není instalační program.</span><span class="sxs-lookup"><span data-stu-id="136c9-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="136c9-114">Vytvoření vhodného knihovna tříd rozhraní .NET projektu pro kód, který chcete balíček.</span><span class="sxs-lookup"><span data-stu-id="136c9-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="136c9-115">Pokud ještě nemáte projektu, můžete vytvořit jednoduchý následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="136c9-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="136c9-116">V sadě Visual Studio, vyberte **soubor > Nový > projekt**, rozbalte **Visual C# > Windows** uzlu, vyberte šablonu "Knihovna tříd", název projektu AppLogger a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="136c9-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="136c9-117">Klikněte pravým tlačítkem na výsledný soubor projektu a vyberte **sestavení** a ujistěte se, vytvoření projektu správně.</span><span class="sxs-lookup"><span data-stu-id="136c9-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="136c9-118">Knihovny DLL nachází v rámci ladění složky (nebo verze, pokud vytváříte tuto konfiguraci místo).</span><span class="sxs-lookup"><span data-stu-id="136c9-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="136c9-119">V rámci skutečné balíčku NuGet samozřejmě budete implementovat mnoho užitečných funkcí, o kterých ostatní mohou vytvářet aplikace.</span><span class="sxs-lookup"><span data-stu-id="136c9-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="136c9-120">V tomto návodu však nebude napsat další kód, protože knihovny tříd ze šablony, stačí vytvořit balíček.</span><span class="sxs-lookup"><span data-stu-id="136c9-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="136c9-121">Vytvoření souboru manifestu balíčku příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="136c9-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="136c9-122">Každý balíček NuGet musí manifestu&mdash; `.nuspec` soubor&mdash;k popisu její obsah a jeho závislosti.</span><span class="sxs-lookup"><span data-stu-id="136c9-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="136c9-123">`nuget spec` Příkaz vytvoří tento soubor pro vás, která pak přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="136c9-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="136c9-124">V tomto příkladu vytvoříte `.nuspec` ze souboru projektu; můžete také vytvořit manifest jinými způsoby jak je popsáno na [vytvořit balíček](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="136c9-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="136c9-125">Otevřete příkazový řádek a přejděte ke složce obsahující soubor projektu (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="136c9-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="136c9-126">Spuštění rozhraní příkazového řádku NuGet `spec` příkaz pro generování manifestu, který se nazývá po projektu, například `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="136c9-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="136c9-127">Otevřete soubor v textovém editoru.</span><span class="sxs-lookup"><span data-stu-id="136c9-127">Open the file in a text editor.</span></span> <span data-ttu-id="136c9-128">Manifest je podobný kódu níže, kde tokeny ve formátu  *$ `<token>` $*  nahrazená při vytváření balíčku hodnotami z Properties/AssemblyInfo.cs projektu soubor.</span><span class="sxs-lookup"><span data-stu-id="136c9-128">The manifest looks something like the code below, where tokens in the form *$`<token>`$* are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="136c9-129">Další informace o tokeny v [vytváření soubor s příponou .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="136c9-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="136c9-130">Vyberte ID balíčku, který je jedinečný v rámci nuget.org. Doporučujeme používat se zásadami vytváření názvů, které jsou popsané v [vytváření balíčku](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="136c9-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="136c9-131">Nezapomeňte aktualizovat autora a popis značky nebo dojde k chybě v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="136c9-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="136c9-132">Tady je aktualizované `.nuspec` souboru jako příklad:</span><span class="sxs-lookup"><span data-stu-id="136c9-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="136c9-133">Pro balíčky vytvořené pro veřejné spotřeby, věnujte zvláštní pozornost `<tags>` elementu, jako jsou tyto značky ostatní najít váš balíček a co provádí.</span><span class="sxs-lookup"><span data-stu-id="136c9-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="136c9-134">Spusťte příkaz pack</span><span class="sxs-lookup"><span data-stu-id="136c9-134">Run the pack command</span></span>

<span data-ttu-id="136c9-135">K vytvoření balíčku NuGet ( `.nupkg` souboru) z projektu, spusťte `pack` příkaz:</span><span class="sxs-lookup"><span data-stu-id="136c9-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="136c9-136">Tento příkaz vytvoří `AppLogger.1.0.0.0.nupkg` pomocí číslo název a verze balíčku z `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="136c9-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="136c9-137">Příkaz vydá upozornění, pokud jste neprovedli aktualizaci různých polí v `.nuspec` soubor z výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="136c9-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="136c9-138">Umožňuje publikovat balíček</span><span class="sxs-lookup"><span data-stu-id="136c9-138">Publish the package</span></span>

<span data-ttu-id="136c9-139">Jakmile máte `.nupkg` souboru ji publikujete pomocí nuget.org `push` příkaz.</span><span class="sxs-lookup"><span data-stu-id="136c9-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="136c9-140">(Alternativně můžete použít [pracovní postup publikování nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="136c9-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="136c9-141">Balíčky, které publikujete nuget.org jsou veřejně viditelné pro ostatní vývojáři.</span><span class="sxs-lookup"><span data-stu-id="136c9-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="136c9-142">K hostování balíčků soukromě, najdete v části [hostování balíčků](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="136c9-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="136c9-143">Vytvořit bezplatný účet na [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), nebo se přihlásit, pokud již účet máte.</span><span class="sxs-lookup"><span data-stu-id="136c9-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="136c9-144">Vytvoření nového účtu odešle e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="136c9-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="136c9-145">Účet je potřeba zkontrolovat, než můžete nahrát balíček.</span><span class="sxs-lookup"><span data-stu-id="136c9-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="136c9-146">Po přihlášení, vyberte jméno uživatele (v pravém horním rohu) a pak vyberte **klíče rozhraní API**.</span><span class="sxs-lookup"><span data-stu-id="136c9-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="136c9-147">Vyberte **vytvořit**, zadejte název klíče, vyberte **vyberte obory > Push**pod **klíč rozhraní API**, zadejte * pro **Glob vzor**, pak Vyberte **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="136c9-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter * for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="136c9-148">Po vytvoření klíče, vyberte **kopie** načíst přístup klíčů budete potřebovat v rozhraní příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="136c9-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Klíč rozhraní API kopírování do schránky.](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="136c9-150">Váš klíč uložit na bezpečném místě a udržování je tajný klíč.</span><span class="sxs-lookup"><span data-stu-id="136c9-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="136c9-151">Pokud váš klíč se omylem zjistí, můžete ho obnovit vždy kdykoli.</span><span class="sxs-lookup"><span data-stu-id="136c9-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="136c9-152">Klíč rozhraní API můžete také odebrat, pokud již nechcete push balíčky prostřednictvím rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="136c9-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="136c9-153">Na příkazovém řádku spusťte následující příkaz zadáte název balíčku a klíč nahraďte hodnotou zkopírovali v kroku 4:</span><span class="sxs-lookup"><span data-stu-id="136c9-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="136c9-154">nuget.exe zobrazuje výsledky procesu publikování:</span><span class="sxs-lookup"><span data-stu-id="136c9-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="136c9-155">Váš profil na nuget.org vyberte **spravovat balíčky** zobrazíte ten právě publikovaný.</span><span class="sxs-lookup"><span data-stu-id="136c9-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="136c9-156">Také obdržíte e-mail s potvrzením.</span><span class="sxs-lookup"><span data-stu-id="136c9-156">You also receive a confirmation email.</span></span> <span data-ttu-id="136c9-157">Všimněte si, že může trvat nějakou dobu vašeho balíčku indexovat a zobrazit ve výsledcích hledání tam, kde ostatní můžete najít.</span><span class="sxs-lookup"><span data-stu-id="136c9-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="136c9-158">Během této doby stránku balíčku zobrazuje následující zpráva:</span><span class="sxs-lookup"><span data-stu-id="136c9-158">During that time your package page shows the message below:</span></span>

    ![Tento balíček nebyl nebyly indexovány.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="136c9-161">**Viry**: všechny balíčky nahrán do nuget.org jsou zkontrolovat viry a odmítnuta, pokud nejsou nalezeny žádné viry.</span><span class="sxs-lookup"><span data-stu-id="136c9-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="136c9-162">Všechny balíčky uvedené v nuget.org také jsou pravidelně kontrolovány.</span><span class="sxs-lookup"><span data-stu-id="136c9-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="136c9-163">A je to!</span><span class="sxs-lookup"><span data-stu-id="136c9-163">And that's it!</span></span> <span data-ttu-id="136c9-164">Právě jste publikovali vaše první balíček NuGet, abyste [nuget.org](https://www.nuget.org/), který ostatní vývojáři mohou použít ve svých vlastních projektů.</span><span class="sxs-lookup"><span data-stu-id="136c9-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="136c9-165">Související témata</span><span class="sxs-lookup"><span data-stu-id="136c9-165">Related topics</span></span>

- [<span data-ttu-id="136c9-166">Vytvoření balíčku</span><span class="sxs-lookup"><span data-stu-id="136c9-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="136c9-167">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="136c9-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="136c9-168">Podpora více cílové rozhraní</span><span class="sxs-lookup"><span data-stu-id="136c9-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="136c9-169">Správa verzí balíčku</span><span class="sxs-lookup"><span data-stu-id="136c9-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="136c9-170">Vytvoření lokalizovaných balíčků</span><span class="sxs-lookup"><span data-stu-id="136c9-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
