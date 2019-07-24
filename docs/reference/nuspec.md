---
title: Odkaz na soubor. nuspec pro NuGet
description: Soubor. nuspec obsahuje metadata balíčku, která se používají při sestavování balíčku a poskytování informací pro uživatele balíčku.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 5b9be55b593890127d8fe0ad1a9357b89527a09a
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433361"
---
# <a name="nuspec-reference"></a><span data-ttu-id="cb9d3-103">odkaz. nuspec</span><span class="sxs-lookup"><span data-stu-id="cb9d3-103">.nuspec reference</span></span>

<span data-ttu-id="cb9d3-104">`.nuspec` Soubor je manifest XML, který obsahuje metadata balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="cb9d3-105">Tento manifest slouží k sestavení balíčku a k poskytování informací pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="cb9d3-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="cb9d3-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-107">In this topic:</span></span>

- [<span data-ttu-id="cb9d3-108">Obecné formuláře a schéma</span><span class="sxs-lookup"><span data-stu-id="cb9d3-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="cb9d3-109">[Náhradní tokeny](#replacement-tokens) (při použití s projektem sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cb9d3-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="cb9d3-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="cb9d3-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="cb9d3-111">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="cb9d3-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="cb9d3-112">Odkazy na sestavení rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cb9d3-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="cb9d3-113">Zahrnutí souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="cb9d3-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="cb9d3-114">Zahrnutí souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="cb9d3-115">Příklady souborů nuspec</span><span class="sxs-lookup"><span data-stu-id="cb9d3-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="cb9d3-116">Kompatibilita typů projektu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-116">Project type compatibility</span></span>

- <span data-ttu-id="cb9d3-117">Použijte `.nuspec` `packages.config`s `nuget.exe pack` pro projekty, které nejsou ve stylu sady SDK, které používají.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="cb9d3-118">Soubor není vyžadován k vytváření balíčků pro projekty ve [stylu sady SDK](../resources/check-project-format.md) (obvykle se jedná o projekty .NET Core a .NET Standard, které používají [atribut SDK](/dotnet/core/tools/csproj#additions)). `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="cb9d3-119">(Všimněte si, `.nuspec` že se generuje při vytváření balíčku.)</span><span class="sxs-lookup"><span data-stu-id="cb9d3-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="cb9d3-120">Pokud `dotnet.exe pack` vytváříte balíček pomocí nebo `msbuild pack target`, doporučujeme místo toho [Zahrnout všechny](../reference/msbuild-targets.md#pack-target) `.nuspec` vlastnosti, které jsou obvykle v souboru v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="cb9d3-121">Místo toho se ale můžete rozhodnout [použít `.nuspec` soubor k `dotnet.exe` balení pomocí `msbuild pack target`nebo ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="cb9d3-122">Pro projekty migrované z `packages.config` aplikace do `.nuspec` [PackageReference](../consume-packages/package-references-in-project-files.md) není pro vytvoření balíčku vyžadován soubor.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="cb9d3-123">Místo toho použijte [MSBuild-t:Pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-123">Instead, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="cb9d3-124">Obecné formuláře a schéma</span><span class="sxs-lookup"><span data-stu-id="cb9d3-124">General form and schema</span></span>

<span data-ttu-id="cb9d3-125">Aktuální `nuspec.xsd` soubor schématu najdete v [úložišti GitHub NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="cb9d3-126">V rámci tohoto schématu `.nuspec` má soubor následující obecný tvar:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="cb9d3-127">V případě jasné vizuální reprezentace schématu otevřete soubor schématu v aplikaci Visual Studio v režimu návrhu a klikněte na odkaz **Průzkumník schémat XML** .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="cb9d3-128">Případně soubor otevřete jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **Zobrazit Průzkumníka schémat XML**.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="cb9d3-129">Jak můžete vidět následující pohled (Pokud je převážně rozbalený):</span><span class="sxs-lookup"><span data-stu-id="cb9d3-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Průzkumník schémat sady Visual Studio s otevřeným nuspec. xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="cb9d3-131">Požadované prvky metadat</span><span class="sxs-lookup"><span data-stu-id="cb9d3-131">Required metadata elements</span></span>

<span data-ttu-id="cb9d3-132">I když následující prvky jsou minimální požadavky na balíček, měli byste zvážit přidání [volitelných prvků metadat](#optional-metadata-elements) pro zlepšení celkového prostředí, které vývojáři mají s vaším balíčkem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="cb9d3-133">Tyto prvky se musí objevit v `<metadata>` rámci elementu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="cb9d3-134">id</span><span class="sxs-lookup"><span data-stu-id="cb9d3-134">id</span></span> 
<span data-ttu-id="cb9d3-135">Identifikátor balíčku bez rozlišení velkých a malých písmen, který musí být jedinečný v rámci nuget.org nebo jakákoli galerie, v níž se balíček nachází.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="cb9d3-136">ID nesmí obsahovat mezery ani znaky, které nejsou platné pro adresu URL a obecně následují pravidla oboru názvů .NET.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="cb9d3-137">Pokyny najdete v tématu [Volba jedinečného identifikátoru balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="cb9d3-138">verze</span><span class="sxs-lookup"><span data-stu-id="cb9d3-138">version</span></span>
<span data-ttu-id="cb9d3-139">Verze balíčku, podle vzoru *hlavní_verze. podverze. Oprava* .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="cb9d3-140">Čísla verzí můžou obsahovat příponu předběžné verze, jak je popsáno v tématu [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="cb9d3-141">description</span><span class="sxs-lookup"><span data-stu-id="cb9d3-141">description</span></span>
<span data-ttu-id="cb9d3-142">Dlouhý popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="cb9d3-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="cb9d3-143">authors</span></span>
<span data-ttu-id="cb9d3-144">Čárkami oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazí v galerii NuGet na nuget.org a používají se pro balíčky křížového odkazu stejnými autory.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="cb9d3-145">Volitelné prvky metadat</span><span class="sxs-lookup"><span data-stu-id="cb9d3-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="cb9d3-146">Vlastníka</span><span class="sxs-lookup"><span data-stu-id="cb9d3-146">owners</span></span>
<span data-ttu-id="cb9d3-147">Čárkami oddělený seznam tvůrců balíčků s použitím názvů profilů v nuget.org. Často se jedná o stejný seznam jako v `authors`a při nahrávání balíčku do NuGet.org se ignoruje. Viz [Správa vlastníků balíčků na NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="cb9d3-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="cb9d3-148">projectUrl</span></span>
<span data-ttu-id="cb9d3-149">Adresa URL domovské stránky balíčku, která se často zobrazuje v uživatelském rozhraní, a také nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="cb9d3-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="cb9d3-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="cb9d3-151">licenseUrl se už nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="cb9d3-152">Místo toho použijte licenci.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-152">Use license instead.</span></span>

<span data-ttu-id="cb9d3-153">Adresa URL licence balíčku, která se často zobrazuje v uživatelská rozhraní jako nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="cb9d3-154">Průkaz</span><span class="sxs-lookup"><span data-stu-id="cb9d3-154">license</span></span>
<span data-ttu-id="cb9d3-155">SPDX licenční výraz nebo cesta k souboru s licencí v balíčku, který se často zobrazuje v uživatelská rozhraní jako nuget.org. Pokud je balíček licencován v rámci společné licence, jako je například MIT nebo BSD-2, použijte přidružený [identifikátor licence SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="cb9d3-156">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="cb9d3-157">NuGet.org akceptuje pouze licenční výrazy, které jsou schváleny v rámci iniciativy Open Source nebo Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="cb9d3-158">Pokud je váš balíček licencován více běžnými licencemi, můžete zadat složenou licenci pomocí [syntaxe výrazu SPDX verze 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="cb9d3-159">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="cb9d3-160">Pokud používáte vlastní licenci, která není podporovaná výrazy licence, můžete zabalit `.txt` soubor nebo `.md` soubor s textem licence.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="cb9d3-161">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-161">For example:</span></span>

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

<span data-ttu-id="cb9d3-162">V případě ekvivalentu MSBuild si prohlédněte [balení licenčního výrazu nebo souboru s licencí](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="cb9d3-163">Přesná Syntaxe výrazů s licenčními výrazy NuGet je popsaná níže v tématu [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="cb9d3-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="cb9d3-164">iconUrl</span></span>
<span data-ttu-id="cb9d3-165">Adresa URL 64 × 64 obrázku s pozadím průhlednosti, která se má použít jako ikona balíčku v zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="cb9d3-166">Ujistěte se, že tento prvek obsahuje *adresu URL přímého obrázku* , a ne adresu URL webové stránky, která obsahuje obrázek.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="cb9d3-167">Pokud například chcete použít image z GitHubu, použijte adresu URL nezpracovaného souboru <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>jako.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="cb9d3-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="cb9d3-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="cb9d3-169">Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="cb9d3-170">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="cb9d3-170">developmentDependency</span></span>
<span data-ttu-id="cb9d3-171">*(2.8+)* Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="cb9d3-172">Pomocí PackageReference (NuGet 4,8 +) Tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="cb9d3-173">Viz [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="cb9d3-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="cb9d3-174">souhrn</span><span class="sxs-lookup"><span data-stu-id="cb9d3-174">summary</span></span>
<span data-ttu-id="cb9d3-175">Krátký popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-175">A short description of the package for UI display.</span></span> <span data-ttu-id="cb9d3-176">`description` Je-li tento parametr vynechán, je použita zkrácená verze nástroje.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="cb9d3-177">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="cb9d3-177">releaseNotes</span></span>
<span data-ttu-id="cb9d3-178">*(1.5+)* Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="cb9d3-179">Úprava</span><span class="sxs-lookup"><span data-stu-id="cb9d3-179">copyright</span></span>
<span data-ttu-id="cb9d3-180">*(1.5+)* Copyright podrobnosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="cb9d3-181">jazyk</span><span class="sxs-lookup"><span data-stu-id="cb9d3-181">language</span></span>
<span data-ttu-id="cb9d3-182">ID národního prostředí balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-182">The locale ID for the package.</span></span> <span data-ttu-id="cb9d3-183">Viz [vytváření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="cb9d3-184">značky</span><span class="sxs-lookup"><span data-stu-id="cb9d3-184">tags</span></span>
<span data-ttu-id="cb9d3-185">Mezerou oddělený seznam značek a klíčových slov, které popisují balíček a pomáhají zjistit balíčky pomocí vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="cb9d3-186">serviceable</span><span class="sxs-lookup"><span data-stu-id="cb9d3-186">serviceable</span></span> 
<span data-ttu-id="cb9d3-187">*(3.3+)* Pouze pro interní NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="cb9d3-188">úložiště</span><span class="sxs-lookup"><span data-stu-id="cb9d3-188">repository</span></span>
<span data-ttu-id="cb9d3-189">Metadata úložiště sestávající ze čtyř volitelných atributů: `type` a `url` *(4.0 +)* a `branch` a `commit` *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-189">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="cb9d3-190">Tyto atributy umožňují mapování `.nupkg` na úložiště, které ho vytvořilo, s potenciálem, který se má považovat za název jednotlivé větve a/nebo na potvrzení hodnoty hash SHA-1, která balíček vytvořila.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-190">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="cb9d3-191">Měla by to být veřejně dostupná adresa URL, kterou lze vyvolat přímo pomocí softwaru pro správu verzí.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="cb9d3-192">Neměla by se jednat o stránku HTML, která je určena pro daný počítač.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="cb9d3-193">Pro odkazování na stránku projektu použijte `projectUrl` místo toho pole.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="cb9d3-194">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-194">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="minclientversion"></a><span data-ttu-id="cb9d3-195">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="cb9d3-195">minClientVersion</span></span>
<span data-ttu-id="cb9d3-196">Určuje minimální verzi klienta NuGet, která může nainstalovat tento balíček, který vynutila NuGet. exe a správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-196">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="cb9d3-197">Tato funkce se používá vždy, když balíček závisí na konkrétních funkcích `.nuspec` souboru, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-197">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="cb9d3-198">Například balíček, který používá `developmentDependency` atribut, by měl pro `minClientVersion`použít hodnotu "2,8".</span><span class="sxs-lookup"><span data-stu-id="cb9d3-198">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="cb9d3-199">Podobně balíček, který používá `contentFiles` element (viz další oddíl), by měl být nastaven `minClientVersion` na "3,3".</span><span class="sxs-lookup"><span data-stu-id="cb9d3-199">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="cb9d3-200">Všimněte si také, že vzhledem k tomu, že klienti NuGet starší než 2,5 nerozpoznávají tento příznak, *vždy* zamítnou instalaci balíčku bez `minClientVersion` ohledu na to, co obsahuje.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-200">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="title"></a><span data-ttu-id="cb9d3-201">název</span><span class="sxs-lookup"><span data-stu-id="cb9d3-201">title</span></span>
<span data-ttu-id="cb9d3-202">Popisný název balíčku, který se dá použít v některých zobrazeních uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-202">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="cb9d3-203">(nuget.org a správce balíčků v aplikaci Visual Studio nezobrazuje název)</span><span class="sxs-lookup"><span data-stu-id="cb9d3-203">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="cb9d3-204">Prvky kolekce</span><span class="sxs-lookup"><span data-stu-id="cb9d3-204">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="cb9d3-205">packageTypes</span><span class="sxs-lookup"><span data-stu-id="cb9d3-205">packageTypes</span></span>
<span data-ttu-id="cb9d3-206">*(3.5 +)* Kolekce nula nebo více `<packageType>` prvků určující typ balíčku, pokud je jiný než tradiční balíček závislostí.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-206">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="cb9d3-207">Každý packageType má atributy *názvu* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-207">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="cb9d3-208">Viz [Nastavení typu balíčku](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-208">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="cb9d3-209">závislosti</span><span class="sxs-lookup"><span data-stu-id="cb9d3-209">dependencies</span></span>
<span data-ttu-id="cb9d3-210">Kolekce nula nebo více `<dependency>` prvků, které určují závislosti pro balíček.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-210">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="cb9d3-211">Každá závislost má atributy *ID*, *verze*, *include* (3. x +) a *Exclude* (3. x +).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-211">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="cb9d3-212">Viz [závislosti](#dependencies-element) níže.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-212">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="cb9d3-213">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="cb9d3-213">frameworkAssemblies</span></span>
<span data-ttu-id="cb9d3-214">*(1,2 +)* Kolekce nula nebo více `<frameworkAssembly>` prvků, které identifikují .NET Framework odkazy na sestavení, které tento balíček vyžaduje, což zajistí přidání odkazů do projektů, které balíček spotřebovává.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-214">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="cb9d3-215">Každý frameworkAssembly má atributy *AssemblyName* a *targetFramework* .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-215">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="cb9d3-216">Viz [určení sestavení rozhraní odkazy v mezipaměti GAC](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-216">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="cb9d3-217">odkazy</span><span class="sxs-lookup"><span data-stu-id="cb9d3-217">references</span></span>
<span data-ttu-id="cb9d3-218">*(1,5 +)* Kolekce nula nebo více `<reference>` prvků pojmenování sestavení ve `lib` složce balíčku, které jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-218">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="cb9d3-219">Každý odkaz má atribut *File* .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-219">Each reference has a *file* attribute.</span></span> <span data-ttu-id="cb9d3-220">`<references>`může také obsahovat `<group>` element s atributem *targetFramework* , který pak obsahuje `<reference>` prvky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-220">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="cb9d3-221">Pokud tento parametr vynecháte, `lib` jsou zahrnuty všechny odkazy v nástroji.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-221">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="cb9d3-222">Viz [zadání explicitních odkazů na sestavení](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-222">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="cb9d3-223">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="cb9d3-223">contentFiles</span></span>
<span data-ttu-id="cb9d3-224">*(3.3 +)* Kolekce `<files>` prvků, které identifikují soubory obsahu, které mají být zahrnuty do náročného projektu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-224">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="cb9d3-225">Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-225">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="cb9d3-226">Viz [Určení souborů, které se mají zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-226">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="cb9d3-227">soubory</span><span class="sxs-lookup"><span data-stu-id="cb9d3-227">files</span></span> 
<span data-ttu-id="cb9d3-228">`<metadata>` `<contentFiles>` Uzel může `<files>` obsahovat uzel jako uzel na `<metadata>`stejné úrovni a podřízená položka v rámci, k určení sestavení a souborů obsahu, které mají být zahrnuty do balíčku. `<package>`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-228">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="cb9d3-229">Podrobnosti najdete v části [zahrnutí souborů sestavení](#including-assembly-files) a [zahrnutí souborů obsahu](#including-content-files) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-229">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="cb9d3-230">Náhradní tokeny</span><span class="sxs-lookup"><span data-stu-id="cb9d3-230">Replacement tokens</span></span>

<span data-ttu-id="cb9d3-231">Při vytváření balíčku `-properties` `.nuspec` `pack` `<metadata>` [ `nuget pack` nahradí příkaz](../reference/cli-reference/cli-ref-pack.md) tokeny $-s oddělovači v uzlu souboru hodnotami, které pocházejí ze souboru projektu nebo přepínače příkazu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-231">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="cb9d3-232">Na příkazovém řádku určíte hodnoty tokenu pomocí `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-232">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="cb9d3-233">Například můžete použít token `$owners$` jako a `$desc$` v `.nuspec` a a zadat hodnoty v době balení následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-233">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="cb9d3-234">Pokud chcete použít hodnoty z projektu, zadejte tokeny popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` `AssemblyInfo.cs` takovém případě nebo `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-234">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="cb9d3-235">Chcete-li použít tyto tokeny, spusťte `nuget pack` se souborem projektu, a ne `.nuspec`pouze.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-235">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="cb9d3-236">Například při použití `$id$` následujícího příkazu jsou tokeny a `$version$` v `.nuspec` souboru nahrazeny hodnotami projektu `AssemblyName` a `AssemblyVersion` :</span><span class="sxs-lookup"><span data-stu-id="cb9d3-236">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="cb9d3-237">Obvykle, když máte projekt, vytvoříte `.nuspec` `nuget spec MyProject.csproj` počáteční, který automaticky obsahuje některé z těchto standardních tokenů.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-237">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="cb9d3-238">Pokud však projekt nemá hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-238">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="cb9d3-239">Pokud navíc změníte hodnoty projektu, nezapomeňte před vytvořením balíčku znovu sestavit. To lze provést pohodlně pomocí `build` přepínače příkazu Pack.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-239">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="cb9d3-240">S výjimkou `$configuration$`jsou hodnoty v projektu použity v předvolbách pro všechny přiřazené ke stejnému tokenu na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-240">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="cb9d3-241">Podpisový</span><span class="sxs-lookup"><span data-stu-id="cb9d3-241">Token</span></span> | <span data-ttu-id="cb9d3-242">Zdroj hodnoty</span><span class="sxs-lookup"><span data-stu-id="cb9d3-242">Value source</span></span> | <span data-ttu-id="cb9d3-243">Value</span><span class="sxs-lookup"><span data-stu-id="cb9d3-243">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="cb9d3-244">**$id $**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-244">**$id$**</span></span> | <span data-ttu-id="cb9d3-245">Soubor projektu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-245">Project file</span></span> | <span data-ttu-id="cb9d3-246">AssemblyName (title) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-246">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="cb9d3-247">**$version $**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-247">**$version$**</span></span> | <span data-ttu-id="cb9d3-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cb9d3-248">AssemblyInfo</span></span> | <span data-ttu-id="cb9d3-249">AssemblyInformationalVersion, pokud je k dispozici, jinak AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="cb9d3-249">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="cb9d3-250">**$author $**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-250">**$author$**</span></span> | <span data-ttu-id="cb9d3-251">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cb9d3-251">AssemblyInfo</span></span> | <span data-ttu-id="cb9d3-252">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="cb9d3-252">AssemblyCompany</span></span> |
| <span data-ttu-id="cb9d3-253">**$title$**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-253">**$title$**</span></span> | <span data-ttu-id="cb9d3-254">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cb9d3-254">AssemblyInfo</span></span> | <span data-ttu-id="cb9d3-255">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="cb9d3-255">AssemblyTitle</span></span> |
| <span data-ttu-id="cb9d3-256">**$description $**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-256">**$description$**</span></span> | <span data-ttu-id="cb9d3-257">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cb9d3-257">AssemblyInfo</span></span> | <span data-ttu-id="cb9d3-258">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="cb9d3-258">AssemblyDescription</span></span> |
| <span data-ttu-id="cb9d3-259">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-259">**$copyright$**</span></span> | <span data-ttu-id="cb9d3-260">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cb9d3-260">AssemblyInfo</span></span> | <span data-ttu-id="cb9d3-261">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="cb9d3-261">AssemblyCopyright</span></span> |
| <span data-ttu-id="cb9d3-262">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-262">**$configuration$**</span></span> | <span data-ttu-id="cb9d3-263">Knihovna DLL sestavení</span><span class="sxs-lookup"><span data-stu-id="cb9d3-263">Assembly DLL</span></span> | <span data-ttu-id="cb9d3-264">Konfigurace použitá pro sestavení sestavení, výchozí nastavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-264">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="cb9d3-265">Všimněte si, že pokud chcete vytvořit balíček pomocí konfigurace vydané verze, vždy `-properties Configuration=Release` použijte příkaz na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-265">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="cb9d3-266">Tokeny lze také použít k překladu cest při zahrnutí [souborů sestavení](#including-assembly-files) a [souborů obsahu](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-266">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="cb9d3-267">Tokeny mají stejné názvy jako vlastnosti MSBuild, což umožňuje vybrat soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-267">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="cb9d3-268">Například pokud v `.nuspec` souboru použijete následující tokeny:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-268">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="cb9d3-269">A sestavíte sestavení, `AssemblyName` jehož `LoggingLibrary` je s `Release` konfigurací `.nuspec` v nástroji MSBuild, výsledné řádky v souboru v balíčku jsou následující:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-269">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="cb9d3-270">Element závislosti</span><span class="sxs-lookup"><span data-stu-id="cb9d3-270">Dependencies element</span></span>

<span data-ttu-id="cb9d3-271">Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvků, které identifikují další balíčky, na kterých závisí balíček nejvyšší úrovně. `<dependencies>`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-271">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="cb9d3-272">Atributy pro každý `<dependency>` z nich jsou následující:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-272">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="cb9d3-273">Atribut</span><span class="sxs-lookup"><span data-stu-id="cb9d3-273">Attribute</span></span> | <span data-ttu-id="cb9d3-274">Popis</span><span class="sxs-lookup"><span data-stu-id="cb9d3-274">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="cb9d3-275">Požadovanou ID balíčku závislosti, například "EntityFramework" a "NUnit", což je název balíčku nuget.org zobrazený na stránce balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-275">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="cb9d3-276">Požadovanou Rozsah verzí, které jsou přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-276">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="cb9d3-277">Přesnou syntaxi najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-277">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="cb9d3-278">include</span><span class="sxs-lookup"><span data-stu-id="cb9d3-278">include</span></span> | <span data-ttu-id="cb9d3-279">Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, kterou chcete zahrnout do finálního balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-279">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="cb9d3-280">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-280">The default value is `all`.</span></span> |
| <span data-ttu-id="cb9d3-281">exclude</span><span class="sxs-lookup"><span data-stu-id="cb9d3-281">exclude</span></span> | <span data-ttu-id="cb9d3-282">Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, která se má vyloučit v konečném balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-282">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="cb9d3-283">Výchozí hodnota je `build,analyzers` , která může být přepsána.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-283">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="cb9d3-284">Ale `content/ ContentFiles` jsou také implicitně vyloučené v konečném balíčku, který nelze přepsat.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-284">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="cb9d3-285">Zadané značky s `exclude` prioritou mají přednost před hodnotami určenými pomocí. `include`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-285">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="cb9d3-286">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-286">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="cb9d3-287">Značka include/Exclude</span><span class="sxs-lookup"><span data-stu-id="cb9d3-287">Include/Exclude tag</span></span> | <span data-ttu-id="cb9d3-288">Ovlivněné složky v cíli</span><span class="sxs-lookup"><span data-stu-id="cb9d3-288">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="cb9d3-289">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="cb9d3-289">contentFiles</span></span> | <span data-ttu-id="cb9d3-290">Obsah</span><span class="sxs-lookup"><span data-stu-id="cb9d3-290">Content</span></span> |
| <span data-ttu-id="cb9d3-291">modul runtime</span><span class="sxs-lookup"><span data-stu-id="cb9d3-291">runtime</span></span> | <span data-ttu-id="cb9d3-292">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="cb9d3-292">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="cb9d3-293">sestavení</span><span class="sxs-lookup"><span data-stu-id="cb9d3-293">compile</span></span> | <span data-ttu-id="cb9d3-294">Knihovna</span><span class="sxs-lookup"><span data-stu-id="cb9d3-294">lib</span></span> |
| <span data-ttu-id="cb9d3-295">sestavení</span><span class="sxs-lookup"><span data-stu-id="cb9d3-295">build</span></span> | <span data-ttu-id="cb9d3-296">Build (MSBuild props and targets)</span><span class="sxs-lookup"><span data-stu-id="cb9d3-296">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="cb9d3-297">nativní</span><span class="sxs-lookup"><span data-stu-id="cb9d3-297">native</span></span> | <span data-ttu-id="cb9d3-298">nativní</span><span class="sxs-lookup"><span data-stu-id="cb9d3-298">native</span></span> |
| <span data-ttu-id="cb9d3-299">žádná</span><span class="sxs-lookup"><span data-stu-id="cb9d3-299">none</span></span> | <span data-ttu-id="cb9d3-300">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="cb9d3-300">No folders</span></span> |
| <span data-ttu-id="cb9d3-301">všechny</span><span class="sxs-lookup"><span data-stu-id="cb9d3-301">all</span></span> | <span data-ttu-id="cb9d3-302">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="cb9d3-302">All folders</span></span> |

<span data-ttu-id="cb9d3-303">Například následující řádky označují závislosti `PackageA` verze 1.1.0 nebo vyšší a `PackageB` verze 1. x.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-303">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="cb9d3-304">Následující řádky označují závislosti pro stejné balíčky, `contentFiles` ale určují, že se mají zahrnout složky `build` `PackageA` a a všechno, ale `native` složky `PackageB`a `compile` .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-304">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="cb9d3-305">Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`jsou závislosti, které existují v tomto projektu, automaticky zahrnuty ve výsledném `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-305">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="cb9d3-306">Skupiny závislostí</span><span class="sxs-lookup"><span data-stu-id="cb9d3-306">Dependency groups</span></span>

<span data-ttu-id="cb9d3-307">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="cb9d3-307">*Version 2.0+*</span></span>

<span data-ttu-id="cb9d3-308">Jako alternativu k jednomu nestrukturovanému seznamu lze závislosti zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci. `<dependencies>`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-308">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="cb9d3-309">Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` prvků.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-309">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="cb9d3-310">Tyto závislosti jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-310">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="cb9d3-311">`<group>` Prvek`targetFramework` bez atributu je použit jako výchozí nebo záložní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-311">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="cb9d3-312">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-312">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="cb9d3-313">Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-313">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="cb9d3-314">Následující příklad ukazuje různé varianty `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-314">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="cb9d3-315">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="cb9d3-315">Explicit assembly references</span></span>

<span data-ttu-id="cb9d3-316">Element je používán projekty pomocí `packages.config` k explicitnímu určení sestavení, na které by měl cílový projekt odkazovat při použití balíčku. `<references>`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-316">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="cb9d3-317">Explicitní odkazy jsou obvykle používány pro sestavení pouze v době návrhu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-317">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="cb9d3-318">Další informace naleznete na stránce věnované [výběru sestavení odkazovaných projekty](../create-packages/select-assemblies-referenced-by-projects.md) , kde najdete další informace.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-318">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="cb9d3-319">Například následující `<references>` element instruuje NuGet, aby přidal odkazy pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že jsou v balíčku k dispozici další sestavení:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-319">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="cb9d3-320">Referenční skupiny</span><span class="sxs-lookup"><span data-stu-id="cb9d3-320">Reference groups</span></span>

<span data-ttu-id="cb9d3-321">Jako alternativu k jednomu nestrukturovanému seznamu lze odkazy zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci. `<references>`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-321">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="cb9d3-322">Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<reference>` prvků.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-322">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="cb9d3-323">Tyto odkazy jsou přidány do projektu, pokud je cílová architektura kompatibilní s profilem rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-323">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="cb9d3-324">`<group>` Prvek`targetFramework` bez atributu je použit jako výchozí nebo záložní seznam odkazů.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-324">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="cb9d3-325">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-325">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="cb9d3-326">Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-326">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="cb9d3-327">Následující příklad ukazuje různé varianty `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-327">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="cb9d3-328">Odkazy na sestavení rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cb9d3-328">Framework assembly references</span></span>

<span data-ttu-id="cb9d3-329">Sestavení rozhraní jsou ta, která jsou součástí rozhraní .NET Framework a měla by již být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-329">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="cb9d3-330">Díky identifikaci těchto sestavení v rámci `<frameworkAssemblies>` elementu může balíček zajistit, aby byly do projektu přidány požadované odkazy v případě, že projekt nemá takové odkazy již.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-330">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="cb9d3-331">Taková sestavení samozřejmě nejsou součástí balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-331">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="cb9d3-332">Element obsahuje nula nebo více `<frameworkAssembly>` elementů, z nichž každý určuje následující atributy: `<frameworkAssemblies>`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-332">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="cb9d3-333">Atribut</span><span class="sxs-lookup"><span data-stu-id="cb9d3-333">Attribute</span></span> | <span data-ttu-id="cb9d3-334">Popis</span><span class="sxs-lookup"><span data-stu-id="cb9d3-334">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb9d3-335">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-335">**assemblyName**</span></span> | <span data-ttu-id="cb9d3-336">Požadovanou Plně kvalifikovaný název sestavení.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-336">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="cb9d3-337">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-337">**targetFramework**</span></span> | <span data-ttu-id="cb9d3-338">Volitelné Určuje cílovou architekturu, na kterou se vztahuje tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-338">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="cb9d3-339">Je-li tento parametr vynechán, znamená to, že odkaz se vztahuje na všechna rozhraní.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-339">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="cb9d3-340">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="cb9d3-340">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="cb9d3-341">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové rozhraní a odkaz na `System.ServiceModel` pro .NET Framework 4,0:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-341">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="cb9d3-342">Zahrnutí souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="cb9d3-342">Including assembly files</span></span>

<span data-ttu-id="cb9d3-343">Pokud budete postupovat podle konvencí popsaných v [tématu Vytvoření balíčku](../create-packages/creating-a-package.md), nemusíte explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-343">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="cb9d3-344">`nuget pack` Příkaz automaticky vybere potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-344">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="cb9d3-345">Když je balíček nainstalován do projektu, NuGet automaticky přidá odkazy na sestavení do knihoven DLL balíčku, *kromě* těch, které jsou pojmenovány `.resources.dll` , protože se předpokládá, že jsou lokalizovaná satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-345">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="cb9d3-346">Z tohoto důvodu `.resources.dll` nepoužívejte pro soubory, které jinak obsahují základní kód balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-346">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="cb9d3-347">Chcete-li obejít toto automatické chování a explicitně řídit, které soubory jsou součástí balíčku, `<files>` umístěte prvek jako `<package>` podřízený objekt `<metadata>`(a na stejné místo) a Identifikujte každý soubor samostatným `<file>` prvkem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-347">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="cb9d3-348">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-348">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="cb9d3-349">S NuGet 2. x a starším a projekty, `packages.config`které `<files>` používají, se element používá také k zahrnutí neměnných souborů obsahu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-349">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="cb9d3-350">S NuGet 3.3 + a projekty PackageReference `<contentFiles>` se místo toho použije element.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-350">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="cb9d3-351">Podrobnosti najdete v části [zahrnutí souborů obsahu](#including-content-files) níže.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-351">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="cb9d3-352">Atributy elementu souboru</span><span class="sxs-lookup"><span data-stu-id="cb9d3-352">File element attributes</span></span>

<span data-ttu-id="cb9d3-353">Každý `<file>` prvek určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-353">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="cb9d3-354">Atribut</span><span class="sxs-lookup"><span data-stu-id="cb9d3-354">Attribute</span></span> | <span data-ttu-id="cb9d3-355">Popis</span><span class="sxs-lookup"><span data-stu-id="cb9d3-355">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb9d3-356">**src**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-356">**src**</span></span> | <span data-ttu-id="cb9d3-357">Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-357">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="cb9d3-358">Cesta je relativní vzhledem k `.nuspec` souboru, pokud není zadána absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-358">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="cb9d3-359">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-359">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cb9d3-360">**cílové**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-360">**target**</span></span> | <span data-ttu-id="cb9d3-361">Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které `lib`musí začínat `build`na, `content`, nebo `tools`.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-361">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="cb9d3-362">Viz [vytvoření. nuspec z pracovního adresáře založeného na konvencích](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-362">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="cb9d3-363">**slevy**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-363">**exclude**</span></span> | <span data-ttu-id="cb9d3-364">Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, `src` jsou odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-364">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="cb9d3-365">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-365">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="cb9d3-366">Příklady</span><span class="sxs-lookup"><span data-stu-id="cb9d3-366">Examples</span></span>

<span data-ttu-id="cb9d3-367">**Jedno sestavení**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-367">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="cb9d3-368">**Samostatné sestavení specifické pro cílovou architekturu**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-368">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="cb9d3-369">**Sada knihoven DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-369">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="cb9d3-370">**Knihovny DLL pro různé architektury**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-370">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="cb9d3-371">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-371">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="cb9d3-372">Zahrnutí souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-372">Including content files</span></span>

<span data-ttu-id="cb9d3-373">Soubory obsahu jsou neměnné soubory, které musí balíček zahrnout do projektu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-373">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="cb9d3-374">Neměnné, nejsou určeny pro úpravy nenáročným projektem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-374">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="cb9d3-375">Mezi příklady souborů obsahu patří:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-375">Example content files include:</span></span>

- <span data-ttu-id="cb9d3-376">Obrázky, které jsou vložené jako prostředky</span><span class="sxs-lookup"><span data-stu-id="cb9d3-376">Images that are embedded as resources</span></span>
- <span data-ttu-id="cb9d3-377">Zdrojové soubory, které jsou již kompilovány</span><span class="sxs-lookup"><span data-stu-id="cb9d3-377">Source files that are already compiled</span></span>
- <span data-ttu-id="cb9d3-378">Skripty, které je potřeba zahrnout do výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-378">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="cb9d3-379">Konfigurační soubory balíčku, které je potřeba zahrnout do projektu, ale nevyžadují žádné změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="cb9d3-379">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="cb9d3-380">Soubory obsahu jsou zahrnuty v balíčku pomocí `<files>` elementu a `content` určení složky v `target` atributu.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-380">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="cb9d3-381">Nicméně tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který místo toho používá `<contentFiles>` element.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-381">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="cb9d3-382">Pro maximální kompatibilitu s spotřebou projektů balíček v ideálním případě Určuje soubory obsahu v obou prvcích.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-382">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="cb9d3-383">Použití elementu Files pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-383">Using the files element for content files</span></span>

<span data-ttu-id="cb9d3-384">Pro soubory obsahu stačí použít stejný formát jako u souborů sestavení, ale určete `content` jako základní složku `target` v atributu, jak je znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-384">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="cb9d3-385">**Základní soubory obsahu**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-385">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="cb9d3-386">**Soubory obsahu s adresářovou strukturou**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-386">**Content files with directory structure**</span></span>

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

<span data-ttu-id="cb9d3-387">**Soubor obsahu specifický pro cílovou architekturu**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-387">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="cb9d3-388">**Soubor obsahu byl zkopírován do složky s tečkou v názvu**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-388">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="cb9d3-389">V takovém případě NuGet zjistí, že rozšíření v `target` neodpovídá rozšíření v `src` nástroji, a proto zpracovává tuto `target` část názvu jako složku:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-389">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="cb9d3-390">**Soubory obsahu bez rozšíření**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-390">**Content files without extensions**</span></span>

<span data-ttu-id="cb9d3-391">Chcete-li zahrnout soubory bez přípony, použijte `*` zástupné znaky nebo `**` :</span><span class="sxs-lookup"><span data-stu-id="cb9d3-391">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="cb9d3-392">**Soubory obsahu s hlubokým umístěním a hlubokou cílovou cestou**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-392">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="cb9d3-393">V tomto případě předpokládá, že vzhledem k příponám souborů ve zdrojové a cílové shodě NuGet předpokládá, že cílem je název souboru, a ne složka:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-393">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="cb9d3-394">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-394">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="cb9d3-395">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-395">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="cb9d3-396">Použití elementu contentFiles pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="cb9d3-396">Using the contentFiles element for content files</span></span>

<span data-ttu-id="cb9d3-397">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="cb9d3-397">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="cb9d3-398">Ve výchozím nastavení balíček umístí obsah do `contentFiles` složky (viz níže) a `nuget pack` zahrne všechny soubory v této složce s použitím výchozích atributů.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-398">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="cb9d3-399">V takovém případě není nutné zahrnout `contentFiles` uzel `.nuspec` do.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-399">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="cb9d3-400">Chcete-li určit, které soubory jsou `<contentFiles>` zahrnuty, prvek určuje `<files>` kolekci prvků, které identifikují přesné soubory.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-400">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="cb9d3-401">Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-401">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="cb9d3-402">Atribut</span><span class="sxs-lookup"><span data-stu-id="cb9d3-402">Attribute</span></span> | <span data-ttu-id="cb9d3-403">Popis</span><span class="sxs-lookup"><span data-stu-id="cb9d3-403">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cb9d3-404">**include**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-404">**include**</span></span> | <span data-ttu-id="cb9d3-405">Požadovanou Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-405">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="cb9d3-406">Cesta je relativní vzhledem k `.nuspec` souboru, pokud není zadána absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-406">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="cb9d3-407">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-407">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cb9d3-408">**slevy**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-408">**exclude**</span></span> | <span data-ttu-id="cb9d3-409">Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, `src` jsou odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-409">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="cb9d3-410">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-410">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="cb9d3-411">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-411">**buildAction**</span></span> | <span data-ttu-id="cb9d3-412">Akce sestavení, která má být přiřazena položce obsahu pro `Content`MSBuild, jako například `Embedded Resource`, `None` `Compile`,, atd. Výchozí hodnota je `Compile`.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-412">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="cb9d3-413">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-413">**copyToOutput**</span></span> | <span data-ttu-id="cb9d3-414">Logická hodnota označující, zda se mají kopírovat položky obsahu do výstupní složky Build (nebo Publishing).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-414">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="cb9d3-415">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-415">The default is false.</span></span> |
| <span data-ttu-id="cb9d3-416">**Flatten**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-416">**flatten**</span></span> | <span data-ttu-id="cb9d3-417">Logická hodnota označující, zda se mají kopírovat položky obsahu do jediné složky ve výstupu sestavení (true), nebo pro zachování struktury složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-417">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="cb9d3-418">Tento příznak funguje pouze v případě, že příznak copyToOutput je nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-418">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="cb9d3-419">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-419">The default is false.</span></span> |

<span data-ttu-id="cb9d3-420">Při instalaci balíčku NuGet aplikuje podřízené prvky `<contentFiles>` od shora dolů.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-420">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="cb9d3-421">Pokud se stejný soubor shoduje s více položkami, uplatní se všechny položky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-421">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="cb9d3-422">Pokud dojde ke konfliktu pro stejný atribut, přepíše položka nejvyšší úrovně nižší položky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-422">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="cb9d3-423">Struktura složky balíčku</span><span class="sxs-lookup"><span data-stu-id="cb9d3-423">Package folder structure</span></span>

<span data-ttu-id="cb9d3-424">Projekt balíčku by měl strukturovat obsah pomocí následujícího vzoru:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-424">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="cb9d3-425">`codeLanguages`může to `cs`být `vb`, `fs` ,`any`, nebo malý ekvivalent daného`$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-425">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="cb9d3-426">`TxM`je libovolný moniker platného cílového rozhraní, který podporuje NuGet (viz [cílové architektury](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="cb9d3-426">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="cb9d3-427">Ke konci této syntaxe může být připojena jakákoli struktura složky.</span><span class="sxs-lookup"><span data-stu-id="cb9d3-427">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="cb9d3-428">Příklad:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-428">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="cb9d3-429">Prázdné složky se můžou `.` použít k odhlášení o poskytování obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-429">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="cb9d3-430">Příklad oddílu contentFiles</span><span class="sxs-lookup"><span data-stu-id="cb9d3-430">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="cb9d3-431">Příklady souborů nuspec</span><span class="sxs-lookup"><span data-stu-id="cb9d3-431">Example nuspec files</span></span>

<span data-ttu-id="cb9d3-432">**Jednoduchá `.nuspec` , která neurčuje závislosti nebo soubory**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-432">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="cb9d3-433">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-433">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="cb9d3-434">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-434">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="cb9d3-435">**A `.nuspec` se sestaveními architektury**</span><span class="sxs-lookup"><span data-stu-id="cb9d3-435">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="cb9d3-436">V tomto příkladu jsou nainstalovány následující pro konkrétní cíle projektu:</span><span class="sxs-lookup"><span data-stu-id="cb9d3-436">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="cb9d3-437">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-437">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="cb9d3-438">. Profil klienta NET4 – >`System.Net`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-438">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="cb9d3-439">Silverlight 3 – >`System.Json`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-439">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="cb9d3-440">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="cb9d3-440">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
