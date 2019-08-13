---
title: Odkaz na soubor. nuspec pro NuGet
description: Soubor. nuspec obsahuje metadata balíčku, která se používají při sestavování balíčku a poskytování informací pro uživatele balíčku.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 67bc95135f746c4a4685773808756df399cbf01e
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959707"
---
# <a name="nuspec-reference"></a><span data-ttu-id="a016d-103">odkaz. nuspec</span><span class="sxs-lookup"><span data-stu-id="a016d-103">.nuspec reference</span></span>

<span data-ttu-id="a016d-104">`.nuspec` Soubor je manifest XML, který obsahuje metadata balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="a016d-105">Tento manifest slouží k sestavení balíčku a k poskytování informací pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="a016d-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="a016d-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="a016d-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="a016d-107">In this topic:</span></span>

- [<span data-ttu-id="a016d-108">Obecné formuláře a schéma</span><span class="sxs-lookup"><span data-stu-id="a016d-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="a016d-109">[Náhradní tokeny](#replacement-tokens) (při použití s projektem sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="a016d-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="a016d-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="a016d-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="a016d-111">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="a016d-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="a016d-112">Odkazy na sestavení rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a016d-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="a016d-113">Zahrnutí souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="a016d-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="a016d-114">Zahrnutí souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="a016d-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="a016d-115">Příklady souborů nuspec</span><span class="sxs-lookup"><span data-stu-id="a016d-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="a016d-116">Kompatibilita typů projektu</span><span class="sxs-lookup"><span data-stu-id="a016d-116">Project type compatibility</span></span>

- <span data-ttu-id="a016d-117">Použijte `.nuspec` `packages.config`s `nuget.exe pack` pro projekty, které nejsou ve stylu sady SDK, které používají.</span><span class="sxs-lookup"><span data-stu-id="a016d-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="a016d-118">Soubor není vyžadován k vytváření balíčků pro projekty ve [stylu sady SDK](../resources/check-project-format.md) (obvykle se jedná o projekty .NET Core a .NET Standard, které používají [atribut SDK](/dotnet/core/tools/csproj#additions)). `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="a016d-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="a016d-119">(Všimněte si, `.nuspec` že se generuje při vytváření balíčku.)</span><span class="sxs-lookup"><span data-stu-id="a016d-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="a016d-120">Pokud `dotnet.exe pack` vytváříte balíček pomocí nebo `msbuild pack target`, doporučujeme místo toho [Zahrnout všechny](../reference/msbuild-targets.md#pack-target) `.nuspec` vlastnosti, které jsou obvykle v souboru v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="a016d-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="a016d-121">Místo toho se ale můžete rozhodnout [použít `.nuspec` soubor k `dotnet.exe` balení pomocí `msbuild pack target`nebo ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="a016d-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="a016d-122">Pro projekty migrované z `packages.config` aplikace do `.nuspec` [PackageReference](../consume-packages/package-references-in-project-files.md) není pro vytvoření balíčku vyžadován soubor.</span><span class="sxs-lookup"><span data-stu-id="a016d-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="a016d-123">Místo toho použijte [MSBuild-t:Pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="a016d-123">Instead, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="a016d-124">Obecné formuláře a schéma</span><span class="sxs-lookup"><span data-stu-id="a016d-124">General form and schema</span></span>

<span data-ttu-id="a016d-125">Aktuální `nuspec.xsd` soubor schématu najdete v [úložišti GitHub NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="a016d-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="a016d-126">V rámci tohoto schématu `.nuspec` má soubor následující obecný tvar:</span><span class="sxs-lookup"><span data-stu-id="a016d-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="a016d-127">V případě jasné vizuální reprezentace schématu otevřete soubor schématu v aplikaci Visual Studio v režimu návrhu a klikněte na odkaz **Průzkumník schémat XML** .</span><span class="sxs-lookup"><span data-stu-id="a016d-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="a016d-128">Případně soubor otevřete jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **Zobrazit Průzkumníka schémat XML**.</span><span class="sxs-lookup"><span data-stu-id="a016d-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="a016d-129">Jak můžete vidět následující pohled (Pokud je převážně rozbalený):</span><span class="sxs-lookup"><span data-stu-id="a016d-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Průzkumník schémat sady Visual Studio s otevřeným nuspec. xsd](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="a016d-131">Požadované prvky metadat</span><span class="sxs-lookup"><span data-stu-id="a016d-131">Required metadata elements</span></span>

<span data-ttu-id="a016d-132">I když následující prvky jsou minimální požadavky na balíček, měli byste zvážit přidání [volitelných prvků metadat](#optional-metadata-elements) pro zlepšení celkového prostředí, které vývojáři mají s vaším balíčkem.</span><span class="sxs-lookup"><span data-stu-id="a016d-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="a016d-133">Tyto prvky se musí objevit v `<metadata>` rámci elementu.</span><span class="sxs-lookup"><span data-stu-id="a016d-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="a016d-134">id</span><span class="sxs-lookup"><span data-stu-id="a016d-134">id</span></span> 
<span data-ttu-id="a016d-135">Identifikátor balíčku bez rozlišení velkých a malých písmen, který musí být jedinečný v rámci nuget.org nebo jakákoli galerie, v níž se balíček nachází.</span><span class="sxs-lookup"><span data-stu-id="a016d-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="a016d-136">ID nesmí obsahovat mezery ani znaky, které nejsou platné pro adresu URL a obecně následují pravidla oboru názvů .NET.</span><span class="sxs-lookup"><span data-stu-id="a016d-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="a016d-137">Pokyny najdete v tématu [Volba jedinečného identifikátoru balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="a016d-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="a016d-138">verze</span><span class="sxs-lookup"><span data-stu-id="a016d-138">version</span></span>
<span data-ttu-id="a016d-139">Verze balíčku, podle vzoru *hlavní_verze. podverze. Oprava* .</span><span class="sxs-lookup"><span data-stu-id="a016d-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="a016d-140">Čísla verzí můžou obsahovat příponu předběžné verze, jak je popsáno v tématu [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="a016d-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="a016d-141">description</span><span class="sxs-lookup"><span data-stu-id="a016d-141">description</span></span>
<span data-ttu-id="a016d-142">Dlouhý popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a016d-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="a016d-143">Autoři</span><span class="sxs-lookup"><span data-stu-id="a016d-143">authors</span></span>
<span data-ttu-id="a016d-144">Čárkami oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazí v galerii NuGet na nuget.org a používají se pro balíčky křížového odkazu stejnými autory.</span><span class="sxs-lookup"><span data-stu-id="a016d-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="a016d-145">Volitelné prvky metadat</span><span class="sxs-lookup"><span data-stu-id="a016d-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="a016d-146">vlastníka</span><span class="sxs-lookup"><span data-stu-id="a016d-146">owners</span></span>
<span data-ttu-id="a016d-147">Čárkami oddělený seznam tvůrců balíčků s použitím názvů profilů v nuget.org. Často se jedná o stejný seznam jako v `authors`a při nahrávání balíčku do NuGet.org se ignoruje. Viz [Správa vlastníků balíčků na NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="a016d-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="a016d-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="a016d-148">projectUrl</span></span>
<span data-ttu-id="a016d-149">Adresa URL domovské stránky balíčku, která se často zobrazuje v uživatelském rozhraní, a také nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a016d-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="a016d-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="a016d-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="a016d-151">licenseUrl se už nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="a016d-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="a016d-152">Místo toho použijte licenci.</span><span class="sxs-lookup"><span data-stu-id="a016d-152">Use license instead.</span></span>

<span data-ttu-id="a016d-153">Adresa URL licence balíčku, která se často zobrazuje v uživatelská rozhraní jako nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a016d-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="a016d-154">průkaz</span><span class="sxs-lookup"><span data-stu-id="a016d-154">license</span></span>
<span data-ttu-id="a016d-155">SPDX licenční výraz nebo cesta k souboru s licencí v balíčku, který se často zobrazuje v uživatelská rozhraní jako nuget.org. Pokud je balíček licencován v rámci společné licence, jako je například MIT nebo BSD-2, použijte přidružený [identifikátor licence SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="a016d-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="a016d-156">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a016d-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="a016d-157">NuGet.org akceptuje pouze licenční výrazy, které jsou schváleny v rámci iniciativy Open Source nebo Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="a016d-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="a016d-158">Pokud je váš balíček licencován více běžnými licencemi, můžete zadat složenou licenci pomocí [syntaxe výrazu SPDX verze 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="a016d-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="a016d-159">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a016d-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="a016d-160">Pokud používáte vlastní licenci, která není podporovaná výrazy licence, můžete zabalit `.txt` soubor nebo `.md` soubor s textem licence.</span><span class="sxs-lookup"><span data-stu-id="a016d-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="a016d-161">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a016d-161">For example:</span></span>

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

<span data-ttu-id="a016d-162">V případě ekvivalentu MSBuild si prohlédněte [balení licenčního výrazu nebo souboru s licencí](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="a016d-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="a016d-163">Přesná Syntaxe výrazů s licenčními výrazy NuGet je popsaná níže v tématu [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="a016d-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="a016d-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="a016d-164">iconUrl</span></span>
<span data-ttu-id="a016d-165">Adresa URL 64 × 64 obrázku s pozadím průhlednosti, která se má použít jako ikona balíčku v zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a016d-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="a016d-166">Ujistěte se, že tento prvek obsahuje *adresu URL přímého obrázku* , a ne adresu URL webové stránky, která obsahuje obrázek.</span><span class="sxs-lookup"><span data-stu-id="a016d-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="a016d-167">Pokud například chcete použít image z GitHubu, použijte adresu URL nezpracovaného souboru <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>jako.</span><span class="sxs-lookup"><span data-stu-id="a016d-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="a016d-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a016d-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="a016d-169">Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="a016d-170">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="a016d-170">developmentDependency</span></span>
<span data-ttu-id="a016d-171">*(2.8+)* Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="a016d-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="a016d-172">Pomocí PackageReference (NuGet 4,8 +) Tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace.</span><span class="sxs-lookup"><span data-stu-id="a016d-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="a016d-173">Viz [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="a016d-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="a016d-174">souhrn</span><span class="sxs-lookup"><span data-stu-id="a016d-174">summary</span></span>
<span data-ttu-id="a016d-175">Krátký popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a016d-175">A short description of the package for UI display.</span></span> <span data-ttu-id="a016d-176">`description` Je-li tento parametr vynechán, je použita zkrácená verze nástroje.</span><span class="sxs-lookup"><span data-stu-id="a016d-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="a016d-177">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="a016d-177">releaseNotes</span></span>
<span data-ttu-id="a016d-178">*(1.5+)* Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="a016d-179">Úprava</span><span class="sxs-lookup"><span data-stu-id="a016d-179">copyright</span></span>
<span data-ttu-id="a016d-180">*(1.5+)* Copyright podrobnosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="a016d-181">jazyk</span><span class="sxs-lookup"><span data-stu-id="a016d-181">language</span></span>
<span data-ttu-id="a016d-182">ID národního prostředí balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-182">The locale ID for the package.</span></span> <span data-ttu-id="a016d-183">Viz [vytváření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a016d-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="a016d-184">značky</span><span class="sxs-lookup"><span data-stu-id="a016d-184">tags</span></span>
<span data-ttu-id="a016d-185">Mezerou oddělený seznam značek a klíčových slov, které popisují balíček a pomáhají zjistit balíčky pomocí vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="a016d-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="a016d-186">serviceable</span><span class="sxs-lookup"><span data-stu-id="a016d-186">serviceable</span></span> 
<span data-ttu-id="a016d-187">*(3.3+)* Pouze pro interní NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="a016d-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="a016d-188">úložiště</span><span class="sxs-lookup"><span data-stu-id="a016d-188">repository</span></span>
<span data-ttu-id="a016d-189">Metadata úložiště sestávající ze čtyř volitelných atributů: `type` a `url` *(4.0 +)* a `branch` a `commit` *(4.6 +)* .</span><span class="sxs-lookup"><span data-stu-id="a016d-189">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="a016d-190">Tyto atributy umožňují mapování `.nupkg` na úložiště, které ho vytvořilo, s potenciálem, který se má považovat za název jednotlivé větve a/nebo na potvrzení hodnoty hash SHA-1, která balíček vytvořila.</span><span class="sxs-lookup"><span data-stu-id="a016d-190">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="a016d-191">Měla by to být veřejně dostupná adresa URL, kterou lze vyvolat přímo pomocí softwaru pro správu verzí.</span><span class="sxs-lookup"><span data-stu-id="a016d-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="a016d-192">Neměla by se jednat o stránku HTML, která je určena pro daný počítač.</span><span class="sxs-lookup"><span data-stu-id="a016d-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="a016d-193">Pro odkazování na stránku projektu použijte `projectUrl` místo toho pole.</span><span class="sxs-lookup"><span data-stu-id="a016d-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="a016d-194">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a016d-194">For example:</span></span>
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

#### <a name="title"></a><span data-ttu-id="a016d-195">název</span><span class="sxs-lookup"><span data-stu-id="a016d-195">title</span></span>
<span data-ttu-id="a016d-196">Popisný název balíčku, který se dá použít v některých zobrazeních uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a016d-196">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="a016d-197">(nuget.org a správce balíčků v aplikaci Visual Studio nezobrazuje název)</span><span class="sxs-lookup"><span data-stu-id="a016d-197">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="a016d-198">Prvky kolekce</span><span class="sxs-lookup"><span data-stu-id="a016d-198">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="a016d-199">packageTypes</span><span class="sxs-lookup"><span data-stu-id="a016d-199">packageTypes</span></span>
<span data-ttu-id="a016d-200">*(3.5 +)* Kolekce nula nebo více `<packageType>` prvků určující typ balíčku, pokud je jiný než tradiční balíček závislostí.</span><span class="sxs-lookup"><span data-stu-id="a016d-200">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="a016d-201">Každý packageType má atributy *názvu* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="a016d-201">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="a016d-202">Viz [Nastavení typu balíčku](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="a016d-202">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="a016d-203">závislosti</span><span class="sxs-lookup"><span data-stu-id="a016d-203">dependencies</span></span>
<span data-ttu-id="a016d-204">Kolekce nula nebo více `<dependency>` prvků, které určují závislosti pro balíček.</span><span class="sxs-lookup"><span data-stu-id="a016d-204">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="a016d-205">Každá závislost má atributy *ID*, *verze*, *include* (3. x +) a *Exclude* (3. x +).</span><span class="sxs-lookup"><span data-stu-id="a016d-205">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="a016d-206">Viz [závislosti](#dependencies-element) níže.</span><span class="sxs-lookup"><span data-stu-id="a016d-206">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="a016d-207">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a016d-207">frameworkAssemblies</span></span>
<span data-ttu-id="a016d-208">*(1,2 +)* Kolekce nula nebo více `<frameworkAssembly>` prvků, které identifikují .NET Framework odkazy na sestavení, které tento balíček vyžaduje, což zajistí přidání odkazů do projektů, které balíček spotřebovává.</span><span class="sxs-lookup"><span data-stu-id="a016d-208">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="a016d-209">Každý frameworkAssembly má atributy *AssemblyName* a *targetFramework* .</span><span class="sxs-lookup"><span data-stu-id="a016d-209">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="a016d-210">Viz [určení sestavení rozhraní odkazy v mezipaměti GAC](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="a016d-210">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="a016d-211">odkazy</span><span class="sxs-lookup"><span data-stu-id="a016d-211">references</span></span>
<span data-ttu-id="a016d-212">*(1,5 +)* Kolekce nula nebo více `<reference>` prvků pojmenování sestavení ve `lib` složce balíčku, které jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="a016d-212">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="a016d-213">Každý odkaz má atribut *File* .</span><span class="sxs-lookup"><span data-stu-id="a016d-213">Each reference has a *file* attribute.</span></span> <span data-ttu-id="a016d-214">`<references>`může také obsahovat `<group>` element s atributem *targetFramework* , který pak obsahuje `<reference>` prvky.</span><span class="sxs-lookup"><span data-stu-id="a016d-214">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="a016d-215">Pokud tento parametr vynecháte, `lib` jsou zahrnuty všechny odkazy v nástroji.</span><span class="sxs-lookup"><span data-stu-id="a016d-215">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="a016d-216">Viz [zadání explicitních odkazů na sestavení](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="a016d-216">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="a016d-217">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a016d-217">contentFiles</span></span>
<span data-ttu-id="a016d-218">*(3.3 +)* Kolekce `<files>` prvků, které identifikují soubory obsahu, které mají být zahrnuty do náročného projektu.</span><span class="sxs-lookup"><span data-stu-id="a016d-218">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="a016d-219">Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu.</span><span class="sxs-lookup"><span data-stu-id="a016d-219">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="a016d-220">Viz [Určení souborů, které se mají zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="a016d-220">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="a016d-221">soubory</span><span class="sxs-lookup"><span data-stu-id="a016d-221">files</span></span> 
<span data-ttu-id="a016d-222">`<metadata>` `<contentFiles>` Uzel může `<files>` obsahovat uzel jako uzel na `<metadata>`stejné úrovni a podřízená položka v rámci, k určení sestavení a souborů obsahu, které mají být zahrnuty do balíčku. `<package>`</span><span class="sxs-lookup"><span data-stu-id="a016d-222">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="a016d-223">Podrobnosti najdete v části [zahrnutí souborů sestavení](#including-assembly-files) a [zahrnutí souborů obsahu](#including-content-files) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="a016d-223">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="a016d-224">atributy metadat</span><span class="sxs-lookup"><span data-stu-id="a016d-224">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="a016d-225">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="a016d-225">minClientVersion</span></span>
<span data-ttu-id="a016d-226">Určuje minimální verzi klienta NuGet, která může nainstalovat tento balíček, který vynutila NuGet. exe a správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a016d-226">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="a016d-227">Tato funkce se používá vždy, když balíček závisí na konkrétních funkcích `.nuspec` souboru, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="a016d-227">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="a016d-228">Například balíček, který používá `developmentDependency` atribut, by měl pro `minClientVersion`použít hodnotu "2,8".</span><span class="sxs-lookup"><span data-stu-id="a016d-228">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="a016d-229">Podobně balíček, který používá `contentFiles` element (viz další oddíl), by měl být nastaven `minClientVersion` na "3,3".</span><span class="sxs-lookup"><span data-stu-id="a016d-229">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="a016d-230">Všimněte si také, že vzhledem k tomu, že klienti NuGet starší než 2,5 nerozpoznávají tento příznak, *vždy* zamítnou instalaci balíčku bez `minClientVersion` ohledu na to, co obsahuje.</span><span class="sxs-lookup"><span data-stu-id="a016d-230">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="a016d-231">Náhradní tokeny</span><span class="sxs-lookup"><span data-stu-id="a016d-231">Replacement tokens</span></span>

<span data-ttu-id="a016d-232">Při vytváření balíčku `-properties` `.nuspec` `pack` `<metadata>` [ `nuget pack` nahradí příkaz](../reference/cli-reference/cli-ref-pack.md) tokeny $-s oddělovači v uzlu souboru hodnotami, které pocházejí ze souboru projektu nebo přepínače příkazu.</span><span class="sxs-lookup"><span data-stu-id="a016d-232">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="a016d-233">Na příkazovém řádku určíte hodnoty tokenu pomocí `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="a016d-233">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="a016d-234">Například můžete použít token `$owners$` jako a `$desc$` v `.nuspec` a a zadat hodnoty v době balení následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a016d-234">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="a016d-235">Pokud chcete použít hodnoty z projektu, zadejte tokeny popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` `AssemblyInfo.cs` takovém případě nebo `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="a016d-235">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="a016d-236">Chcete-li použít tyto tokeny, spusťte `nuget pack` se souborem projektu, a ne `.nuspec`pouze.</span><span class="sxs-lookup"><span data-stu-id="a016d-236">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="a016d-237">Například při použití `$id$` následujícího příkazu jsou tokeny a `$version$` v `.nuspec` souboru nahrazeny hodnotami projektu `AssemblyName` a `AssemblyVersion` :</span><span class="sxs-lookup"><span data-stu-id="a016d-237">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="a016d-238">Obvykle, když máte projekt, vytvoříte `.nuspec` `nuget spec MyProject.csproj` počáteční, který automaticky obsahuje některé z těchto standardních tokenů.</span><span class="sxs-lookup"><span data-stu-id="a016d-238">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="a016d-239">Pokud však projekt nemá hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="a016d-239">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="a016d-240">Pokud navíc změníte hodnoty projektu, nezapomeňte před vytvořením balíčku znovu sestavit. To lze provést pohodlně pomocí `build` přepínače příkazu Pack.</span><span class="sxs-lookup"><span data-stu-id="a016d-240">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="a016d-241">S výjimkou `$configuration$`jsou hodnoty v projektu použity v předvolbách pro všechny přiřazené ke stejnému tokenu na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="a016d-241">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="a016d-242">Podpisový</span><span class="sxs-lookup"><span data-stu-id="a016d-242">Token</span></span> | <span data-ttu-id="a016d-243">Zdroj hodnoty</span><span class="sxs-lookup"><span data-stu-id="a016d-243">Value source</span></span> | <span data-ttu-id="a016d-244">Value</span><span class="sxs-lookup"><span data-stu-id="a016d-244">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="a016d-245">**$id $**</span><span class="sxs-lookup"><span data-stu-id="a016d-245">**$id$**</span></span> | <span data-ttu-id="a016d-246">Soubor projektu</span><span class="sxs-lookup"><span data-stu-id="a016d-246">Project file</span></span> | <span data-ttu-id="a016d-247">AssemblyName (title) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="a016d-247">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="a016d-248">**$version $**</span><span class="sxs-lookup"><span data-stu-id="a016d-248">**$version$**</span></span> | <span data-ttu-id="a016d-249">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a016d-249">AssemblyInfo</span></span> | <span data-ttu-id="a016d-250">AssemblyInformationalVersion, pokud je k dispozici, jinak AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="a016d-250">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="a016d-251">**$author $**</span><span class="sxs-lookup"><span data-stu-id="a016d-251">**$author$**</span></span> | <span data-ttu-id="a016d-252">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a016d-252">AssemblyInfo</span></span> | <span data-ttu-id="a016d-253">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="a016d-253">AssemblyCompany</span></span> |
| <span data-ttu-id="a016d-254">**$title$**</span><span class="sxs-lookup"><span data-stu-id="a016d-254">**$title$**</span></span> | <span data-ttu-id="a016d-255">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a016d-255">AssemblyInfo</span></span> | <span data-ttu-id="a016d-256">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="a016d-256">AssemblyTitle</span></span> |
| <span data-ttu-id="a016d-257">**$description $**</span><span class="sxs-lookup"><span data-stu-id="a016d-257">**$description$**</span></span> | <span data-ttu-id="a016d-258">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a016d-258">AssemblyInfo</span></span> | <span data-ttu-id="a016d-259">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="a016d-259">AssemblyDescription</span></span> |
| <span data-ttu-id="a016d-260">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="a016d-260">**$copyright$**</span></span> | <span data-ttu-id="a016d-261">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="a016d-261">AssemblyInfo</span></span> | <span data-ttu-id="a016d-262">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="a016d-262">AssemblyCopyright</span></span> |
| <span data-ttu-id="a016d-263">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="a016d-263">**$configuration$**</span></span> | <span data-ttu-id="a016d-264">Knihovna DLL sestavení</span><span class="sxs-lookup"><span data-stu-id="a016d-264">Assembly DLL</span></span> | <span data-ttu-id="a016d-265">Konfigurace použitá pro sestavení sestavení, výchozí nastavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="a016d-265">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="a016d-266">Všimněte si, že pokud chcete vytvořit balíček pomocí konfigurace vydané verze, vždy `-properties Configuration=Release` použijte příkaz na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="a016d-266">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="a016d-267">Tokeny lze také použít k překladu cest při zahrnutí [souborů sestavení](#including-assembly-files) a [souborů obsahu](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="a016d-267">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="a016d-268">Tokeny mají stejné názvy jako vlastnosti MSBuild, což umožňuje vybrat soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="a016d-268">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="a016d-269">Například pokud v `.nuspec` souboru použijete následující tokeny:</span><span class="sxs-lookup"><span data-stu-id="a016d-269">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="a016d-270">A sestavíte sestavení, `AssemblyName` jehož `LoggingLibrary` je s `Release` konfigurací `.nuspec` v nástroji MSBuild, výsledné řádky v souboru v balíčku jsou následující:</span><span class="sxs-lookup"><span data-stu-id="a016d-270">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="a016d-271">Element závislosti</span><span class="sxs-lookup"><span data-stu-id="a016d-271">Dependencies element</span></span>

<span data-ttu-id="a016d-272">Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvků, které identifikují další balíčky, na kterých závisí balíček nejvyšší úrovně. `<dependencies>`</span><span class="sxs-lookup"><span data-stu-id="a016d-272">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="a016d-273">Atributy pro každý `<dependency>` z nich jsou následující:</span><span class="sxs-lookup"><span data-stu-id="a016d-273">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="a016d-274">Atribut</span><span class="sxs-lookup"><span data-stu-id="a016d-274">Attribute</span></span> | <span data-ttu-id="a016d-275">Popis</span><span class="sxs-lookup"><span data-stu-id="a016d-275">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="a016d-276">Požadovanou ID balíčku závislosti, například "EntityFramework" a "NUnit", což je název balíčku nuget.org zobrazený na stránce balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-276">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="a016d-277">Požadovanou Rozsah verzí, které jsou přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="a016d-277">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="a016d-278">Přesnou syntaxi najdete v tématu [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) .</span><span class="sxs-lookup"><span data-stu-id="a016d-278">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> <span data-ttu-id="a016d-279">Zástupné verze (plovoucí) nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="a016d-279">Wildcard (floating) versions are not supported.</span></span> |
| <span data-ttu-id="a016d-280">include</span><span class="sxs-lookup"><span data-stu-id="a016d-280">include</span></span> | <span data-ttu-id="a016d-281">Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, kterou chcete zahrnout do finálního balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="a016d-282">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="a016d-282">The default value is `all`.</span></span> |
| <span data-ttu-id="a016d-283">exclude</span><span class="sxs-lookup"><span data-stu-id="a016d-283">exclude</span></span> | <span data-ttu-id="a016d-284">Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, která se má vyloučit v konečném balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-284">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="a016d-285">Výchozí hodnota je `build,analyzers` , která může být přepsána.</span><span class="sxs-lookup"><span data-stu-id="a016d-285">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="a016d-286">Ale `content/ ContentFiles` jsou také implicitně vyloučené v konečném balíčku, který nelze přepsat.</span><span class="sxs-lookup"><span data-stu-id="a016d-286">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="a016d-287">Zadané značky s `exclude` prioritou mají přednost před hodnotami určenými pomocí. `include`</span><span class="sxs-lookup"><span data-stu-id="a016d-287">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="a016d-288">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="a016d-288">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="a016d-289">Značka include/Exclude</span><span class="sxs-lookup"><span data-stu-id="a016d-289">Include/Exclude tag</span></span> | <span data-ttu-id="a016d-290">Ovlivněné složky v cíli</span><span class="sxs-lookup"><span data-stu-id="a016d-290">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="a016d-291">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a016d-291">contentFiles</span></span> | <span data-ttu-id="a016d-292">Obsah</span><span class="sxs-lookup"><span data-stu-id="a016d-292">Content</span></span> |
| <span data-ttu-id="a016d-293">modul runtime</span><span class="sxs-lookup"><span data-stu-id="a016d-293">runtime</span></span> | <span data-ttu-id="a016d-294">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a016d-294">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="a016d-295">sestavení</span><span class="sxs-lookup"><span data-stu-id="a016d-295">compile</span></span> | <span data-ttu-id="a016d-296">Knihovna</span><span class="sxs-lookup"><span data-stu-id="a016d-296">lib</span></span> |
| <span data-ttu-id="a016d-297">sestavení</span><span class="sxs-lookup"><span data-stu-id="a016d-297">build</span></span> | <span data-ttu-id="a016d-298">Build (MSBuild props and targets)</span><span class="sxs-lookup"><span data-stu-id="a016d-298">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="a016d-299">nativní</span><span class="sxs-lookup"><span data-stu-id="a016d-299">native</span></span> | <span data-ttu-id="a016d-300">nativní</span><span class="sxs-lookup"><span data-stu-id="a016d-300">native</span></span> |
| <span data-ttu-id="a016d-301">žádná</span><span class="sxs-lookup"><span data-stu-id="a016d-301">none</span></span> | <span data-ttu-id="a016d-302">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="a016d-302">No folders</span></span> |
| <span data-ttu-id="a016d-303">všechny</span><span class="sxs-lookup"><span data-stu-id="a016d-303">all</span></span> | <span data-ttu-id="a016d-304">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="a016d-304">All folders</span></span> |

<span data-ttu-id="a016d-305">Například následující řádky označují závislosti `PackageA` verze 1.1.0 nebo vyšší a `PackageB` verze 1. x.</span><span class="sxs-lookup"><span data-stu-id="a016d-305">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="a016d-306">Následující řádky označují závislosti pro stejné balíčky, `contentFiles` ale určují, že se mají zahrnout složky `build` `PackageA` a a všechno, ale `native` složky `PackageB`a `compile` .</span><span class="sxs-lookup"><span data-stu-id="a016d-306">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="a016d-307">Při vytváření `.nuspec` z projektu pomocí nástroje `nuget spec`nejsou závislosti, které existují v tomto projektu, automaticky zahrnuty ve výsledném `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="a016d-307">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="a016d-308">Místo toho použijte `nuget pack myproject.csproj`a získejte soubor *. nuspec* v rámci generovaného souboru *. nupkg* .</span><span class="sxs-lookup"><span data-stu-id="a016d-308">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="a016d-309">This *. nuspec* obsahuje závislosti.</span><span class="sxs-lookup"><span data-stu-id="a016d-309">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="a016d-310">Skupiny závislostí</span><span class="sxs-lookup"><span data-stu-id="a016d-310">Dependency groups</span></span>

<span data-ttu-id="a016d-311">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="a016d-311">*Version 2.0+*</span></span>

<span data-ttu-id="a016d-312">Jako alternativu k jednomu nestrukturovanému seznamu lze závislosti zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci. `<dependencies>`</span><span class="sxs-lookup"><span data-stu-id="a016d-312">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="a016d-313">Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` prvků.</span><span class="sxs-lookup"><span data-stu-id="a016d-313">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="a016d-314">Tyto závislosti jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="a016d-314">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a016d-315">`<group>` Prvek`targetFramework` bez atributu je použit jako výchozí nebo záložní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="a016d-315">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="a016d-316">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="a016d-316">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a016d-317">Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.</span><span class="sxs-lookup"><span data-stu-id="a016d-317">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="a016d-318">Následující příklad ukazuje různé varianty `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="a016d-318">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="a016d-319">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="a016d-319">Explicit assembly references</span></span>

<span data-ttu-id="a016d-320">Element je používán projekty pomocí `packages.config` k explicitnímu určení sestavení, na které by měl cílový projekt odkazovat při použití balíčku. `<references>`</span><span class="sxs-lookup"><span data-stu-id="a016d-320">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="a016d-321">Explicitní odkazy jsou obvykle používány pro sestavení pouze v době návrhu.</span><span class="sxs-lookup"><span data-stu-id="a016d-321">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="a016d-322">Další informace naleznete na stránce věnované [výběru sestavení odkazovaných projekty](../create-packages/select-assemblies-referenced-by-projects.md) , kde najdete další informace.</span><span class="sxs-lookup"><span data-stu-id="a016d-322">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="a016d-323">Například následující `<references>` element instruuje NuGet, aby přidal odkazy pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že jsou v balíčku k dispozici další sestavení:</span><span class="sxs-lookup"><span data-stu-id="a016d-323">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="a016d-324">Referenční skupiny</span><span class="sxs-lookup"><span data-stu-id="a016d-324">Reference groups</span></span>

<span data-ttu-id="a016d-325">Jako alternativu k jednomu nestrukturovanému seznamu lze odkazy zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci. `<references>`</span><span class="sxs-lookup"><span data-stu-id="a016d-325">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="a016d-326">Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<reference>` prvků.</span><span class="sxs-lookup"><span data-stu-id="a016d-326">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="a016d-327">Tyto odkazy jsou přidány do projektu, pokud je cílová architektura kompatibilní s profilem rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="a016d-327">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="a016d-328">`<group>` Prvek`targetFramework` bez atributu je použit jako výchozí nebo záložní seznam odkazů.</span><span class="sxs-lookup"><span data-stu-id="a016d-328">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="a016d-329">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="a016d-329">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="a016d-330">Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.</span><span class="sxs-lookup"><span data-stu-id="a016d-330">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="a016d-331">Následující příklad ukazuje různé varianty `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="a016d-331">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="a016d-332">Odkazy na sestavení rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="a016d-332">Framework assembly references</span></span>

<span data-ttu-id="a016d-333">Sestavení rozhraní jsou ta, která jsou součástí rozhraní .NET Framework a měla by již být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač.</span><span class="sxs-lookup"><span data-stu-id="a016d-333">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="a016d-334">Díky identifikaci těchto sestavení v rámci `<frameworkAssemblies>` elementu může balíček zajistit, aby byly do projektu přidány požadované odkazy v případě, že projekt nemá takové odkazy již.</span><span class="sxs-lookup"><span data-stu-id="a016d-334">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="a016d-335">Taková sestavení samozřejmě nejsou součástí balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="a016d-335">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="a016d-336">Element obsahuje nula nebo více `<frameworkAssembly>` elementů, z nichž každý určuje následující atributy: `<frameworkAssemblies>`</span><span class="sxs-lookup"><span data-stu-id="a016d-336">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="a016d-337">Atribut</span><span class="sxs-lookup"><span data-stu-id="a016d-337">Attribute</span></span> | <span data-ttu-id="a016d-338">Popis</span><span class="sxs-lookup"><span data-stu-id="a016d-338">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a016d-339">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="a016d-339">**assemblyName**</span></span> | <span data-ttu-id="a016d-340">Požadovanou Plně kvalifikovaný název sestavení.</span><span class="sxs-lookup"><span data-stu-id="a016d-340">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="a016d-341">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="a016d-341">**targetFramework**</span></span> | <span data-ttu-id="a016d-342">Volitelné Určuje cílovou architekturu, na kterou se vztahuje tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="a016d-342">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="a016d-343">Je-li tento parametr vynechán, znamená to, že odkaz se vztahuje na všechna rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a016d-343">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="a016d-344">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="a016d-344">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="a016d-345">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové rozhraní a odkaz na `System.ServiceModel` pro .NET Framework 4,0:</span><span class="sxs-lookup"><span data-stu-id="a016d-345">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="a016d-346">Zahrnutí souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="a016d-346">Including assembly files</span></span>

<span data-ttu-id="a016d-347">Pokud budete postupovat podle konvencí popsaných v [tématu Vytvoření balíčku](../create-packages/creating-a-package.md), nemusíte explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="a016d-347">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="a016d-348">`nuget pack` Příkaz automaticky vybere potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="a016d-348">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="a016d-349">Když je balíček nainstalován do projektu, NuGet automaticky přidá odkazy na sestavení do knihoven DLL balíčku, *kromě* těch, které jsou pojmenovány `.resources.dll` , protože se předpokládá, že jsou lokalizovaná satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="a016d-349">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="a016d-350">Z tohoto důvodu `.resources.dll` nepoužívejte pro soubory, které jinak obsahují základní kód balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-350">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="a016d-351">Chcete-li obejít toto automatické chování a explicitně řídit, které soubory jsou součástí balíčku, `<files>` umístěte prvek jako `<package>` podřízený objekt `<metadata>`(a na stejné místo) a Identifikujte každý soubor samostatným `<file>` prvkem.</span><span class="sxs-lookup"><span data-stu-id="a016d-351">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="a016d-352">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a016d-352">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="a016d-353">S NuGet 2. x a starším a projekty, `packages.config`které `<files>` používají, se element používá také k zahrnutí neměnných souborů obsahu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="a016d-353">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="a016d-354">S NuGet 3.3 + a projekty PackageReference `<contentFiles>` se místo toho použije element.</span><span class="sxs-lookup"><span data-stu-id="a016d-354">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="a016d-355">Podrobnosti najdete v části [zahrnutí souborů obsahu](#including-content-files) níže.</span><span class="sxs-lookup"><span data-stu-id="a016d-355">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="a016d-356">Atributy elementu souboru</span><span class="sxs-lookup"><span data-stu-id="a016d-356">File element attributes</span></span>

<span data-ttu-id="a016d-357">Každý `<file>` prvek určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="a016d-357">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="a016d-358">Atribut</span><span class="sxs-lookup"><span data-stu-id="a016d-358">Attribute</span></span> | <span data-ttu-id="a016d-359">Popis</span><span class="sxs-lookup"><span data-stu-id="a016d-359">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a016d-360">**src**</span><span class="sxs-lookup"><span data-stu-id="a016d-360">**src**</span></span> | <span data-ttu-id="a016d-361">Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem.</span><span class="sxs-lookup"><span data-stu-id="a016d-361">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a016d-362">Cesta je relativní vzhledem k `.nuspec` souboru, pokud není zadána absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="a016d-362">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="a016d-363">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="a016d-363">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a016d-364">**cílové**</span><span class="sxs-lookup"><span data-stu-id="a016d-364">**target**</span></span> | <span data-ttu-id="a016d-365">Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které `lib`musí začínat `build`na, `content`, nebo `tools`.</span><span class="sxs-lookup"><span data-stu-id="a016d-365">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="a016d-366">Viz [vytvoření. nuspec z pracovního adresáře založeného na konvencích](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="a016d-366">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="a016d-367">**slevy**</span><span class="sxs-lookup"><span data-stu-id="a016d-367">**exclude**</span></span> | <span data-ttu-id="a016d-368">Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, `src` jsou odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="a016d-368">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a016d-369">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="a016d-369">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="a016d-370">Příklady</span><span class="sxs-lookup"><span data-stu-id="a016d-370">Examples</span></span>

<span data-ttu-id="a016d-371">**Jedno sestavení**</span><span class="sxs-lookup"><span data-stu-id="a016d-371">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="a016d-372">**Samostatné sestavení specifické pro cílovou architekturu**</span><span class="sxs-lookup"><span data-stu-id="a016d-372">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="a016d-373">**Sada knihoven DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="a016d-373">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="a016d-374">**Knihovny DLL pro různé architektury**</span><span class="sxs-lookup"><span data-stu-id="a016d-374">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="a016d-375">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="a016d-375">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="a016d-376">Zahrnutí souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="a016d-376">Including content files</span></span>

<span data-ttu-id="a016d-377">Soubory obsahu jsou neměnné soubory, které musí balíček zahrnout do projektu.</span><span class="sxs-lookup"><span data-stu-id="a016d-377">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="a016d-378">Neměnné, nejsou určeny pro úpravy nenáročným projektem.</span><span class="sxs-lookup"><span data-stu-id="a016d-378">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="a016d-379">Mezi příklady souborů obsahu patří:</span><span class="sxs-lookup"><span data-stu-id="a016d-379">Example content files include:</span></span>

- <span data-ttu-id="a016d-380">Obrázky, které jsou vložené jako prostředky</span><span class="sxs-lookup"><span data-stu-id="a016d-380">Images that are embedded as resources</span></span>
- <span data-ttu-id="a016d-381">Zdrojové soubory, které jsou již kompilovány</span><span class="sxs-lookup"><span data-stu-id="a016d-381">Source files that are already compiled</span></span>
- <span data-ttu-id="a016d-382">Skripty, které je potřeba zahrnout do výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="a016d-382">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="a016d-383">Konfigurační soubory balíčku, které je potřeba zahrnout do projektu, ale nevyžadují žádné změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="a016d-383">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="a016d-384">Soubory obsahu jsou zahrnuty v balíčku pomocí `<files>` elementu a `content` určení složky v `target` atributu.</span><span class="sxs-lookup"><span data-stu-id="a016d-384">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="a016d-385">Nicméně tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který místo toho používá `<contentFiles>` element.</span><span class="sxs-lookup"><span data-stu-id="a016d-385">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="a016d-386">Pro maximální kompatibilitu s spotřebou projektů balíček v ideálním případě Určuje soubory obsahu v obou prvcích.</span><span class="sxs-lookup"><span data-stu-id="a016d-386">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="a016d-387">Použití elementu Files pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="a016d-387">Using the files element for content files</span></span>

<span data-ttu-id="a016d-388">Pro soubory obsahu stačí použít stejný formát jako u souborů sestavení, ale určete `content` jako základní složku `target` v atributu, jak je znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="a016d-388">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="a016d-389">**Základní soubory obsahu**</span><span class="sxs-lookup"><span data-stu-id="a016d-389">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="a016d-390">**Soubory obsahu s adresářovou strukturou**</span><span class="sxs-lookup"><span data-stu-id="a016d-390">**Content files with directory structure**</span></span>

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

<span data-ttu-id="a016d-391">**Soubor obsahu specifický pro cílovou architekturu**</span><span class="sxs-lookup"><span data-stu-id="a016d-391">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="a016d-392">**Soubor obsahu byl zkopírován do složky s tečkou v názvu**</span><span class="sxs-lookup"><span data-stu-id="a016d-392">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="a016d-393">V takovém případě NuGet zjistí, že rozšíření v `target` neodpovídá rozšíření v `src` nástroji, a proto zpracovává tuto `target` část názvu jako složku:</span><span class="sxs-lookup"><span data-stu-id="a016d-393">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="a016d-394">**Soubory obsahu bez rozšíření**</span><span class="sxs-lookup"><span data-stu-id="a016d-394">**Content files without extensions**</span></span>

<span data-ttu-id="a016d-395">Chcete-li zahrnout soubory bez přípony, použijte `*` zástupné znaky nebo `**` :</span><span class="sxs-lookup"><span data-stu-id="a016d-395">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="a016d-396">**Soubory obsahu s hlubokým umístěním a hlubokou cílovou cestou**</span><span class="sxs-lookup"><span data-stu-id="a016d-396">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="a016d-397">V tomto případě předpokládá, že vzhledem k příponám souborů ve zdrojové a cílové shodě NuGet předpokládá, že cílem je název souboru, a ne složka:</span><span class="sxs-lookup"><span data-stu-id="a016d-397">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="a016d-398">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="a016d-398">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="a016d-399">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="a016d-399">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="a016d-400">Použití elementu contentFiles pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="a016d-400">Using the contentFiles element for content files</span></span>

<span data-ttu-id="a016d-401">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="a016d-401">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="a016d-402">Ve výchozím nastavení balíček umístí obsah do `contentFiles` složky (viz níže) a `nuget pack` zahrne všechny soubory v této složce s použitím výchozích atributů.</span><span class="sxs-lookup"><span data-stu-id="a016d-402">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="a016d-403">V takovém případě není nutné zahrnout `contentFiles` uzel `.nuspec` do.</span><span class="sxs-lookup"><span data-stu-id="a016d-403">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="a016d-404">Chcete-li určit, které soubory jsou `<contentFiles>` zahrnuty, prvek určuje `<files>` kolekci prvků, které identifikují přesné soubory.</span><span class="sxs-lookup"><span data-stu-id="a016d-404">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="a016d-405">Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu:</span><span class="sxs-lookup"><span data-stu-id="a016d-405">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="a016d-406">Atribut</span><span class="sxs-lookup"><span data-stu-id="a016d-406">Attribute</span></span> | <span data-ttu-id="a016d-407">Popis</span><span class="sxs-lookup"><span data-stu-id="a016d-407">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a016d-408">**include**</span><span class="sxs-lookup"><span data-stu-id="a016d-408">**include**</span></span> | <span data-ttu-id="a016d-409">Požadovanou Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem.</span><span class="sxs-lookup"><span data-stu-id="a016d-409">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="a016d-410">Cesta je relativní ke `contentFiles` složce, pokud není zadána absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="a016d-410">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="a016d-411">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="a016d-411">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a016d-412">**slevy**</span><span class="sxs-lookup"><span data-stu-id="a016d-412">**exclude**</span></span> | <span data-ttu-id="a016d-413">Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, `src` jsou odděleny středníkem.</span><span class="sxs-lookup"><span data-stu-id="a016d-413">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="a016d-414">Zástupný znak `*` je povolen a dvojitý zástupný `**` znak implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="a016d-414">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="a016d-415">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="a016d-415">**buildAction**</span></span> | <span data-ttu-id="a016d-416">Akce sestavení, která má být přiřazena položce obsahu pro `Content`MSBuild, jako například `Embedded Resource`, `None` `Compile`,, atd. Výchozí hodnota je `Compile`.</span><span class="sxs-lookup"><span data-stu-id="a016d-416">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="a016d-417">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="a016d-417">**copyToOutput**</span></span> | <span data-ttu-id="a016d-418">Logická hodnota označující, zda se mají kopírovat položky obsahu do výstupní složky Build (nebo Publishing).</span><span class="sxs-lookup"><span data-stu-id="a016d-418">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="a016d-419">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="a016d-419">The default is false.</span></span> |
| <span data-ttu-id="a016d-420">**Flatten**</span><span class="sxs-lookup"><span data-stu-id="a016d-420">**flatten**</span></span> | <span data-ttu-id="a016d-421">Logická hodnota označující, zda se mají kopírovat položky obsahu do jediné složky ve výstupu sestavení (true), nebo pro zachování struktury složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="a016d-421">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="a016d-422">Tento příznak funguje pouze v případě, že příznak copyToOutput je nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="a016d-422">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="a016d-423">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="a016d-423">The default is false.</span></span> |

<span data-ttu-id="a016d-424">Při instalaci balíčku NuGet aplikuje podřízené prvky `<contentFiles>` od shora dolů.</span><span class="sxs-lookup"><span data-stu-id="a016d-424">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="a016d-425">Pokud se stejný soubor shoduje s více položkami, uplatní se všechny položky.</span><span class="sxs-lookup"><span data-stu-id="a016d-425">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="a016d-426">Pokud dojde ke konfliktu pro stejný atribut, přepíše položka nejvyšší úrovně nižší položky.</span><span class="sxs-lookup"><span data-stu-id="a016d-426">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="a016d-427">Struktura složky balíčku</span><span class="sxs-lookup"><span data-stu-id="a016d-427">Package folder structure</span></span>

<span data-ttu-id="a016d-428">Projekt balíčku by měl strukturovat obsah pomocí následujícího vzoru:</span><span class="sxs-lookup"><span data-stu-id="a016d-428">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="a016d-429">`codeLanguages`může to `cs`být `vb`, `fs` ,`any`, nebo malý ekvivalent daného`$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="a016d-429">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="a016d-430">`TxM`je libovolný moniker platného cílového rozhraní, který podporuje NuGet (viz [cílové architektury](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="a016d-430">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="a016d-431">Ke konci této syntaxe může být připojena jakákoli struktura složky.</span><span class="sxs-lookup"><span data-stu-id="a016d-431">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="a016d-432">Příklad:</span><span class="sxs-lookup"><span data-stu-id="a016d-432">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="a016d-433">Prázdné složky se můžou `.` použít k odhlášení o poskytování obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="a016d-433">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="a016d-434">Příklad oddílu contentFiles</span><span class="sxs-lookup"><span data-stu-id="a016d-434">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="a016d-435">Příklady souborů nuspec</span><span class="sxs-lookup"><span data-stu-id="a016d-435">Example nuspec files</span></span>

<span data-ttu-id="a016d-436">**Jednoduchá `.nuspec` , která neurčuje závislosti nebo soubory**</span><span class="sxs-lookup"><span data-stu-id="a016d-436">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="a016d-437">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="a016d-437">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="a016d-438">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="a016d-438">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="a016d-439">**A `.nuspec` se sestaveními architektury**</span><span class="sxs-lookup"><span data-stu-id="a016d-439">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="a016d-440">V tomto příkladu jsou nainstalovány následující pro konkrétní cíle projektu:</span><span class="sxs-lookup"><span data-stu-id="a016d-440">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="a016d-441">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="a016d-441">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="a016d-442">. Profil klienta NET4 – >`System.Net`</span><span class="sxs-lookup"><span data-stu-id="a016d-442">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="a016d-443">Silverlight 3 – >`System.Json`</span><span class="sxs-lookup"><span data-stu-id="a016d-443">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="a016d-444">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="a016d-444">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
