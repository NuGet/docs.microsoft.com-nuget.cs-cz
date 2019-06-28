---
title: Odkaz na soubor souboru .nuspec pro NuGet
description: Souboru .nuspec soubor obsahuje metadata balíčků používat při vytváření balíčku a zadejte informace pro spotřebitele balíčku.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: e4c57c0580fe9018703291c08d60e559f95183dc
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426207"
---
# <a name="nuspec-reference"></a><span data-ttu-id="bf721-103">odkaz na souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="bf721-103">.nuspec reference</span></span>

<span data-ttu-id="bf721-104">A `.nuspec` je soubor manifestu XML, který obsahuje metadata balíčků.</span><span class="sxs-lookup"><span data-stu-id="bf721-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="bf721-105">Tento manifest slouží k vytvoření balíčku a zadejte informace pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="bf721-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="bf721-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="bf721-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="bf721-107">In this topic:</span></span>

- [<span data-ttu-id="bf721-108">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="bf721-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="bf721-109">[Nahrazení tokeny](#replacement-tokens) (při použití s projektu sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="bf721-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="bf721-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="bf721-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="bf721-111">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="bf721-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="bf721-112">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="bf721-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="bf721-113">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="bf721-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="bf721-114">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="bf721-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="bf721-115">Příklad souboru nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="bf721-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="bf721-116">Kompatibilita typů projektu</span><span class="sxs-lookup"><span data-stu-id="bf721-116">Project type compatibility</span></span>

- <span data-ttu-id="bf721-117">Použít `.nuspec` s `nuget.exe pack` bez SDK-style projekty, které používají `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="bf721-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="bf721-118">A `.nuspec` soubor není nezbytný k vytváření balíčků pro projekty založenými na sadě SDK (projekty .NET Core a .NET Standard, které používají [SDK atribut](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="bf721-118">A `.nuspec` file is not required to create packages for SDK-style projects (.NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="bf721-119">(Všimněte si, že `.nuspec` se vygeneruje, když vytvoříte balíček.)</span><span class="sxs-lookup"><span data-stu-id="bf721-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="bf721-120">Při vytváření balíčku pomocí `dotnet.exe pack` nebo `msbuild pack target`, doporučujeme vám [zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` místo souboru v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="bf721-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="bf721-121">Ale můžete místo toho nastavit [použít `.nuspec` souboru se zabalit pomocí `dotnet.exe` nebo `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="bf721-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="bf721-122">Pro projekty migrované z `packages.config` k [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` soubor není nezbytný k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="bf721-123">Místo toho použijte [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="bf721-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="bf721-124">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="bf721-124">General form and schema</span></span>

<span data-ttu-id="bf721-125">Aktuální `nuspec.xsd` soubor schématu najdete v [úložiště NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="bf721-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="bf721-126">V tomto schématu `.nuspec` soubor má následující Obecné formuláře:</span><span class="sxs-lookup"><span data-stu-id="bf721-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="bf721-127">Vizuální znázornění schématu, otevřete soubor schématu v sadě Visual Studio v režimu návrhu a klikněte **Průzkumníka schémat XML** odkaz.</span><span class="sxs-lookup"><span data-stu-id="bf721-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="bf721-128">Alternativně otevřete soubor jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **zobrazení Průzkumníka schémat XML**.</span><span class="sxs-lookup"><span data-stu-id="bf721-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="bf721-129">V obou případech, které získáte zobrazení jako na následující (v rozbaleném většinou):</span><span class="sxs-lookup"><span data-stu-id="bf721-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Průzkumníka schémat s nuspec.xsd otevřít](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="bf721-131">Prvky požadovaná metadata</span><span class="sxs-lookup"><span data-stu-id="bf721-131">Required metadata elements</span></span>

<span data-ttu-id="bf721-132">I když tyto prvky jsou minimální požadavky pro balíček, měli byste zvážit přidání [volitelná metadata prvky](#optional-metadata-elements) zlepšit celkové prostředí mají vývojáři součástí vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="bf721-133">Tyto prvky musí být uvedena v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="bf721-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="bf721-134">id</span><span class="sxs-lookup"><span data-stu-id="bf721-134">id</span></span> 
<span data-ttu-id="bf721-135">Identifikátor balíčku velká a malá písmena, která musí být jedinečný v rámci nuget.org nebo cokoli jiného balíčku se nachází v galerii.</span><span class="sxs-lookup"><span data-stu-id="bf721-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="bf721-136">ID nemůže obsahovat mezery nebo znaky, které nejsou platné pro adresu URL a obvykle postupují podle pravidla oboru názvů .NET.</span><span class="sxs-lookup"><span data-stu-id="bf721-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="bf721-137">Zobrazit [výběr balíčku jedinečný identifikátor](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) pokyny.</span><span class="sxs-lookup"><span data-stu-id="bf721-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="bf721-138">verze</span><span class="sxs-lookup"><span data-stu-id="bf721-138">version</span></span>
<span data-ttu-id="bf721-139">Verze balíčku, následující *hlavníverze.podverze.oprava* vzor.</span><span class="sxs-lookup"><span data-stu-id="bf721-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="bf721-140">Čísla verzí může obsahovat příponu předběžné verze, jak je popsáno v [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="bf721-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="bf721-141">description</span><span class="sxs-lookup"><span data-stu-id="bf721-141">description</span></span>
<span data-ttu-id="bf721-142">Dlouhý popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="bf721-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="bf721-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="bf721-143">authors</span></span>
<span data-ttu-id="bf721-144">Čárkou oddělený seznam autorů balíčků, odpovídající názvy profilů na nuget.org. Tyto jsou zobrazeny v galerii NuGet na nuget.org a slouží k křížový odkaz balíčky stejné autory.</span><span class="sxs-lookup"><span data-stu-id="bf721-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="bf721-145">Volitelná metadata elementy</span><span class="sxs-lookup"><span data-stu-id="bf721-145">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="bf721-146">název</span><span class="sxs-lookup"><span data-stu-id="bf721-146">title</span></span>
<span data-ttu-id="bf721-147">Lidské popisný název balíčku, obvykle používaných v uživatelském rozhraní na webech nuget.org a Správce balíčků v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf721-147">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="bf721-148">Pokud není zadán, použije se ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-148">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="bf721-149">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="bf721-149">owners</span></span>
<span data-ttu-id="bf721-150">Čárkou oddělený seznam Tvůrce balíčku pomocí názvy profilů na nuget.org. To je často seznamu stejné jako v `authors`a je ignorován při nahrávání balíčku do nuget.org. Zobrazit [vlastníky Správa balíčků na nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="bf721-150">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="bf721-151">projectUrl</span><span class="sxs-lookup"><span data-stu-id="bf721-151">projectUrl</span></span>
<span data-ttu-id="bf721-152">Adresa URL domovské stránky balíčku, často zobrazuje v uživatelském rozhraní nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bf721-152">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="bf721-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="bf721-153">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="bf721-154">licenseUrl je zastaralé.</span><span class="sxs-lookup"><span data-stu-id="bf721-154">licenseUrl is being deprecated.</span></span> <span data-ttu-id="bf721-155">Místo toho použijte licenci.</span><span class="sxs-lookup"><span data-stu-id="bf721-155">Use license instead.</span></span>

<span data-ttu-id="bf721-156">Adresa URL licence balíčku, často zobrazuje v uživatelském rozhraní nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bf721-156">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="license"></a><span data-ttu-id="bf721-157">Licence</span><span class="sxs-lookup"><span data-stu-id="bf721-157">license</span></span>
<span data-ttu-id="bf721-158">Výraz SPDX licence nebo cesta k souboru licencí v rámci balíčku, často zobrazuje v uživatelském rozhraní nuget.org. V případě, že licencujete balíčku v rámci běžných licence, jako je například BSD-2klauzule nebo MIT, použijte přidružený identifikátor SPDX licence.</span><span class="sxs-lookup"><span data-stu-id="bf721-158">An SPDX license expression or path to a license file within the package, often shown in UI displays as well as nuget.org. If you’re licensing the package under a common license such as BSD-2-Clause or MIT, use the associated SPDX license identifier.</span></span><br><span data-ttu-id="bf721-159">Příklad: `<license type="expression">MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="bf721-159">For example: `<license type="expression">MIT</license>`</span></span>

<span data-ttu-id="bf721-160">Tady je úplný seznam [SPDX licence identifikátory](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="bf721-160">Here is the complete list of [SPDX license identifiers](https://spdx.org/licenses/).</span></span> <span data-ttu-id="bf721-161">NuGet.org přijímá pouze OSI nebo licenci FSF schválení licence při použití výrazu typu.</span><span class="sxs-lookup"><span data-stu-id="bf721-161">NuGet.org accepts only OSI or FSF approved licenses when using license type expression.</span></span>

<span data-ttu-id="bf721-162">Pokud váš balíček je licencován několik běžných licence, můžete zadat složené licencí pomocí [SPDX výraz syntaxe verze 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="bf721-162">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span><br><span data-ttu-id="bf721-163">Příklad: `<license type="expression">BSD-2-Clause OR MIT</license>`</span><span class="sxs-lookup"><span data-stu-id="bf721-163">For example: `<license type="expression">BSD-2-Clause OR MIT</license>`</span></span>

<span data-ttu-id="bf721-164">Pokud používáte licenci, která ještě není přiřazený identifikátor SPDX, nebo vlastní licenci, můžete zabalit do souboru (pouze `.txt` nebo `.md`) s textem licence.</span><span class="sxs-lookup"><span data-stu-id="bf721-164">If you are using a license that hasn’t been assigned an SPDX identifier, or it is a custom license, you can package a file (only `.txt` or `.md`) with the license text.</span></span> <span data-ttu-id="bf721-165">Příklad:</span><span class="sxs-lookup"><span data-stu-id="bf721-165">For example:</span></span>
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="bf721-166">Ekvivalent MSBuild, podívejte se na [balení výrazu licence nebo licenční soubor](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="bf721-166">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="bf721-167">Syntaxe výrazů licence NuGet je popsaný dole v [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="bf721-167">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="bf721-168">iconUrl</span><span class="sxs-lookup"><span data-stu-id="bf721-168">iconUrl</span></span>
<span data-ttu-id="bf721-169">Adresa URL pro bitovou kopii 64 x 64 s průhlednost pozadí použít jako ikona pro balíček zobrazená v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="bf721-169">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="bf721-170">Ujistěte se, obsahuje tento element *přímá adresa URL obrázku* nikoli adresa URL webové stránky, který obsahuje bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="bf721-170">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="bf721-171">Například pokud chcete použít některou image z Githubu, použijte soubor raw, jako je adresa URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="bf721-171">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="bf721-172">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="bf721-172">requireLicenseAcceptance</span></span>
<span data-ttu-id="bf721-173">Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-173">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="bf721-174">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="bf721-174">developmentDependency</span></span>
<span data-ttu-id="bf721-175">*(2.8+)* Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="bf721-175">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="bf721-176">S PackageReference (NuGet 4.8 +) tento příznak také znamená, že vyloučí kompilace prostředků z kompilace.</span><span class="sxs-lookup"><span data-stu-id="bf721-176">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="bf721-177">Zobrazit [DevelopmentDependency podporu pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="bf721-177">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>
#### <a name="summary"></a><span data-ttu-id="bf721-178">souhrn</span><span class="sxs-lookup"><span data-stu-id="bf721-178">summary</span></span>
<span data-ttu-id="bf721-179">Krátký popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="bf721-179">A short description of the package for UI display.</span></span> <span data-ttu-id="bf721-180">Pokud tento parametr vynechán, zkrácená verze `description` se používá.</span><span class="sxs-lookup"><span data-stu-id="bf721-180">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="bf721-181">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="bf721-181">releaseNotes</span></span>
<span data-ttu-id="bf721-182">*(1.5+)* Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-182">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="bf721-183">Copyright</span><span class="sxs-lookup"><span data-stu-id="bf721-183">copyright</span></span>
<span data-ttu-id="bf721-184">*(1.5+)* Copyright podrobnosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-184">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="bf721-185">jazyk</span><span class="sxs-lookup"><span data-stu-id="bf721-185">language</span></span>
<span data-ttu-id="bf721-186">ID národního prostředí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="bf721-186">The locale ID for the package.</span></span> <span data-ttu-id="bf721-187">Zobrazit [vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="bf721-187">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="bf721-188">značky</span><span class="sxs-lookup"><span data-stu-id="bf721-188">tags</span></span>
<span data-ttu-id="bf721-189">Mezerami oddělený seznam značek a klíčových slov, které popisují balíček a podpora zjistitelnost balíčků prostřednictvím vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="bf721-189">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="bf721-190">možnost změny</span><span class="sxs-lookup"><span data-stu-id="bf721-190">serviceable</span></span> 
<span data-ttu-id="bf721-191">*(3.3+)* Pouze pro interní NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="bf721-191">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="bf721-192">úložiště</span><span class="sxs-lookup"><span data-stu-id="bf721-192">repository</span></span>
<span data-ttu-id="bf721-193">Metadata úložiště, skládající se z čtyři volitelné atributy: *typ* a *url* *(4.0 +)* , a *větev* a  *potvrzení* *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="bf721-193">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="bf721-194">Tyto atributy umožňují namapovat .nupkg do úložiště, který sestavilo, má potenciál, chcete-li získat podrobné jako jednotlivé větev nebo potvrzení změn, které sestaven balíček.</span><span class="sxs-lookup"><span data-stu-id="bf721-194">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="bf721-195">To by měl být veřejně dostupnou adresu url, který lze vyvolat přímo pomocí softwaru pro řízení verzí.</span><span class="sxs-lookup"><span data-stu-id="bf721-195">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="bf721-196">Neměl by být stránku html jako ten je určený pro počítače.</span><span class="sxs-lookup"><span data-stu-id="bf721-196">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="bf721-197">Pro odkazování na stránku projektu, použijte `projectUrl` pole, místo toho.</span><span class="sxs-lookup"><span data-stu-id="bf721-197">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="bf721-198">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="bf721-198">minClientVersion</span></span>
<span data-ttu-id="bf721-199">Určuje minimální verzi klienta NuGet, který můžete nainstalovat tento balíček, vynucuje nuget.exe a Správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf721-199">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="bf721-200">Používá se pokaždé, když se balíček závisí na konkrétních funkcí služby `.nuspec` souborů, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="bf721-200">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="bf721-201">Třeba balíček pomocí `developmentDependency` atribut by měl určovat "2.8" pro `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="bf721-201">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="bf721-202">Obdobně balíček pomocí `contentFiles` – element (viz další části) by měl nastavit `minClientVersion` na "3.3".</span><span class="sxs-lookup"><span data-stu-id="bf721-202">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="bf721-203">Upozorňujeme také, že klienti NuGet před 2.5 nedokáže rozpoznat tento příznak jsou *vždy* odmítnout instalace balíčku bez ohledu na to, co `minClientVersion` obsahuje.</span><span class="sxs-lookup"><span data-stu-id="bf721-203">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="bf721-204">Elementy v kolekci</span><span class="sxs-lookup"><span data-stu-id="bf721-204">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="bf721-205">packageTypes</span><span class="sxs-lookup"><span data-stu-id="bf721-205">packageTypes</span></span>
<span data-ttu-id="bf721-206">*(3.5 +)*  Kolekce nula nebo více `<packageType>` elementy typu balíčku Pokud než tradiční závislost balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-206">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="bf721-207">Každý packageType má atributy *název* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="bf721-207">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="bf721-208">Zobrazit [nastavení typ balíčku](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="bf721-208">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="bf721-209">závislosti</span><span class="sxs-lookup"><span data-stu-id="bf721-209">dependencies</span></span>
<span data-ttu-id="bf721-210">Kolekce nula nebo více `<dependency>` prvky určení závislostí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="bf721-210">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="bf721-211">Každá závislost má atributy *id*, *verze*, *zahrnují* (3.x+), a *vyloučit* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="bf721-211">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="bf721-212">Zobrazit [závislosti](#dependencies-element) níže.</span><span class="sxs-lookup"><span data-stu-id="bf721-212">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="bf721-213">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="bf721-213">frameworkAssemblies</span></span>
<span data-ttu-id="bf721-214">*(1.2 +)*  Kolekce nula nebo více `<frameworkAssembly>` prvků identifikace odkazy na sestavení rozhraní .NET Framework, které vyžaduje tento balíček, které zajišťuje, že jsou přidány odkazy na projekty využívající balíček.</span><span class="sxs-lookup"><span data-stu-id="bf721-214">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="bf721-215">Má každý frameworkAssembly *assemblyName* a *targetFramework* atributy.</span><span class="sxs-lookup"><span data-stu-id="bf721-215">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="bf721-216">Zobrazit [zadání framework sestavení odkazuje na globální mezipaměti](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="bf721-216">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="bf721-217">odkazy</span><span class="sxs-lookup"><span data-stu-id="bf721-217">references</span></span>
<span data-ttu-id="bf721-218">*(1.5 +)*  Kolekce nula nebo více `<reference>` prvky názvy sestavení v balíčku `lib` složku, která jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="bf721-218">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="bf721-219">Každý odkaz má *souboru* atribut.</span><span class="sxs-lookup"><span data-stu-id="bf721-219">Each reference has a *file* attribute.</span></span> <span data-ttu-id="bf721-220">`<references>` může také obsahovat `<group>` element s *targetFramework* atribut, pak obsahující `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="bf721-220">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="bf721-221">Pokud tento parametr vynechán, všechny odkazy v `lib` jsou zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="bf721-221">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="bf721-222">Zobrazit [odkazy na sestavení explicitní určení](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="bf721-222">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="bf721-223">contentFiles</span><span class="sxs-lookup"><span data-stu-id="bf721-223">contentFiles</span></span>
<span data-ttu-id="bf721-224">*(3.3 +)*  Kolekce `<files>` prvky, které identifikují soubory obsahu, které mají být zahrnuty náročné projektu.</span><span class="sxs-lookup"><span data-stu-id="bf721-224">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="bf721-225">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů.</span><span class="sxs-lookup"><span data-stu-id="bf721-225">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="bf721-226">Zobrazit [určující soubory, které chcete zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="bf721-226">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="bf721-227">soubory</span><span class="sxs-lookup"><span data-stu-id="bf721-227">files</span></span> 
<span data-ttu-id="bf721-228">`<package>` Uzel může obsahovat `<files>` uzel na stejné úrovni k `<metadata>`a `<contentFiles>` dítě `<metadata>`, určete, jaké soubory sestavení a obsah zahrnout do balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-228">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="bf721-229">Zobrazit [včetně souborů sestavení](#including-assembly-files) a [včetně soubory obsahu](#including-content-files) dále v tomto tématu podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="bf721-229">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="bf721-230">Nahrazování tokenů</span><span class="sxs-lookup"><span data-stu-id="bf721-230">Replacement tokens</span></span>

<span data-ttu-id="bf721-231">Při vytváření balíčku, [ `nuget pack` příkaz](../tools/cli-ref-pack.md) nahradí $oddělených tokenů v `.nuspec` souboru `<metadata>` uzlu s hodnotami, které pocházejí ze souboru projektu nebo `pack` příkazu `-properties`přepínat.</span><span class="sxs-lookup"><span data-stu-id="bf721-231">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="bf721-232">Na příkazovém řádku zadáte hodnoty tokenu s `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="bf721-232">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="bf721-233">Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a zadejte hodnoty v následujícím způsobem balení čas:</span><span class="sxs-lookup"><span data-stu-id="bf721-233">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="bf721-234">Chcete-li hodnoty z projektu, zadat tokenů popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` například `AssemblyInfo.cs` nebo `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="bf721-234">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="bf721-235">Pokud chcete použít tyto tokeny, spusťte `nuget pack` do souboru projektu namísto pouze `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="bf721-235">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="bf721-236">Například, když pomocí následujícího příkazu `$id$` a `$version$` tokeny v `.nuspec` souboru jsou nahrazeny projektu `AssemblyName` a `AssemblyVersion` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="bf721-236">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="bf721-237">Obvykle, když máte projekt, vytvoříte `.nuspec` zpočátku pomocí `nuget spec MyProject.csproj` což automaticky zahrnuje některé z těchto standardních tokenů.</span><span class="sxs-lookup"><span data-stu-id="bf721-237">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="bf721-238">Nicméně, pokud projekt neobsahuje hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` selže.</span><span class="sxs-lookup"><span data-stu-id="bf721-238">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="bf721-239">Navíc pokud můžete změnit hodnoty projektu, je nutné znovu sestavit před vytvořením balíčku. To můžete udělat jednoduše pomocí příkazu pack `build` přepnout.</span><span class="sxs-lookup"><span data-stu-id="bf721-239">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="bf721-240">S výjimkou produktů `$configuration$`, jsou hodnoty v projektu použít preferenci pro libovolné přiřazen stejný token v příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="bf721-240">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="bf721-241">Podpisový</span><span class="sxs-lookup"><span data-stu-id="bf721-241">Token</span></span> | <span data-ttu-id="bf721-242">Hodnota zdroje</span><span class="sxs-lookup"><span data-stu-id="bf721-242">Value source</span></span> | <span data-ttu-id="bf721-243">Hodnota</span><span class="sxs-lookup"><span data-stu-id="bf721-243">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="bf721-244">**$id$**</span><span class="sxs-lookup"><span data-stu-id="bf721-244">**$id$**</span></span> | <span data-ttu-id="bf721-245">soubor projektu</span><span class="sxs-lookup"><span data-stu-id="bf721-245">Project file</span></span> | <span data-ttu-id="bf721-246">AssemblyName (název) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="bf721-246">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="bf721-247">**$version$**</span><span class="sxs-lookup"><span data-stu-id="bf721-247">**$version$**</span></span> | <span data-ttu-id="bf721-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="bf721-248">AssemblyInfo</span></span> | <span data-ttu-id="bf721-249">AssemblyInformationalVersion, pokud jsou k dispozici, jinak AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="bf721-249">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="bf721-250">**$author$**</span><span class="sxs-lookup"><span data-stu-id="bf721-250">**$author$**</span></span> | <span data-ttu-id="bf721-251">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="bf721-251">AssemblyInfo</span></span> | <span data-ttu-id="bf721-252">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="bf721-252">AssemblyCompany</span></span> |
| <span data-ttu-id="bf721-253">**$title$**</span><span class="sxs-lookup"><span data-stu-id="bf721-253">**$title$**</span></span> | <span data-ttu-id="bf721-254">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="bf721-254">AssemblyInfo</span></span> | <span data-ttu-id="bf721-255">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="bf721-255">AssemblyTitle</span></span> |
| <span data-ttu-id="bf721-256">**$description$**</span><span class="sxs-lookup"><span data-stu-id="bf721-256">**$description$**</span></span> | <span data-ttu-id="bf721-257">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="bf721-257">AssemblyInfo</span></span> | <span data-ttu-id="bf721-258">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="bf721-258">AssemblyDescription</span></span> |
| <span data-ttu-id="bf721-259">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="bf721-259">**$copyright$**</span></span> | <span data-ttu-id="bf721-260">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="bf721-260">AssemblyInfo</span></span> | <span data-ttu-id="bf721-261">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="bf721-261">AssemblyCopyright</span></span> |
| <span data-ttu-id="bf721-262">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="bf721-262">**$configuration$**</span></span> | <span data-ttu-id="bf721-263">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="bf721-263">Assembly DLL</span></span> | <span data-ttu-id="bf721-264">Konfigurace použitý k vytvoření sestavení, jako výchozí se použije k ladění.</span><span class="sxs-lookup"><span data-stu-id="bf721-264">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="bf721-265">Všimněte si, že pokud chcete vytvořit balíček pomocí konfiguraci vydané verze, vždy používáte `-properties Configuration=Release` na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="bf721-265">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="bf721-266">Tokeny je také možné přeložit cesty, jakmile zahrnete [soubory sestavení](#including-assembly-files) a [obsah souborů](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="bf721-266">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="bf721-267">Tokeny mají stejné názvy jako vlastnosti nástroje MSBuild, což umožňuje vyberte soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="bf721-267">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="bf721-268">Například, pokud použijete následující klíčová slova v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="bf721-268">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="bf721-269">A vytvoření sestavení jehož `AssemblyName` je `LoggingLibrary` s `Release` konfigurace v nástroji MSBuild, výsledný vstupující `.nuspec` souborů v balíčku je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bf721-269">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="bf721-270">Dependencies – element</span><span class="sxs-lookup"><span data-stu-id="bf721-270">Dependencies element</span></span>

<span data-ttu-id="bf721-271">`<dependencies>` Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvky, které určují další balíčky, na kterých závisí balíček nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="bf721-271">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="bf721-272">Atributy pro každý `<dependency>` jsou následující:</span><span class="sxs-lookup"><span data-stu-id="bf721-272">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="bf721-273">Atribut</span><span class="sxs-lookup"><span data-stu-id="bf721-273">Attribute</span></span> | <span data-ttu-id="bf721-274">Popis</span><span class="sxs-lookup"><span data-stu-id="bf721-274">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="bf721-275">(Povinné) Ukazuje, na stránce balíček pro ID balíčku závislosti, jako je například "EntityFramework" a "NUnit", což je název balíčku nuget.org.</span><span class="sxs-lookup"><span data-stu-id="bf721-275">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="bf721-276">(Povinné) Rozsah verzí přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="bf721-276">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="bf721-277">Zobrazit [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) přesnou syntaxi.</span><span class="sxs-lookup"><span data-stu-id="bf721-277">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="bf721-278">include</span><span class="sxs-lookup"><span data-stu-id="bf721-278">include</span></span> | <span data-ttu-id="bf721-279">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti, které mají být zahrnuty do koncového balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-279">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="bf721-280">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="bf721-280">The default value is `all`.</span></span> |
| <span data-ttu-id="bf721-281">exclude</span><span class="sxs-lookup"><span data-stu-id="bf721-281">exclude</span></span> | <span data-ttu-id="bf721-282">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti pro vyloučení ve finálním balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-282">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="bf721-283">Výchozí hodnota je `build,analyzers` může být přepsání.</span><span class="sxs-lookup"><span data-stu-id="bf721-283">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="bf721-284">Ale `content/ ContentFiles` nevylučují se také implicitně ve finálním balíčku, který nelze přepsání.</span><span class="sxs-lookup"><span data-stu-id="bf721-284">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="bf721-285">Značky s `exclude` přednost zadaným `include`.</span><span class="sxs-lookup"><span data-stu-id="bf721-285">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="bf721-286">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="bf721-286">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="bf721-287">Zahrnutí a vyloučení značek</span><span class="sxs-lookup"><span data-stu-id="bf721-287">Include/Exclude tag</span></span> | <span data-ttu-id="bf721-288">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="bf721-288">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="bf721-289">contentFiles</span><span class="sxs-lookup"><span data-stu-id="bf721-289">contentFiles</span></span> | <span data-ttu-id="bf721-290">Obsah</span><span class="sxs-lookup"><span data-stu-id="bf721-290">Content</span></span> |
| <span data-ttu-id="bf721-291">modul runtime</span><span class="sxs-lookup"><span data-stu-id="bf721-291">runtime</span></span> | <span data-ttu-id="bf721-292">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="bf721-292">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="bf721-293">Kompilace</span><span class="sxs-lookup"><span data-stu-id="bf721-293">compile</span></span> | <span data-ttu-id="bf721-294">lib</span><span class="sxs-lookup"><span data-stu-id="bf721-294">lib</span></span> |
| <span data-ttu-id="bf721-295">sestavení</span><span class="sxs-lookup"><span data-stu-id="bf721-295">build</span></span> | <span data-ttu-id="bf721-296">sestavení (cíle a vlastnosti nástroje MSBuild)</span><span class="sxs-lookup"><span data-stu-id="bf721-296">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="bf721-297">nativní</span><span class="sxs-lookup"><span data-stu-id="bf721-297">native</span></span> | <span data-ttu-id="bf721-298">nativní</span><span class="sxs-lookup"><span data-stu-id="bf721-298">native</span></span> |
| <span data-ttu-id="bf721-299">žádná</span><span class="sxs-lookup"><span data-stu-id="bf721-299">none</span></span> | <span data-ttu-id="bf721-300">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="bf721-300">No folders</span></span> |
| <span data-ttu-id="bf721-301">všechny</span><span class="sxs-lookup"><span data-stu-id="bf721-301">all</span></span> | <span data-ttu-id="bf721-302">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="bf721-302">All folders</span></span> |

<span data-ttu-id="bf721-303">Například následující řádky signalizovat závislosti na `PackageA` verze 1.1.0 nebo vyšší, a `PackageB` verzi 1.x.</span><span class="sxs-lookup"><span data-stu-id="bf721-303">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="bf721-304">Následující řádky označují závislostí na stejné balíčky, ale zadané k vložení `contentFiles` a `build` složky `PackageA` a všechno, co ale `native` a `compile` složky `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="bf721-304">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="bf721-305">Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`, závislosti, které existují v tomto projektu jsou automaticky obsažené ve výsledné `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="bf721-305">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="bf721-306">Závislostí skupin</span><span class="sxs-lookup"><span data-stu-id="bf721-306">Dependency groups</span></span>

<span data-ttu-id="bf721-307">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="bf721-307">*Version 2.0+*</span></span>

<span data-ttu-id="bf721-308">Jako alternativu k jednomu seznamu bez stromové struktury, se dá nastavit závislosti podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="bf721-308">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="bf721-309">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<dependency>` elementy.</span><span class="sxs-lookup"><span data-stu-id="bf721-309">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="bf721-310">Tyto závislosti jsou nainstalovány společně, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="bf721-310">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="bf721-311">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="bf721-311">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="bf721-312">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="bf721-312">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="bf721-313">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="bf721-313">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="bf721-314">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="bf721-314">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="bf721-315">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="bf721-315">Explicit assembly references</span></span>

<span data-ttu-id="bf721-316">`<references>` Element je používán projektů s použitím `packages.config` explicitně zadejte sestavení, které by měly odkazovat na cílový projekt, při použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-316">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="bf721-317">Explicitní odkazy se obvykle používají pro pouze na sestavení doby návrhu.</span><span class="sxs-lookup"><span data-stu-id="bf721-317">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="bf721-318">Další informace naleznete na stránce na [výběr sestavení odkazovaných projektů](../create-packages/select-assemblies-referenced-by-projects.md) Další informace.</span><span class="sxs-lookup"><span data-stu-id="bf721-318">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="bf721-319">Například následující `<references>` element dává pokyn NuGet pro přidání odkazů na pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že existují další sestavení v balíčku:</span><span class="sxs-lookup"><span data-stu-id="bf721-319">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="bf721-320">Referenční skupiny</span><span class="sxs-lookup"><span data-stu-id="bf721-320">Reference groups</span></span>

<span data-ttu-id="bf721-321">Jako alternativu k jednomu plochého seznamu lze upravit odkazy podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<references>`.</span><span class="sxs-lookup"><span data-stu-id="bf721-321">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="bf721-322">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="bf721-322">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="bf721-323">Tyto odkazy jsou přidány do projektu, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="bf721-323">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="bf721-324">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznamu odkazů.</span><span class="sxs-lookup"><span data-stu-id="bf721-324">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="bf721-325">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="bf721-325">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="bf721-326">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="bf721-326">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="bf721-327">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="bf721-327">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="bf721-328">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="bf721-328">Framework assembly references</span></span>

<span data-ttu-id="bf721-329">Sestavení rozhraní jsou ty, které jsou součástí rozhraní .NET framework a by už měla být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač.</span><span class="sxs-lookup"><span data-stu-id="bf721-329">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="bf721-330">Určením těchto sestavení v rámci `<frameworkAssemblies>` elementu balíčku můžete zajistit, že požadované odkazy jsou přidány do projektu, v případě, že projekt již nemá tyto odkazy.</span><span class="sxs-lookup"><span data-stu-id="bf721-330">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="bf721-331">Takové sestavení, samozřejmě, nejsou obsažené v balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="bf721-331">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="bf721-332">`<frameworkAssemblies>` Prvek obsahuje nula nebo více `<frameworkAssembly>` prvky, z nichž každý určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="bf721-332">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="bf721-333">Atribut</span><span class="sxs-lookup"><span data-stu-id="bf721-333">Attribute</span></span> | <span data-ttu-id="bf721-334">Popis</span><span class="sxs-lookup"><span data-stu-id="bf721-334">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf721-335">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="bf721-335">**assemblyName**</span></span> | <span data-ttu-id="bf721-336">(Povinné) Plně kvalifikovaný název.</span><span class="sxs-lookup"><span data-stu-id="bf721-336">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="bf721-337">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="bf721-337">**targetFramework**</span></span> | <span data-ttu-id="bf721-338">(Volitelné) Určuje cílovou architekturu, pro který platí tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="bf721-338">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="bf721-339">Pokud tento parametr vynechán, označuje, že odkaz použije pro všechny platformy.</span><span class="sxs-lookup"><span data-stu-id="bf721-339">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="bf721-340">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="bf721-340">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="bf721-341">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové platformy a odkaz na `System.ServiceModel` pro pouze rozhraní .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="bf721-341">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="bf721-342">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="bf721-342">Including assembly files</span></span>

<span data-ttu-id="bf721-343">Pokud budete postupovat podle konvence je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md), není potřeba explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="bf721-343">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="bf721-344">`nuget pack` Příkaz automaticky převezme potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="bf721-344">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="bf721-345">Při instalaci do projektu balíček NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* ty, které jsou pojmenovány `.resources.dll` vzhledem k tomu, že se budou považovat za lokalizovaná satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="bf721-345">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="bf721-346">Z tohoto důvodu se vyhněte se použití `.resources.dll` pro soubory, které jinak obsahují základní balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="bf721-346">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="bf721-347">Toto automatické chování obejít a explicitně kontrolovat soubory, které jsou obsažené v balíčku, umístěte `<files>` jako podřízený element `<package>` (a na stejné úrovni `<metadata>`), identifikuje každý soubor se samostatným `<file>` element.</span><span class="sxs-lookup"><span data-stu-id="bf721-347">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="bf721-348">Příklad:</span><span class="sxs-lookup"><span data-stu-id="bf721-348">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="bf721-349">Nuget 2.x a dřívějších verzí a projekty pomocí `packages.config`, `<files>` element slouží také k neměnné obsahu soubory k zahrnutí při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="bf721-349">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="bf721-350">S NuGet 3.3 + i na PackageReference `<contentFiles>` elementu je použita.</span><span class="sxs-lookup"><span data-stu-id="bf721-350">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="bf721-351">Zobrazit [včetně soubory obsahu](#including-content-files) níže podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="bf721-351">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="bf721-352">Atributy souboru</span><span class="sxs-lookup"><span data-stu-id="bf721-352">File element attributes</span></span>

<span data-ttu-id="bf721-353">Každý `<file>` prvek určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="bf721-353">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="bf721-354">Atribut</span><span class="sxs-lookup"><span data-stu-id="bf721-354">Attribute</span></span> | <span data-ttu-id="bf721-355">Popis</span><span class="sxs-lookup"><span data-stu-id="bf721-355">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf721-356">**src**</span><span class="sxs-lookup"><span data-stu-id="bf721-356">**src**</span></span> | <span data-ttu-id="bf721-357">Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="bf721-357">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="bf721-358">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="bf721-358">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="bf721-359">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="bf721-359">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="bf721-360">**target**</span><span class="sxs-lookup"><span data-stu-id="bf721-360">**target**</span></span> | <span data-ttu-id="bf721-361">Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které musí začínat `lib`, `content`, `build`, nebo `tools`.</span><span class="sxs-lookup"><span data-stu-id="bf721-361">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="bf721-362">Zobrazit [vytváření souboru .nuspec z pracovního adresáře podle úmluvy](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="bf721-362">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="bf721-363">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="bf721-363">**exclude**</span></span> | <span data-ttu-id="bf721-364">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="bf721-364">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="bf721-365">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="bf721-365">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="bf721-366">Příklady</span><span class="sxs-lookup"><span data-stu-id="bf721-366">Examples</span></span>

<span data-ttu-id="bf721-367">**Jediné sestavení**</span><span class="sxs-lookup"><span data-stu-id="bf721-367">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="bf721-368">**Jediné sestavení specifická pro rozhraní .NET framework**</span><span class="sxs-lookup"><span data-stu-id="bf721-368">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="bf721-369">**Sada knihovny DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="bf721-369">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="bf721-370">**Knihovny DLL pro různá rozhraní**</span><span class="sxs-lookup"><span data-stu-id="bf721-370">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="bf721-371">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="bf721-371">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="bf721-372">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="bf721-372">Including content files</span></span>

<span data-ttu-id="bf721-373">Soubory obsahu jsou neměnné soubory, které je potřeba zahrnout do projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="bf721-373">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="bf721-374">Je neměnný, nejsou určeny k používání projektu změnit.</span><span class="sxs-lookup"><span data-stu-id="bf721-374">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="bf721-375">Příklad obsahu souborů patří:</span><span class="sxs-lookup"><span data-stu-id="bf721-375">Example content files include:</span></span>

- <span data-ttu-id="bf721-376">Bitové kopie, které jsou vloženy jako prostředky</span><span class="sxs-lookup"><span data-stu-id="bf721-376">Images that are embedded as resources</span></span>
- <span data-ttu-id="bf721-377">Zdrojové soubory, které jsou již kompilován</span><span class="sxs-lookup"><span data-stu-id="bf721-377">Source files that are already compiled</span></span>
- <span data-ttu-id="bf721-378">Skripty, které musí být součástí výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="bf721-378">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="bf721-379">Konfigurační soubory pro balíček, který mají být zahrnuti do projektu, ale není třeba žádné změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="bf721-379">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="bf721-380">Obsahu souborů jsou součástí balíčku pomocí `<files>` elementu, určení `content` složky `target` atribut.</span><span class="sxs-lookup"><span data-stu-id="bf721-380">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="bf721-381">Ale tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který používá místo toho `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="bf721-381">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="bf721-382">Balíček pro maximální kompatibility s využívání projektů v ideálním případě Určuje soubory obsahu v obou elementech.</span><span class="sxs-lookup"><span data-stu-id="bf721-382">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="bf721-383">Pomocí elementu souborů pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="bf721-383">Using the files element for content files</span></span>

<span data-ttu-id="bf721-384">Pro soubory obsahu, stačí použít stejný formát jako soubory sestavení, ale zadat `content` jako základní složka v `target` atributu, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="bf721-384">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="bf721-385">**Soubory základního obsahu**</span><span class="sxs-lookup"><span data-stu-id="bf721-385">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="bf721-386">**Soubory obsahu s adresářovou strukturu**</span><span class="sxs-lookup"><span data-stu-id="bf721-386">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="bf721-387">**Soubor s obsahem specifické pro cílové prostředí**</span><span class="sxs-lookup"><span data-stu-id="bf721-387">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="bf721-388">**Zkopírovat do složky s tečkou v názvu souboru obsahu**</span><span class="sxs-lookup"><span data-stu-id="bf721-388">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="bf721-389">V takovém případě se zobrazí NuGet, který rozšíření v `target` se neshoduje s příponou v `src` a proto zpracovává tuto část názvu v `target` jako složka:</span><span class="sxs-lookup"><span data-stu-id="bf721-389">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="bf721-390">**Soubory obsahu bez přípony**</span><span class="sxs-lookup"><span data-stu-id="bf721-390">**Content files without extensions**</span></span>

<span data-ttu-id="bf721-391">Chcete-li zahrnout soubory bez přípony, použijte `*` nebo `**` zástupné znaky:</span><span class="sxs-lookup"><span data-stu-id="bf721-391">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="bf721-392">**Soubory obsahu se hloubkové cesty a hloubkové cílem**</span><span class="sxs-lookup"><span data-stu-id="bf721-392">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="bf721-393">V takovém případě protože přípony zdrojovou a cílovou odpovídají, NuGet předpokládá, že cíl je název souboru a nikoliv složka:</span><span class="sxs-lookup"><span data-stu-id="bf721-393">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="bf721-394">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="bf721-394">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="bf721-395">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="bf721-395">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="bf721-396">Pomocí elementu contentFiles pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="bf721-396">Using the contentFiles element for content files</span></span>

<span data-ttu-id="bf721-397">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="bf721-397">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="bf721-398">Ve výchozím nastavení, umístí balíček obsahu `contentFiles` složky (viz níže) a `nuget pack` zahrnuty všechny soubory ve složce pomocí výchozí atributy.</span><span class="sxs-lookup"><span data-stu-id="bf721-398">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="bf721-399">V tomto případě není nutné zahrnout `contentFiles` uzlu `.nuspec` vůbec.</span><span class="sxs-lookup"><span data-stu-id="bf721-399">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="bf721-400">K řízení souborů, které jsou zahrnuty `<contentFiles>` prvek určuje je kolekce `<files>` mezi prvky, které identifikují přesné soubory patří.</span><span class="sxs-lookup"><span data-stu-id="bf721-400">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="bf721-401">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů:</span><span class="sxs-lookup"><span data-stu-id="bf721-401">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="bf721-402">Atribut</span><span class="sxs-lookup"><span data-stu-id="bf721-402">Attribute</span></span> | <span data-ttu-id="bf721-403">Popis</span><span class="sxs-lookup"><span data-stu-id="bf721-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf721-404">**include**</span><span class="sxs-lookup"><span data-stu-id="bf721-404">**include**</span></span> | <span data-ttu-id="bf721-405">(Povinné) Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="bf721-405">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="bf721-406">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="bf721-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="bf721-407">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="bf721-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="bf721-408">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="bf721-408">**exclude**</span></span> | <span data-ttu-id="bf721-409">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="bf721-409">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="bf721-410">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="bf721-410">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="bf721-411">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="bf721-411">**buildAction**</span></span> | <span data-ttu-id="bf721-412">Akce sestavení zařadit do obsahu položky nástroje MSBuild, jako například `Content`, `None`, `Embedded Resource`, `Compile`atd. Výchozí hodnota je `Compile`.</span><span class="sxs-lookup"><span data-stu-id="bf721-412">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="bf721-413">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="bf721-413">**copyToOutput**</span></span> | <span data-ttu-id="bf721-414">Logická hodnota označující, jestli se má kopírovat položky obsahu pro sestavení (nebo publikovat) výstupní složka.</span><span class="sxs-lookup"><span data-stu-id="bf721-414">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="bf721-415">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="bf721-415">The default is false.</span></span> |
| <span data-ttu-id="bf721-416">**Sloučit**</span><span class="sxs-lookup"><span data-stu-id="bf721-416">**flatten**</span></span> | <span data-ttu-id="bf721-417">Logická hodnota označující, zda se můžete kopírovat položky obsahu na jedinou složku ve výstupu sestavení (pravda), nebo zachovat strukturu složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="bf721-417">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="bf721-418">Tento příznak funguje pouze v případě copyToOutput příznak je nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="bf721-418">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="bf721-419">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="bf721-419">The default is false.</span></span> |

<span data-ttu-id="bf721-420">Při instalaci balíčku NuGet platí podřízených elementů `<contentFiles>` shora dolů.</span><span class="sxs-lookup"><span data-stu-id="bf721-420">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="bf721-421">Pokud se shodují na stejný soubor několik záznamů se použijí všechny položky.</span><span class="sxs-lookup"><span data-stu-id="bf721-421">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="bf721-422">Položky navrchu přepíše nižší položky dojde ke konfliktu pro stejný atribut.</span><span class="sxs-lookup"><span data-stu-id="bf721-422">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="bf721-423">Struktura složky balíčku</span><span class="sxs-lookup"><span data-stu-id="bf721-423">Package folder structure</span></span>

<span data-ttu-id="bf721-424">Projekt balíčku strukturovat obsahu pomocí následujícímu vzoru:</span><span class="sxs-lookup"><span data-stu-id="bf721-424">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="bf721-425">`codeLanguages` může být `cs`, `vb`, `fs`, `any`, nebo malým ekvivalentem znaku danou `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="bf721-425">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="bf721-426">`TxM` je všechny moniker právní cílového rozhraní, která podporuje NuGet (viz [platforem](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="bf721-426">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="bf721-427">Složky libovolné struktury složek může připojen na konec této syntaxe.</span><span class="sxs-lookup"><span data-stu-id="bf721-427">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="bf721-428">Příklad:</span><span class="sxs-lookup"><span data-stu-id="bf721-428">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="bf721-429">Můžete použít prázdné složky `.` chcete vyjádřit výslovný nesouhlas poskytnutí obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="bf721-429">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="bf721-430">Vzorový oddíl contentFiles</span><span class="sxs-lookup"><span data-stu-id="bf721-430">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="bf721-431">Příklad souboru nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="bf721-431">Example nuspec files</span></span>

<span data-ttu-id="bf721-432">**Jednoduchý `.nuspec` , která neurčuje závislosti nebo souborů**</span><span class="sxs-lookup"><span data-stu-id="bf721-432">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="bf721-433">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="bf721-433">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="bf721-434">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="bf721-434">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="bf721-435">**A `.nuspec` se sestaveními rozhraní framework**</span><span class="sxs-lookup"><span data-stu-id="bf721-435">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="bf721-436">V tomto příkladu tímto se nainstalují pro konkrétní projekt cílí:</span><span class="sxs-lookup"><span data-stu-id="bf721-436">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="bf721-437">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="bf721-437">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="bf721-438">. NET4 -> Client Profile `System.Net`</span><span class="sxs-lookup"><span data-stu-id="bf721-438">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="bf721-439">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="bf721-439">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="bf721-440">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="bf721-440">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
