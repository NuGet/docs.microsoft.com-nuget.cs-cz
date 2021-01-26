---
title: Balíčky NuGet v šablonách sady Visual Studio
description: Pokyny, jak zahrnout balíčky NuGet jako součást šablon projektů a položek sady Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 82a0121bb3144b7f28f677185039c0fe15cc2bf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780085"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="2db59-103">Balíčky v šablonách sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2db59-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="2db59-104">Šablony projektů a položek sady Visual Studio často potřebují zajistit, aby při vytvoření projektu nebo položky byly nainstalovány určité balíčky.</span><span class="sxs-lookup"><span data-stu-id="2db59-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="2db59-105">Například šablona ASP.NET MVC 3 nainstaluje jQuery, modernizr a další balíčky.</span><span class="sxs-lookup"><span data-stu-id="2db59-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="2db59-106">Pro podporu tohoto nástroje můžou autoři šablon dát pokyn NuGet k instalaci potřebných balíčků místo jednotlivých knihoven.</span><span class="sxs-lookup"><span data-stu-id="2db59-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="2db59-107">Vývojáři pak tyto balíčky můžou později snadno aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="2db59-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="2db59-108">Další informace o vytváření vlastních šablon najdete v tématu [Postupy: vytváření šablon projektů](/visualstudio/ide/how-to-create-project-templates) nebo [vytváření vlastních šablon projektů a položek](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="2db59-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="2db59-109">Zbývající část této části popisuje konkrétní kroky, které je potřeba provést při vytváření šablony pro správné zahrnutí balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="2db59-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="2db59-110">Přidání balíčků do šablony</span><span class="sxs-lookup"><span data-stu-id="2db59-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="2db59-111">Osvědčené postupy</span><span class="sxs-lookup"><span data-stu-id="2db59-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="2db59-112">Příklad najdete v [ukázce NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="2db59-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="2db59-113">Přidání balíčků do šablony</span><span class="sxs-lookup"><span data-stu-id="2db59-113">Adding packages to a template</span></span>

<span data-ttu-id="2db59-114">Při vytvoření instance šablony se vyvolá [Průvodce šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) , který načte seznam balíčků k instalaci společně s informacemi o tom, kde tyto balíčky najít.</span><span class="sxs-lookup"><span data-stu-id="2db59-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="2db59-115">Balíčky mohou být vloženy do VSIX, vloženy do šablony nebo umístěny na místním pevném disku. v takovém případě použijete klíč registru pro odkazování na cestu k souboru.</span><span class="sxs-lookup"><span data-stu-id="2db59-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="2db59-116">Podrobnosti o těchto umístěních jsou uvedené dále v této části.</span><span class="sxs-lookup"><span data-stu-id="2db59-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="2db59-117">Předinstalované balíčky fungují pomocí [průvodců šablonou](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="2db59-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="2db59-118">Speciální průvodce, který se vyvolá při vytváření instance šablony.</span><span class="sxs-lookup"><span data-stu-id="2db59-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="2db59-119">Průvodce načte seznam balíčků, které je potřeba nainstalovat, a předá tyto informace do příslušných rozhraní API NuGet.</span><span class="sxs-lookup"><span data-stu-id="2db59-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="2db59-120">Postup zahrnutí balíčků do šablony:</span><span class="sxs-lookup"><span data-stu-id="2db59-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="2db59-121">Do `vstemplate` souboru přidejte odkaz na Průvodce šablonou NuGet přidáním [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elementu:</span><span class="sxs-lookup"><span data-stu-id="2db59-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="2db59-122">`NuGet.VisualStudio.Interop.dll` je sestavení, které obsahuje pouze `TemplateWizard` třídu, což je jednoduchá obálka, která volá do samotné implementace v `NuGet.VisualStudio.dll` .</span><span class="sxs-lookup"><span data-stu-id="2db59-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="2db59-123">Verze sestavení se nikdy nezmění, aby šablony projektů a položek pokračovaly v práci s novými verzemi NuGet.</span><span class="sxs-lookup"><span data-stu-id="2db59-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="2db59-124">Přidat seznam balíčků k instalaci v projektu:</span><span class="sxs-lookup"><span data-stu-id="2db59-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="2db59-125">Průvodce podporuje více `<package>` prvků pro podporu více zdrojů balíčků.</span><span class="sxs-lookup"><span data-stu-id="2db59-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="2db59-126">`id` `version` Atributy i jsou povinné, což znamená, že se nainstaluje konkrétní verze balíčku i v případě, že je k dispozici novější verze.</span><span class="sxs-lookup"><span data-stu-id="2db59-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="2db59-127">Tím zabráníte tomu, aby se aktualizace balíčků přerušujíy v šabloně, takže se možnost aktualizace balíčku aktualizuje na vývojáře pomocí šablony.</span><span class="sxs-lookup"><span data-stu-id="2db59-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="2db59-128">Zadejte úložiště, ve kterém může NuGet najít balíčky, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="2db59-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="2db59-129">Úložiště balíčků VSIX</span><span class="sxs-lookup"><span data-stu-id="2db59-129">VSIX package repository</span></span>

<span data-ttu-id="2db59-130">Doporučený přístup k nasazení šablon projektů a položek sady Visual Studio je [rozšíření VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) , protože umožňuje zabalit více šablon projektů a položek dohromady a umožňuje vývojářům snadno vyhledat šablony pomocí Správce rozšíření vs nebo galerie sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2db59-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="2db59-131">Aktualizace rozšíření je také snadné nasadit pomocí [mechanismu automatických aktualizací správce rozšíření sady Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="2db59-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="2db59-132">Samotný VSIX může sloužit jako zdroj pro balíčky, které šablona vyžaduje:</span><span class="sxs-lookup"><span data-stu-id="2db59-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="2db59-133">Upravte `<packages>` prvek v souboru následujícím `.vstemplate` způsobem:</span><span class="sxs-lookup"><span data-stu-id="2db59-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="2db59-134">`repository`Atribut určuje typ úložiště, jako by `extension` byl ale `repositoryId` jedinečný identifikátor samotného VSIX (Jedná se o hodnotu `ID` atributu v `vsixmanifest` souboru rozšíření, viz [Referenční dokumentace schématu rozšíření VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="2db59-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="2db59-135">Umístěte `nupkg` soubory do složky pojmenované v `Packages` rámci VSIX.</span><span class="sxs-lookup"><span data-stu-id="2db59-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="2db59-136">Přidejte potřebné soubory balíčku jako `<Asset>` v `vsixmanifest` souboru (viz Referenční dokumentace [schématu rozšíření VSIX 2,0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="2db59-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="2db59-137">Všimněte si, že můžete doručovat balíčky na stejném VSIX jako šablony projektu nebo je můžete umístit do samostatného souboru VSIX, pokud to pro váš scénář bude smysluplnější.</span><span class="sxs-lookup"><span data-stu-id="2db59-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="2db59-138">Ale neodkazujte na žádný VSIX, přes který nemáte kontrolu, protože změny tohoto rozšíření by mohly přerušit vaši šablonu.</span><span class="sxs-lookup"><span data-stu-id="2db59-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="2db59-139">Úložiště balíčků šablon</span><span class="sxs-lookup"><span data-stu-id="2db59-139">Template package repository</span></span>

<span data-ttu-id="2db59-140">Pokud distribuujete pouze jednu šablonu projektu nebo položky a nepotřebujete zabalit více šablon dohromady, můžete použít jednodušší, ale omezený přístup, který obsahuje balíčky přímo v souboru ZIP šablony projektu nebo položky:</span><span class="sxs-lookup"><span data-stu-id="2db59-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="2db59-141">Upravte `<packages>` prvek v souboru následujícím `.vstemplate` způsobem:</span><span class="sxs-lookup"><span data-stu-id="2db59-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="2db59-142">`repository`Atribut má hodnotu `template` a `repositoryId` atribut není požadován.</span><span class="sxs-lookup"><span data-stu-id="2db59-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="2db59-143">Umístěte balíčky do kořenové složky souboru ZIP šablony projektu nebo položky.</span><span class="sxs-lookup"><span data-stu-id="2db59-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="2db59-144">Všimněte si, že použití tohoto přístupu v souboru VSIX, který obsahuje více šablon, vede k zbytečným dispozici determinističtějšíům, pokud je jeden nebo více balíčků běžné pro šablony.</span><span class="sxs-lookup"><span data-stu-id="2db59-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="2db59-145">V takových případech použijte [VSIX jako úložiště](#vsix-package-repository) , jak je popsáno v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="2db59-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="2db59-146">Cesta ke složce zadané v registru</span><span class="sxs-lookup"><span data-stu-id="2db59-146">Registry-specified folder path</span></span>

<span data-ttu-id="2db59-147">Sady SDK, které jsou nainstalované pomocí MSI, můžou instalovat balíčky NuGet přímo v počítači vývojáře.</span><span class="sxs-lookup"><span data-stu-id="2db59-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="2db59-148">Díky tomu jsou okamžitě k dispozici při použití šablony projektu nebo položky, nikoli při jejich extrakci během této doby.</span><span class="sxs-lookup"><span data-stu-id="2db59-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="2db59-149">Tento přístup používají šablony ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2db59-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="2db59-150">Instalační balíčky MSI nainstalujte do počítače.</span><span class="sxs-lookup"><span data-stu-id="2db59-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="2db59-151">Můžete instalovat pouze `.nupkg` soubory, nebo je můžete nainstalovat spolu s rozbaleným obsahem, který při použití šablony uloží další krok.</span><span class="sxs-lookup"><span data-stu-id="2db59-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="2db59-152">V takovém případě postupujte podle standardní struktury složek NuGet `.nupkg` , kde jsou soubory v kořenové složce, a pak každý balíček má jako název podsložky podsložku s identifikátorem ID/verze.</span><span class="sxs-lookup"><span data-stu-id="2db59-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="2db59-153">Zadejte klíč registru pro identifikaci umístění balíčku:</span><span class="sxs-lookup"><span data-stu-id="2db59-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="2db59-154">Umístění klíče: buď na úrovni počítače `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` , nebo pokud je to pro jednotlivé uživatele nainstalované šablony a balíčky, případně použít `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="2db59-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="2db59-155">Název klíče: použijte název, který je pro vás jedinečný.</span><span class="sxs-lookup"><span data-stu-id="2db59-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="2db59-156">Například šablony ASP.NET MVC 4 pro VS 2012 use `AspNetMvc4VS11` .</span><span class="sxs-lookup"><span data-stu-id="2db59-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="2db59-157">Hodnoty: úplná cesta ke složce Packages.</span><span class="sxs-lookup"><span data-stu-id="2db59-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="2db59-158">V `<packages>` elementu v `.vstemplate` souboru přidejte atribut `repository="registry"` a v atributu zadejte název klíče registru `keyName` .</span><span class="sxs-lookup"><span data-stu-id="2db59-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="2db59-159">Pokud máte předběžné rozbalení balíčků, použijte `isPreunzipped="true"` atribut.</span><span class="sxs-lookup"><span data-stu-id="2db59-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="2db59-160">*(NuGet 3.2 +)* Pokud chcete vynutit sestavení během návrhu na konci instalace balíčku, přidejte `forceDesignTimeBuild="true"` atribut.</span><span class="sxs-lookup"><span data-stu-id="2db59-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="2db59-161">Jako optimalizaci přidejte, `skipAssemblyReferences="true"` protože již vlastní šablona obsahuje nezbytné odkazy.</span><span class="sxs-lookup"><span data-stu-id="2db59-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="2db59-162">Osvědčené postupy</span><span class="sxs-lookup"><span data-stu-id="2db59-162">Best Practices</span></span>

1. <span data-ttu-id="2db59-163">Deklarace závislosti na VSIX NuGet přidáním odkazu do manifestu VSIX:</span><span class="sxs-lookup"><span data-stu-id="2db59-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="2db59-164">Vyžadovat, aby byly šablony projektů a položek uloženy při vytváření, včetně [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) v `.vstemplate` souboru.</span><span class="sxs-lookup"><span data-stu-id="2db59-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="2db59-165">Šablony neobsahují soubor a neobsahují `packages.config` ani žádné odkazy nebo obsah, které by se přidaly při instalaci balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="2db59-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
