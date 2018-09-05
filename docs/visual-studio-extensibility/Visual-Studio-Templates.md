---
title: Balíčky NuGet ve šablony sady Visual Studio
description: Pokyny, včetně balíčků NuGet jako součást šablony projektů a položek aplikace Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550507"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="bd750-103">Balíčky v šablony sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd750-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="bd750-104">Šablony projektů a položek aplikace Visual Studio je často potřeba zajistit, že některé balíčky se nainstalují při vytvoření projektu nebo položky.</span><span class="sxs-lookup"><span data-stu-id="bd750-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="bd750-105">Například šablony ASP.NET MVC 3 nainstalovat, jQuery, Modernizr a další balíčky.</span><span class="sxs-lookup"><span data-stu-id="bd750-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="bd750-106">Z toho důvodu autoři šablon můžete dát pokyn NuGet k instalaci potřebné balíčky, nikoli jednotlivých knihoven.</span><span class="sxs-lookup"><span data-stu-id="bd750-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="bd750-107">Vývojáři tedy můžete snadno aktualizovat tyto balíčky kdykoli později.</span><span class="sxs-lookup"><span data-stu-id="bd750-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="bd750-108">Další informace o vytváření samotné šablony, najdete v tématu [postupy: vytváření šablon projektu](/visualstudio/ide/how-to-create-project-templates) nebo [vytváření vlastních šablon projektů a položek](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="bd750-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="bd750-109">Zbytek tohoto oddílu popisuje zvláštní postup provést, když šablonu správně zahrnout balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="bd750-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="bd750-110">Přidávají se balíčky do šablony</span><span class="sxs-lookup"><span data-stu-id="bd750-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="bd750-111">Osvědčené postupy</span><span class="sxs-lookup"><span data-stu-id="bd750-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="bd750-112">Příklad najdete v tématu [NuGetInVsTemplates ukázka](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="bd750-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="bd750-113">Přidávají se balíčky do šablony</span><span class="sxs-lookup"><span data-stu-id="bd750-113">Adding packages to a template</span></span>

<span data-ttu-id="bd750-114">Při vytváření instance šablony [Průvodce šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) se vyvolá k načtení seznamu balíčků, které mají nainstalovat společně s informacemi o tom, kde najít tyto balíčky.</span><span class="sxs-lookup"><span data-stu-id="bd750-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="bd750-115">Balíčky může být vložen do VSIX, vložené v šabloně nebo umístěný na místní pevný disk v takovém případě odkazují na cestu k souboru pomocí klíče registru.</span><span class="sxs-lookup"><span data-stu-id="bd750-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="bd750-116">Podrobnosti na tato místa jsou uvedeny dále v této části.</span><span class="sxs-lookup"><span data-stu-id="bd750-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="bd750-117">Předinstalované balíčky pracovat pomocí [průvodců pro šablony](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="bd750-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="bd750-118">Speciální průvodce získá vyvolat získává vytvoření instance šablony.</span><span class="sxs-lookup"><span data-stu-id="bd750-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="bd750-119">Průvodce načte seznam balíčků, které je potřeba nainstalovat a předá tyto informace do příslušné NuGet rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="bd750-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="bd750-120">Postup do šablony zahrnout balíčky:</span><span class="sxs-lookup"><span data-stu-id="bd750-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="bd750-121">Ve vaší `vstemplate` přidejte odkaz na Průvodce šablonou NuGet tak, že přidáte [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span><span class="sxs-lookup"><span data-stu-id="bd750-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="bd750-122">`NuGet.VisualStudio.Interop.dll` je sestavení, který obsahuje pouze `TemplateWizard` třídu, která představuje jednoduchou obálku, která volá aktuální implementaci v `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="bd750-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="bd750-123">Verze sestavení se nikdy nezmění tak, že šablony projektu/položky pokračovat v práci s novými verzemi nástroje NuGet.</span><span class="sxs-lookup"><span data-stu-id="bd750-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="bd750-124">Přidáte seznam balíčků pro instalaci v projektu:</span><span class="sxs-lookup"><span data-stu-id="bd750-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="bd750-125">Průvodce podporuje více `<package>` prvky pro podporu více zdroje balíčků.</span><span class="sxs-lookup"><span data-stu-id="bd750-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="bd750-126">Jak `id` a `version` atributy jsou požadovány, což znamená, že konkrétní verzi balíčku se nainstaluje i v případě, že je k dispozici novější verze.</span><span class="sxs-lookup"><span data-stu-id="bd750-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="bd750-127">Aktualizace balíčků zabrání dopadem na dřívější kód šablony byste museli opustit možnost Aktualizovat balíček pro vývojáře pomocí šablony.</span><span class="sxs-lookup"><span data-stu-id="bd750-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="bd750-128">Zadáním úložiště NuGet kde najdete balíčky, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="bd750-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="bd750-129">Úložiště balíčků VSIX</span><span class="sxs-lookup"><span data-stu-id="bd750-129">VSIX package repository</span></span>

<span data-ttu-id="bd750-130">Doporučené nasazení přístup pro šablony sady Visual Studio projekt/položka je [rozšíření VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) protože umožňuje zabalit více šablon projektu/položky společně a umožňuje vývojářům snadné nalezení šablony Použití Správce rozšíření VS nebo Galerie sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd750-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="bd750-131">Aktualizace rozšíření jsou také snadno nasadit pomocí [mechanizmus automatických aktualizací Správce rozšíření pro Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="bd750-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="bd750-132">VSIX sám může sloužit jako zdroj pro balíčky vyžadované šablonou:</span><span class="sxs-lookup"><span data-stu-id="bd750-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="bd750-133">Upravit `<packages>` prvek `.vstemplate` to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bd750-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="bd750-134">`repository` Atribut určuje typ úložiště jako `extension` při `repositoryId` je jedinečný identifikátor souboru VSIX, samotný (jedná se o hodnotu z `ID` atribut do rozšíření `vsixmanifest` souborů naleznete v tématu [ VSIX Extension Schema 2.0 – referenční informace](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="bd750-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="bd750-135">Místo vaše `nupkg` soubory ve složce volá `Packages` ve VSIX.</span><span class="sxs-lookup"><span data-stu-id="bd750-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="bd750-136">Přidání souborů potřebný balíček jako `<Asset>` ve vaší `vsixmanifest` souboru (naleznete v tématu [VSIX Extension Schema 2.0 referenční informace](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="bd750-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="bd750-137">Všimněte si, že můžete doručujte balíčky do stejného VSIX jako projekt šablony nebo je můžete umístit do samostatného souboru VSIX a pokud se díky tomu větší smysl pro váš scénář.</span><span class="sxs-lookup"><span data-stu-id="bd750-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="bd750-138">Neodkazovat však žádné VSIX nad tím, které nemají ovládací prvek, protože změny tohoto rozšíření může poškodit šablony.</span><span class="sxs-lookup"><span data-stu-id="bd750-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="bd750-139">Úložiště balíčků šablony</span><span class="sxs-lookup"><span data-stu-id="bd750-139">Template package repository</span></span>

<span data-ttu-id="bd750-140">Pokud je distribuován pouze jeden projekt/položka šablony a nemusíte balíček více šablon najednou, můžete použít jednodušší, ale více omezený přístup, který obsahuje balíčky přímo v souboru ZIP šablony projektu/položky:</span><span class="sxs-lookup"><span data-stu-id="bd750-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="bd750-141">Upravit `<packages>` prvek `.vstemplate` to následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bd750-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="bd750-142">`repository` Atribut má hodnotu `template` a `repositoryId` atribut se nevyžaduje.</span><span class="sxs-lookup"><span data-stu-id="bd750-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="bd750-143">Umístěte balíčky v kořenové složce soubor ZIP šablony projektu/položky.</span><span class="sxs-lookup"><span data-stu-id="bd750-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="bd750-144">Všimněte si, že použití tohoto přístupu v rozšíření VSIX, který obsahuje více šablon vede ke zbytečné determinističtější když jeden nebo více balíčků, které jsou společné pro šablony.</span><span class="sxs-lookup"><span data-stu-id="bd750-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="bd750-145">V takovém případě použijte [VSIX jako úložiště](#vsix-package-repository) jak je popsáno v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="bd750-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="bd750-146">Cesta ke složce zadat registru</span><span class="sxs-lookup"><span data-stu-id="bd750-146">Registry-specified folder path</span></span>

<span data-ttu-id="bd750-147">Sady SDK, které se instalují pomocí MSI můžete nainstalovat balíčky NuGet přímo na počítači pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="bd750-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="bd750-148">Toto usnadňuje je k dispozici při šablonu projektu nebo položky se používá, namísto nutnosti jejich extrakci během této doby.</span><span class="sxs-lookup"><span data-stu-id="bd750-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="bd750-149">Šablony ASP.NET pomocí tohoto postupu.</span><span class="sxs-lookup"><span data-stu-id="bd750-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="bd750-150">Máte MSI nainstalujte balíčky do počítače.</span><span class="sxs-lookup"><span data-stu-id="bd750-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="bd750-151">Můžete nainstalovat pouze `.nupkg` soubory, nebo můžete nainstalovat ty spolu s rozšířené obsah, který uloží na další krok při použití této šablony.</span><span class="sxs-lookup"><span data-stu-id="bd750-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="bd750-152">V tomto případě mají následující strukturu složky standardní Nugetu ve které `.nupkg` jsou soubory v kořenové složce a potom každý balíček obsahuje podsložku s pár id a verzi jako název podsložky.</span><span class="sxs-lookup"><span data-stu-id="bd750-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="bd750-153">Zapsat klíč registru pro určení umístění balíčku:</span><span class="sxs-lookup"><span data-stu-id="bd750-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="bd750-154">Klíč umístění: buď celý počítač `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` nebo pokud je nainstalována na uživatele šablony a balíčky, případně použít. `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="bd750-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="bd750-155">Název klíče: použijte název, který je jedinečný pro vás.</span><span class="sxs-lookup"><span data-stu-id="bd750-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="bd750-156">Například šablony ASP.NET MVC 4 pro sadu VS 2012 použití `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="bd750-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="bd750-157">Hodnoty: úplná cesta ke složce balíčků.</span><span class="sxs-lookup"><span data-stu-id="bd750-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="bd750-158">V `<packages>` prvek `.vstemplate` přidejte atribut `repository="registry"` a zadejte název klíče registru v `keyName` atribut.</span><span class="sxs-lookup"><span data-stu-id="bd750-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="bd750-159">Pokud jste předem odblokujte balíčků, použijte `isPreunzipped="true"` atribut.</span><span class="sxs-lookup"><span data-stu-id="bd750-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="bd750-160">*(NuGet 3.2 +)*  Pokud chcete vynutit sestavení doby návrhu na konci instalace balíčku, přidejte `forceDesignTimeBuild="true"` atribut.</span><span class="sxs-lookup"><span data-stu-id="bd750-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="bd750-161">Optimalizace, přidejte `skipAssemblyReferences="true"` protože samotné šablony již obsahuje potřebné odkazy.</span><span class="sxs-lookup"><span data-stu-id="bd750-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="bd750-162">Doporučené postupy</span><span class="sxs-lookup"><span data-stu-id="bd750-162">Best Practices</span></span>

1. <span data-ttu-id="bd750-163">Deklaruje závislost na NuGet VSIX tak, že přidáte na ni odkaz v manifestu VSIX:</span><span class="sxs-lookup"><span data-stu-id="bd750-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="bd750-164">Vyžadují šablony projektu/položky mají být uloženy vytváření zahrnutím [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) v `.vstemplate` souboru.</span><span class="sxs-lookup"><span data-stu-id="bd750-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="bd750-165">Šablony nejsou zahrnuté `packages.config` souborů a nezahrnuje nebo odkazy nebo obsah, který se přidá při instalaci balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="bd750-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
