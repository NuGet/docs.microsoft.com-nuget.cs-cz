---
title: Odkaz na soubor příponou .nuspec pro NuGet
description: Soubor s příponou .nuspec obsahuje metadata balíčků použít při vytváření balíčku a poskytnout informace k příjemce balíčku.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 2ff83538f9f1cf3bd4ed616ec8f5f1aef3ffd9d6
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818539"
---
# <a name="nuspec-reference"></a><span data-ttu-id="b0dcb-103">referenční dokumentace příponou .nuspec</span><span class="sxs-lookup"><span data-stu-id="b0dcb-103">.nuspec reference</span></span>

<span data-ttu-id="b0dcb-104">A `.nuspec` je soubor manifestu XML, který obsahuje metadata balíčků.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="b0dcb-105">Tento manifest se používá k vytvoření balíčku a zadejte informace k příjemce.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="b0dcb-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="b0dcb-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-107">In this topic:</span></span>

- [<span data-ttu-id="b0dcb-108">Obecné formuláře a schématu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="b0dcb-109">[Nahrazení tokeny](#replacement-tokens) (při použití s projekt sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b0dcb-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="b0dcb-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="b0dcb-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="b0dcb-111">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="b0dcb-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="b0dcb-112">Odkazy na sestavení Framework</span><span class="sxs-lookup"><span data-stu-id="b0dcb-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="b0dcb-113">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="b0dcb-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="b0dcb-114">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="b0dcb-115">Příklady</span><span class="sxs-lookup"><span data-stu-id="b0dcb-115">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="b0dcb-116">Obecné formuláře a schématu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-116">General form and schema</span></span>

<span data-ttu-id="b0dcb-117">Aktuální `nuspec.xsd` soubor schématu najdete v [úložiště NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="b0dcb-118">V tomto schématu `.nuspec` soubor má následující Obecné formuláře:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="b0dcb-119">Pro zřetelné vizuální reprezentace schématu, otevřete soubor schématu v sadě Visual Studio v režimu návrhu a klikněte na **Explorer schématu XML** odkaz.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="b0dcb-120">Můžete také otevřít soubor jako kód, klikněte pravým tlačítkem myši v editoru a vyberte **zobrazit Explorer schématu XML**.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="b0dcb-121">V obou případech, které získáte zobrazení stejný, jako je pod (většinou rozšířit):</span><span class="sxs-lookup"><span data-stu-id="b0dcb-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Schéma Průzkumníka Visual Studio s nuspec.xsd otevřít](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="b0dcb-123">Atributy metadat</span><span class="sxs-lookup"><span data-stu-id="b0dcb-123">Metadata attributes</span></span>

<span data-ttu-id="b0dcb-124">`<metadata>` Element podporuje atributy popsané v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-124">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="b0dcb-125">Atribut</span><span class="sxs-lookup"><span data-stu-id="b0dcb-125">Attribute</span></span> | <span data-ttu-id="b0dcb-126">Požadováno</span><span class="sxs-lookup"><span data-stu-id="b0dcb-126">Required</span></span> | <span data-ttu-id="b0dcb-127">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-127">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="b0dcb-128">**MinClientVersion**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-128">**minClientVersion**</span></span> | <span data-ttu-id="b0dcb-129">Ne</span><span class="sxs-lookup"><span data-stu-id="b0dcb-129">No</span></span> | <span data-ttu-id="b0dcb-130">Určuje minimální verzi klienta NuGet, který můžete nainstalovat tento balíček vynucováno nuget.exe a Správce balíčků Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-130">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="b0dcb-131">Používá se vždy, když balíček závisí na specifické funkce `.nuspec` souborů, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-131">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="b0dcb-132">Například balíčku pomocí `developmentDependency` atribut by měl určovat "2.8" pro `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-132">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="b0dcb-133">Podobně balíčku pomocí `contentFiles` (viz další část) musí nastavit element `minClientVersion` k "3.3".</span><span class="sxs-lookup"><span data-stu-id="b0dcb-133">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="b0dcb-134">Poznámka: protože klienty NuGet před 2.5 nerozpoznávají tento příznak, budou *vždy* odmítnout k instalaci balíčku bez ohledu na to, co `minClientVersion` obsahuje.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-134">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="b0dcb-135">Požadovaná metadata elementy</span><span class="sxs-lookup"><span data-stu-id="b0dcb-135">Required metadata elements</span></span>

<span data-ttu-id="b0dcb-136">I když tyto prvky jsou minimální požadavky pro balíček, měli byste zvážit přidání [volitelná metadata elementy](#optional-metadata-elements) celkové lepší vývojáři mají spolu s balíčkem.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-136">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="b0dcb-137">Tyto prvky musí být v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-137">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="b0dcb-138">Prvek</span><span class="sxs-lookup"><span data-stu-id="b0dcb-138">Element</span></span> | <span data-ttu-id="b0dcb-139">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0dcb-140">**id**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-140">**id**</span></span> | <span data-ttu-id="b0dcb-141">Identifikátor balíčku velká a malá písmena, která musí být jedinečný v rámci nuget.org nebo jiná balíčku se nachází v galerii.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-141">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="b0dcb-142">ID nesmí obsahovat mezery nebo znaky, které nejsou platné pro adresu URL a obecně podle oboru názvů pravidla technologie .NET.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-142">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="b0dcb-143">V tématu [výběr balíčku jedinečný identifikátor](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) pokyny.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-143">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="b0dcb-144">**Verze**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-144">**version**</span></span> | <span data-ttu-id="b0dcb-145">Verze balíčku, následující *major.minor.patch* vzor.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-145">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="b0dcb-146">Čísla verzí může zahrnovat příponu předběžné verze, jak je popsáno v [Správa verzí balíčku](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-146">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="b0dcb-147">**Popis**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-147">**description**</span></span> | <span data-ttu-id="b0dcb-148">Dlouhý popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-148">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="b0dcb-149">**Autoři**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-149">**authors**</span></span> | <span data-ttu-id="b0dcb-150">Seznam balíčků autoři, odpovídající profil názvy v nuget.org oddělených čárkami. Tyto jsou zobrazeny v galerii NuGet v nuget.org a jsou používané pro křížovou balíčky autory stejné.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="b0dcb-151">Volitelná metadata elementy</span><span class="sxs-lookup"><span data-stu-id="b0dcb-151">Optional metadata elements</span></span>

<span data-ttu-id="b0dcb-152">Může se zobrazit tyto prvky v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-152">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="b0dcb-153">Jednotlivé prvky</span><span class="sxs-lookup"><span data-stu-id="b0dcb-153">Single elements</span></span>

| <span data-ttu-id="b0dcb-154">Prvek</span><span class="sxs-lookup"><span data-stu-id="b0dcb-154">Element</span></span> | <span data-ttu-id="b0dcb-155">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-155">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0dcb-156">**Název**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-156">**title**</span></span> | <span data-ttu-id="b0dcb-157">Lidské popisný název balíčku, obvykle používaných v zobrazení uživatelského rozhraní na nuget.org a Správce balíčků v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-157">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="b0dcb-158">Pokud není zadaný, použije se ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-158">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="b0dcb-159">**Vlastníci**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-159">**owners**</span></span> | <span data-ttu-id="b0dcb-160">Seznam creators balíček pomocí profilu názvy v nuget.org oddělených čárkami. Tento problém je často seznamu stejné jako v `authors`a při odesílání balíčku pro nuget.org ignorováno. V tématu [Správa vlastníků balíčku na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-160">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="b0dcb-161">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-161">**projectUrl**</span></span> | <span data-ttu-id="b0dcb-162">Zobrazí adresu URL pro domovskou stránku balíčku, často se zobrazí v uživatelském rozhraní a také nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-162">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="b0dcb-163">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-163">**licenseUrl**</span></span> | <span data-ttu-id="b0dcb-164">Adresa URL pro balíčku licenci, často se zobrazí v zobrazení uživatelského rozhraní, jakož i nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-164">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="b0dcb-165">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-165">**iconUrl**</span></span> | <span data-ttu-id="b0dcb-166">Adresu URL pro bitovou kopii 64 x 64 s průhlednost pozadí chcete použít jako ikonu balíčku v zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-166">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="b0dcb-167">Ujistěte se, obsahuje tento element *přímá adresa URL obrázku* nikoli adresa URL webové stránky, který obsahuje bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-167">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="b0dcb-168">Například pokud chcete použít bitovou kopii z Githubu, použijte soubor raw, jako adresa URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-168">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> |
| <span data-ttu-id="b0dcb-169">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-169">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="b0dcb-170">Logická hodnota určující, jestli klient musí zobrazovat výzvu k příjemce tak, aby přijímal licenční balíček před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-170">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="b0dcb-171">**DevelopmentDependency**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-171">**developmentDependency**</span></span> | <span data-ttu-id="b0dcb-172">*(2.8 +)*  A logickou hodnotu určující, zda tento balíček je označit jako vývoj jen závislost, která zabraňuje balíček zahrnutí v závislosti na dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-172">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="b0dcb-173">**Souhrn**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-173">**summary**</span></span> | <span data-ttu-id="b0dcb-174">Stručný popis balíčku pro zobrazení uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-174">A short description of the package for UI display.</span></span> <span data-ttu-id="b0dcb-175">Pokud tento parametr vynechán, zkrácený verzi `description` se používá.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-175">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="b0dcb-176">**ReleaseNotes**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-176">**releaseNotes**</span></span> | <span data-ttu-id="b0dcb-177">*(1.5 +)*  Popis změn provedených v této verzi balíčku, často se používá v uživatelském rozhraní, jako **aktualizace** karta nástroje Visual Studio Správce balíčků místo Popis balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-177">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="b0dcb-178">**Copyright**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-178">**copyright**</span></span> | <span data-ttu-id="b0dcb-179">*(1.5 +)*  Copyright podrobnosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-179">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="b0dcb-180">**Jazyk**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-180">**language**</span></span> | <span data-ttu-id="b0dcb-181">ID národního prostředí pro daný balíček.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-181">The locale ID for the package.</span></span> <span data-ttu-id="b0dcb-182">V tématu [vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-182">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="b0dcb-183">**Značky**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-183">**tags**</span></span>  | <span data-ttu-id="b0dcb-184">Mezerami oddělený seznam značek a klíčová slova, která popisují možnosti rozpoznání balíčku a podpory balíčků prostřednictvím vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-184">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="b0dcb-185">**možnost změny**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-185">**serviceable**</span></span> | <span data-ttu-id="b0dcb-186">*(3.3 +)*  Pouze pro interní NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-186">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="b0dcb-187">Elementy v kolekci</span><span class="sxs-lookup"><span data-stu-id="b0dcb-187">Collection elements</span></span>

| <span data-ttu-id="b0dcb-188">Prvek</span><span class="sxs-lookup"><span data-stu-id="b0dcb-188">Element</span></span> | <span data-ttu-id="b0dcb-189">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-189">Description</span></span> |
| --- | --- |
<span data-ttu-id="b0dcb-190">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-190">**packageTypes**</span></span> | <span data-ttu-id="b0dcb-191">*(3.5 +)*  Kolekce nula nebo více `<packageType>` elementy určení typu balíčku Pokud než tradiční závislost balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-191">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="b0dcb-192">Každý packageType má atributy *název* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-192">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="b0dcb-193">V tématu [nastavení typ balíčku](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-193">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="b0dcb-194">**Závislosti**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-194">**dependencies**</span></span> | <span data-ttu-id="b0dcb-195">Kolekce nula nebo více `<dependency>` elementy určení závislostí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-195">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="b0dcb-196">Každá závislost má atributy *id*, *verze*, *zahrnují* (3.x+), a *vyloučit* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-196">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="b0dcb-197">V tématu [závislosti](#dependencies) níže.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-197">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="b0dcb-198">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-198">**frameworkAssemblies**</span></span> | <span data-ttu-id="b0dcb-199">*(1.2 +)*  Kolekce nula nebo více `<frameworkAssembly>` elementy identifikace odkazy na sestavení rozhraní .NET Framework, které tento balíček vyžaduje, což zajistí, že odkazy jsou přidány do projekty využívající balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-199">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="b0dcb-200">Má každý frameworkAssembly *assemblyName* a *targetFramework* atributy.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-200">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="b0dcb-201">V tématu [zadání sestavení rozhraní odkazuje GAC](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-201">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="b0dcb-202">**Odkazy**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-202">**references**</span></span> | <span data-ttu-id="b0dcb-203">*(1.5 +)*  Kolekce nula nebo více `<reference>` elementy pojmenování sestavení v balíčku `lib` složky, které jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-203">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="b0dcb-204">Má každý odkaz *souboru* atribut.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-204">Each reference has a *file* attribute.</span></span> <span data-ttu-id="b0dcb-205">`<references>` může také obsahovat `<group>` element s *targetFramework* atribut, který pak obsahuje `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-205">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="b0dcb-206">Pokud tento parametr vynechán, všechny odkazy v `lib` jsou zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-206">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="b0dcb-207">V tématu [zadání odkazy na sestavení explicitní](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-207">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="b0dcb-208">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-208">**contentFiles**</span></span> | <span data-ttu-id="b0dcb-209">*(3.3 +)*  Kolekce `<files>` prvky, které identifikují soubory obsahu pro zahrnutí do projektu náročná.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-209">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="b0dcb-210">Tyto soubory jsou určeny sadu atributů, které popisují, jak mají být použity v rámci systému projektu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-210">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="b0dcb-211">V tématu [určující soubory, které chcete zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-211">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="b0dcb-212">Files – element</span><span class="sxs-lookup"><span data-stu-id="b0dcb-212">Files element</span></span>

<span data-ttu-id="b0dcb-213">`<package>` Uzel může obsahovat `<files>` uzlu na stejnou úroveň jako `<metadata>`a nebo `<contentFiles>` dítěte mladšího `<metadata>`, určete, které soubory sestavení a obsah balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-213">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="b0dcb-214">V tématu [včetně souborů sestavení](#including-assembly-files) a [včetně soubory obsahu](#including-content-files) dál v tomto tématu podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-214">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="b0dcb-215">Nahrazení tokenů</span><span class="sxs-lookup"><span data-stu-id="b0dcb-215">Replacement tokens</span></span>

<span data-ttu-id="b0dcb-216">Při vytváření balíčku, [ `nuget pack` příkaz](../tools/cli-ref-pack.md) nahrazuje oddělený $ tokeny v `.nuspec` souboru `<metadata>` uzlu s hodnotami, které pocházejí z buď soubor projektu nebo `pack` příkazu `-properties`přepínače.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-216">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="b0dcb-217">Na příkazovém řádku, zadejte hodnoty tokenu s `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-217">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="b0dcb-218">Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a zadejte hodnoty v balení čas následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-218">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="b0dcb-219">Chcete-li použít hodnoty z projektu, zadejte tokeny popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` například `AssemblyInfo.cs` nebo `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-219">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="b0dcb-220">Pokud chcete použít tyto tokeny, spusťte `nuget pack` do souboru projektu spíše než jenom `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-220">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="b0dcb-221">Například když pomocí následujícího příkazu `$id$` a `$version$` tokeny v `.nuspec` soubor se nahradí projektu `AssemblyName` a `AssemblyVersion` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-221">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="b0dcb-222">Obvykle, když máte projekt, můžete vytvořit `.nuspec` původně pomocí `nuget spec MyProject.csproj` který automaticky zahrnuje některé tyto standardní tokeny.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-222">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="b0dcb-223">Ale pokud projektu chybí hodnoty pro požadované `.nuspec` elementy, pak `nuget pack` selže.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-223">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="b0dcb-224">Kromě toho pokud změníte projektu hodnoty, je nutné znovu vytvořit před vytvořením balíčku. To lze provést pohodlně pomocí příkazu pack `build` přepínače.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-224">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="b0dcb-225">S výjimkou produktů `$configuration$`, jsou všechny přiřazen stejný token na příkazovém řádku použít hodnoty v projektu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-225">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="b0dcb-226">Token</span><span class="sxs-lookup"><span data-stu-id="b0dcb-226">Token</span></span> | <span data-ttu-id="b0dcb-227">Hodnota zdroje</span><span class="sxs-lookup"><span data-stu-id="b0dcb-227">Value source</span></span> | <span data-ttu-id="b0dcb-228">Hodnota</span><span class="sxs-lookup"><span data-stu-id="b0dcb-228">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="b0dcb-229">**$id$**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-229">**$id$**</span></span> | <span data-ttu-id="b0dcb-230">soubor projektu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-230">Project file</span></span> | <span data-ttu-id="b0dcb-231">AssemblyName (title) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-231">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="b0dcb-232">**$version$**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-232">**$version$**</span></span> | <span data-ttu-id="b0dcb-233">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b0dcb-233">AssemblyInfo</span></span> | <span data-ttu-id="b0dcb-234">AssemblyInformationalVersion, pokud existuje, jinak hodnota AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="b0dcb-234">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="b0dcb-235">**$author$**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-235">**$author$**</span></span> | <span data-ttu-id="b0dcb-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b0dcb-236">AssemblyInfo</span></span> | <span data-ttu-id="b0dcb-237">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="b0dcb-237">AssemblyCompany</span></span> |
| <span data-ttu-id="b0dcb-238">**$title$**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-238">**$title$**</span></span> | <span data-ttu-id="b0dcb-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b0dcb-239">AssemblyInfo</span></span> | <span data-ttu-id="b0dcb-240">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="b0dcb-240">AssemblyTitle</span></span> |
| <span data-ttu-id="b0dcb-241">**$description$**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-241">**$description$**</span></span> | <span data-ttu-id="b0dcb-242">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b0dcb-242">AssemblyInfo</span></span> | <span data-ttu-id="b0dcb-243">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="b0dcb-243">AssemblyDescription</span></span> |
| <span data-ttu-id="b0dcb-244">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-244">**$copyright$**</span></span> | <span data-ttu-id="b0dcb-245">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="b0dcb-245">AssemblyInfo</span></span> | <span data-ttu-id="b0dcb-246">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="b0dcb-246">AssemblyCopyright</span></span> |
| <span data-ttu-id="b0dcb-247">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-247">**$configuration$**</span></span> | <span data-ttu-id="b0dcb-248">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="b0dcb-248">Assembly DLL</span></span> | <span data-ttu-id="b0dcb-249">Konfigurace použitá k vytvoření sestavení, jako výchozí bude použit k ladění.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-249">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="b0dcb-250">Upozorňujeme, že pokud chcete vytvořit balíček pomocí konfigurace verze, můžete vždy použít `-properties Configuration=Release` na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-250">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="b0dcb-251">Tokeny lze také vyřešit cesty, jakmile zahrnete [soubory sestavení](#including-assembly-files) a [obsahu souborů](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-251">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="b0dcb-252">Tokeny mají stejné názvy jako vlastnosti nástroje MSBuild, což umožňuje vyberte soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-252">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="b0dcb-253">Například, pokud používáte následující klíčová slova v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-253">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="b0dcb-254">A vytváření sestavení jejichž `AssemblyName` je `LoggingLibrary` s `Release` konfigurace v nástroji MSBuild, výsledná řádků v `.nuspec` souboru v balíčku je následující:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-254">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="b0dcb-255">Závislosti</span><span class="sxs-lookup"><span data-stu-id="b0dcb-255">Dependencies</span></span>

<span data-ttu-id="b0dcb-256">`<dependencies>` v rámci `<metadata>` obsahuje libovolný počet `<dependency>` elementy, které identifikují další balíčky, na kterých závisí balíček nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-256">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="b0dcb-257">Atributy pro každou `<dependency>` jsou následující:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-257">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="b0dcb-258">Atribut</span><span class="sxs-lookup"><span data-stu-id="b0dcb-258">Attribute</span></span> | <span data-ttu-id="b0dcb-259">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-259">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="b0dcb-260">(Povinné) ID balíčku závislosti, jako je například "EntityFramework" a "NUnit", což je název nuget.org balíčku se zobrazí na stránce balíček.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-260">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="b0dcb-261">(Povinné) Rozsah verze přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-261">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="b0dcb-262">V tématu [Správa verzí balíčku](../reference/package-versioning.md#version-ranges-and-wildcards) pro přesná syntaxe.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-262">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="b0dcb-263">include</span><span class="sxs-lookup"><span data-stu-id="b0dcb-263">include</span></span> | <span data-ttu-id="b0dcb-264">Čárkami oddělený seznam zahrnutí a vyloučení značky (viz níže), která určuje závislosti, které chcete zahrnout do konečné balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-264">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="b0dcb-265">Výchozí hodnota je `none`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-265">The default value is `none`.</span></span> |
| <span data-ttu-id="b0dcb-266">exclude</span><span class="sxs-lookup"><span data-stu-id="b0dcb-266">exclude</span></span> | <span data-ttu-id="b0dcb-267">Čárkami oddělený seznam zahrnutí a vyloučení značky (viz níže), která určuje závislosti k vyloučení z poslední balíček.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-267">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="b0dcb-268">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-268">The  default value is `all`.</span></span> <span data-ttu-id="b0dcb-269">Značky s `exclude` mají přednost před uvedenými s `include`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-269">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="b0dcb-270">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-270">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="b0dcb-271">Zahrnutí a vyloučení značky</span><span class="sxs-lookup"><span data-stu-id="b0dcb-271">Include/Exclude tag</span></span> | <span data-ttu-id="b0dcb-272">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="b0dcb-272">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="b0dcb-273">contentFiles</span><span class="sxs-lookup"><span data-stu-id="b0dcb-273">contentFiles</span></span> | <span data-ttu-id="b0dcb-274">Obsah</span><span class="sxs-lookup"><span data-stu-id="b0dcb-274">Content</span></span> |
| <span data-ttu-id="b0dcb-275">modul runtime</span><span class="sxs-lookup"><span data-stu-id="b0dcb-275">runtime</span></span> | <span data-ttu-id="b0dcb-276">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="b0dcb-276">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="b0dcb-277">Kompilace</span><span class="sxs-lookup"><span data-stu-id="b0dcb-277">compile</span></span> | <span data-ttu-id="b0dcb-278">Lib</span><span class="sxs-lookup"><span data-stu-id="b0dcb-278">lib</span></span> |
| <span data-ttu-id="b0dcb-279">sestavení</span><span class="sxs-lookup"><span data-stu-id="b0dcb-279">build</span></span> | <span data-ttu-id="b0dcb-280">sestavení (MSBuild props a cíle)</span><span class="sxs-lookup"><span data-stu-id="b0dcb-280">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="b0dcb-281">nativní</span><span class="sxs-lookup"><span data-stu-id="b0dcb-281">native</span></span> | <span data-ttu-id="b0dcb-282">nativní</span><span class="sxs-lookup"><span data-stu-id="b0dcb-282">native</span></span> |
| <span data-ttu-id="b0dcb-283">žádná</span><span class="sxs-lookup"><span data-stu-id="b0dcb-283">none</span></span> | <span data-ttu-id="b0dcb-284">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="b0dcb-284">No folders</span></span> |
| <span data-ttu-id="b0dcb-285">všechny</span><span class="sxs-lookup"><span data-stu-id="b0dcb-285">all</span></span> | <span data-ttu-id="b0dcb-286">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="b0dcb-286">All folders</span></span> |

<span data-ttu-id="b0dcb-287">Například následující řádky označovat závislosti na `PackageA` verze 1.1.0 nebo vyšší, a `PackageB` verze 1.x.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-287">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="b0dcb-288">Následující řádky znamenat závislostí na stejné balíčky, ale zadat zahrnout `contentFiles` a `build` složky `PackageA` a všechno ale `native` a `compile` složky `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="b0dcb-288">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="b0dcb-289">Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`, závislosti, které existují v tomto projektu jsou automaticky součástí výsledná `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-289">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="b0dcb-290">Závislost skupiny</span><span class="sxs-lookup"><span data-stu-id="b0dcb-290">Dependency groups</span></span>

<span data-ttu-id="b0dcb-291">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-291">*Version 2.0+*</span></span>

<span data-ttu-id="b0dcb-292">Jako alternativu k jediný plochý seznam závislosti lze podle profil framework cílový projekt pomocí `<group>` elementů v rámci `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-292">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="b0dcb-293">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nula nebo více `<dependency>` elementy.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-293">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="b0dcb-294">Tyto závislosti jsou nainstalovány společně při cílovém Frameworku, který je kompatibilní s profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-294">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="b0dcb-295">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam závislosti.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-295">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="b0dcb-296">V tématu [cílové rozhraní](../reference/target-frameworks.md) pro identifikátory přesný framework.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-296">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="b0dcb-297">Formát skupiny nelze smíšeného s jako plochý seznam.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-297">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="b0dcb-298">Následující příklad ukazuje různých variant `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-298">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="b0dcb-299">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="b0dcb-299">Explicit assembly references</span></span>

<span data-ttu-id="b0dcb-300">`<references>` Element explicitně určuje ta sestavení, které cílový projekt by měl odkazovat při použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-300">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="b0dcb-301">Když se nachází tento element, NuGet přidáte odkazy na sestavení pouze uvedené; nepřidá odkazy pro všechny ostatní sestavení v balíčku `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-301">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="b0dcb-302">Například následující `<references>` element dá pokyn NuGet, čímž přidáte odkazy na pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že existují další sestavení v balíčku:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-302">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="b0dcb-303">Explicitní odkazy jsou obvykle používány pro návrh jen sestavení.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-303">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="b0dcb-304">Při použití [kontrakty kódu](/dotnet/framework/debug-trace-profile/code-contracts), například sestavení smlouvy musí být vedle sestavení modulu runtime, která budou posílení, aby Visual Studio můžete najít, ale sestavení kontrakt nemusí být odkazuje projektu nebo zkopírovat do projektu `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-304">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="b0dcb-305">Podobně explicitní odkazy lze systémů testů jednotek, jako je například XUnit, který se musí jeho nástroje pro sestavení vedle sestavení za běhu, ale nemá potřebovat, je zahrnuta jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-305">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="b0dcb-306">Odkazové skupiny</span><span class="sxs-lookup"><span data-stu-id="b0dcb-306">Reference groups</span></span>

<span data-ttu-id="b0dcb-307">Jako alternativu k jediný plochý seznam odkazů na lze podle profil framework cílový projekt pomocí `<group>` elementů v rámci `<references>`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-307">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="b0dcb-308">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nula nebo více `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-308">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="b0dcb-309">Tyto odkazy se přidají do projektu, když cílovém Frameworku, který je kompatibilní s profilem framework projektu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-309">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="b0dcb-310">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam odkazů.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="b0dcb-311">V tématu [cílové rozhraní](../reference/target-frameworks.md) pro identifikátory přesný framework.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="b0dcb-312">Formát skupiny nelze smíšeného s jako plochý seznam.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="b0dcb-313">Následující příklad ukazuje různých variant `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-313">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="b0dcb-314">Odkazy na sestavení Framework</span><span class="sxs-lookup"><span data-stu-id="b0dcb-314">Framework assembly references</span></span>

<span data-ttu-id="b0dcb-315">Sestavení architektury jsou ty, které jsou součástí rozhraní .NET framework a by už měla být v globální mezipaměti sestavení (GAC) pro všechny daný počítač.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-315">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="b0dcb-316">Určením těchto sestavení v rámci `<frameworkAssemblies>` elementu balíček můžete zajistit, že požadované odkazy jsou přidány do projektu, v případě, že projekt již nemá tyto odkazy.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-316">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="b0dcb-317">Takové sestavení samozřejmě nejsou zahrnuty v balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-317">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="b0dcb-318">`<frameworkAssemblies>` Element obsahuje nula nebo více `<frameworkAssembly>` prvky, z nichž každý určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-318">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="b0dcb-319">Atribut</span><span class="sxs-lookup"><span data-stu-id="b0dcb-319">Attribute</span></span> | <span data-ttu-id="b0dcb-320">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-320">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0dcb-321">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-321">**assemblyName**</span></span> | <span data-ttu-id="b0dcb-322">(Povinné) Plně kvalifikovaný název.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-322">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="b0dcb-323">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-323">**targetFramework**</span></span> | <span data-ttu-id="b0dcb-324">(Volitelné) Určuje cílový framework, pro kterou platí tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-324">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="b0dcb-325">Pokud tento parametr vynechán, označuje, že odkaz na použije pro všechna rozhraní.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-325">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="b0dcb-326">V tématu [cílové rozhraní](../reference/target-frameworks.md) pro identifikátory přesný framework.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-326">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="b0dcb-327">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové architektury a odkaz na `System.ServiceModel` pro pouze rozhraní .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-327">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="b0dcb-328">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="b0dcb-328">Including assembly files</span></span>

<span data-ttu-id="b0dcb-329">Pokud budete postupovat podle konvence popsané v [vytváření balíčku](../create-packages/creating-a-package.md), není nutné explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-329">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="b0dcb-330">`nuget pack` Příkaz automaticky převezme potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-330">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="b0dcb-331">Při instalaci balíčku do projektu NuGet automaticky přidá odkazy na sestavení pro knihovny DLL balíčku, *s výjimkou* ty, které jsou s názvem `.resources.dll` vzhledem k tomu, že se předpokládá, že lokalizované satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-331">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="b0dcb-332">Z tohoto důvodu vyhýbat se používání `.resources.dll` pro soubory, které jinak obsahují nezbytné balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-332">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="b0dcb-333">Nepoužívat toto automatické chování a explicitně řídit soubory, které jsou součástí balíčku, umístit `<files>` jako podřízený element `<package>` (a na stejné úrovni jako `<metadata>`), identifikace každý soubor s samostatné `<file>` element.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-333">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="b0dcb-334">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-334">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="b0dcb-335">U balíčku NuGet 2.x a starší a projektů pomocí `packages.config`, `<files>` element se používá i k zahrnují neměnné soubory obsahu při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-335">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="b0dcb-336">S NuGet 3.3 + a projekty PackageReference `<contentFiles>` element se používá místo.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-336">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="b0dcb-337">V tématu [včetně soubory obsahu](#including-content-files) níže podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-337">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="b0dcb-338">Element atributy souboru</span><span class="sxs-lookup"><span data-stu-id="b0dcb-338">File element attributes</span></span>

<span data-ttu-id="b0dcb-339">Každý `<file>` element určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-339">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="b0dcb-340">Atribut</span><span class="sxs-lookup"><span data-stu-id="b0dcb-340">Attribute</span></span> | <span data-ttu-id="b0dcb-341">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-341">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0dcb-342">**src**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-342">**src**</span></span> | <span data-ttu-id="b0dcb-343">Umístění souboru nebo soubory, které chcete zahrnout, podstoupí vyloučení určeného `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-343">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="b0dcb-344">Cesta je vzhledem k `.nuspec` souboru uvedeno absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-344">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="b0dcb-345">Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-345">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="b0dcb-346">**cíl**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-346">**target**</span></span> | <span data-ttu-id="b0dcb-347">Relativní cesta ke složce v rámci balíčku umístění zdrojových souborů, které musí začínat `lib`, `content`, `build`, nebo `tools`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-347">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="b0dcb-348">V tématu [vytváření příponou .nuspec z pracovního adresáře založené na konvenci](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-348">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="b0dcb-349">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-349">**exclude**</span></span> | <span data-ttu-id="b0dcb-350">Seznam oddělený středníkem souborů nebo vzorů souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-350">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="b0dcb-351">Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-351">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="b0dcb-352">Příklady</span><span class="sxs-lookup"><span data-stu-id="b0dcb-352">Examples</span></span>

<span data-ttu-id="b0dcb-353">**Jednoho sestavení**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-353">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="b0dcb-354">**Jediné sestavení, které jsou specifické pro cílové prostředí**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-354">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="b0dcb-355">**Sada knihovny DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-355">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="b0dcb-356">**Knihovny DLL pro různé rozhraní**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-356">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="b0dcb-357">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-357">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="b0dcb-358">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-358">Including content files</span></span>

<span data-ttu-id="b0dcb-359">Soubory obsahu jsou neměnné soubory, které je potřeba zahrnout do projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-359">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="b0dcb-360">Se nedá změnit, nejsou určeny k využívání projektu upravit.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-360">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="b0dcb-361">Soubory obsahu příklad patří:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-361">Example content files include:</span></span>

- <span data-ttu-id="b0dcb-362">Bitové kopie, které jsou vloženy jako prostředky</span><span class="sxs-lookup"><span data-stu-id="b0dcb-362">Images that are embedded as resources</span></span>
- <span data-ttu-id="b0dcb-363">Zdrojové soubory, které jsou již kompilovat</span><span class="sxs-lookup"><span data-stu-id="b0dcb-363">Source files that are already compiled</span></span>
- <span data-ttu-id="b0dcb-364">Skripty, které musí být součástí výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-364">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="b0dcb-365">Konfigurační soubory pro balíček, který mají být zahrnuti v projektu, ale nemusí změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="b0dcb-365">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="b0dcb-366">Obsahu souborů jsou součástí balíčku pomocí `<files>` elementu, určení `content` složky v `target` atribut.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-366">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="b0dcb-367">Ale tyto soubory jsou při instalaci balíčku v projektu pomocí PackageReference, který používá místo ignorovány `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-367">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="b0dcb-368">Pro maximální kompatibility s využívání projekty balíček v ideálním případě Určuje soubory obsahu v obou elementů.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-368">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="b0dcb-369">Pomocí elementu soubory souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-369">Using the files element for content files</span></span>

<span data-ttu-id="b0dcb-370">Pro soubory obsahu, stačí použít stejný formát jako soubory sestavení, ale zadat `content` jako základní složka v `target` atribut podle následujících příkladů.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-370">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="b0dcb-371">**Základní soubory obsahu**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-371">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="b0dcb-372">**Soubory obsahu s adresářovou strukturu**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-372">**Content files with directory structure**</span></span>

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

<span data-ttu-id="b0dcb-373">**Obsah souboru, které jsou specifické pro cílové prostředí**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-373">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="b0dcb-374">**Zkopírován do složky s tečkou v názvu souboru obsahu**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-374">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="b0dcb-375">V takovém případě který NuGet uvidí rozšíření v `target` se neshoduje s příponou v `src` a proto považuje část názvu v `target` jako složku:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-375">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="b0dcb-376">**Soubory obsahu bez přípony**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-376">**Content files without extensions**</span></span>

<span data-ttu-id="b0dcb-377">Chcete-li zahrnout soubory bez přípony, použijte `*` nebo `**` zástupné znaky:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-377">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="b0dcb-378">**Soubory obsahu s hloubkovým cestou a hloubkového cíl**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-378">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="b0dcb-379">V takovém případě protože přípony souborů zdrojové a cílové shodují, NuGet předpokládá, že cíl je název souboru a nikoliv složka:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-379">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="b0dcb-380">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-380">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="b0dcb-381">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-381">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="b0dcb-382">Pomocí elementu contentFiles souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="b0dcb-382">Using the contentFiles element for content files</span></span>

<span data-ttu-id="b0dcb-383">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="b0dcb-383">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="b0dcb-384">Výchozí umístění obsahu v balíčku `contentFiles` složky (viz níže) a `nuget pack` zahrnuty všechny soubory v této složce pomocí výchozí atributy.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-384">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="b0dcb-385">V takovém případě není nutné zahrnovat `contentFiles` uzlu `.nuspec` vůbec.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-385">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="b0dcb-386">K řízení, které soubory jsou zahrnuty `<contentFiles>` element určuje je kolekce `<files>` prvky, které identifikují přesný soubory patří.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-386">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="b0dcb-387">Tyto soubory jsou určeny sadu atributů, které popisují, jak mají být použity v rámci systému projektu:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-387">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="b0dcb-388">Atribut</span><span class="sxs-lookup"><span data-stu-id="b0dcb-388">Attribute</span></span> | <span data-ttu-id="b0dcb-389">Popis</span><span class="sxs-lookup"><span data-stu-id="b0dcb-389">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0dcb-390">**Zahrnout**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-390">**include**</span></span> | <span data-ttu-id="b0dcb-391">(Povinné) Umístění souboru nebo soubory, které chcete zahrnout, podstoupí vyloučení určeného `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-391">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="b0dcb-392">Cesta je vzhledem k `.nuspec` souboru uvedeno absolutní cesta.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-392">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="b0dcb-393">Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-393">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="b0dcb-394">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-394">**exclude**</span></span> | <span data-ttu-id="b0dcb-395">Seznam oddělený středníkem souborů nebo vzorů souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-395">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="b0dcb-396">Zástupný znak `*` je povolen a dvojité zástupných znaků `**` znamená rekurzivní složky hledání.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-396">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="b0dcb-397">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-397">**buildAction**</span></span> | <span data-ttu-id="b0dcb-398">Akce sestavení přiřadit položku obsahu pro MSBuild, jako například `Content`, `None`, `Embedded Resource`, `Compile`atd. Výchozí hodnota je `Compile`.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-398">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="b0dcb-399">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-399">**copyToOutput**</span></span> | <span data-ttu-id="b0dcb-400">Logická hodnota, která určuje, zda zkopírovat obsahu položky do sestavení (nebo publikování) výstupní složky.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-400">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="b0dcb-401">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-401">The default is false.</span></span> |
| <span data-ttu-id="b0dcb-402">**vyrovnání**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-402">**flatten**</span></span> | <span data-ttu-id="b0dcb-403">Logická hodnota, která určuje, jestli kopírování obsahu položky do jediné složky ve výstupu sestavení (true) nebo chcete zachovat struktura složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-403">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="b0dcb-404">Tento příznak pouze funguje, když je příznak copyToOutput nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-404">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="b0dcb-405">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-405">The default is false.</span></span> |

<span data-ttu-id="b0dcb-406">Při instalaci balíčku, NuGet platí podřízených elementů `<contentFiles>` shora dolů.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-406">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="b0dcb-407">Pokud stejný soubor shodovat s více položek se použijí všechny položky.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-407">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="b0dcb-408">Položka nejvyšší přepíše nižší položky, pokud dojde ke konfliktu pro stejný atribut.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-408">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="b0dcb-409">Struktura složek balíčku</span><span class="sxs-lookup"><span data-stu-id="b0dcb-409">Package folder structure</span></span>

<span data-ttu-id="b0dcb-410">Balíček projekt by měl struktury obsah pomocí následujícího vzorce:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-410">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="b0dcb-411">`codeLanguages` může být `cs`, `vb`, `fs`, `any`, nebo malá ekvivalent danou `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-411">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="b0dcb-412">`TxM` je všechny Přezdívka právní cílový framework, který NuGet podporuje (viz [cílové rozhraní](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="b0dcb-412">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="b0dcb-413">Libovolné struktury složek může připojen na konec této syntaxe.</span><span class="sxs-lookup"><span data-stu-id="b0dcb-413">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="b0dcb-414">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-414">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="b0dcb-415">Můžete použít prázdné složky `.` pro vyjádření výslovného nesouhlasu poskytování obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-415">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="b0dcb-416">Příklad contentFiles části</span><span class="sxs-lookup"><span data-stu-id="b0dcb-416">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="b0dcb-417">Příklad příponou .nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="b0dcb-417">Example .nuspec files</span></span>

<span data-ttu-id="b0dcb-418">**Jednoduchý `.nuspec` která neurčuje závislosti nebo soubory**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-418">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="b0dcb-419">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-419">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="b0dcb-420">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-420">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="b0dcb-421">**A `.nuspec` s framework sestavení**</span><span class="sxs-lookup"><span data-stu-id="b0dcb-421">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="b0dcb-422">V tomto příkladu následující se nainstalují pro konkrétní projekt cíle:</span><span class="sxs-lookup"><span data-stu-id="b0dcb-422">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="b0dcb-423">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-423">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="b0dcb-424">. NET4 -> Client Profile `System.Net`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-424">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="b0dcb-425">-> Silverlight 3 `System.Json`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-425">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="b0dcb-426">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-426">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="b0dcb-427">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="b0dcb-427">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
