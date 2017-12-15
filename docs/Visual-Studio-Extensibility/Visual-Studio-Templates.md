---
title: "Balíčky NuGet ve šablony sady Visual Studio | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: "Pokyny včetně balíčků NuGet v rámci šablon projektů a položek v sadě Visual Studio."
keywords: "NuGet v sadě Visual Studio, šablony projektů Visual Studio, položka šablony sady Visual Studio, balíčky v projektu šablony, balíčky v šablonách položek"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="a6fc6-104">Balíčky v šablony sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6fc6-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="a6fc6-105">Projektů a položek šablony sady Visual Studio se často potřeba zajistit, že některé balíčky instalují do při vytváření projektu nebo položky.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-105">Visual Studio project and item templates often need to ensure that certain packages are installed into when the project or item is created.</span></span> <span data-ttu-id="a6fc6-106">Například šablony ASP.NET MVC 3 nainstaluje jQuery, Modernizr a dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="a6fc6-107">Za tímto účelem šablony autorům určit, aby NuGet k instalaci potřebné balíčky, nikoli jednotlivých knihoven.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="a6fc6-108">Vývojáři tedy můžete snadno aktualizovat tyto balíčky kdykoli později.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="a6fc6-109">Další informace o vytváření šablon sami, najdete v tématu [vytváření šablon projektů a položek v sadě Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) nebo [vytváření vlastních šablon projektů a položek s Visual Studio SDK](https://msdn.microsoft.com/library/ff527340.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6fc6-109">To learn more about authoring templates themselves, refer to [Creating Project and Item Templates in Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) or [Creating Custom Project and Item Templates with the Visual Studio SDK](https://msdn.microsoft.com/library/ff527340.aspx).</span></span>

<span data-ttu-id="a6fc6-110">Zbývající část Tato část popisuje konkrétní kroky pro zajištění správně zahrnout balíčků NuGet při vytváření šablony.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="a6fc6-111">Přidávání balíčků do šablony</span><span class="sxs-lookup"><span data-stu-id="a6fc6-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="a6fc6-112">Doporučené postupy</span><span class="sxs-lookup"><span data-stu-id="a6fc6-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="a6fc6-113">Příklad, naleznete v části [NuGetInVsTemplates ukázka](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="a6fc6-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>


## <a name="adding-packages-to-a-template"></a><span data-ttu-id="a6fc6-114">Přidávání balíčků do šablony</span><span class="sxs-lookup"><span data-stu-id="a6fc6-114">Adding packages to a template</span></span>

<span data-ttu-id="a6fc6-115">Při vytváření instance šablony [Průvodce šablonou](https://msdn.microsoft.com/library/ms185301.aspx) je vyvolána k načíst seznam balíčků, které mají nainstalovat společně s informacemi o tom, kde najít tyto balíčky.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-115">When a template is instantiated, a [template wizard](https://msdn.microsoft.com/library/ms185301.aspx) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="a6fc6-116">Balíčky mohou být vložených ve VSIX, vložené v šabloně nebo umístěné na místním pevném disku v takovém případě pomocí klíče registru tak, aby odkazovaly cesta k souboru.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="a6fc6-117">Podrobnosti o těchto umístění jsou uvedeny později v této části.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="a6fc6-118">Předinstalované balíčky pomocí fungovalo [průvodců pro šablony](http://msdn.microsoft.com/library/ms185301.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6fc6-118">Preinstalled packages work using [template wizards](http://msdn.microsoft.com/library/ms185301.aspx).</span></span> <span data-ttu-id="a6fc6-119">Speciální Průvodce volán získá vytvoření instance šablony.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="a6fc6-120">Průvodce načte seznam balíčků, které je potřeba nainstalovat a předá tyto informace k rozhraním API odpovídající NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="a6fc6-121">Postup do šablony zahrnout balíčky:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="a6fc6-122">Ve vaší `vstemplate` soubor, přidejte odkaz na Průvodce šablonou NuGet přidáním [ `WizardExtension` ](http://msdn.microsoft.com/library/ms171411.aspx) element:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="a6fc6-123">`NuGet.VisualStudio.Interop.dll`je sestavení obsahující pouze `TemplateWizard` třídy, která představuje jednoduchý obálku, který volá do skutečné implementace v `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="a6fc6-124">Verze sestavení se nikdy změnit tak, aby šablon projektu nebo položek pokračovat v práci s novými verzemi nástroje NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="a6fc6-125">Přidáte seznam balíčků pro instalaci v projektu:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="a6fc6-126">*(NuGet 2.2.1+)*  Průvodce podporuje více `<package>` elementy pro podporu více zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="a6fc6-127">Jak `id` a `version` atributy jsou požadovány, což znamená, že konkrétní verze balíčku se nainstalují i v případě, že je k dispozici novější verze.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="a6fc6-128">Aktualizace balíčků zabrání nejnovější šablony, a rozhodnout pro daný balíček aktualizovat vývojáře pomocí šablony.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>


1. <span data-ttu-id="a6fc6-129">Zadejte úložiště NuGet kde najdete balíčky, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="a6fc6-130">Úložiště balíčku VSIX</span><span class="sxs-lookup"><span data-stu-id="a6fc6-130">VSIX package repository</span></span>

<span data-ttu-id="a6fc6-131">Doporučené nasazení přístup pro šablony sady Visual Studio nebo položka projektu je [VSIX rozšíření](http://msdn.microsoft.com/library/ff363239.aspx) protože umožňuje sbalit několik šablon projektu/položky společně a umožňuje vývojářům snadno zjistit vaše šablony pomocí Správce rozšíření VS nebo Galerii Visual Studia.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](http://msdn.microsoft.com/library/ff363239.aspx) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="a6fc6-132">Aktualizace pro rozšíření jsou také snadno nasadit pomocí [mechanizmus automatických aktualizací Visual Studio rozšíření Manager](http://msdn.microsoft.com/library/dd997169.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6fc6-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](http://msdn.microsoft.com/library/dd997169.aspx).</span></span>

<span data-ttu-id="a6fc6-133">VSIX samotné může sloužit jako zdroj pro balíčky vyžadované šablonou:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="a6fc6-134">Změnit `<packages>` element v `.vstemplate` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="a6fc6-135">`repository` Atribut určuje typ úložiště jako `extension` při `repositoryId` je jedinečný identifikátor VSIX samotné (to je hodnota [ `ID` atribut](http://msdn.microsoft.com/library/dd393688.aspx) v rozšíření `vsixmanifest` souboru).</span><span class="sxs-lookup"><span data-stu-id="a6fc6-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the [`ID` attribute](http://msdn.microsoft.com/library/dd393688.aspx) in the extension’s `vsixmanifest` file).</span></span>

1. <span data-ttu-id="a6fc6-136">Místní vaše `nupkg` soubory ve složce nazývají `Packages` ve VSIX.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>
1. <span data-ttu-id="a6fc6-137">Přidat soubory potřebný balíček jako [vlastní rozšíření obsah](http://msdn.microsoft.com/library/dd393737.aspx) ve vaší `source.extension.vsixmanifest` souboru.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-137">Add the necessary package files as [custom extension content](http://msdn.microsoft.com/library/dd393737.aspx) in your `source.extension.vsixmanifest` file.</span></span> <span data-ttu-id="a6fc6-138">Pokud používáte schéma 2.0 by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-138">If you're using the 2.0 schema it should look like this:</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    <span data-ttu-id="a6fc6-139">Pokud používáte schéma 1.0 by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-139">If you're using the 1.0 schema it should look like this:</span></span>

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
    ```

1. <span data-ttu-id="a6fc6-140">Poznámka: abyste mohli zajistit balíčků ve stejné VSIX jako šablony projektu nebo můžete je umístit do samostatné VSIX to další pro váš scénář.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-140">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="a6fc6-141">Neodkazujte však žádné VSIX, přes který nemáte ovládací prvek, protože změny tohoto rozšíření by mohlo způsobit narušení vaší šablony.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-141">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>


### <a name="template-package-repository"></a><span data-ttu-id="a6fc6-142">Úložiště balíčků šablony</span><span class="sxs-lookup"><span data-stu-id="a6fc6-142">Template package repository</span></span>

<span data-ttu-id="a6fc6-143">Pokud je distribuován pouze jednu projektu nebo položku šablonu a nemusíte balíček několik šablon společně, můžete použít jednodušší, i když omezenější přístup, který obsahuje balíčky přímo v souboru ZIP šablony projektu/položky:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-143">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="a6fc6-144">Změnit `<packages>` element v `.vstemplate` následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-144">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="a6fc6-145">`repository` Atribut má hodnotu `template` a `repositoryId` atribut se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-145">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="a6fc6-146">Umístěte balíčky v kořenové složce soubor ZIP šablony projektu/položky.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-146">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="a6fc6-147">Všimněte si, že použití tohoto přístupu v VSIX, který obsahuje několik šablon vede k tomu nepotřebné když jeden nebo více balíčků, které jsou společné pro šablony.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-147">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="a6fc6-148">V takových případech použít [VSIX jako úložiště](#vsix-package-repository) jak je popsáno v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-148">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>


### <a name="registry-specified-folder-path"></a><span data-ttu-id="a6fc6-149">Cesta ke složce zadat registru</span><span class="sxs-lookup"><span data-stu-id="a6fc6-149">Registry-specified folder path</span></span>

<span data-ttu-id="a6fc6-150">Sady SDK, které se instalují pomocí souboru MSI mohou instalovat balíčky NuGet přímo na počítači pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-150">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="a6fc6-151">Tato díky je k dispozici při šablonu projektu nebo položky se používá, namísto nutnosti extrahovat je během této doby.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-151">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="a6fc6-152">Tuto metodu použijte šablony ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-152">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="a6fc6-153">Máte MSI instalovat balíčky do počítače.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-153">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="a6fc6-154">Můžete nainstalovat pouze `.nupkg` soubory, nebo můžete nainstalovat těch, které společně s rozšířené obsah, který uloží na další krok, pokud šablony.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-154">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="a6fc6-155">V takovém případě postupujte podle NuGet standardní struktuře složek ve kterém `.nupkg` jsou soubory v kořenové složce a potom každý balíček obsahuje podsložky dvojice id a verzi jako název podsložky.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-155">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="a6fc6-156">Zapsat klíč registru pro určení umístění balíčku:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-156">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="a6fc6-157">Klíč umístění: buď úrovni celého `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` nebo pokud je nainstalována na uživatele šablony a balíčky, případně použít.`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="a6fc6-157">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="a6fc6-158">Název klíče: použijte název, který je jedinečný pro vás.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-158">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="a6fc6-159">Například šablony ASP.NET MVC 4 pro sadu VS 2012 použití `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-159">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="a6fc6-160">Hodnoty: úplná cesta ke složce balíčků.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-160">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="a6fc6-161">V `<packages>` element v `.vstemplate` soubor, přidejte atribut `repository="registry"` a zadejte název klíče v registru `keyName` atribut.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-161">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="a6fc6-162">Pokud máte předem unzipped vlastních balíčků, použijte `isPreunzipped="true"` atribut.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-162">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="a6fc6-163">*(NuGet 3.2 +)*  Pokud chcete vynutit sestavení návrhu na konci instalace balíčku, přidejte `forceDesignTimeBuild="true"` atribut.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-163">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="a6fc6-164">Jako optimalizace, přidejte `skipAssemblyReferences="true"` protože samotné šablony již obsahuje odkazy na nezbytné.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-164">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="a6fc6-165">Doporučené postupy</span><span class="sxs-lookup"><span data-stu-id="a6fc6-165">Best Practices</span></span>

1. <span data-ttu-id="a6fc6-166">Závislost na NuGet VSIX deklarujte přidáním odkazu k němu v manifestu VSIX:</span><span class="sxs-lookup"><span data-stu-id="a6fc6-166">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="a6fc6-167">Vyžadovat šablon projektu nebo položek uložit na vytváření nastavením [ `<PromptForSaveOnCreation>` ](http://msdn.microsoft.com/library/twfxayz5.aspx) v `.vstemplate` souboru.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-167">Require project/item templates to be saved on creation by setting [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="a6fc6-168">Šablony neobsahují `packages.config` nebo `project.json` souboru a nezahrnují nebo žádné odkazy nebo obsah, který by byl přidán, když se instalují balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6fc6-168">Templates do not include a `packages.config` or `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
