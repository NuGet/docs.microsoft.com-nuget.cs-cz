---
title: Odkaz na soubor souboru .nuspec pro NuGet
description: Souboru .nuspec soubor obsahuje metadata balíčků používat při vytváření balíčku a zadejte informace pro spotřebitele balíčku.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: fd6ecab05a392a2a0b4ddf1ac15eb108f2653703
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842402"
---
# <a name="nuspec-reference"></a><span data-ttu-id="52ad5-103">odkaz na souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="52ad5-103">.nuspec reference</span></span>

<span data-ttu-id="52ad5-104">A `.nuspec` je soubor manifestu XML, který obsahuje metadata balíčků.</span><span class="sxs-lookup"><span data-stu-id="52ad5-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="52ad5-105">Tento manifest slouží k vytvoření balíčku a zadejte informace pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="52ad5-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="52ad5-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="52ad5-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="52ad5-107">In this topic:</span></span>

- [<span data-ttu-id="52ad5-108">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="52ad5-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="52ad5-109">[Nahrazení tokeny](#replacement-tokens) (při použití s projektu sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="52ad5-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="52ad5-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="52ad5-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="52ad5-111">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="52ad5-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="52ad5-112">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="52ad5-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="52ad5-113">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="52ad5-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="52ad5-114">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="52ad5-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="52ad5-115">Příklad souboru nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="52ad5-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="52ad5-116">Kompatibilita typů projektu</span><span class="sxs-lookup"><span data-stu-id="52ad5-116">Project type compatibility</span></span>

- <span data-ttu-id="52ad5-117">Použít `.nuspec` s `nuget.exe pack` bez SDK-style projekty, které používají `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="52ad5-118">A `.nuspec` souboru není nutné k vytváření balíčků pro [projekty založenými na sadě SDK](../resources/check-project-format.md) (obvykle projekty .NET Core a .NET Standard, které používají [SDK atribut](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="52ad5-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="52ad5-119">(Všimněte si, že `.nuspec` se vygeneruje, když vytvoříte balíček.)</span><span class="sxs-lookup"><span data-stu-id="52ad5-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="52ad5-120">Při vytváření balíčku pomocí `dotnet.exe pack` nebo `msbuild pack target`, doporučujeme vám [zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` místo souboru v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="52ad5-121">Ale můžete místo toho nastavit [použít `.nuspec` souboru se zabalit pomocí `dotnet.exe` nebo `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="52ad5-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="52ad5-122">Pro projekty migrované z `packages.config` k [PackageReference](../consume-packages/package-references-in-project-files.md), `.nuspec` soubor není nezbytný k vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="52ad5-123">Místo toho použijte [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="52ad5-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="52ad5-124">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="52ad5-124">General form and schema</span></span>

<span data-ttu-id="52ad5-125">Aktuální `nuspec.xsd` soubor schématu najdete v [úložiště NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="52ad5-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="52ad5-126">V tomto schématu `.nuspec` soubor má následující Obecné formuláře:</span><span class="sxs-lookup"><span data-stu-id="52ad5-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="52ad5-127">Vizuální znázornění schématu, otevřete soubor schématu v sadě Visual Studio v režimu návrhu a klikněte **Průzkumníka schémat XML** odkaz.</span><span class="sxs-lookup"><span data-stu-id="52ad5-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="52ad5-128">Alternativně otevřete soubor jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **zobrazení Průzkumníka schémat XML**.</span><span class="sxs-lookup"><span data-stu-id="52ad5-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="52ad5-129">V obou případech, které získáte zobrazení jako na následující (v rozbaleném většinou):</span><span class="sxs-lookup"><span data-stu-id="52ad5-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Průzkumníka schémat s nuspec.xsd otevřít](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="52ad5-131">Prvky požadovaná metadata</span><span class="sxs-lookup"><span data-stu-id="52ad5-131">Required metadata elements</span></span>

<span data-ttu-id="52ad5-132">I když tyto prvky jsou minimální požadavky pro balíček, měli byste zvážit přidání [volitelná metadata prvky](#optional-metadata-elements) zlepšit celkové prostředí mají vývojáři součástí vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="52ad5-133">Tyto prvky musí být uvedena v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="52ad5-134">id</span><span class="sxs-lookup"><span data-stu-id="52ad5-134">id</span></span> 
<span data-ttu-id="52ad5-135">Identifikátor balíčku velká a malá písmena, která musí být jedinečný v rámci nuget.org nebo cokoli jiného balíčku se nachází v galerii.</span><span class="sxs-lookup"><span data-stu-id="52ad5-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="52ad5-136">ID nemůže obsahovat mezery nebo znaky, které nejsou platné pro adresu URL a obvykle postupují podle pravidla oboru názvů .NET.</span><span class="sxs-lookup"><span data-stu-id="52ad5-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="52ad5-137">Zobrazit [výběr balíčku jedinečný identifikátor](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) pokyny.</span><span class="sxs-lookup"><span data-stu-id="52ad5-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="52ad5-138">verze</span><span class="sxs-lookup"><span data-stu-id="52ad5-138">version</span></span>
<span data-ttu-id="52ad5-139">Verze balíčku, následující *hlavníverze.podverze.oprava* vzor.</span><span class="sxs-lookup"><span data-stu-id="52ad5-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="52ad5-140">Čísla verzí může obsahovat příponu předběžné verze, jak je popsáno v [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="52ad5-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="52ad5-141">description</span><span class="sxs-lookup"><span data-stu-id="52ad5-141">description</span></span>
<span data-ttu-id="52ad5-142">Dlouhý popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="52ad5-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="52ad5-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="52ad5-143">authors</span></span>
<span data-ttu-id="52ad5-144">Čárkou oddělený seznam autorů balíčků, odpovídající názvy profilů na nuget.org. Tyto jsou zobrazeny v galerii NuGet na nuget.org a slouží k křížový odkaz balíčky stejné autory.</span><span class="sxs-lookup"><span data-stu-id="52ad5-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="52ad5-145">Volitelná metadata elementy</span><span class="sxs-lookup"><span data-stu-id="52ad5-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="52ad5-146">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="52ad5-146">owners</span></span>
<span data-ttu-id="52ad5-147">Čárkou oddělený seznam Tvůrce balíčku pomocí názvy profilů na nuget.org. To je často seznamu stejné jako v `authors`a je ignorován při nahrávání balíčku do nuget.org. Zobrazit [vlastníky Správa balíčků na nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="52ad5-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="52ad5-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="52ad5-148">projectUrl</span></span>
<span data-ttu-id="52ad5-149">Adresa URL domovské stránky balíčku, často zobrazuje v uživatelském rozhraní nuget.org.</span><span class="sxs-lookup"><span data-stu-id="52ad5-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="52ad5-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="52ad5-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="52ad5-151">licenseUrl je zastaralé.</span><span class="sxs-lookup"><span data-stu-id="52ad5-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="52ad5-152">Místo toho použijte licenci.</span><span class="sxs-lookup"><span data-stu-id="52ad5-152">Use license instead.</span></span>

<span data-ttu-id="52ad5-153">Adresa URL licence balíčku, často zobrazuje v uživatelská rozhraní, jako je nuget.org.</span><span class="sxs-lookup"><span data-stu-id="52ad5-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="52ad5-154">Licence</span><span class="sxs-lookup"><span data-stu-id="52ad5-154">license</span></span>
<span data-ttu-id="52ad5-155">Výraz SPDX licence nebo cesta k souboru licencí v rámci balíčku, často zobrazuje v uživatelská rozhraní, jako je nuget.org. V případě, že licencujete balíčku v rámci běžných licence, jako je MIT nebo BSD 2 klauzule, použijte přidruženého [SPDX licence identifikátor](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="52ad5-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="52ad5-156">Příklad:</span><span class="sxs-lookup"><span data-stu-id="52ad5-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="52ad5-157">NuGet.org přijímá pouze výrazy licence, které schválí Open Source iniciativa nebo Bezplatný Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="52ad5-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="52ad5-158">Pokud váš balíček je licencován několik běžných licence, můžete zadat složené licencí pomocí [SPDX výraz syntaxe verze 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="52ad5-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="52ad5-159">Příklad:</span><span class="sxs-lookup"><span data-stu-id="52ad5-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="52ad5-160">Pokud používáte vlastní licenci, která nepodporuje výrazy licence, můžete zabalit `.txt` nebo `.md` soubor s textem licence.</span><span class="sxs-lookup"><span data-stu-id="52ad5-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="52ad5-161">Příklad:</span><span class="sxs-lookup"><span data-stu-id="52ad5-161">For example:</span></span>

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

<span data-ttu-id="52ad5-162">Ekvivalent MSBuild, podívejte se na [balení výrazu licence nebo licenční soubor](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="52ad5-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="52ad5-163">Syntaxe výrazů licence NuGet je popsaný dole v [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="52ad5-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="52ad5-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="52ad5-164">iconUrl</span></span>
<span data-ttu-id="52ad5-165">Adresa URL pro bitovou kopii 64 x 64 s průhlednost pozadí použít jako ikona pro balíček zobrazená v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="52ad5-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="52ad5-166">Ujistěte se, obsahuje tento element *přímá adresa URL obrázku* nikoli adresa URL webové stránky, který obsahuje bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="52ad5-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="52ad5-167">Například pokud chcete použít některou image z Githubu, použijte soubor raw, jako je adresa URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="52ad5-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="52ad5-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="52ad5-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="52ad5-169">Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="52ad5-170">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="52ad5-170">developmentDependency</span></span>
<span data-ttu-id="52ad5-171">*(2.8+)* Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="52ad5-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="52ad5-172">S PackageReference (NuGet 4.8 +) tento příznak také znamená, že vyloučí kompilace prostředků z kompilace.</span><span class="sxs-lookup"><span data-stu-id="52ad5-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="52ad5-173">Zobrazit [DevelopmentDependency podporu pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="52ad5-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="52ad5-174">souhrn</span><span class="sxs-lookup"><span data-stu-id="52ad5-174">summary</span></span>
<span data-ttu-id="52ad5-175">Krátký popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="52ad5-175">A short description of the package for UI display.</span></span> <span data-ttu-id="52ad5-176">Pokud tento parametr vynechán, zkrácená verze `description` se používá.</span><span class="sxs-lookup"><span data-stu-id="52ad5-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="52ad5-177">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="52ad5-177">releaseNotes</span></span>
<span data-ttu-id="52ad5-178">*(1.5+)* Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="52ad5-179">Copyright</span><span class="sxs-lookup"><span data-stu-id="52ad5-179">copyright</span></span>
<span data-ttu-id="52ad5-180">*(1.5+)* Copyright podrobnosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="52ad5-181">jazyk</span><span class="sxs-lookup"><span data-stu-id="52ad5-181">language</span></span>
<span data-ttu-id="52ad5-182">ID národního prostředí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="52ad5-182">The locale ID for the package.</span></span> <span data-ttu-id="52ad5-183">Zobrazit [vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="52ad5-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="52ad5-184">značky</span><span class="sxs-lookup"><span data-stu-id="52ad5-184">tags</span></span>
<span data-ttu-id="52ad5-185">Mezerami oddělený seznam značek a klíčových slov, které popisují balíček a podpora zjistitelnost balíčků prostřednictvím vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="52ad5-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="52ad5-186">možnost změny</span><span class="sxs-lookup"><span data-stu-id="52ad5-186">serviceable</span></span> 
<span data-ttu-id="52ad5-187">*(3.3+)* Pouze pro interní NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="52ad5-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="52ad5-188">úložiště</span><span class="sxs-lookup"><span data-stu-id="52ad5-188">repository</span></span>
<span data-ttu-id="52ad5-189">Metadata úložiště, skládající se z čtyři volitelné atributy: *typ* a *url* *(4.0 +)* , a *větev* a  *potvrzení* *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="52ad5-189">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="52ad5-190">Tyto atributy umožňují namapovat .nupkg do úložiště, který sestavilo, má potenciál, chcete-li získat podrobné jako jednotlivé větev nebo potvrzení změn, které sestaven balíček.</span><span class="sxs-lookup"><span data-stu-id="52ad5-190">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="52ad5-191">To by měl být veřejně dostupnou adresu url, který lze vyvolat přímo pomocí softwaru pro řízení verzí.</span><span class="sxs-lookup"><span data-stu-id="52ad5-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="52ad5-192">Neměl by být stránku html jako ten je určený pro počítače.</span><span class="sxs-lookup"><span data-stu-id="52ad5-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="52ad5-193">Pro odkazování na stránku projektu, použijte `projectUrl` pole, místo toho.</span><span class="sxs-lookup"><span data-stu-id="52ad5-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="52ad5-194">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="52ad5-194">minClientVersion</span></span>
<span data-ttu-id="52ad5-195">Určuje minimální verzi klienta NuGet, který můžete nainstalovat tento balíček, vynucuje nuget.exe a Správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52ad5-195">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="52ad5-196">Používá se pokaždé, když se balíček závisí na konkrétních funkcí služby `.nuspec` souborů, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="52ad5-196">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="52ad5-197">Třeba balíček pomocí `developmentDependency` atribut by měl určovat "2.8" pro `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-197">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="52ad5-198">Obdobně balíček pomocí `contentFiles` – element (viz další části) by měl nastavit `minClientVersion` na "3.3".</span><span class="sxs-lookup"><span data-stu-id="52ad5-198">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="52ad5-199">Upozorňujeme také, že klienti NuGet před 2.5 nedokáže rozpoznat tento příznak jsou *vždy* odmítnout instalace balíčku bez ohledu na to, co `minClientVersion` obsahuje.</span><span class="sxs-lookup"><span data-stu-id="52ad5-199">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="title"></a><span data-ttu-id="52ad5-200">název</span><span class="sxs-lookup"><span data-stu-id="52ad5-200">title</span></span>
<span data-ttu-id="52ad5-201">Zobrazí lidských popisný název balíčku, který může být použit v některých uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="52ad5-201">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="52ad5-202">(nuget.org a Správce balíčků v sadě Visual Studio nezobrazovat nadpis)</span><span class="sxs-lookup"><span data-stu-id="52ad5-202">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="52ad5-203">Elementy v kolekci</span><span class="sxs-lookup"><span data-stu-id="52ad5-203">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="52ad5-204">packageTypes</span><span class="sxs-lookup"><span data-stu-id="52ad5-204">packageTypes</span></span>
<span data-ttu-id="52ad5-205">*(3.5 +)*  Kolekce nula nebo více `<packageType>` elementy typu balíčku Pokud než tradiční závislost balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-205">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="52ad5-206">Každý packageType má atributy *název* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="52ad5-206">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="52ad5-207">Zobrazit [nastavení typ balíčku](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="52ad5-207">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="52ad5-208">závislosti</span><span class="sxs-lookup"><span data-stu-id="52ad5-208">dependencies</span></span>
<span data-ttu-id="52ad5-209">Kolekce nula nebo více `<dependency>` prvky určení závislostí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="52ad5-209">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="52ad5-210">Každá závislost má atributy *id*, *verze*, *zahrnují* (3.x+), a *vyloučit* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="52ad5-210">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="52ad5-211">Zobrazit [závislosti](#dependencies-element) níže.</span><span class="sxs-lookup"><span data-stu-id="52ad5-211">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="52ad5-212">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="52ad5-212">frameworkAssemblies</span></span>
<span data-ttu-id="52ad5-213">*(1.2 +)*  Kolekce nula nebo více `<frameworkAssembly>` prvků identifikace odkazy na sestavení rozhraní .NET Framework, které vyžaduje tento balíček, které zajišťuje, že jsou přidány odkazy na projekty využívající balíček.</span><span class="sxs-lookup"><span data-stu-id="52ad5-213">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="52ad5-214">Má každý frameworkAssembly *assemblyName* a *targetFramework* atributy.</span><span class="sxs-lookup"><span data-stu-id="52ad5-214">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="52ad5-215">Zobrazit [zadání framework sestavení odkazuje na globální mezipaměti](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="52ad5-215">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="52ad5-216">odkazy</span><span class="sxs-lookup"><span data-stu-id="52ad5-216">references</span></span>
<span data-ttu-id="52ad5-217">*(1.5 +)*  Kolekce nula nebo více `<reference>` prvky názvy sestavení v balíčku `lib` složku, která jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="52ad5-217">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="52ad5-218">Každý odkaz má *souboru* atribut.</span><span class="sxs-lookup"><span data-stu-id="52ad5-218">Each reference has a *file* attribute.</span></span> <span data-ttu-id="52ad5-219">`<references>` může také obsahovat `<group>` element s *targetFramework* atribut, pak obsahující `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="52ad5-219">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="52ad5-220">Pokud tento parametr vynechán, všechny odkazy v `lib` jsou zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="52ad5-220">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="52ad5-221">Zobrazit [odkazy na sestavení explicitní určení](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="52ad5-221">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="52ad5-222">contentFiles</span><span class="sxs-lookup"><span data-stu-id="52ad5-222">contentFiles</span></span>
<span data-ttu-id="52ad5-223">*(3.3 +)*  Kolekce `<files>` prvky, které identifikují soubory obsahu, které mají být zahrnuty náročné projektu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-223">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="52ad5-224">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů.</span><span class="sxs-lookup"><span data-stu-id="52ad5-224">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="52ad5-225">Zobrazit [určující soubory, které chcete zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="52ad5-225">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="52ad5-226">soubory</span><span class="sxs-lookup"><span data-stu-id="52ad5-226">files</span></span> 
<span data-ttu-id="52ad5-227">`<package>` Uzel může obsahovat `<files>` uzel na stejné úrovni k `<metadata>`a `<contentFiles>` dítě `<metadata>`, určete, jaké soubory sestavení a obsah zahrnout do balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-227">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="52ad5-228">Zobrazit [včetně souborů sestavení](#including-assembly-files) a [včetně soubory obsahu](#including-content-files) dále v tomto tématu podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="52ad5-228">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="52ad5-229">Nahrazování tokenů</span><span class="sxs-lookup"><span data-stu-id="52ad5-229">Replacement tokens</span></span>

<span data-ttu-id="52ad5-230">Při vytváření balíčku, [ `nuget pack` příkaz](../tools/cli-ref-pack.md) nahradí $oddělených tokenů v `.nuspec` souboru `<metadata>` uzlu s hodnotami, které pocházejí ze souboru projektu nebo `pack` příkazu `-properties`přepínat.</span><span class="sxs-lookup"><span data-stu-id="52ad5-230">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="52ad5-231">Na příkazovém řádku zadáte hodnoty tokenu s `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-231">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="52ad5-232">Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a zadejte hodnoty v následujícím způsobem balení čas:</span><span class="sxs-lookup"><span data-stu-id="52ad5-232">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="52ad5-233">Chcete-li hodnoty z projektu, zadat tokenů popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` například `AssemblyInfo.cs` nebo `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="52ad5-233">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="52ad5-234">Pokud chcete použít tyto tokeny, spusťte `nuget pack` do souboru projektu namísto pouze `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-234">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="52ad5-235">Například, když pomocí následujícího příkazu `$id$` a `$version$` tokeny v `.nuspec` souboru jsou nahrazeny projektu `AssemblyName` a `AssemblyVersion` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="52ad5-235">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="52ad5-236">Obvykle, když máte projekt, vytvoříte `.nuspec` zpočátku pomocí `nuget spec MyProject.csproj` což automaticky zahrnuje některé z těchto standardních tokenů.</span><span class="sxs-lookup"><span data-stu-id="52ad5-236">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="52ad5-237">Nicméně, pokud projekt neobsahuje hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` selže.</span><span class="sxs-lookup"><span data-stu-id="52ad5-237">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="52ad5-238">Navíc pokud můžete změnit hodnoty projektu, je nutné znovu sestavit před vytvořením balíčku. To můžete udělat jednoduše pomocí příkazu pack `build` přepnout.</span><span class="sxs-lookup"><span data-stu-id="52ad5-238">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="52ad5-239">S výjimkou produktů `$configuration$`, jsou hodnoty v projektu použít preferenci pro libovolné přiřazen stejný token v příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-239">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="52ad5-240">Podpisový</span><span class="sxs-lookup"><span data-stu-id="52ad5-240">Token</span></span> | <span data-ttu-id="52ad5-241">Hodnota zdroje</span><span class="sxs-lookup"><span data-stu-id="52ad5-241">Value source</span></span> | <span data-ttu-id="52ad5-242">Value</span><span class="sxs-lookup"><span data-stu-id="52ad5-242">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="52ad5-243">**$id$**</span><span class="sxs-lookup"><span data-stu-id="52ad5-243">**$id$**</span></span> | <span data-ttu-id="52ad5-244">soubor projektu</span><span class="sxs-lookup"><span data-stu-id="52ad5-244">Project file</span></span> | <span data-ttu-id="52ad5-245">AssemblyName (název) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="52ad5-245">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="52ad5-246">**$version$**</span><span class="sxs-lookup"><span data-stu-id="52ad5-246">**$version$**</span></span> | <span data-ttu-id="52ad5-247">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="52ad5-247">AssemblyInfo</span></span> | <span data-ttu-id="52ad5-248">AssemblyInformationalVersion, pokud jsou k dispozici, jinak AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="52ad5-248">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="52ad5-249">**$author$**</span><span class="sxs-lookup"><span data-stu-id="52ad5-249">**$author$**</span></span> | <span data-ttu-id="52ad5-250">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="52ad5-250">AssemblyInfo</span></span> | <span data-ttu-id="52ad5-251">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="52ad5-251">AssemblyCompany</span></span> |
| <span data-ttu-id="52ad5-252">**$title$**</span><span class="sxs-lookup"><span data-stu-id="52ad5-252">**$title$**</span></span> | <span data-ttu-id="52ad5-253">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="52ad5-253">AssemblyInfo</span></span> | <span data-ttu-id="52ad5-254">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="52ad5-254">AssemblyTitle</span></span> |
| <span data-ttu-id="52ad5-255">**$description$**</span><span class="sxs-lookup"><span data-stu-id="52ad5-255">**$description$**</span></span> | <span data-ttu-id="52ad5-256">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="52ad5-256">AssemblyInfo</span></span> | <span data-ttu-id="52ad5-257">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="52ad5-257">AssemblyDescription</span></span> |
| <span data-ttu-id="52ad5-258">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="52ad5-258">**$copyright$**</span></span> | <span data-ttu-id="52ad5-259">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="52ad5-259">AssemblyInfo</span></span> | <span data-ttu-id="52ad5-260">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="52ad5-260">AssemblyCopyright</span></span> |
| <span data-ttu-id="52ad5-261">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="52ad5-261">**$configuration$**</span></span> | <span data-ttu-id="52ad5-262">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="52ad5-262">Assembly DLL</span></span> | <span data-ttu-id="52ad5-263">Konfigurace použitý k vytvoření sestavení, jako výchozí se použije k ladění.</span><span class="sxs-lookup"><span data-stu-id="52ad5-263">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="52ad5-264">Všimněte si, že pokud chcete vytvořit balíček pomocí konfiguraci vydané verze, vždy používáte `-properties Configuration=Release` na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-264">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="52ad5-265">Tokeny je také možné přeložit cesty, jakmile zahrnete [soubory sestavení](#including-assembly-files) a [obsah souborů](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="52ad5-265">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="52ad5-266">Tokeny mají stejné názvy jako vlastnosti nástroje MSBuild, což umožňuje vyberte soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="52ad5-266">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="52ad5-267">Například, pokud použijete následující klíčová slova v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="52ad5-267">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="52ad5-268">A vytvoření sestavení jehož `AssemblyName` je `LoggingLibrary` s `Release` konfigurace v nástroji MSBuild, výsledný vstupující `.nuspec` souborů v balíčku je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="52ad5-268">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="52ad5-269">Dependencies – element</span><span class="sxs-lookup"><span data-stu-id="52ad5-269">Dependencies element</span></span>

<span data-ttu-id="52ad5-270">`<dependencies>` Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvky, které určují další balíčky, na kterých závisí balíček nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="52ad5-270">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="52ad5-271">Atributy pro každý `<dependency>` jsou následující:</span><span class="sxs-lookup"><span data-stu-id="52ad5-271">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="52ad5-272">Atribut</span><span class="sxs-lookup"><span data-stu-id="52ad5-272">Attribute</span></span> | <span data-ttu-id="52ad5-273">Popis</span><span class="sxs-lookup"><span data-stu-id="52ad5-273">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="52ad5-274">(Povinné) Ukazuje, na stránce balíček pro ID balíčku závislosti, jako je například "EntityFramework" a "NUnit", což je název balíčku nuget.org.</span><span class="sxs-lookup"><span data-stu-id="52ad5-274">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="52ad5-275">(Povinné) Rozsah verzí přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="52ad5-275">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="52ad5-276">Zobrazit [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) přesnou syntaxi.</span><span class="sxs-lookup"><span data-stu-id="52ad5-276">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="52ad5-277">include</span><span class="sxs-lookup"><span data-stu-id="52ad5-277">include</span></span> | <span data-ttu-id="52ad5-278">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti, které mají být zahrnuty do koncového balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-278">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="52ad5-279">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-279">The default value is `all`.</span></span> |
| <span data-ttu-id="52ad5-280">exclude</span><span class="sxs-lookup"><span data-stu-id="52ad5-280">exclude</span></span> | <span data-ttu-id="52ad5-281">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti pro vyloučení ve finálním balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="52ad5-282">Výchozí hodnota je `build,analyzers` může být přepsání.</span><span class="sxs-lookup"><span data-stu-id="52ad5-282">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="52ad5-283">Ale `content/ ContentFiles` nevylučují se také implicitně ve finálním balíčku, který nelze přepsání.</span><span class="sxs-lookup"><span data-stu-id="52ad5-283">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="52ad5-284">Značky s `exclude` přednost zadaným `include`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-284">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="52ad5-285">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-285">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="52ad5-286">Zahrnutí a vyloučení značek</span><span class="sxs-lookup"><span data-stu-id="52ad5-286">Include/Exclude tag</span></span> | <span data-ttu-id="52ad5-287">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="52ad5-287">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="52ad5-288">contentFiles</span><span class="sxs-lookup"><span data-stu-id="52ad5-288">contentFiles</span></span> | <span data-ttu-id="52ad5-289">Obsah</span><span class="sxs-lookup"><span data-stu-id="52ad5-289">Content</span></span> |
| <span data-ttu-id="52ad5-290">modul runtime</span><span class="sxs-lookup"><span data-stu-id="52ad5-290">runtime</span></span> | <span data-ttu-id="52ad5-291">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="52ad5-291">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="52ad5-292">Kompilace</span><span class="sxs-lookup"><span data-stu-id="52ad5-292">compile</span></span> | <span data-ttu-id="52ad5-293">lib</span><span class="sxs-lookup"><span data-stu-id="52ad5-293">lib</span></span> |
| <span data-ttu-id="52ad5-294">sestavení</span><span class="sxs-lookup"><span data-stu-id="52ad5-294">build</span></span> | <span data-ttu-id="52ad5-295">sestavení (cíle a vlastnosti nástroje MSBuild)</span><span class="sxs-lookup"><span data-stu-id="52ad5-295">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="52ad5-296">nativní</span><span class="sxs-lookup"><span data-stu-id="52ad5-296">native</span></span> | <span data-ttu-id="52ad5-297">nativní</span><span class="sxs-lookup"><span data-stu-id="52ad5-297">native</span></span> |
| <span data-ttu-id="52ad5-298">žádná</span><span class="sxs-lookup"><span data-stu-id="52ad5-298">none</span></span> | <span data-ttu-id="52ad5-299">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="52ad5-299">No folders</span></span> |
| <span data-ttu-id="52ad5-300">všechny</span><span class="sxs-lookup"><span data-stu-id="52ad5-300">all</span></span> | <span data-ttu-id="52ad5-301">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="52ad5-301">All folders</span></span> |

<span data-ttu-id="52ad5-302">Například následující řádky signalizovat závislosti na `PackageA` verze 1.1.0 nebo vyšší, a `PackageB` verzi 1.x.</span><span class="sxs-lookup"><span data-stu-id="52ad5-302">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="52ad5-303">Následující řádky označují závislostí na stejné balíčky, ale zadané k vložení `contentFiles` a `build` složky `PackageA` a všechno, co ale `native` a `compile` složky `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="52ad5-303">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="52ad5-304">Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`, závislosti, které existují v tomto projektu jsou automaticky obsažené ve výsledné `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="52ad5-304">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="52ad5-305">Závislostí skupin</span><span class="sxs-lookup"><span data-stu-id="52ad5-305">Dependency groups</span></span>

<span data-ttu-id="52ad5-306">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="52ad5-306">*Version 2.0+*</span></span>

<span data-ttu-id="52ad5-307">Jako alternativu k jednomu seznamu bez stromové struktury, se dá nastavit závislosti podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-307">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="52ad5-308">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<dependency>` elementy.</span><span class="sxs-lookup"><span data-stu-id="52ad5-308">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="52ad5-309">Tyto závislosti jsou nainstalovány společně, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-309">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="52ad5-310">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="52ad5-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="52ad5-311">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="52ad5-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="52ad5-312">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="52ad5-313">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="52ad5-313">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="52ad5-314">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="52ad5-314">Explicit assembly references</span></span>

<span data-ttu-id="52ad5-315">`<references>` Element je používán projektů s použitím `packages.config` explicitně zadejte sestavení, které by měly odkazovat na cílový projekt, při použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-315">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="52ad5-316">Explicitní odkazy se obvykle používají pro pouze na sestavení doby návrhu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-316">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="52ad5-317">Další informace naleznete na stránce na [výběr sestavení odkazovaných projektů](../create-packages/select-assemblies-referenced-by-projects.md) Další informace.</span><span class="sxs-lookup"><span data-stu-id="52ad5-317">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="52ad5-318">Například následující `<references>` element dává pokyn NuGet pro přidání odkazů na pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že existují další sestavení v balíčku:</span><span class="sxs-lookup"><span data-stu-id="52ad5-318">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="52ad5-319">Referenční skupiny</span><span class="sxs-lookup"><span data-stu-id="52ad5-319">Reference groups</span></span>

<span data-ttu-id="52ad5-320">Jako alternativu k jednomu plochého seznamu lze upravit odkazy podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<references>`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-320">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="52ad5-321">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="52ad5-321">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="52ad5-322">Tyto odkazy jsou přidány do projektu, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-322">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="52ad5-323">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznamu odkazů.</span><span class="sxs-lookup"><span data-stu-id="52ad5-323">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="52ad5-324">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="52ad5-324">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="52ad5-325">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-325">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="52ad5-326">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="52ad5-326">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="52ad5-327">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="52ad5-327">Framework assembly references</span></span>

<span data-ttu-id="52ad5-328">Sestavení rozhraní jsou ty, které jsou součástí rozhraní .NET framework a by už měla být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač.</span><span class="sxs-lookup"><span data-stu-id="52ad5-328">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="52ad5-329">Určením těchto sestavení v rámci `<frameworkAssemblies>` elementu balíčku můžete zajistit, že požadované odkazy jsou přidány do projektu, v případě, že projekt již nemá tyto odkazy.</span><span class="sxs-lookup"><span data-stu-id="52ad5-329">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="52ad5-330">Takové sestavení, samozřejmě, nejsou obsažené v balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="52ad5-330">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="52ad5-331">`<frameworkAssemblies>` Prvek obsahuje nula nebo více `<frameworkAssembly>` prvky, z nichž každý určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="52ad5-331">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="52ad5-332">Atribut</span><span class="sxs-lookup"><span data-stu-id="52ad5-332">Attribute</span></span> | <span data-ttu-id="52ad5-333">Popis</span><span class="sxs-lookup"><span data-stu-id="52ad5-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52ad5-334">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="52ad5-334">**assemblyName**</span></span> | <span data-ttu-id="52ad5-335">(Povinné) Plně kvalifikovaný název.</span><span class="sxs-lookup"><span data-stu-id="52ad5-335">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="52ad5-336">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="52ad5-336">**targetFramework**</span></span> | <span data-ttu-id="52ad5-337">(Volitelné) Určuje cílovou architekturu, pro který platí tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="52ad5-337">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="52ad5-338">Pokud tento parametr vynechán, označuje, že odkaz použije pro všechny platformy.</span><span class="sxs-lookup"><span data-stu-id="52ad5-338">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="52ad5-339">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="52ad5-339">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="52ad5-340">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové platformy a odkaz na `System.ServiceModel` pro pouze rozhraní .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="52ad5-340">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="52ad5-341">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="52ad5-341">Including assembly files</span></span>

<span data-ttu-id="52ad5-342">Pokud budete postupovat podle konvence je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md), není potřeba explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="52ad5-342">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="52ad5-343">`nuget pack` Příkaz automaticky převezme potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="52ad5-343">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="52ad5-344">Při instalaci do projektu balíček NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* ty, které jsou pojmenovány `.resources.dll` vzhledem k tomu, že se budou považovat za lokalizovaná satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="52ad5-344">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="52ad5-345">Z tohoto důvodu se vyhněte se použití `.resources.dll` pro soubory, které jinak obsahují základní balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-345">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="52ad5-346">Toto automatické chování obejít a explicitně kontrolovat soubory, které jsou obsažené v balíčku, umístěte `<files>` jako podřízený element `<package>` (a na stejné úrovni `<metadata>`), identifikuje každý soubor se samostatným `<file>` element.</span><span class="sxs-lookup"><span data-stu-id="52ad5-346">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="52ad5-347">Příklad:</span><span class="sxs-lookup"><span data-stu-id="52ad5-347">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="52ad5-348">Nuget 2.x a dřívějších verzí a projekty pomocí `packages.config`, `<files>` element slouží také k neměnné obsahu soubory k zahrnutí při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="52ad5-348">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="52ad5-349">S NuGet 3.3 + i na PackageReference `<contentFiles>` elementu je použita.</span><span class="sxs-lookup"><span data-stu-id="52ad5-349">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="52ad5-350">Zobrazit [včetně soubory obsahu](#including-content-files) níže podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="52ad5-350">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="52ad5-351">Atributy souboru</span><span class="sxs-lookup"><span data-stu-id="52ad5-351">File element attributes</span></span>

<span data-ttu-id="52ad5-352">Každý `<file>` prvek určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="52ad5-352">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="52ad5-353">Atribut</span><span class="sxs-lookup"><span data-stu-id="52ad5-353">Attribute</span></span> | <span data-ttu-id="52ad5-354">Popis</span><span class="sxs-lookup"><span data-stu-id="52ad5-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52ad5-355">**src**</span><span class="sxs-lookup"><span data-stu-id="52ad5-355">**src**</span></span> | <span data-ttu-id="52ad5-356">Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="52ad5-356">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="52ad5-357">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-357">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="52ad5-358">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="52ad5-358">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="52ad5-359">**target**</span><span class="sxs-lookup"><span data-stu-id="52ad5-359">**target**</span></span> | <span data-ttu-id="52ad5-360">Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které musí začínat `lib`, `content`, `build`, nebo `tools`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-360">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="52ad5-361">Zobrazit [vytváření souboru .nuspec z pracovního adresáře podle úmluvy](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="52ad5-361">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="52ad5-362">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="52ad5-362">**exclude**</span></span> | <span data-ttu-id="52ad5-363">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="52ad5-363">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="52ad5-364">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="52ad5-364">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="52ad5-365">Příklady</span><span class="sxs-lookup"><span data-stu-id="52ad5-365">Examples</span></span>

<span data-ttu-id="52ad5-366">**Jediné sestavení**</span><span class="sxs-lookup"><span data-stu-id="52ad5-366">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="52ad5-367">**Jediné sestavení specifická pro rozhraní .NET framework**</span><span class="sxs-lookup"><span data-stu-id="52ad5-367">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="52ad5-368">**Sada knihovny DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="52ad5-368">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="52ad5-369">**Knihovny DLL pro různá rozhraní**</span><span class="sxs-lookup"><span data-stu-id="52ad5-369">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="52ad5-370">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="52ad5-370">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="52ad5-371">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="52ad5-371">Including content files</span></span>

<span data-ttu-id="52ad5-372">Soubory obsahu jsou neměnné soubory, které je potřeba zahrnout do projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="52ad5-372">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="52ad5-373">Je neměnný, nejsou určeny k používání projektu změnit.</span><span class="sxs-lookup"><span data-stu-id="52ad5-373">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="52ad5-374">Příklad obsahu souborů patří:</span><span class="sxs-lookup"><span data-stu-id="52ad5-374">Example content files include:</span></span>

- <span data-ttu-id="52ad5-375">Bitové kopie, které jsou vloženy jako prostředky</span><span class="sxs-lookup"><span data-stu-id="52ad5-375">Images that are embedded as resources</span></span>
- <span data-ttu-id="52ad5-376">Zdrojové soubory, které jsou již kompilován</span><span class="sxs-lookup"><span data-stu-id="52ad5-376">Source files that are already compiled</span></span>
- <span data-ttu-id="52ad5-377">Skripty, které musí být součástí výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="52ad5-377">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="52ad5-378">Konfigurační soubory pro balíček, který mají být zahrnuti do projektu, ale není třeba žádné změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="52ad5-378">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="52ad5-379">Obsahu souborů jsou součástí balíčku pomocí `<files>` elementu, určení `content` složky `target` atribut.</span><span class="sxs-lookup"><span data-stu-id="52ad5-379">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="52ad5-380">Ale tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který používá místo toho `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-380">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="52ad5-381">Balíček pro maximální kompatibility s využívání projektů v ideálním případě Určuje soubory obsahu v obou elementech.</span><span class="sxs-lookup"><span data-stu-id="52ad5-381">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="52ad5-382">Pomocí elementu souborů pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="52ad5-382">Using the files element for content files</span></span>

<span data-ttu-id="52ad5-383">Pro soubory obsahu, stačí použít stejný formát jako soubory sestavení, ale zadat `content` jako základní složka v `target` atributu, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-383">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="52ad5-384">**Soubory základního obsahu**</span><span class="sxs-lookup"><span data-stu-id="52ad5-384">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="52ad5-385">**Soubory obsahu s adresářovou strukturu**</span><span class="sxs-lookup"><span data-stu-id="52ad5-385">**Content files with directory structure**</span></span>

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

<span data-ttu-id="52ad5-386">**Soubor s obsahem specifické pro cílové prostředí**</span><span class="sxs-lookup"><span data-stu-id="52ad5-386">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="52ad5-387">**Zkopírovat do složky s tečkou v názvu souboru obsahu**</span><span class="sxs-lookup"><span data-stu-id="52ad5-387">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="52ad5-388">V takovém případě se zobrazí NuGet, který rozšíření v `target` se neshoduje s příponou v `src` a proto zpracovává tuto část názvu v `target` jako složka:</span><span class="sxs-lookup"><span data-stu-id="52ad5-388">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="52ad5-389">**Soubory obsahu bez přípony**</span><span class="sxs-lookup"><span data-stu-id="52ad5-389">**Content files without extensions**</span></span>

<span data-ttu-id="52ad5-390">Chcete-li zahrnout soubory bez přípony, použijte `*` nebo `**` zástupné znaky:</span><span class="sxs-lookup"><span data-stu-id="52ad5-390">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="52ad5-391">**Soubory obsahu se hloubkové cesty a hloubkové cílem**</span><span class="sxs-lookup"><span data-stu-id="52ad5-391">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="52ad5-392">V takovém případě protože přípony zdrojovou a cílovou odpovídají, NuGet předpokládá, že cíl je název souboru a nikoliv složka:</span><span class="sxs-lookup"><span data-stu-id="52ad5-392">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="52ad5-393">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="52ad5-393">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="52ad5-394">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="52ad5-394">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="52ad5-395">Pomocí elementu contentFiles pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="52ad5-395">Using the contentFiles element for content files</span></span>

<span data-ttu-id="52ad5-396">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="52ad5-396">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="52ad5-397">Ve výchozím nastavení, umístí balíček obsahu `contentFiles` složky (viz níže) a `nuget pack` zahrnuty všechny soubory ve složce pomocí výchozí atributy.</span><span class="sxs-lookup"><span data-stu-id="52ad5-397">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="52ad5-398">V tomto případě není nutné zahrnout `contentFiles` uzlu `.nuspec` vůbec.</span><span class="sxs-lookup"><span data-stu-id="52ad5-398">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="52ad5-399">K řízení souborů, které jsou zahrnuty `<contentFiles>` prvek určuje je kolekce `<files>` mezi prvky, které identifikují přesné soubory patří.</span><span class="sxs-lookup"><span data-stu-id="52ad5-399">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="52ad5-400">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů:</span><span class="sxs-lookup"><span data-stu-id="52ad5-400">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="52ad5-401">Atribut</span><span class="sxs-lookup"><span data-stu-id="52ad5-401">Attribute</span></span> | <span data-ttu-id="52ad5-402">Popis</span><span class="sxs-lookup"><span data-stu-id="52ad5-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52ad5-403">**include**</span><span class="sxs-lookup"><span data-stu-id="52ad5-403">**include**</span></span> | <span data-ttu-id="52ad5-404">(Povinné) Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="52ad5-404">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="52ad5-405">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="52ad5-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="52ad5-406">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="52ad5-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="52ad5-407">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="52ad5-407">**exclude**</span></span> | <span data-ttu-id="52ad5-408">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="52ad5-408">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="52ad5-409">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="52ad5-409">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="52ad5-410">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="52ad5-410">**buildAction**</span></span> | <span data-ttu-id="52ad5-411">Akce sestavení zařadit do obsahu položky nástroje MSBuild, jako například `Content`, `None`, `Embedded Resource`, `Compile`atd. Výchozí hodnota je `Compile`.</span><span class="sxs-lookup"><span data-stu-id="52ad5-411">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="52ad5-412">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="52ad5-412">**copyToOutput**</span></span> | <span data-ttu-id="52ad5-413">Logická hodnota označující, jestli se má kopírovat položky obsahu pro sestavení (nebo publikovat) výstupní složka.</span><span class="sxs-lookup"><span data-stu-id="52ad5-413">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="52ad5-414">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="52ad5-414">The default is false.</span></span> |
| <span data-ttu-id="52ad5-415">**Sloučit**</span><span class="sxs-lookup"><span data-stu-id="52ad5-415">**flatten**</span></span> | <span data-ttu-id="52ad5-416">Logická hodnota označující, zda se můžete kopírovat položky obsahu na jedinou složku ve výstupu sestavení (pravda), nebo zachovat strukturu složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="52ad5-416">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="52ad5-417">Tento příznak funguje pouze v případě copyToOutput příznak je nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="52ad5-417">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="52ad5-418">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="52ad5-418">The default is false.</span></span> |

<span data-ttu-id="52ad5-419">Při instalaci balíčku NuGet platí podřízených elementů `<contentFiles>` shora dolů.</span><span class="sxs-lookup"><span data-stu-id="52ad5-419">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="52ad5-420">Pokud se shodují na stejný soubor několik záznamů se použijí všechny položky.</span><span class="sxs-lookup"><span data-stu-id="52ad5-420">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="52ad5-421">Položky navrchu přepíše nižší položky dojde ke konfliktu pro stejný atribut.</span><span class="sxs-lookup"><span data-stu-id="52ad5-421">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="52ad5-422">Struktura složky balíčku</span><span class="sxs-lookup"><span data-stu-id="52ad5-422">Package folder structure</span></span>

<span data-ttu-id="52ad5-423">Projekt balíčku strukturovat obsahu pomocí následujícímu vzoru:</span><span class="sxs-lookup"><span data-stu-id="52ad5-423">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="52ad5-424">`codeLanguages` může být `cs`, `vb`, `fs`, `any`, nebo malým ekvivalentem znaku danou `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="52ad5-424">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="52ad5-425">`TxM` je všechny moniker právní cílového rozhraní, která podporuje NuGet (viz [platforem](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="52ad5-425">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="52ad5-426">Složky libovolné struktury složek může připojen na konec této syntaxe.</span><span class="sxs-lookup"><span data-stu-id="52ad5-426">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="52ad5-427">Příklad:</span><span class="sxs-lookup"><span data-stu-id="52ad5-427">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="52ad5-428">Můžete použít prázdné složky `.` chcete vyjádřit výslovný nesouhlas poskytnutí obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="52ad5-428">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="52ad5-429">Vzorový oddíl contentFiles</span><span class="sxs-lookup"><span data-stu-id="52ad5-429">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="52ad5-430">Příklad souboru nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="52ad5-430">Example nuspec files</span></span>

<span data-ttu-id="52ad5-431">**Jednoduchý `.nuspec` , která neurčuje závislosti nebo souborů**</span><span class="sxs-lookup"><span data-stu-id="52ad5-431">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="52ad5-432">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="52ad5-432">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="52ad5-433">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="52ad5-433">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="52ad5-434">**A `.nuspec` se sestaveními rozhraní framework**</span><span class="sxs-lookup"><span data-stu-id="52ad5-434">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="52ad5-435">V tomto příkladu tímto se nainstalují pro konkrétní projekt cílí:</span><span class="sxs-lookup"><span data-stu-id="52ad5-435">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="52ad5-436">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="52ad5-436">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="52ad5-437">. NET4 -> Client Profile `System.Net`</span><span class="sxs-lookup"><span data-stu-id="52ad5-437">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="52ad5-438">Silverlight 3 -> `System.Json`</span><span class="sxs-lookup"><span data-stu-id="52ad5-438">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="52ad5-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="52ad5-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
