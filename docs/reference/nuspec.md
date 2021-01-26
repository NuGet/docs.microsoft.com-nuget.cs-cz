---
title: Odkaz na soubor. nuspec pro NuGet
description: Soubor. nuspec obsahuje metadata balíčku, která se používají při sestavování balíčku a poskytování informací pro uživatele balíčku.
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6a68b07c42e6abf4ad57d0129fa76d7dd620145f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777678"
---
# <a name="nuspec-reference"></a><span data-ttu-id="3b270-103">odkaz. nuspec</span><span class="sxs-lookup"><span data-stu-id="3b270-103">.nuspec reference</span></span>

<span data-ttu-id="3b270-104">`.nuspec`Soubor je manifest XML, který obsahuje metadata balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="3b270-105">Tento manifest slouží k sestavení balíčku a k poskytování informací pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="3b270-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="3b270-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="3b270-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="3b270-107">In this topic:</span></span>

- [<span data-ttu-id="3b270-108">Obecné formuláře a schéma</span><span class="sxs-lookup"><span data-stu-id="3b270-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="3b270-109">[Náhradní tokeny](#replacement-tokens) (při použití s projektem sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3b270-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="3b270-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="3b270-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="3b270-111">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="3b270-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="3b270-112">Odkazy na sestavení rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3b270-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="3b270-113">Zahrnutí souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="3b270-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="3b270-114">Zahrnutí souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="3b270-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="3b270-115">Příklady souborů nuspec</span><span class="sxs-lookup"><span data-stu-id="3b270-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="3b270-116">Kompatibilita typů projektu</span><span class="sxs-lookup"><span data-stu-id="3b270-116">Project type compatibility</span></span>

- <span data-ttu-id="3b270-117">Použijte `.nuspec` s `nuget.exe pack` pro projekty, které nejsou ve stylu sady SDK, které používají `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="3b270-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="3b270-118">`.nuspec`Soubor není vyžadován k vytváření balíčků pro projekty ve [stylu sady SDK](../resources/check-project-format.md) (obvykle se jedná o projekty .net Core a .NET Standard, které používají [atribut SDK](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="3b270-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="3b270-119">(Všimněte si, že `.nuspec` se generuje při vytváření balíčku.)</span><span class="sxs-lookup"><span data-stu-id="3b270-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="3b270-120">Pokud vytváříte balíček pomocí `dotnet.exe pack` nebo, doporučujeme `msbuild pack target` místo toho [Zahrnout všechny vlastnosti](../reference/msbuild-targets.md#pack-target) , které jsou obvykle v `.nuspec` souboru v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="3b270-121">Místo toho se ale můžete rozhodnout [použít `.nuspec` soubor k balení pomocí `dotnet.exe` nebo `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="3b270-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="3b270-122">Pro projekty migrované z aplikace `packages.config` do [PackageReference](../consume-packages/package-references-in-project-files.md)není pro `.nuspec` Vytvoření balíčku vyžadován soubor.</span><span class="sxs-lookup"><span data-stu-id="3b270-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="3b270-123">Místo toho použijte [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="3b270-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="3b270-124">Obecné formuláře a schéma</span><span class="sxs-lookup"><span data-stu-id="3b270-124">General form and schema</span></span>

<span data-ttu-id="3b270-125">Aktuální `nuspec.xsd` soubor schématu najdete v [úložišti GitHub NuGet](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="3b270-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="3b270-126">V rámci tohoto schématu `.nuspec` má soubor následující obecný tvar:</span><span class="sxs-lookup"><span data-stu-id="3b270-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="3b270-127">V případě jasné vizuální reprezentace schématu otevřete soubor schématu v aplikaci Visual Studio v režimu návrhu a klikněte na odkaz **Průzkumník schémat XML** .</span><span class="sxs-lookup"><span data-stu-id="3b270-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="3b270-128">Případně soubor otevřete jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **Zobrazit Průzkumníka schémat XML**.</span><span class="sxs-lookup"><span data-stu-id="3b270-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="3b270-129">Jak můžete vidět následující pohled (Pokud je převážně rozbalený):</span><span class="sxs-lookup"><span data-stu-id="3b270-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Průzkumník schémat sady Visual Studio s otevřeným nuspec. xsd](media/SchemaExplorer.png)

<span data-ttu-id="3b270-131">Všechny názvy elementů XML v souboru. nuspec rozlišují velká a malá písmena, stejně jako v případě XML obecně.</span><span class="sxs-lookup"><span data-stu-id="3b270-131">All XML element names in the .nuspec file are case-sensitive, as is the case for XML in general.</span></span> <span data-ttu-id="3b270-132">Například použití elementu metadata `<description>` je správné a není `<Description>` správné.</span><span class="sxs-lookup"><span data-stu-id="3b270-132">For example, using the metadata element `<description>` is correct and `<Description>` is not correct.</span></span> <span data-ttu-id="3b270-133">Správná velikost písmen pro každý název elementu je popsána níže.</span><span class="sxs-lookup"><span data-stu-id="3b270-133">The proper casing for each element name is documented below.</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="3b270-134">Požadované prvky metadat</span><span class="sxs-lookup"><span data-stu-id="3b270-134">Required metadata elements</span></span>

<span data-ttu-id="3b270-135">I když následující prvky jsou minimální požadavky na balíček, měli byste zvážit přidání [volitelných prvků metadat](#optional-metadata-elements) pro zlepšení celkového prostředí, které vývojáři mají s vaším balíčkem.</span><span class="sxs-lookup"><span data-stu-id="3b270-135">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="3b270-136">Tyto prvky se musí objevit v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="3b270-136">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="3b270-137">id</span><span class="sxs-lookup"><span data-stu-id="3b270-137">id</span></span> 
<span data-ttu-id="3b270-138">Identifikátor balíčku bez rozlišení velkých a malých písmen, který musí být jedinečný v rámci nuget.org nebo jakákoli galerie, v níž se balíček nachází.</span><span class="sxs-lookup"><span data-stu-id="3b270-138">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="3b270-139">ID nesmí obsahovat mezery ani znaky, které nejsou platné pro adresu URL a obecně následují pravidla oboru názvů .NET.</span><span class="sxs-lookup"><span data-stu-id="3b270-139">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="3b270-140">Pokyny najdete v tématu [Volba jedinečného identifikátoru balíčku](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .</span><span class="sxs-lookup"><span data-stu-id="3b270-140">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>

<span data-ttu-id="3b270-141">Při nahrávání balíčku do nuget.org `id` je pole omezeno na 128 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-141">When uploading a package to nuget.org, the `id` field is limited to 128 characters.</span></span>

#### <a name="version"></a><span data-ttu-id="3b270-142">verze</span><span class="sxs-lookup"><span data-stu-id="3b270-142">version</span></span>
<span data-ttu-id="3b270-143">Verze balíčku, podle vzoru *hlavní_verze. podverze. Oprava* .</span><span class="sxs-lookup"><span data-stu-id="3b270-143">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="3b270-144">Čísla verzí můžou obsahovat příponu předběžné verze, jak je popsáno v tématu [Správa verzí balíčků](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="3b270-144">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 

<span data-ttu-id="3b270-145">Při nahrávání balíčku do nuget.org `version` je pole omezeno na 64 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-145">When uploading a package to nuget.org, the `version` field is limited to 64 characters.</span></span>

#### <a name="description"></a><span data-ttu-id="3b270-146">description</span><span class="sxs-lookup"><span data-stu-id="3b270-146">description</span></span>
<span data-ttu-id="3b270-147">Popis balíčku pro zobrazení uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="3b270-147">A description of the package for UI display.</span></span>

<span data-ttu-id="3b270-148">Při nahrávání balíčku do nuget.org `description` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-148">When uploading a package to nuget.org, the `description` field is limited to 4000 characters.</span></span>

#### <a name="authors"></a><span data-ttu-id="3b270-149">Autoři</span><span class="sxs-lookup"><span data-stu-id="3b270-149">authors</span></span>
<span data-ttu-id="3b270-150">Čárkami oddělený seznam autorů balíčků, které odpovídají názvům profilů v nuget.org. Ty se zobrazí v galerii NuGet na nuget.org a používají se pro balíčky křížového odkazu stejnými autory.</span><span class="sxs-lookup"><span data-stu-id="3b270-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

<span data-ttu-id="3b270-151">Při nahrávání balíčku do nuget.org `authors` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-151">When uploading a package to nuget.org, the `authors` field is limited to 4000 characters.</span></span>

### <a name="optional-metadata-elements"></a><span data-ttu-id="3b270-152">Volitelné prvky metadat</span><span class="sxs-lookup"><span data-stu-id="3b270-152">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="3b270-153">vlastníka</span><span class="sxs-lookup"><span data-stu-id="3b270-153">owners</span></span>
> [!Important]
> <span data-ttu-id="3b270-154">Vlastníci jsou zastaralí.</span><span class="sxs-lookup"><span data-stu-id="3b270-154">owners is deprecated.</span></span> <span data-ttu-id="3b270-155">Místo toho použijte autory.</span><span class="sxs-lookup"><span data-stu-id="3b270-155">Use authors instead.</span></span>

<span data-ttu-id="3b270-156">Čárkami oddělený seznam tvůrců balíčků s použitím názvů profilů v nuget.org. Často se jedná o stejný seznam jako v a `authors` při nahrávání balíčku do NuGet.org se ignoruje. Viz [Správa vlastníků balíčků na NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="3b270-156">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="3b270-157">projectUrl</span><span class="sxs-lookup"><span data-stu-id="3b270-157">projectUrl</span></span>
<span data-ttu-id="3b270-158">Adresa URL domovské stránky balíčku, která se často zobrazuje v uživatelském rozhraní, a také nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3b270-158">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

<span data-ttu-id="3b270-159">Při nahrávání balíčku do nuget.org `projectUrl` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-159">When uploading a package to nuget.org, the `projectUrl` field is limited to 4000 characters.</span></span>

#### <a name="licenseurl"></a><span data-ttu-id="3b270-160">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="3b270-160">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="3b270-161">licenseUrl je zastaralá.</span><span class="sxs-lookup"><span data-stu-id="3b270-161">licenseUrl is deprecated.</span></span> <span data-ttu-id="3b270-162">Místo toho použijte licenci.</span><span class="sxs-lookup"><span data-stu-id="3b270-162">Use license instead.</span></span>

<span data-ttu-id="3b270-163">Adresa URL licence balíčku, která se často zobrazuje v uživatelská rozhraní jako nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3b270-163">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

<span data-ttu-id="3b270-164">Při nahrávání balíčku do nuget.org `licenseUrl` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-164">When uploading a package to nuget.org, the `licenseUrl` field is limited to 4000 characters.</span></span>

#### <a name="license"></a><span data-ttu-id="3b270-165">license</span><span class="sxs-lookup"><span data-stu-id="3b270-165">license</span></span>

<span data-ttu-id="3b270-166">*Podporováno s **balíčky NuGet 4.9.0** a novějšími*</span><span class="sxs-lookup"><span data-stu-id="3b270-166">*Supported with **NuGet 4.9.0** and above*</span></span>

<span data-ttu-id="3b270-167">SPDX licenční výraz nebo cesta k souboru s licencí v balíčku, který se často zobrazuje v uživatelská rozhraní jako nuget.org. Pokud je balíček licencován v rámci společné licence, jako je například MIT nebo BSD-2, použijte přidružený [identifikátor licence SPDX](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="3b270-167">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="3b270-168">Například:</span><span class="sxs-lookup"><span data-stu-id="3b270-168">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="3b270-169">NuGet.org akceptuje pouze licenční výrazy, které jsou schváleny v rámci iniciativy Open Source nebo Free Software Foundation.</span><span class="sxs-lookup"><span data-stu-id="3b270-169">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="3b270-170">Pokud je váš balíček licencován více běžnými licencemi, můžete zadat složenou licenci pomocí [syntaxe výrazu SPDX verze 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="3b270-170">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="3b270-171">Například:</span><span class="sxs-lookup"><span data-stu-id="3b270-171">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="3b270-172">Pokud používáte vlastní licenci, která není podporovaná výrazy licence, můžete zabalit `.txt` soubor nebo `.md` soubor s textem licence.</span><span class="sxs-lookup"><span data-stu-id="3b270-172">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="3b270-173">Například:</span><span class="sxs-lookup"><span data-stu-id="3b270-173">For example:</span></span>

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

<span data-ttu-id="3b270-174">V případě ekvivalentu MSBuild si prohlédněte [balení licenčního výrazu nebo souboru s licencí](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="3b270-174">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="3b270-175">Přesná Syntaxe výrazů s licenčními výrazy NuGet je popsaná níže v tématu [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="3b270-175">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>

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

#### <a name="iconurl"></a><span data-ttu-id="3b270-176">iconUrl</span><span class="sxs-lookup"><span data-stu-id="3b270-176">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="3b270-177">iconUrl je zastaralá.</span><span class="sxs-lookup"><span data-stu-id="3b270-177">iconUrl is deprecated.</span></span> <span data-ttu-id="3b270-178">Místo toho použijte ikonu.</span><span class="sxs-lookup"><span data-stu-id="3b270-178">Use icon instead.</span></span>

<span data-ttu-id="3b270-179">Adresa URL 128 × 128 obrázku s pozadím průhlednosti, která se má použít jako ikona balíčku v zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3b270-179">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="3b270-180">Ujistěte se, že tento prvek obsahuje *adresu URL přímého obrázku* , a ne adresu URL webové stránky, která obsahuje obrázek.</span><span class="sxs-lookup"><span data-stu-id="3b270-180">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="3b270-181">Pokud například chcete použít image z GitHubu, použijte adresu URL nezpracovaného souboru, jako je <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>.</span><span class="sxs-lookup"><span data-stu-id="3b270-181">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

<span data-ttu-id="3b270-182">Při nahrávání balíčku do nuget.org `iconUrl` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-182">When uploading a package to nuget.org, the `iconUrl` field is limited to 4000 characters.</span></span>

#### <a name="icon"></a><span data-ttu-id="3b270-183">ikona</span><span class="sxs-lookup"><span data-stu-id="3b270-183">icon</span></span>

<span data-ttu-id="3b270-184">*Podporováno s **balíčky NuGet 5.3.0** a novějšími*</span><span class="sxs-lookup"><span data-stu-id="3b270-184">*Supported with **NuGet 5.3.0** and above*</span></span>

<span data-ttu-id="3b270-185">Jedná se o cestu k souboru obrázku v rámci balíčku, který se často zobrazuje v uživatelská rozhraní jako ikona balíčku jako nuget.org.</span><span class="sxs-lookup"><span data-stu-id="3b270-185">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="3b270-186">Velikost souboru obrázku je omezená na 1 MB.</span><span class="sxs-lookup"><span data-stu-id="3b270-186">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="3b270-187">Podporované formáty souborů zahrnují JPEG a PNG.</span><span class="sxs-lookup"><span data-stu-id="3b270-187">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="3b270-188">Doporučujeme, abyste 128 × 128 rozlišení obrazu.</span><span class="sxs-lookup"><span data-stu-id="3b270-188">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="3b270-189">Například při vytváření balíčku pomocí nuget.exe přidejte do své služby nuspec následující:</span><span class="sxs-lookup"><span data-stu-id="3b270-189">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="3b270-190">Ikona balíčku nuspec vzorek</span><span class="sxs-lookup"><span data-stu-id="3b270-190">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="3b270-191">V případě ekvivalentu MSBuild se podíváme na [balení souboru obrázku ikony](msbuild-targets.md#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="3b270-191">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="3b270-192">Můžete zadat obojí `icon` a `iconUrl` pro zajištění zpětné kompatibility se zdroji, které nepodporují `icon` .</span><span class="sxs-lookup"><span data-stu-id="3b270-192">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="3b270-193">Visual Studio bude podporovat `icon` balíčky ze zdroje založeného na složce v budoucí verzi.</span><span class="sxs-lookup"><span data-stu-id="3b270-193">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="3b270-194">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="3b270-194">requireLicenseAcceptance</span></span>
<span data-ttu-id="3b270-195">Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence k balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-195">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="3b270-196">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="3b270-196">developmentDependency</span></span>
<span data-ttu-id="3b270-197">*(2.8 +)* Logická hodnota určující, zda je balíček označen pouze pro vývoj, což zabrání zahrnutí balíčku jako závislosti v jiných balíčcích.</span><span class="sxs-lookup"><span data-stu-id="3b270-197">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="3b270-198">Pomocí PackageReference (NuGet 4,8 +) Tento příznak také znamená, že vyloučí prostředky při kompilaci z kompilace.</span><span class="sxs-lookup"><span data-stu-id="3b270-198">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="3b270-199">Viz [Podpora DevelopmentDependency pro PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="3b270-199">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="3b270-200">shrnutí</span><span class="sxs-lookup"><span data-stu-id="3b270-200">summary</span></span>
> [!Important]
> <span data-ttu-id="3b270-201">`summary` se již nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="3b270-201">`summary` is being deprecated.</span></span> <span data-ttu-id="3b270-202">Místo toho použijte `description`.</span><span class="sxs-lookup"><span data-stu-id="3b270-202">Use `description` instead.</span></span>

<span data-ttu-id="3b270-203">Krátký popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3b270-203">A short description of the package for UI display.</span></span> <span data-ttu-id="3b270-204">Je-li tento parametr vynechán, je použita zkrácená verze nástroje `description` .</span><span class="sxs-lookup"><span data-stu-id="3b270-204">If omitted, a truncated version of `description` is used.</span></span>

<span data-ttu-id="3b270-205">Při nahrávání balíčku do nuget.org `summary` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-205">When uploading a package to nuget.org, the `summary` field is limited to 4000 characters.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="3b270-206">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="3b270-206">releaseNotes</span></span>
<span data-ttu-id="3b270-207">*(1,5 +)* Popis změn provedených v této verzi balíčku, který se často používá v uživatelském rozhraní jako karta **aktualizace** správce balíčků sady Visual Studio místo popisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-207">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

<span data-ttu-id="3b270-208">Při nahrávání balíčku do nuget.org `releaseNotes` je pole omezeno na 35 000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-208">When uploading a package to nuget.org, the `releaseNotes` field is limited to 35,000 characters.</span></span>

#### <a name="copyright"></a><span data-ttu-id="3b270-209">označení autorských práv,</span><span class="sxs-lookup"><span data-stu-id="3b270-209">copyright</span></span>
<span data-ttu-id="3b270-210">*(1,5 +)* Podrobnosti o autorských právech pro balíček.</span><span class="sxs-lookup"><span data-stu-id="3b270-210">*(1.5+)* Copyright details for the package.</span></span>

<span data-ttu-id="3b270-211">Při nahrávání balíčku do nuget.org `copyright` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-211">When uploading a package to nuget.org, the `copyright` field is limited to 4000 characters.</span></span>

#### <a name="language"></a><span data-ttu-id="3b270-212">language</span><span class="sxs-lookup"><span data-stu-id="3b270-212">language</span></span>
<span data-ttu-id="3b270-213">ID národního prostředí balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-213">The locale ID for the package.</span></span> <span data-ttu-id="3b270-214">Viz [vytváření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="3b270-214">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="3b270-215">tags</span><span class="sxs-lookup"><span data-stu-id="3b270-215">tags</span></span>
<span data-ttu-id="3b270-216">Mezerou oddělený seznam značek a klíčových slov, které popisují balíček a pomáhají zjistit balíčky pomocí vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="3b270-216">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

<span data-ttu-id="3b270-217">Při nahrávání balíčku do nuget.org `tags` je pole omezeno na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-217">When uploading a package to nuget.org, the `tags` field is limited to 4000 characters.</span></span>

#### <a name="serviceable"></a><span data-ttu-id="3b270-218">serviceable</span><span class="sxs-lookup"><span data-stu-id="3b270-218">serviceable</span></span> 
<span data-ttu-id="3b270-219">*(3.3 +)* Pouze pro interní použití NuGet.</span><span class="sxs-lookup"><span data-stu-id="3b270-219">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="3b270-220">úložiště</span><span class="sxs-lookup"><span data-stu-id="3b270-220">repository</span></span>
<span data-ttu-id="3b270-221">Metadata úložiště sestávající ze čtyř volitelných atributů: `type` a `url` *(4.0 +)* a `branch` a `commit` *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="3b270-221">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="3b270-222">Tyto atributy umožňují mapování na `.nupkg` úložiště, které ho vytvořilo, s potenciálem, který se má považovat za název jednotlivé větve a/nebo na potvrzení hodnoty hash SHA-1, která balíček vytvořila.</span><span class="sxs-lookup"><span data-stu-id="3b270-222">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="3b270-223">Měla by to být veřejně dostupná adresa URL, kterou lze vyvolat přímo pomocí softwaru pro správu verzí.</span><span class="sxs-lookup"><span data-stu-id="3b270-223">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="3b270-224">Neměla by se jednat o stránku HTML, která je určena pro daný počítač.</span><span class="sxs-lookup"><span data-stu-id="3b270-224">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="3b270-225">Pro odkazování na stránku projektu použijte `projectUrl` místo toho pole.</span><span class="sxs-lookup"><span data-stu-id="3b270-225">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="3b270-226">Například:</span><span class="sxs-lookup"><span data-stu-id="3b270-226">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

<span data-ttu-id="3b270-227">Při nahrávání balíčku do nuget.org `type` je atribut omezen na 100 znaků a `url` atribut je omezen na 4000 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-227">When uploading a package to nuget.org, the `type` attribute is limited to 100 characters and the `url` attribute is limited to 4000 characters.</span></span>

#### <a name="title"></a><span data-ttu-id="3b270-228">title</span><span class="sxs-lookup"><span data-stu-id="3b270-228">title</span></span>
<span data-ttu-id="3b270-229">Popisný název balíčku, který se dá použít v některých zobrazeních uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3b270-229">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="3b270-230">(nuget.org a správce balíčků v aplikaci Visual Studio nezobrazuje název)</span><span class="sxs-lookup"><span data-stu-id="3b270-230">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

<span data-ttu-id="3b270-231">Při nahrávání balíčku do nuget.org `title` je pole omezeno na 256 znaků, ale nepoužívá se pro účely zobrazení.</span><span class="sxs-lookup"><span data-stu-id="3b270-231">When uploading a package to nuget.org, the `title` field is limited to 256 characters but is not used for any display purposes.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="3b270-232">Prvky kolekce</span><span class="sxs-lookup"><span data-stu-id="3b270-232">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="3b270-233">packageTypes</span><span class="sxs-lookup"><span data-stu-id="3b270-233">packageTypes</span></span>
<span data-ttu-id="3b270-234">*(3.5 +)* Kolekce nula nebo více `<packageType>` prvků určující typ balíčku, pokud je jiný než tradiční balíček závislostí.</span><span class="sxs-lookup"><span data-stu-id="3b270-234">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="3b270-235">Každý packageType má atributy *názvu* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="3b270-235">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="3b270-236">Viz [Nastavení typu balíčku](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="3b270-236">See [Setting a package type](../create-packages/set-package-type.md).</span></span>

#### <a name="dependencies"></a><span data-ttu-id="3b270-237">závislosti</span><span class="sxs-lookup"><span data-stu-id="3b270-237">dependencies</span></span>
<span data-ttu-id="3b270-238">Kolekce nula nebo více prvků, které `<dependency>` určují závislosti pro balíček.</span><span class="sxs-lookup"><span data-stu-id="3b270-238">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="3b270-239">Každá závislost má atributy *ID*, *verze*, *include* (3. x +) a *Exclude* (3. x +).</span><span class="sxs-lookup"><span data-stu-id="3b270-239">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="3b270-240">Viz [závislosti](#dependencies-element) níže.</span><span class="sxs-lookup"><span data-stu-id="3b270-240">See [Dependencies](#dependencies-element) below.</span></span>

#### <a name="frameworkassemblies"></a><span data-ttu-id="3b270-241">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="3b270-241">frameworkAssemblies</span></span>
<span data-ttu-id="3b270-242">*(1,2 +)* Kolekce nula nebo více `<frameworkAssembly>` prvků, které identifikují .NET Framework odkazy na sestavení, které tento balíček vyžaduje, což zajistí přidání odkazů do projektů, které balíček spotřebovává.</span><span class="sxs-lookup"><span data-stu-id="3b270-242">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="3b270-243">Každý frameworkAssembly má atributy *AssemblyName* a *targetFramework* .</span><span class="sxs-lookup"><span data-stu-id="3b270-243">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="3b270-244">Viz [určení sestavení rozhraní odkazy v mezipaměti GAC](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="3b270-244">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>

#### <a name="references"></a><span data-ttu-id="3b270-245">odkazy</span><span class="sxs-lookup"><span data-stu-id="3b270-245">references</span></span>
<span data-ttu-id="3b270-246">*(1,5 +)* Kolekce nula nebo více `<reference>` prvků pojmenování sestavení ve `lib` složce balíčku, které jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="3b270-246">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="3b270-247">Každý odkaz má atribut *File* .</span><span class="sxs-lookup"><span data-stu-id="3b270-247">Each reference has a *file* attribute.</span></span> <span data-ttu-id="3b270-248">`<references>` může také obsahovat `<group>` element s atributem *targetFramework* , který pak obsahuje `<reference>` prvky.</span><span class="sxs-lookup"><span data-stu-id="3b270-248">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="3b270-249">Pokud tento parametr vynecháte, jsou zahrnuty všechny odkazy v nástroji `lib` .</span><span class="sxs-lookup"><span data-stu-id="3b270-249">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="3b270-250">Viz [zadání explicitních odkazů na sestavení](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="3b270-250">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>

#### <a name="contentfiles"></a><span data-ttu-id="3b270-251">contentFiles</span><span class="sxs-lookup"><span data-stu-id="3b270-251">contentFiles</span></span>
<span data-ttu-id="3b270-252">*(3.3 +)* Kolekce `<files>` prvků, které identifikují soubory obsahu, které mají být zahrnuty do náročného projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-252">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="3b270-253">Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-253">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="3b270-254">Viz [Určení souborů, které se mají zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="3b270-254">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>

#### <a name="files"></a><span data-ttu-id="3b270-255">files</span><span class="sxs-lookup"><span data-stu-id="3b270-255">files</span></span> 
<span data-ttu-id="3b270-256">`<package>`Uzel může obsahovat `<files>` uzel jako uzel na stejné úrovni `<metadata>` a `<contentFiles>` podřízená položka v rámci `<metadata>` , k určení sestavení a souborů obsahu, které mají být zahrnuty do balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-256">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="3b270-257">Podrobnosti najdete v části [zahrnutí souborů sestavení](#including-assembly-files) a [zahrnutí souborů obsahu](#including-content-files) dále v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="3b270-257">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="3b270-258">atributy metadat</span><span class="sxs-lookup"><span data-stu-id="3b270-258">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="3b270-259">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="3b270-259">minClientVersion</span></span>
<span data-ttu-id="3b270-260">Určuje minimální verzi klienta NuGet, která může nainstalovat tento balíček vynutila nuget.exe a správcem balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3b270-260">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="3b270-261">Tato funkce se používá vždy, když balíček závisí na konkrétních funkcích `.nuspec` souboru, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="3b270-261">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="3b270-262">Například balíček, který používá atribut, `developmentDependency` by měl pro použít hodnotu "2,8" `minClientVersion` .</span><span class="sxs-lookup"><span data-stu-id="3b270-262">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="3b270-263">Podobně balíček, který používá `contentFiles` element (viz další oddíl), by měl být nastaven `minClientVersion` na "3,3".</span><span class="sxs-lookup"><span data-stu-id="3b270-263">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="3b270-264">Všimněte si také, že vzhledem k tomu, že klienti NuGet starší než 2,5 nerozpoznávají tento příznak, *vždy* zamítnou instalaci balíčku bez ohledu na to, co `minClientVersion` obsahuje.</span><span class="sxs-lookup"><span data-stu-id="3b270-264">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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

## <a name="replacement-tokens"></a><span data-ttu-id="3b270-265">Náhradní tokeny</span><span class="sxs-lookup"><span data-stu-id="3b270-265">Replacement tokens</span></span>

<span data-ttu-id="3b270-266">Při vytváření balíčku nahradí [ `nuget pack` příkaz](../reference/cli-reference/cli-ref-pack.md) tokeny $-s oddělovači v `.nuspec` `<metadata>` uzlu souboru hodnotami, které pocházejí ze souboru projektu nebo `pack` `-properties` přepínače příkazu.</span><span class="sxs-lookup"><span data-stu-id="3b270-266">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="3b270-267">Na příkazovém řádku určíte hodnoty tokenu pomocí `nuget pack -properties <name>=<value>;<name>=<value>` .</span><span class="sxs-lookup"><span data-stu-id="3b270-267">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="3b270-268">Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a a zadat hodnoty v době balení následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="3b270-268">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="3b270-269">Pokud chcete použít hodnoty z projektu, zadejte tokeny popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` takovém případě `AssemblyInfo.cs` nebo `AssemblyInfo.vb` ).</span><span class="sxs-lookup"><span data-stu-id="3b270-269">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="3b270-270">Chcete-li použít tyto tokeny, spusťte `nuget pack` se souborem projektu, a ne pouze `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="3b270-270">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="3b270-271">Například při použití následujícího příkazu `$id$` `$version$` jsou tokeny a v `.nuspec` souboru nahrazeny `AssemblyName` hodnotami projektu a `AssemblyVersion` :</span><span class="sxs-lookup"><span data-stu-id="3b270-271">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="3b270-272">Obvykle, když máte projekt, vytvoříte `.nuspec` počáteční, `nuget spec MyProject.csproj` který automaticky obsahuje některé z těchto standardních tokenů.</span><span class="sxs-lookup"><span data-stu-id="3b270-272">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="3b270-273">Pokud však projekt nemá hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="3b270-273">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="3b270-274">Pokud navíc změníte hodnoty projektu, nezapomeňte před vytvořením balíčku znovu sestavit. To lze provést pohodlně pomocí přepínače příkazu Pack `build` .</span><span class="sxs-lookup"><span data-stu-id="3b270-274">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="3b270-275">S výjimkou `$configuration$` jsou hodnoty v projektu použity v předvolbách pro všechny přiřazené ke stejnému tokenu na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="3b270-275">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="3b270-276">Token</span><span class="sxs-lookup"><span data-stu-id="3b270-276">Token</span></span> | <span data-ttu-id="3b270-277">Zdroj hodnoty</span><span class="sxs-lookup"><span data-stu-id="3b270-277">Value source</span></span> | <span data-ttu-id="3b270-278">Hodnota</span><span class="sxs-lookup"><span data-stu-id="3b270-278">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="3b270-279">**$id $**</span><span class="sxs-lookup"><span data-stu-id="3b270-279">**$id$**</span></span> | <span data-ttu-id="3b270-280">Soubor projektu</span><span class="sxs-lookup"><span data-stu-id="3b270-280">Project file</span></span> | <span data-ttu-id="3b270-281">AssemblyName (title) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="3b270-281">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="3b270-282">**$version $**</span><span class="sxs-lookup"><span data-stu-id="3b270-282">**$version$**</span></span> | <span data-ttu-id="3b270-283">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="3b270-283">AssemblyInfo</span></span> | <span data-ttu-id="3b270-284">AssemblyInformationalVersion, pokud je k dispozici, jinak AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="3b270-284">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="3b270-285">**$author $**</span><span class="sxs-lookup"><span data-stu-id="3b270-285">**$author$**</span></span> | <span data-ttu-id="3b270-286">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="3b270-286">AssemblyInfo</span></span> | <span data-ttu-id="3b270-287">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="3b270-287">AssemblyCompany</span></span> |
| <span data-ttu-id="3b270-288">**$title $**</span><span class="sxs-lookup"><span data-stu-id="3b270-288">**$title$**</span></span> | <span data-ttu-id="3b270-289">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="3b270-289">AssemblyInfo</span></span> | <span data-ttu-id="3b270-290">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="3b270-290">AssemblyTitle</span></span> |
| <span data-ttu-id="3b270-291">**$description $**</span><span class="sxs-lookup"><span data-stu-id="3b270-291">**$description$**</span></span> | <span data-ttu-id="3b270-292">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="3b270-292">AssemblyInfo</span></span> | <span data-ttu-id="3b270-293">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="3b270-293">AssemblyDescription</span></span> |
| <span data-ttu-id="3b270-294">**$copyright $**</span><span class="sxs-lookup"><span data-stu-id="3b270-294">**$copyright$**</span></span> | <span data-ttu-id="3b270-295">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="3b270-295">AssemblyInfo</span></span> | <span data-ttu-id="3b270-296">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="3b270-296">AssemblyCopyright</span></span> |
| <span data-ttu-id="3b270-297">**$configuration $**</span><span class="sxs-lookup"><span data-stu-id="3b270-297">**$configuration$**</span></span> | <span data-ttu-id="3b270-298">Knihovna DLL sestavení</span><span class="sxs-lookup"><span data-stu-id="3b270-298">Assembly DLL</span></span> | <span data-ttu-id="3b270-299">Konfigurace použitá pro sestavení sestavení, výchozí nastavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="3b270-299">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="3b270-300">Všimněte si, že pokud chcete vytvořit balíček pomocí konfigurace vydané verze, vždy použijte `-properties Configuration=Release` příkaz na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="3b270-300">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="3b270-301">Tokeny lze také použít k překladu cest při zahrnutí [souborů sestavení](#including-assembly-files) a [souborů obsahu](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="3b270-301">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="3b270-302">Tokeny mají stejné názvy jako vlastnosti MSBuild, což umožňuje vybrat soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="3b270-302">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="3b270-303">Například pokud v souboru použijete následující tokeny `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="3b270-303">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="3b270-304">A sestavíte sestavení `AssemblyName` , jehož je `LoggingLibrary` s `Release` konfigurací v nástroji MSBuild, výsledné řádky v `.nuspec` souboru v balíčku jsou následující:</span><span class="sxs-lookup"><span data-stu-id="3b270-304">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="3b270-305">Element závislosti</span><span class="sxs-lookup"><span data-stu-id="3b270-305">Dependencies element</span></span>

<span data-ttu-id="3b270-306">`<dependencies>`Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvků, které identifikují další balíčky, na kterých závisí balíček nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="3b270-306">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="3b270-307">Atributy pro každý z nich `<dependency>` jsou následující:</span><span class="sxs-lookup"><span data-stu-id="3b270-307">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="3b270-308">Atribut</span><span class="sxs-lookup"><span data-stu-id="3b270-308">Attribute</span></span> | <span data-ttu-id="3b270-309">Popis</span><span class="sxs-lookup"><span data-stu-id="3b270-309">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="3b270-310">Požadovanou ID balíčku závislosti, například "EntityFramework" a "NUnit", což je název balíčku nuget.org zobrazený na stránce balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-310">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="3b270-311">Požadovanou Rozsah verzí, které jsou přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="3b270-311">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="3b270-312">Přesnou syntaxi najdete v tématu [Správa verzí balíčků](../concepts/package-versioning.md#version-ranges) .</span><span class="sxs-lookup"><span data-stu-id="3b270-312">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="3b270-313">Plovoucí verze se nepodporují.</span><span class="sxs-lookup"><span data-stu-id="3b270-313">Floating versions are not supported.</span></span> |
| <span data-ttu-id="3b270-314">include</span><span class="sxs-lookup"><span data-stu-id="3b270-314">include</span></span> | <span data-ttu-id="3b270-315">Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, kterou chcete zahrnout do finálního balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-315">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="3b270-316">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="3b270-316">The default value is `all`.</span></span> |
| <span data-ttu-id="3b270-317">vyloučení</span><span class="sxs-lookup"><span data-stu-id="3b270-317">exclude</span></span> | <span data-ttu-id="3b270-318">Seznam značek include/Exclude oddělených čárkami (viz níže) označující závislost, která se má vyloučit v konečném balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-318">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="3b270-319">Výchozí hodnota je, `build,analyzers` která může být přepsána.</span><span class="sxs-lookup"><span data-stu-id="3b270-319">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="3b270-320">Ale `content/ ContentFiles` jsou také implicitně vyloučené v konečném balíčku, který nelze přepsat.</span><span class="sxs-lookup"><span data-stu-id="3b270-320">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="3b270-321">Zadané značky s `exclude` prioritou mají přednost před hodnotami určenými pomocí `include` .</span><span class="sxs-lookup"><span data-stu-id="3b270-321">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="3b270-322">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="3b270-322">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

<span data-ttu-id="3b270-323">Při nahrávání balíčku do nuget.org je atribut každého objektu závislosti `id` omezen na 128 znaků a `version` atribut je omezen na 256 znaků.</span><span class="sxs-lookup"><span data-stu-id="3b270-323">When uploading a package to nuget.org, each dependency's `id` attribute is limited to 128 characters and the `version` attribute is limited to 256 characters.</span></span>

| <span data-ttu-id="3b270-324">Značka include/Exclude</span><span class="sxs-lookup"><span data-stu-id="3b270-324">Include/Exclude tag</span></span> | <span data-ttu-id="3b270-325">Ovlivněné složky v cíli</span><span class="sxs-lookup"><span data-stu-id="3b270-325">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="3b270-326">contentFiles</span><span class="sxs-lookup"><span data-stu-id="3b270-326">contentFiles</span></span> | <span data-ttu-id="3b270-327">Content</span><span class="sxs-lookup"><span data-stu-id="3b270-327">Content</span></span> |
| <span data-ttu-id="3b270-328">modul runtime</span><span class="sxs-lookup"><span data-stu-id="3b270-328">runtime</span></span> | <span data-ttu-id="3b270-329">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="3b270-329">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="3b270-330">kompilovat</span><span class="sxs-lookup"><span data-stu-id="3b270-330">compile</span></span> | <span data-ttu-id="3b270-331">Knihovna</span><span class="sxs-lookup"><span data-stu-id="3b270-331">lib</span></span> |
| <span data-ttu-id="3b270-332">sestavení</span><span class="sxs-lookup"><span data-stu-id="3b270-332">build</span></span> | <span data-ttu-id="3b270-333">Build (MSBuild props and targets)</span><span class="sxs-lookup"><span data-stu-id="3b270-333">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="3b270-334">nativní</span><span class="sxs-lookup"><span data-stu-id="3b270-334">native</span></span> | <span data-ttu-id="3b270-335">nativní</span><span class="sxs-lookup"><span data-stu-id="3b270-335">native</span></span> |
| <span data-ttu-id="3b270-336">žádné</span><span class="sxs-lookup"><span data-stu-id="3b270-336">none</span></span> | <span data-ttu-id="3b270-337">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="3b270-337">No folders</span></span> |
| <span data-ttu-id="3b270-338">Vše</span><span class="sxs-lookup"><span data-stu-id="3b270-338">all</span></span> | <span data-ttu-id="3b270-339">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="3b270-339">All folders</span></span> |

<span data-ttu-id="3b270-340">Například následující řádky označují závislosti `PackageA` verze 1.1.0 nebo vyšší a `PackageB` verze 1. x.</span><span class="sxs-lookup"><span data-stu-id="3b270-340">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="3b270-341">Následující řádky označují závislosti pro stejné balíčky, ale určují, že se mají zahrnout `contentFiles` `build` složky a a `PackageA` všechno, ale `native` složky a `compile` `PackageB` .</span><span class="sxs-lookup"><span data-stu-id="3b270-341">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="3b270-342">Při vytváření `.nuspec` z projektu pomocí nástroje nejsou `nuget spec` závislosti, které existují v tomto projektu, automaticky zahrnuty ve výsledném `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="3b270-342">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="3b270-343">Místo toho použijte `nuget pack myproject.csproj` a získejte soubor *. nuspec* v rámci generovaného souboru *. nupkg* .</span><span class="sxs-lookup"><span data-stu-id="3b270-343">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="3b270-344">This *. nuspec* obsahuje závislosti.</span><span class="sxs-lookup"><span data-stu-id="3b270-344">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="3b270-345">Skupiny závislostí</span><span class="sxs-lookup"><span data-stu-id="3b270-345">Dependency groups</span></span>

<span data-ttu-id="3b270-346">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="3b270-346">*Version 2.0+*</span></span>

<span data-ttu-id="3b270-347">Jako alternativu k jednomu nestrukturovanému seznamu lze závislosti zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci `<dependencies>` .</span><span class="sxs-lookup"><span data-stu-id="3b270-347">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="3b270-348">Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` prvků.</span><span class="sxs-lookup"><span data-stu-id="3b270-348">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="3b270-349">Tyto závislosti jsou nainstalovány společně, pokud je cílový rámec kompatibilní s profilem rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-349">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="3b270-350">`<group>`Prvek bez `targetFramework` atributu je použit jako výchozí nebo záložní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="3b270-350">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="3b270-351">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="3b270-351">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="3b270-352">Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.</span><span class="sxs-lookup"><span data-stu-id="3b270-352">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="3b270-353">Formát [monikeru cílového rozhraní (TFM)](../reference/target-frameworks.md) , který se používá ve `lib/ref` složce, se liší v porovnání s TFM použitým v `dependency groups` .</span><span class="sxs-lookup"><span data-stu-id="3b270-353">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="3b270-354">Pokud cílové architektury deklarované v `dependencies group` a ve `lib/ref` složce souboru nemají `.nuspec` přesné shody, `pack` příkaz vyvolá [Upozornění NuGet NU5128](../reference/errors-and-warnings/nu5128.md).</span><span class="sxs-lookup"><span data-stu-id="3b270-354">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="3b270-355">Následující příklad ukazuje různé varianty `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="3b270-355">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="3b270-356">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="3b270-356">Explicit assembly references</span></span>

<span data-ttu-id="3b270-357">`<references>`Element je používán projekty pomocí `packages.config` k explicitnímu určení sestavení, na které by měl cílový projekt odkazovat při použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-357">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="3b270-358">Explicitní odkazy jsou obvykle používány pro sestavení pouze v době návrhu.</span><span class="sxs-lookup"><span data-stu-id="3b270-358">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="3b270-359">Další informace naleznete na stránce věnované [výběru sestavení odkazovaných projekty](../create-packages/select-assemblies-referenced-by-projects.md) , kde najdete další informace.</span><span class="sxs-lookup"><span data-stu-id="3b270-359">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="3b270-360">Například následující `<references>` element instruuje NuGet, aby přidal odkazy pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že jsou v balíčku k dispozici další sestavení:</span><span class="sxs-lookup"><span data-stu-id="3b270-360">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="3b270-361">Referenční skupiny</span><span class="sxs-lookup"><span data-stu-id="3b270-361">Reference groups</span></span>

<span data-ttu-id="3b270-362">Jako alternativu k jednomu nestrukturovanému seznamu lze odkazy zadat podle profilu rozhraní cílového projektu pomocí `<group>` elementů v rámci `<references>` .</span><span class="sxs-lookup"><span data-stu-id="3b270-362">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="3b270-363">Každá skupina má atribut s názvem `targetFramework` a obsahuje nula nebo více `<reference>` prvků.</span><span class="sxs-lookup"><span data-stu-id="3b270-363">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="3b270-364">Tyto odkazy jsou přidány do projektu, pokud je cílová architektura kompatibilní s profilem rozhraní projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-364">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="3b270-365">`<group>`Prvek bez `targetFramework` atributu je použit jako výchozí nebo záložní seznam odkazů.</span><span class="sxs-lookup"><span data-stu-id="3b270-365">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="3b270-366">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="3b270-366">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="3b270-367">Formát skupiny nelze vzájemně kombinovat s nestrukturovaným seznamem.</span><span class="sxs-lookup"><span data-stu-id="3b270-367">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="3b270-368">Následující příklad ukazuje různé varianty `<group>` elementu:</span><span class="sxs-lookup"><span data-stu-id="3b270-368">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="3b270-369">Odkazy na sestavení rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3b270-369">Framework assembly references</span></span>

<span data-ttu-id="3b270-370">Sestavení rozhraní jsou ta, která jsou součástí rozhraní .NET Framework a měla by již být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač.</span><span class="sxs-lookup"><span data-stu-id="3b270-370">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="3b270-371">Díky identifikaci těchto sestavení v rámci `<frameworkAssemblies>` elementu může balíček zajistit, aby byly do projektu přidány požadované odkazy v případě, že projekt nemá takové odkazy již.</span><span class="sxs-lookup"><span data-stu-id="3b270-371">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="3b270-372">Taková sestavení samozřejmě nejsou součástí balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="3b270-372">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="3b270-373">`<frameworkAssemblies>`Element obsahuje nula nebo více `<frameworkAssembly>` elementů, z nichž každý určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="3b270-373">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="3b270-374">Atribut</span><span class="sxs-lookup"><span data-stu-id="3b270-374">Attribute</span></span> | <span data-ttu-id="3b270-375">Popis</span><span class="sxs-lookup"><span data-stu-id="3b270-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b270-376">**Doplňk**</span><span class="sxs-lookup"><span data-stu-id="3b270-376">**assemblyName**</span></span> | <span data-ttu-id="3b270-377">Požadovanou Plně kvalifikovaný název sestavení.</span><span class="sxs-lookup"><span data-stu-id="3b270-377">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="3b270-378">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="3b270-378">**targetFramework**</span></span> | <span data-ttu-id="3b270-379">Volitelné Určuje cílovou architekturu, na kterou se vztahuje tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="3b270-379">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="3b270-380">Je-li tento parametr vynechán, znamená to, že odkaz se vztahuje na všechna rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3b270-380">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="3b270-381">Přesné identifikátory rozhraní naleznete v tématu [cílová rozhraní](../reference/target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="3b270-381">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="3b270-382">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové rozhraní a odkaz na `System.ServiceModel` pro .NET Framework 4,0:</span><span class="sxs-lookup"><span data-stu-id="3b270-382">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="3b270-383">Zahrnutí souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="3b270-383">Including assembly files</span></span>

<span data-ttu-id="3b270-384">Pokud budete postupovat podle konvencí popsaných v [tématu Vytvoření balíčku](../create-packages/creating-a-package.md), nemusíte explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="3b270-384">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="3b270-385">`nuget pack`Příkaz automaticky vybere potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="3b270-385">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="3b270-386">Když je balíček nainstalován do projektu, NuGet automaticky přidá odkazy na sestavení do knihoven DLL balíčku, *kromě* těch, které jsou pojmenovány, `.resources.dll` protože se předpokládá, že jsou lokalizovaná satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="3b270-386">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="3b270-387">Z tohoto důvodu nepoužívejte `.resources.dll` pro soubory, které jinak obsahují základní kód balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-387">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="3b270-388">Chcete-li obejít toto automatické chování a explicitně řídit, které soubory jsou součástí balíčku, umístěte `<files>` prvek jako podřízený objekt `<package>` (a na stejné místo `<metadata>` ) a Identifikujte každý soubor samostatným `<file>` prvkem.</span><span class="sxs-lookup"><span data-stu-id="3b270-388">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="3b270-389">Například:</span><span class="sxs-lookup"><span data-stu-id="3b270-389">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="3b270-390">S NuGet 2. x a starším a projekty, `packages.config` které používají, se `<files>` element používá také k zahrnutí neměnných souborů obsahu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="3b270-390">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="3b270-391">S NuGet 3.3 + a projekty PackageReference se `<contentFiles>` místo toho použije element.</span><span class="sxs-lookup"><span data-stu-id="3b270-391">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="3b270-392">Podrobnosti najdete v části [zahrnutí souborů obsahu](#including-content-files) níže.</span><span class="sxs-lookup"><span data-stu-id="3b270-392">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="3b270-393">Atributy elementu souboru</span><span class="sxs-lookup"><span data-stu-id="3b270-393">File element attributes</span></span>

<span data-ttu-id="3b270-394">Každý `<file>` prvek určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="3b270-394">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="3b270-395">Atribut</span><span class="sxs-lookup"><span data-stu-id="3b270-395">Attribute</span></span> | <span data-ttu-id="3b270-396">Popis</span><span class="sxs-lookup"><span data-stu-id="3b270-396">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b270-397">**src**</span><span class="sxs-lookup"><span data-stu-id="3b270-397">**src**</span></span> | <span data-ttu-id="3b270-398">Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem.</span><span class="sxs-lookup"><span data-stu-id="3b270-398">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="3b270-399">Cesta je relativní vzhledem k `.nuspec` souboru, pokud není zadána absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="3b270-399">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="3b270-400">Zástupný znak `*` je povolen a dvojitý zástupný znak `**` implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="3b270-400">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="3b270-401">**cílové**</span><span class="sxs-lookup"><span data-stu-id="3b270-401">**target**</span></span> | <span data-ttu-id="3b270-402">Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které musí začínat `lib` na, `content` , `build` nebo `tools` .</span><span class="sxs-lookup"><span data-stu-id="3b270-402">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="3b270-403">Viz [vytvoření. nuspec z pracovního adresáře založeného na konvencích](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="3b270-403">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="3b270-404">**vyloučení**</span><span class="sxs-lookup"><span data-stu-id="3b270-404">**exclude**</span></span> | <span data-ttu-id="3b270-405">Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, jsou odděleny středníkem `src` .</span><span class="sxs-lookup"><span data-stu-id="3b270-405">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="3b270-406">Zástupný znak `*` je povolen a dvojitý zástupný znak `**` implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="3b270-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="3b270-407">Příklady</span><span class="sxs-lookup"><span data-stu-id="3b270-407">Examples</span></span>

<span data-ttu-id="3b270-408">**Jedno sestavení**</span><span class="sxs-lookup"><span data-stu-id="3b270-408">**Single assembly**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

<span data-ttu-id="3b270-409">**Samostatné sestavení specifické pro cílovou architekturu**</span><span class="sxs-lookup"><span data-stu-id="3b270-409">**Single assembly specific to a target framework**</span></span>

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

<span data-ttu-id="3b270-410">**Sada knihoven DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="3b270-410">**Set of DLLs using a wildcard**</span></span>

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

<span data-ttu-id="3b270-411">**Knihovny DLL pro různé architektury**</span><span class="sxs-lookup"><span data-stu-id="3b270-411">**DLLs for different frameworks**</span></span>

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

<span data-ttu-id="3b270-412">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="3b270-412">**Excluding files**</span></span>

```
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
```

## <a name="including-content-files"></a><span data-ttu-id="3b270-413">Zahrnutí souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="3b270-413">Including content files</span></span>

<span data-ttu-id="3b270-414">Soubory obsahu jsou neměnné soubory, které musí balíček zahrnout do projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-414">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="3b270-415">Neměnné, nejsou určeny pro úpravy nenáročným projektem.</span><span class="sxs-lookup"><span data-stu-id="3b270-415">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="3b270-416">Mezi příklady souborů obsahu patří:</span><span class="sxs-lookup"><span data-stu-id="3b270-416">Example content files include:</span></span>

- <span data-ttu-id="3b270-417">Obrázky, které jsou vložené jako prostředky</span><span class="sxs-lookup"><span data-stu-id="3b270-417">Images that are embedded as resources</span></span>
- <span data-ttu-id="3b270-418">Zdrojové soubory, které jsou již kompilovány</span><span class="sxs-lookup"><span data-stu-id="3b270-418">Source files that are already compiled</span></span>
- <span data-ttu-id="3b270-419">Skripty, které je potřeba zahrnout do výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="3b270-419">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="3b270-420">Konfigurační soubory balíčku, které je potřeba zahrnout do projektu, ale nevyžadují žádné změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="3b270-420">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="3b270-421">Soubory obsahu jsou zahrnuty v balíčku pomocí `<files>` elementu a určení `content` složky v `target` atributu.</span><span class="sxs-lookup"><span data-stu-id="3b270-421">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="3b270-422">Nicméně tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který místo toho používá `<contentFiles>` element.</span><span class="sxs-lookup"><span data-stu-id="3b270-422">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="3b270-423">Pro maximální kompatibilitu s spotřebou projektů balíček v ideálním případě Určuje soubory obsahu v obou prvcích.</span><span class="sxs-lookup"><span data-stu-id="3b270-423">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="3b270-424">Použití elementu Files pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="3b270-424">Using the files element for content files</span></span>

<span data-ttu-id="3b270-425">Pro soubory obsahu stačí použít stejný formát jako u souborů sestavení, ale určete `content` jako základní složku v atributu, jak je `target` znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="3b270-425">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="3b270-426">**Základní soubory obsahu**</span><span class="sxs-lookup"><span data-stu-id="3b270-426">**Basic content files**</span></span>

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

<span data-ttu-id="3b270-427">**Soubory obsahu s adresářovou strukturou**</span><span class="sxs-lookup"><span data-stu-id="3b270-427">**Content files with directory structure**</span></span>

```
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
```

<span data-ttu-id="3b270-428">**Soubor obsahu specifický pro cílovou architekturu**</span><span class="sxs-lookup"><span data-stu-id="3b270-428">**Content file specific to a target framework**</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

<span data-ttu-id="3b270-429">**Soubor obsahu byl zkopírován do složky s tečkou v názvu**</span><span class="sxs-lookup"><span data-stu-id="3b270-429">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="3b270-430">V takovém případě NuGet zjistí, že rozšíření v `target` neodpovídá rozšíření v nástroji `src` , a proto zpracovává tuto část názvu `target` jako složku:</span><span class="sxs-lookup"><span data-stu-id="3b270-430">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

<span data-ttu-id="3b270-431">**Soubory obsahu bez rozšíření**</span><span class="sxs-lookup"><span data-stu-id="3b270-431">**Content files without extensions**</span></span>

<span data-ttu-id="3b270-432">Chcete-li zahrnout soubory bez přípony, použijte `*` `**` zástupné znaky nebo:</span><span class="sxs-lookup"><span data-stu-id="3b270-432">To include files without an extension, use the `*` or `**` wildcards:</span></span>

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

<span data-ttu-id="3b270-433">**Soubory obsahu s hlubokým umístěním a hlubokou cílovou cestou**</span><span class="sxs-lookup"><span data-stu-id="3b270-433">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="3b270-434">V tomto případě předpokládá, že vzhledem k příponám souborů ve zdrojové a cílové shodě NuGet předpokládá, že cílem je název souboru, a ne složka:</span><span class="sxs-lookup"><span data-stu-id="3b270-434">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

<span data-ttu-id="3b270-435">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="3b270-435">**Renaming a content file in the package**</span></span>

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

<span data-ttu-id="3b270-436">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="3b270-436">**Excluding files**</span></span>

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="3b270-437">Použití elementu contentFiles pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="3b270-437">Using the contentFiles element for content files</span></span>

<span data-ttu-id="3b270-438">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="3b270-438">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="3b270-439">Ve výchozím nastavení balíček umístí obsah do `contentFiles` složky (viz níže) a `nuget pack` zahrne všechny soubory v této složce s použitím výchozích atributů.</span><span class="sxs-lookup"><span data-stu-id="3b270-439">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="3b270-440">V takovém případě není nutné zahrnout `contentFiles` uzel do `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="3b270-440">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="3b270-441">Chcete-li určit, které soubory jsou zahrnuty, `<contentFiles>` prvek určuje kolekci `<files>` prvků, které identifikují přesné soubory.</span><span class="sxs-lookup"><span data-stu-id="3b270-441">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="3b270-442">Tyto soubory jsou zadány pomocí sady atributů, které popisují, jak by měly být použity v rámci systému projektu:</span><span class="sxs-lookup"><span data-stu-id="3b270-442">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="3b270-443">Atribut</span><span class="sxs-lookup"><span data-stu-id="3b270-443">Attribute</span></span> | <span data-ttu-id="3b270-444">Popis</span><span class="sxs-lookup"><span data-stu-id="3b270-444">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b270-445">**připojit**</span><span class="sxs-lookup"><span data-stu-id="3b270-445">**include**</span></span> | <span data-ttu-id="3b270-446">Požadovanou Umístění souboru nebo souborů, které mají být zahrnuty, v závislosti na vyloučení určených `exclude` atributem.</span><span class="sxs-lookup"><span data-stu-id="3b270-446">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="3b270-447">Cesta je relativní ke složce, `contentFiles` Pokud není zadána absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="3b270-447">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="3b270-448">Zástupný znak `*` je povolen a dvojitý zástupný znak `**` implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="3b270-448">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="3b270-449">**vyloučení**</span><span class="sxs-lookup"><span data-stu-id="3b270-449">**exclude**</span></span> | <span data-ttu-id="3b270-450">Seznam souborů nebo vzorů souborů, které mají být vyloučeny z umístění, jsou odděleny středníkem `src` .</span><span class="sxs-lookup"><span data-stu-id="3b270-450">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="3b270-451">Zástupný znak `*` je povolen a dvojitý zástupný znak `**` implikuje hledání rekurzivní složky.</span><span class="sxs-lookup"><span data-stu-id="3b270-451">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="3b270-452">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="3b270-452">**buildAction**</span></span> | <span data-ttu-id="3b270-453">Akce sestavení, která má být přiřazena položce obsahu pro MSBuild, jako například `Content` ,,, `None` `Embedded Resource` `Compile` atd. Výchozí hodnota je `Compile` .</span><span class="sxs-lookup"><span data-stu-id="3b270-453">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="3b270-454">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="3b270-454">**copyToOutput**</span></span> | <span data-ttu-id="3b270-455">Logická hodnota označující, zda se mají kopírovat položky obsahu do výstupní složky Build (nebo Publishing).</span><span class="sxs-lookup"><span data-stu-id="3b270-455">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="3b270-456">Výchozí hodnotou je hodnota false.</span><span class="sxs-lookup"><span data-stu-id="3b270-456">The default is false.</span></span> |
| <span data-ttu-id="3b270-457">**Flatten**</span><span class="sxs-lookup"><span data-stu-id="3b270-457">**flatten**</span></span> | <span data-ttu-id="3b270-458">Logická hodnota označující, zda se mají kopírovat položky obsahu do jediné složky ve výstupu sestavení (true), nebo pro zachování struktury složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="3b270-458">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="3b270-459">Tento příznak funguje pouze v případě, že příznak copyToOutput je nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="3b270-459">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="3b270-460">Výchozí hodnotou je hodnota false.</span><span class="sxs-lookup"><span data-stu-id="3b270-460">The default is false.</span></span> |

<span data-ttu-id="3b270-461">Při instalaci balíčku NuGet aplikuje podřízené prvky `<contentFiles>` od shora dolů.</span><span class="sxs-lookup"><span data-stu-id="3b270-461">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="3b270-462">Pokud se stejný soubor shoduje s více položkami, uplatní se všechny položky.</span><span class="sxs-lookup"><span data-stu-id="3b270-462">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="3b270-463">Pokud dojde ke konfliktu pro stejný atribut, přepíše položka nejvyšší úrovně nižší položky.</span><span class="sxs-lookup"><span data-stu-id="3b270-463">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="3b270-464">Struktura složky balíčku</span><span class="sxs-lookup"><span data-stu-id="3b270-464">Package folder structure</span></span>

<span data-ttu-id="3b270-465">Projekt balíčku by měl strukturovat obsah pomocí následujícího vzoru:</span><span class="sxs-lookup"><span data-stu-id="3b270-465">The package project should structure content using the following pattern:</span></span>

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- <span data-ttu-id="3b270-466">`codeLanguages` může `cs` to být, `vb` ,, `fs` `any` nebo malý ekvivalent daného `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="3b270-466">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="3b270-467">`TxM` je libovolný moniker platného cílového rozhraní, který podporuje NuGet (viz [cílové architektury](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="3b270-467">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="3b270-468">Ke konci této syntaxe může být připojena jakákoli struktura složky.</span><span class="sxs-lookup"><span data-stu-id="3b270-468">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="3b270-469">Například:</span><span class="sxs-lookup"><span data-stu-id="3b270-469">For example:</span></span>

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

<span data-ttu-id="3b270-470">Prázdné složky se můžou použít `.` k odhlášení o poskytování obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="3b270-470">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a><span data-ttu-id="3b270-471">Příklad oddílu contentFiles</span><span class="sxs-lookup"><span data-stu-id="3b270-471">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="3b270-472">Referenční skupiny rozhraní</span><span class="sxs-lookup"><span data-stu-id="3b270-472">Framework reference groups</span></span>

<span data-ttu-id="3b270-473">*Pouze verze 5.1 + wih PackageReference*</span><span class="sxs-lookup"><span data-stu-id="3b270-473">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="3b270-474">Odkazy na rozhraní jsou koncept .NET Core, který představuje sdílené architektury, jako je WPF nebo model Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="3b270-474">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="3b270-475">Zadáte-li sdílené rozhraní, balíček zajistí, že všechny jeho závislosti rozhraní jsou zahrnuty do odkazujícího projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-475">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="3b270-476">Každý `<group>` prvek vyžaduje `targetFramework` atribut a nula nebo více `<frameworkReference>` prvků.</span><span class="sxs-lookup"><span data-stu-id="3b270-476">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="3b270-477">Následující příklad ukazuje nuspec vygenerovaný pro projekt .NET Core WPF.</span><span class="sxs-lookup"><span data-stu-id="3b270-477">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="3b270-478">Mějte na paměti, že ruční vytváření nuspecs obsahujících odkazy na rozhraní se nedoporučuje.</span><span class="sxs-lookup"><span data-stu-id="3b270-478">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="3b270-479">Místo toho zvažte použití sady [targets](msbuild-targets.md) Pack, které budou automaticky odvodit z projektu.</span><span class="sxs-lookup"><span data-stu-id="3b270-479">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="3b270-480">Příklady souborů nuspec</span><span class="sxs-lookup"><span data-stu-id="3b270-480">Example nuspec files</span></span>

<span data-ttu-id="3b270-481">**Jednoduchá `.nuspec` , která neurčuje závislosti nebo soubory**</span><span class="sxs-lookup"><span data-stu-id="3b270-481">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="3b270-482">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="3b270-482">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="3b270-483">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="3b270-483">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="3b270-484">**A `.nuspec` se sestaveními architektury**</span><span class="sxs-lookup"><span data-stu-id="3b270-484">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="3b270-485">V tomto příkladu jsou nainstalovány následující pro konkrétní cíle projektu:</span><span class="sxs-lookup"><span data-stu-id="3b270-485">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="3b270-486">. NET4-> `System.Web` , `System.Net`</span><span class="sxs-lookup"><span data-stu-id="3b270-486">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="3b270-487">. Profil klienta NET4 – > `System.Net`</span><span class="sxs-lookup"><span data-stu-id="3b270-487">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="3b270-488">Silverlight 3 – > `System.Json`</span><span class="sxs-lookup"><span data-stu-id="3b270-488">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="3b270-489">WindowsPhone – > `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="3b270-489">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
