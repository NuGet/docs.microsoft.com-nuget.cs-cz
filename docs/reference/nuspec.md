---
title: Odkaz na soubor souboru .nuspec pro NuGet
description: Souboru .nuspec soubor obsahuje metadata balíčků používat při vytváření balíčku a zadejte informace pro spotřebitele balíčku.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6d190d9fdb26d76fa8e46b7d283c1857cfab26e9
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508033"
---
# <a name="nuspec-reference"></a><span data-ttu-id="aa3b2-103">odkaz na souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="aa3b2-103">.nuspec reference</span></span>

<span data-ttu-id="aa3b2-104">A `.nuspec` je soubor manifestu XML, který obsahuje metadata balíčků.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="aa3b2-105">Tento manifest slouží k vytvoření balíčku a zadejte informace pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="aa3b2-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="aa3b2-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-107">In this topic:</span></span>

- [<span data-ttu-id="aa3b2-108">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="aa3b2-109">[Nahrazení tokeny](#replacement-tokens) (při použití s projektu sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="aa3b2-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="aa3b2-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="aa3b2-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="aa3b2-111">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="aa3b2-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="aa3b2-112">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="aa3b2-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="aa3b2-113">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="aa3b2-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="aa3b2-114">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="aa3b2-115">Příklad souboru nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="aa3b2-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="aa3b2-116">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-116">General form and schema</span></span>

<span data-ttu-id="aa3b2-117">Aktuální `nuspec.xsd` soubor schématu najdete v [úložiště NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="aa3b2-118">V tomto schématu `.nuspec` soubor má následující Obecné formuláře:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="aa3b2-119">Vizuální znázornění schématu, otevřete soubor schématu v sadě Visual Studio v režimu návrhu a klikněte **Průzkumníka schémat XML** odkaz.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="aa3b2-120">Alternativně otevřete soubor jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **zobrazení Průzkumníka schémat XML**.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="aa3b2-121">V obou případech, které získáte zobrazení jako na následující (v rozbaleném většinou):</span><span class="sxs-lookup"><span data-stu-id="aa3b2-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Průzkumníka schémat s nuspec.xsd otevřít](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="aa3b2-123">Metadata atributů</span><span class="sxs-lookup"><span data-stu-id="aa3b2-123">Metadata attributes</span></span>

### <a name="required-metadata-elements"></a><span data-ttu-id="aa3b2-124">Prvky požadovaná metadata</span><span class="sxs-lookup"><span data-stu-id="aa3b2-124">Required metadata elements</span></span>

<span data-ttu-id="aa3b2-125">I když tyto prvky jsou minimální požadavky pro balíček, měli byste zvážit přidání [volitelná metadata prvky](#optional-metadata-elements) zlepšit celkové prostředí mají vývojáři součástí vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-125">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="aa3b2-126">Tyto prvky musí být uvedena v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-126">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="aa3b2-127">Prvek</span><span class="sxs-lookup"><span data-stu-id="aa3b2-127">Element</span></span> | <span data-ttu-id="aa3b2-128">Popis</span><span class="sxs-lookup"><span data-stu-id="aa3b2-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa3b2-129">**id**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-129">**id**</span></span> | <span data-ttu-id="aa3b2-130">Identifikátor balíčku velká a malá písmena, která musí být jedinečný v rámci nuget.org nebo cokoli jiného balíčku se nachází v galerii.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-130">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="aa3b2-131">ID nemůže obsahovat mezery nebo znaky, které nejsou platné pro adresu URL a obvykle postupují podle pravidla oboru názvů .NET.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-131">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="aa3b2-132">Zobrazit [výběr balíčku jedinečný identifikátor](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) pokyny.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-132">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="aa3b2-133">**Verze**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-133">**version**</span></span> | <span data-ttu-id="aa3b2-134">Verze balíčku, následující *hlavníverze.podverze.oprava* vzor.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-134">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="aa3b2-135">Čísla verzí může obsahovat příponu předběžné verze, jak je popsáno v [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-135">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="aa3b2-136">**Popis**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-136">**description**</span></span> | <span data-ttu-id="aa3b2-137">Dlouhý popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-137">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="aa3b2-138">**Autoři**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-138">**authors**</span></span> | <span data-ttu-id="aa3b2-139">Čárkou oddělený seznam autorů balíčků, odpovídající názvy profilů na nuget.org. Tyto jsou zobrazeny v galerii NuGet na nuget.org a slouží k křížový odkaz balíčky stejné autory.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-139">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="aa3b2-140">Volitelná metadata elementy</span><span class="sxs-lookup"><span data-stu-id="aa3b2-140">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="aa3b2-141">Název</span><span class="sxs-lookup"><span data-stu-id="aa3b2-141">title</span></span>
<span data-ttu-id="aa3b2-142">Lidské popisný název balíčku, obvykle používaných v uživatelském rozhraní na webech nuget.org a Správce balíčků v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-142">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="aa3b2-143">Pokud není zadán, použije se ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-143">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="aa3b2-144">Vlastníci</span><span class="sxs-lookup"><span data-stu-id="aa3b2-144">owners</span></span>
<span data-ttu-id="aa3b2-145">Čárkou oddělený seznam Tvůrce balíčku pomocí názvy profilů na nuget.org. To je často seznamu stejné jako v `authors`a je ignorován při nahrávání balíčku do nuget.org. Zobrazit [vlastníky Správa balíčků na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-145">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="aa3b2-146">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="aa3b2-146">projectUrl</span></span>
<span data-ttu-id="aa3b2-147">Adresa URL domovské stránky balíčku, často zobrazuje v uživatelském rozhraní nuget.org.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-147">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="aa3b2-148">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="aa3b2-148">licenseUrl</span></span>
<span data-ttu-id="aa3b2-149">Adresa URL licence balíčku, často zobrazuje v uživatelském rozhraní nuget.org.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-149">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="aa3b2-150">IconUrl</span><span class="sxs-lookup"><span data-stu-id="aa3b2-150">iconUrl</span></span>
<span data-ttu-id="aa3b2-151">Adresa URL pro bitovou kopii 64 x 64 s průhlednost pozadí použít jako ikona pro balíček zobrazená v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-151">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="aa3b2-152">Ujistěte se, obsahuje tento element *přímá adresa URL obrázku* nikoli adresa URL webové stránky, který obsahuje bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-152">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="aa3b2-153">Například pokud chcete použít některou image z Githubu, použijte soubor raw, jako je adresa URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-153">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="aa3b2-154">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="aa3b2-154">requireLicenseAcceptance</span></span>
<span data-ttu-id="aa3b2-155">Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-155">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="aa3b2-156">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="aa3b2-156">developmentDependency</span></span>
<span data-ttu-id="aa3b2-157">*(2.8 +)*  Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-157">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span>
#### <a name="summary"></a><span data-ttu-id="aa3b2-158">souhrn</span><span class="sxs-lookup"><span data-stu-id="aa3b2-158">summary</span></span>
<span data-ttu-id="aa3b2-159">Krátký popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-159">A short description of the package for UI display.</span></span> <span data-ttu-id="aa3b2-160">Pokud tento parametr vynechán, zkrácená verze `description` se používá.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-160">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="aa3b2-161">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="aa3b2-161">releaseNotes</span></span>
<span data-ttu-id="aa3b2-162">*(1.5 +)*  Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-162">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="aa3b2-163">Copyright</span><span class="sxs-lookup"><span data-stu-id="aa3b2-163">copyright</span></span>
<span data-ttu-id="aa3b2-164">*(1.5 +)*  Copyright podrobnosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-164">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="aa3b2-165">jazyk</span><span class="sxs-lookup"><span data-stu-id="aa3b2-165">language</span></span>
<span data-ttu-id="aa3b2-166">ID národního prostředí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-166">The locale ID for the package.</span></span> <span data-ttu-id="aa3b2-167">Zobrazit [vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-167">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="aa3b2-168">značky</span><span class="sxs-lookup"><span data-stu-id="aa3b2-168">tags</span></span>
<span data-ttu-id="aa3b2-169">Mezerami oddělený seznam značek a klíčových slov, které popisují balíček a podpora zjistitelnost balíčků prostřednictvím vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-169">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="aa3b2-170">možnost změny</span><span class="sxs-lookup"><span data-stu-id="aa3b2-170">serviceable</span></span> 
<span data-ttu-id="aa3b2-171">*(3.3 +)*  Pouze pro interní NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-171">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="aa3b2-172">úložiště</span><span class="sxs-lookup"><span data-stu-id="aa3b2-172">repository</span></span>
<span data-ttu-id="aa3b2-173">Metadata úložiště, skládající se z čtyři volitelné atributy: *typ* a *url* *(4.0 +)*, a *větev* a  *potvrzení* *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-173">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="aa3b2-174">Tyto atributy umožňují namapovat .nupkg do úložiště, který sestavilo, má potenciál, chcete-li získat podrobné jako jednotlivé větev nebo potvrzení změn, které sestaven balíček.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-174">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="aa3b2-175">To by měl být veřejně dostupnou adresu url, který lze vyvolat přímo pomocí softwaru pro řízení verzí.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-175">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="aa3b2-176">Neměl by být stránku html jako ten je určený pro počítače.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-176">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="aa3b2-177">Pro odkazování na stránku projektu, použijte `projectUrl` pole namísto. |</span><span class="sxs-lookup"><span data-stu-id="aa3b2-177">For linking to project page, use the `projectUrl` field, instead.|</span></span>
#### <a name="minclientversion"></a><span data-ttu-id="aa3b2-178">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="aa3b2-178">minClientVersion</span></span>
<span data-ttu-id="aa3b2-179">Určuje minimální verzi klienta NuGet, který můžete nainstalovat tento balíček, vynucuje nuget.exe a Správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-179">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="aa3b2-180">Používá se pokaždé, když se balíček závisí na konkrétních funkcí služby `.nuspec` souborů, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-180">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="aa3b2-181">Třeba balíček pomocí `developmentDependency` atribut by měl určovat "2.8" pro `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-181">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="aa3b2-182">Obdobně balíček pomocí `contentFiles` – element (viz další části) by měl nastavit `minClientVersion` na "3.3".</span><span class="sxs-lookup"><span data-stu-id="aa3b2-182">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="aa3b2-183">Upozorňujeme také, že klienti NuGet před 2.5 nedokáže rozpoznat tento příznak jsou *vždy* odmítnout instalace balíčku bez ohledu na to, co `minClientVersion` obsahuje.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-183">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="aa3b2-184">Elementy v kolekci</span><span class="sxs-lookup"><span data-stu-id="aa3b2-184">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="aa3b2-185">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="aa3b2-185">packageTypes</span></span>
<span data-ttu-id="aa3b2-186">*(3.5 +)*  Kolekce nula nebo více `<packageType>` elementy typu balíčku Pokud než tradiční závislost balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-186">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="aa3b2-187">Každý packageType má atributy *název* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-187">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="aa3b2-188">Zobrazit [nastavení typ balíčku](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-188">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="aa3b2-189">závislosti</span><span class="sxs-lookup"><span data-stu-id="aa3b2-189">dependencies</span></span>
<span data-ttu-id="aa3b2-190">Kolekce nula nebo více `<dependency>` prvky určení závislostí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-190">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="aa3b2-191">Každá závislost má atributy *id*, *verze*, *zahrnují* (3.x+), a *vyloučit* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-191">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="aa3b2-192">Zobrazit [závislosti](#dependencies-element) níže.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-192">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="aa3b2-193">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="aa3b2-193">frameworkAssemblies</span></span>
<span data-ttu-id="aa3b2-194">*(1.2 +)*  Kolekce nula nebo více `<frameworkAssembly>` prvků identifikace odkazy na sestavení rozhraní .NET Framework, které vyžaduje tento balíček, které zajišťuje, že jsou přidány odkazy na projekty využívající balíček.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-194">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="aa3b2-195">Má každý frameworkAssembly *assemblyName* a *targetFramework* atributy.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-195">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="aa3b2-196">Zobrazit [zadání framework sestavení odkazuje na globální mezipaměti](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-196">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="aa3b2-197">odkazy</span><span class="sxs-lookup"><span data-stu-id="aa3b2-197">references</span></span>
<span data-ttu-id="aa3b2-198">*(1.5 +)*  Kolekce nula nebo více `<reference>` prvky názvy sestavení v balíčku `lib` složku, která jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-198">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="aa3b2-199">Každý odkaz má *souboru* atribut.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-199">Each reference has a *file* attribute.</span></span> <span data-ttu-id="aa3b2-200">`<references>` může také obsahovat `<group>` element s *targetFramework* atribut, pak obsahující `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-200">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="aa3b2-201">Pokud tento parametr vynechán, všechny odkazy v `lib` jsou zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-201">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="aa3b2-202">Zobrazit [odkazy na sestavení explicitní určení](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-202">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="aa3b2-203">contentFiles</span><span class="sxs-lookup"><span data-stu-id="aa3b2-203">contentFiles</span></span>
<span data-ttu-id="aa3b2-204">*(3.3 +)*  Kolekce `<files>` prvky, které identifikují soubory obsahu, které mají být zahrnuty náročné projektu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-204">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="aa3b2-205">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-205">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="aa3b2-206">Zobrazit [určující soubory, které chcete zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-206">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="aa3b2-207">soubory </span><span class="sxs-lookup"><span data-stu-id="aa3b2-207">files</span></span> 
<span data-ttu-id="aa3b2-208">`<package>` Uzel může obsahovat `<files>` uzel na stejné úrovni k `<metadata>`a nebo `<contentFiles>` dítě `<metadata>`, určete, jaké soubory sestavení a obsah zahrnout do balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-208">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="aa3b2-209">Zobrazit [včetně souborů sestavení](#including-assembly-files) a [včetně soubory obsahu](#including-content-files) dále v tomto tématu podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-209">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="aa3b2-210">Nahrazování tokenů</span><span class="sxs-lookup"><span data-stu-id="aa3b2-210">Replacement tokens</span></span>

<span data-ttu-id="aa3b2-211">Při vytváření balíčku, [ `nuget pack` příkaz](../tools/cli-ref-pack.md) nahradí $oddělených tokenů v `.nuspec` souboru `<metadata>` uzlu s hodnotami, které pocházejí ze souboru projektu nebo `pack` příkazu `-properties`přepínat.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-211">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="aa3b2-212">Na příkazovém řádku zadáte hodnoty tokenu s `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-212">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="aa3b2-213">Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a zadejte hodnoty v následujícím způsobem balení čas:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-213">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="aa3b2-214">Chcete-li hodnoty z projektu, zadat tokenů popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` například `AssemblyInfo.cs` nebo `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-214">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="aa3b2-215">Pokud chcete použít tyto tokeny, spusťte `nuget pack` do souboru projektu namísto pouze `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-215">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="aa3b2-216">Například, když pomocí následujícího příkazu `$id$` a `$version$` tokeny v `.nuspec` souboru jsou nahrazeny projektu `AssemblyName` a `AssemblyVersion` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-216">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="aa3b2-217">Obvykle, když máte projekt, vytvoříte `.nuspec` zpočátku pomocí `nuget spec MyProject.csproj` což automaticky zahrnuje některé z těchto standardních tokenů.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-217">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="aa3b2-218">Nicméně, pokud projekt neobsahuje hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` selže.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-218">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="aa3b2-219">Navíc pokud můžete změnit hodnoty projektu, je nutné znovu sestavit před vytvořením balíčku. To můžete udělat jednoduše pomocí příkazu pack `build` přepnout.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-219">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="aa3b2-220">S výjimkou produktů `$configuration$`, jsou hodnoty v projektu použít preferenci pro libovolné přiřazen stejný token v příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-220">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="aa3b2-221">Token</span><span class="sxs-lookup"><span data-stu-id="aa3b2-221">Token</span></span> | <span data-ttu-id="aa3b2-222">Hodnota zdroje</span><span class="sxs-lookup"><span data-stu-id="aa3b2-222">Value source</span></span> | <span data-ttu-id="aa3b2-223">Hodnota</span><span class="sxs-lookup"><span data-stu-id="aa3b2-223">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="aa3b2-224">**$id$**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-224">**$id$**</span></span> | <span data-ttu-id="aa3b2-225">soubor projektu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-225">Project file</span></span> | <span data-ttu-id="aa3b2-226">AssemblyName (název) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-226">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="aa3b2-227">**$version$**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-227">**$version$**</span></span> | <span data-ttu-id="aa3b2-228">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aa3b2-228">AssemblyInfo</span></span> | <span data-ttu-id="aa3b2-229">AssemblyInformationalVersion, pokud jsou k dispozici, jinak AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="aa3b2-229">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="aa3b2-230">**$author$**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-230">**$author$**</span></span> | <span data-ttu-id="aa3b2-231">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aa3b2-231">AssemblyInfo</span></span> | <span data-ttu-id="aa3b2-232">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="aa3b2-232">AssemblyCompany</span></span> |
| <span data-ttu-id="aa3b2-233">**$title$**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-233">**$title$**</span></span> | <span data-ttu-id="aa3b2-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aa3b2-234">AssemblyInfo</span></span> | <span data-ttu-id="aa3b2-235">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="aa3b2-235">AssemblyTitle</span></span> |
| <span data-ttu-id="aa3b2-236">**$description$**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-236">**$description$**</span></span> | <span data-ttu-id="aa3b2-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aa3b2-237">AssemblyInfo</span></span> | <span data-ttu-id="aa3b2-238">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="aa3b2-238">AssemblyDescription</span></span> |
| <span data-ttu-id="aa3b2-239">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-239">**$copyright$**</span></span> | <span data-ttu-id="aa3b2-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="aa3b2-240">AssemblyInfo</span></span> | <span data-ttu-id="aa3b2-241">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="aa3b2-241">AssemblyCopyright</span></span> |
| <span data-ttu-id="aa3b2-242">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-242">**$configuration$**</span></span> | <span data-ttu-id="aa3b2-243">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="aa3b2-243">Assembly DLL</span></span> | <span data-ttu-id="aa3b2-244">Konfigurace použitý k vytvoření sestavení, jako výchozí se použije k ladění.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-244">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="aa3b2-245">Všimněte si, že pokud chcete vytvořit balíček pomocí konfiguraci vydané verze, vždy používáte `-properties Configuration=Release` na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-245">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="aa3b2-246">Tokeny je také možné přeložit cesty, jakmile zahrnete [soubory sestavení](#including-assembly-files) a [obsah souborů](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-246">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="aa3b2-247">Tokeny mají stejné názvy jako vlastnosti nástroje MSBuild, což umožňuje vyberte soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-247">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="aa3b2-248">Například, pokud použijete následující klíčová slova v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-248">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="aa3b2-249">A vytvoření sestavení jehož `AssemblyName` je `LoggingLibrary` s `Release` konfigurace v nástroji MSBuild, výsledný vstupující `.nuspec` souborů v balíčku je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-249">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="aa3b2-250">Dependencies – element</span><span class="sxs-lookup"><span data-stu-id="aa3b2-250">Dependencies element</span></span>

<span data-ttu-id="aa3b2-251">`<dependencies>` Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvky, které určují další balíčky, na kterých závisí balíček nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-251">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="aa3b2-252">Atributy pro každý `<dependency>` jsou následující:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-252">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="aa3b2-253">Atribut</span><span class="sxs-lookup"><span data-stu-id="aa3b2-253">Attribute</span></span> | <span data-ttu-id="aa3b2-254">Popis</span><span class="sxs-lookup"><span data-stu-id="aa3b2-254">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="aa3b2-255">(Povinné) Ukazuje, na stránce balíček pro ID balíčku závislosti, jako je například "EntityFramework" a "NUnit", což je název balíčku nuget.org.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-255">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="aa3b2-256">(Povinné) Rozsah verzí přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-256">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="aa3b2-257">Zobrazit [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) přesnou syntaxi.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-257">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="aa3b2-258">include</span><span class="sxs-lookup"><span data-stu-id="aa3b2-258">include</span></span> | <span data-ttu-id="aa3b2-259">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti, které mají být zahrnuty do koncového balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-259">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="aa3b2-260">Výchozí hodnota je `none`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-260">The default value is `none`.</span></span> |
| <span data-ttu-id="aa3b2-261">exclude</span><span class="sxs-lookup"><span data-stu-id="aa3b2-261">exclude</span></span> | <span data-ttu-id="aa3b2-262">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti pro vyloučení ve finálním balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="aa3b2-263">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-263">The  default value is `all`.</span></span> <span data-ttu-id="aa3b2-264">Značky s `exclude` přednost zadaným `include`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-264">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="aa3b2-265">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-265">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="aa3b2-266">Zahrnutí a vyloučení značek</span><span class="sxs-lookup"><span data-stu-id="aa3b2-266">Include/Exclude tag</span></span> | <span data-ttu-id="aa3b2-267">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="aa3b2-267">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="aa3b2-268">contentFiles</span><span class="sxs-lookup"><span data-stu-id="aa3b2-268">contentFiles</span></span> | <span data-ttu-id="aa3b2-269">Obsah</span><span class="sxs-lookup"><span data-stu-id="aa3b2-269">Content</span></span> |
| <span data-ttu-id="aa3b2-270">modul runtime</span><span class="sxs-lookup"><span data-stu-id="aa3b2-270">runtime</span></span> | <span data-ttu-id="aa3b2-271">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="aa3b2-271">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="aa3b2-272">Kompilace</span><span class="sxs-lookup"><span data-stu-id="aa3b2-272">compile</span></span> | <span data-ttu-id="aa3b2-273">lib</span><span class="sxs-lookup"><span data-stu-id="aa3b2-273">lib</span></span> |
| <span data-ttu-id="aa3b2-274">sestavení</span><span class="sxs-lookup"><span data-stu-id="aa3b2-274">build</span></span> | <span data-ttu-id="aa3b2-275">sestavení (cíle a vlastnosti nástroje MSBuild)</span><span class="sxs-lookup"><span data-stu-id="aa3b2-275">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="aa3b2-276">nativní</span><span class="sxs-lookup"><span data-stu-id="aa3b2-276">native</span></span> | <span data-ttu-id="aa3b2-277">nativní</span><span class="sxs-lookup"><span data-stu-id="aa3b2-277">native</span></span> |
| <span data-ttu-id="aa3b2-278">žádná</span><span class="sxs-lookup"><span data-stu-id="aa3b2-278">none</span></span> | <span data-ttu-id="aa3b2-279">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="aa3b2-279">No folders</span></span> |
| <span data-ttu-id="aa3b2-280">všechny</span><span class="sxs-lookup"><span data-stu-id="aa3b2-280">all</span></span> | <span data-ttu-id="aa3b2-281">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="aa3b2-281">All folders</span></span> |

<span data-ttu-id="aa3b2-282">Například následující řádky signalizovat závislosti na `PackageA` verze 1.1.0 nebo vyšší, a `PackageB` verzi 1.x.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-282">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="aa3b2-283">Následující řádky označují závislostí na stejné balíčky, ale zadané k vložení `contentFiles` a `build` složky `PackageA` a všechno, co ale `native` a `compile` složky `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="aa3b2-283">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="aa3b2-284">Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`, závislosti, které existují v tomto projektu jsou automaticky obsažené ve výsledné `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-284">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="aa3b2-285">Závislostí skupin</span><span class="sxs-lookup"><span data-stu-id="aa3b2-285">Dependency groups</span></span>

<span data-ttu-id="aa3b2-286">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="aa3b2-286">*Version 2.0+*</span></span>

<span data-ttu-id="aa3b2-287">Jako alternativu k jednomu seznamu bez stromové struktury, se dá nastavit závislosti podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-287">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="aa3b2-288">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<dependency>` elementy.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-288">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="aa3b2-289">Tyto závislosti jsou nainstalovány společně, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-289">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="aa3b2-290">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-290">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="aa3b2-291">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-291">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="aa3b2-292">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-292">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="aa3b2-293">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-293">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="aa3b2-294">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="aa3b2-294">Explicit assembly references</span></span>

<span data-ttu-id="aa3b2-295">`<references>` Prvek explicitně určuje sestavení, které by měly odkazovat na cílový projekt, při použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-295">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="aa3b2-296">Pokud tento prvek je k dispozici, NuGet přidat odkazy pouze na uvedené sestavení; nepřidá odkazy pro jiná sestavení v balíčku `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-296">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="aa3b2-297">Například následující `<references>` element dává pokyn NuGet pro přidání odkazů na pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že existují další sestavení v balíčku:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-297">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="aa3b2-298">Explicitní odkazy se obvykle používají pro pouze na sestavení doby návrhu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-298">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="aa3b2-299">Při použití [kontrakty kódu](/dotnet/framework/debug-trace-profile/code-contracts), například sestavení kontraktu musí být vedle sestavení modulu runtime, které se rozšiřují, aby Visual Studio můžete najít, ale kontrakt sestavení nemusí být odkazuje projekt nebo zkopírovat do projektu `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-299">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="aa3b2-300">Podobně je možné explicitní odkazy pro rozhraní pro testování částí, jako jsou XUnit, která potřebuje jeho nástroje pro sestavení vedle sestavení modulu runtime, ale nemá potřebovat, který je zahrnutý jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-300">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="aa3b2-301">Referenční skupiny</span><span class="sxs-lookup"><span data-stu-id="aa3b2-301">Reference groups</span></span>

<span data-ttu-id="aa3b2-302">Jako alternativu k jednomu plochého seznamu lze upravit odkazy podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<references>`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-302">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="aa3b2-303">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-303">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="aa3b2-304">Tyto odkazy jsou přidány do projektu, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-304">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="aa3b2-305">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznamu odkazů.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-305">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="aa3b2-306">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-306">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="aa3b2-307">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-307">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="aa3b2-308">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-308">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="aa3b2-309">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="aa3b2-309">Framework assembly references</span></span>

<span data-ttu-id="aa3b2-310">Sestavení rozhraní jsou ty, které jsou součástí rozhraní .NET framework a by už měla být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-310">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="aa3b2-311">Určením těchto sestavení v rámci `<frameworkAssemblies>` elementu balíčku můžete zajistit, že požadované odkazy jsou přidány do projektu, v případě, že projekt již nemá tyto odkazy.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-311">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="aa3b2-312">Takové sestavení, samozřejmě, nejsou obsažené v balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-312">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="aa3b2-313">`<frameworkAssemblies>` Prvek obsahuje nula nebo více `<frameworkAssembly>` prvky, z nichž každý určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-313">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="aa3b2-314">Atribut</span><span class="sxs-lookup"><span data-stu-id="aa3b2-314">Attribute</span></span> | <span data-ttu-id="aa3b2-315">Popis</span><span class="sxs-lookup"><span data-stu-id="aa3b2-315">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa3b2-316">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-316">**assemblyName**</span></span> | <span data-ttu-id="aa3b2-317">(Povinné) Plně kvalifikovaný název.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-317">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="aa3b2-318">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-318">**targetFramework**</span></span> | <span data-ttu-id="aa3b2-319">(Volitelné) Určuje cílovou architekturu, pro který platí tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-319">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="aa3b2-320">Pokud tento parametr vynechán, označuje, že odkaz použije pro všechny platformy.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-320">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="aa3b2-321">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-321">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="aa3b2-322">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové platformy a odkaz na `System.ServiceModel` pro pouze rozhraní .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-322">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="aa3b2-323">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="aa3b2-323">Including assembly files</span></span>

<span data-ttu-id="aa3b2-324">Pokud budete postupovat podle konvence je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md), není potřeba explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-324">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="aa3b2-325">`nuget pack` Příkaz automaticky převezme potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-325">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="aa3b2-326">Při instalaci do projektu balíček NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* ty, které jsou pojmenovány `.resources.dll` vzhledem k tomu, že se budou považovat za lokalizovaná satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-326">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="aa3b2-327">Z tohoto důvodu se vyhněte se použití `.resources.dll` pro soubory, které jinak obsahují základní balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-327">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="aa3b2-328">Toto automatické chování obejít a explicitně kontrolovat soubory, které jsou obsažené v balíčku, umístěte `<files>` jako podřízený element `<package>` (a na stejné úrovni `<metadata>`), identifikuje každý soubor se samostatným `<file>` element.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-328">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="aa3b2-329">Příklad:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-329">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="aa3b2-330">Nuget 2.x a dřívějších verzí a projekty pomocí `packages.config`, `<files>` element slouží také k neměnné obsahu soubory k zahrnutí při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-330">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="aa3b2-331">S NuGet 3.3 + i na PackageReference `<contentFiles>` elementu je použita.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-331">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="aa3b2-332">Zobrazit [včetně soubory obsahu](#including-content-files) níže podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-332">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="aa3b2-333">Atributy souboru</span><span class="sxs-lookup"><span data-stu-id="aa3b2-333">File element attributes</span></span>

<span data-ttu-id="aa3b2-334">Každý `<file>` prvek určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-334">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="aa3b2-335">Atribut</span><span class="sxs-lookup"><span data-stu-id="aa3b2-335">Attribute</span></span> | <span data-ttu-id="aa3b2-336">Popis</span><span class="sxs-lookup"><span data-stu-id="aa3b2-336">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa3b2-337">**src**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-337">**src**</span></span> | <span data-ttu-id="aa3b2-338">Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-338">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="aa3b2-339">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-339">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="aa3b2-340">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-340">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="aa3b2-341">**Cíl**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-341">**target**</span></span> | <span data-ttu-id="aa3b2-342">Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které musí začínat `lib`, `content`, `build`, nebo `tools`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-342">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="aa3b2-343">Zobrazit [vytváření souboru .nuspec z pracovního adresáře podle úmluvy](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-343">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="aa3b2-344">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-344">**exclude**</span></span> | <span data-ttu-id="aa3b2-345">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-345">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="aa3b2-346">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-346">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="aa3b2-347">Příklady</span><span class="sxs-lookup"><span data-stu-id="aa3b2-347">Examples</span></span>

<span data-ttu-id="aa3b2-348">**Jediné sestavení**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-348">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="aa3b2-349">**Jediné sestavení specifická pro rozhraní .NET framework**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-349">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="aa3b2-350">**Sada knihovny DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-350">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="aa3b2-351">**Knihovny DLL pro různá rozhraní**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-351">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="aa3b2-352">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-352">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="aa3b2-353">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-353">Including content files</span></span>

<span data-ttu-id="aa3b2-354">Soubory obsahu jsou neměnné soubory, které je potřeba zahrnout do projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-354">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="aa3b2-355">Je neměnný, nejsou určeny k používání projektu změnit.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-355">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="aa3b2-356">Příklad obsahu souborů patří:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-356">Example content files include:</span></span>

- <span data-ttu-id="aa3b2-357">Bitové kopie, které jsou vloženy jako prostředky</span><span class="sxs-lookup"><span data-stu-id="aa3b2-357">Images that are embedded as resources</span></span>
- <span data-ttu-id="aa3b2-358">Zdrojové soubory, které jsou již kompilován</span><span class="sxs-lookup"><span data-stu-id="aa3b2-358">Source files that are already compiled</span></span>
- <span data-ttu-id="aa3b2-359">Skripty, které musí být součástí výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-359">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="aa3b2-360">Konfigurační soubory pro balíček, který mají být zahrnuti do projektu, ale není třeba žádné změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="aa3b2-360">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="aa3b2-361">Obsahu souborů jsou součástí balíčku pomocí `<files>` elementu, určení `content` složky `target` atribut.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-361">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="aa3b2-362">Ale tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který používá místo toho `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-362">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="aa3b2-363">Balíček pro maximální kompatibility s využívání projektů v ideálním případě Určuje soubory obsahu v obou elementech.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-363">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="aa3b2-364">Pomocí elementu souborů pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-364">Using the files element for content files</span></span>

<span data-ttu-id="aa3b2-365">Pro soubory obsahu, stačí použít stejný formát jako soubory sestavení, ale zadat `content` jako základní složka v `target` atributu, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-365">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="aa3b2-366">**Soubory základního obsahu**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-366">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="aa3b2-367">**Soubory obsahu s adresářovou strukturu**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-367">**Content files with directory structure**</span></span>

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

<span data-ttu-id="aa3b2-368">**Soubor s obsahem specifické pro cílové prostředí**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-368">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="aa3b2-369">**Zkopírovat do složky s tečkou v názvu souboru obsahu**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-369">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="aa3b2-370">V takovém případě se zobrazí NuGet, který rozšíření v `target` se neshoduje s příponou v `src` a proto zpracovává tuto část názvu v `target` jako složka:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-370">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="aa3b2-371">**Soubory obsahu bez přípony**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-371">**Content files without extensions**</span></span>

<span data-ttu-id="aa3b2-372">Chcete-li zahrnout soubory bez přípony, použijte `*` nebo `**` zástupné znaky:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-372">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="aa3b2-373">**Soubory obsahu se hloubkové cesty a hloubkové cílem**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-373">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="aa3b2-374">V takovém případě protože přípony zdrojovou a cílovou odpovídají, NuGet předpokládá, že cíl je název souboru a nikoliv složka:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-374">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="aa3b2-375">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-375">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="aa3b2-376">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-376">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="aa3b2-377">Pomocí elementu contentFiles pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="aa3b2-377">Using the contentFiles element for content files</span></span>

<span data-ttu-id="aa3b2-378">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="aa3b2-378">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="aa3b2-379">Ve výchozím nastavení, umístí balíček obsahu `contentFiles` složky (viz níže) a `nuget pack` zahrnuty všechny soubory ve složce pomocí výchozí atributy.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-379">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="aa3b2-380">V tomto případě není nutné zahrnout `contentFiles` uzlu `.nuspec` vůbec.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-380">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="aa3b2-381">K řízení souborů, které jsou zahrnuty `<contentFiles>` prvek určuje je kolekce `<files>` mezi prvky, které identifikují přesné soubory patří.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-381">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="aa3b2-382">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-382">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="aa3b2-383">Atribut</span><span class="sxs-lookup"><span data-stu-id="aa3b2-383">Attribute</span></span> | <span data-ttu-id="aa3b2-384">Popis</span><span class="sxs-lookup"><span data-stu-id="aa3b2-384">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aa3b2-385">**Zahrnout**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-385">**include**</span></span> | <span data-ttu-id="aa3b2-386">(Povinné) Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-386">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="aa3b2-387">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-387">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="aa3b2-388">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-388">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="aa3b2-389">**Vyloučení**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-389">**exclude**</span></span> | <span data-ttu-id="aa3b2-390">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-390">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="aa3b2-391">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="aa3b2-392">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-392">**buildAction**</span></span> | <span data-ttu-id="aa3b2-393">Akce sestavení zařadit do obsahu položky nástroje MSBuild, jako například `Content`, `None`, `Embedded Resource`, `Compile`atd. Výchozí hodnota je `Compile`.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-393">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="aa3b2-394">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-394">**copyToOutput**</span></span> | <span data-ttu-id="aa3b2-395">Logická hodnota označující, jestli se má kopírovat položky obsahu pro sestavení (nebo publikovat) výstupní složka.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-395">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="aa3b2-396">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-396">The default is false.</span></span> |
| <span data-ttu-id="aa3b2-397">**Sloučit**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-397">**flatten**</span></span> | <span data-ttu-id="aa3b2-398">Logická hodnota označující, zda se můžete kopírovat položky obsahu na jedinou složku ve výstupu sestavení (pravda), nebo zachovat strukturu složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-398">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="aa3b2-399">Tento příznak funguje pouze v případě copyToOutput příznak je nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-399">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="aa3b2-400">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-400">The default is false.</span></span> |

<span data-ttu-id="aa3b2-401">Při instalaci balíčku NuGet platí podřízených elementů `<contentFiles>` shora dolů.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-401">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="aa3b2-402">Pokud se shodují na stejný soubor několik záznamů se použijí všechny položky.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-402">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="aa3b2-403">Položky navrchu přepíše nižší položky dojde ke konfliktu pro stejný atribut.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-403">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="aa3b2-404">Struktura složky balíčku</span><span class="sxs-lookup"><span data-stu-id="aa3b2-404">Package folder structure</span></span>

<span data-ttu-id="aa3b2-405">Projekt balíčku strukturovat obsahu pomocí následujícímu vzoru:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-405">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="aa3b2-406">`codeLanguages` může být `cs`, `vb`, `fs`, `any`, nebo malým ekvivalentem znaku danou `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="aa3b2-406">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="aa3b2-407">`TxM` je všechny moniker právní cílového rozhraní, která podporuje NuGet (viz [platforem](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="aa3b2-407">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="aa3b2-408">Složky libovolné struktury složek může připojen na konec této syntaxe.</span><span class="sxs-lookup"><span data-stu-id="aa3b2-408">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="aa3b2-409">Příklad:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-409">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="aa3b2-410">Můžete použít prázdné složky `.` chcete vyjádřit výslovný nesouhlas poskytnutí obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-410">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="aa3b2-411">Vzorový oddíl contentFiles</span><span class="sxs-lookup"><span data-stu-id="aa3b2-411">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="aa3b2-412">Příklad souboru nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="aa3b2-412">Example nuspec files</span></span>

<span data-ttu-id="aa3b2-413">**Jednoduchý `.nuspec` , která neurčuje závislosti nebo souborů**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-413">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="aa3b2-414">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-414">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="aa3b2-415">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-415">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="aa3b2-416">**A `.nuspec` se sestaveními rozhraní framework**</span><span class="sxs-lookup"><span data-stu-id="aa3b2-416">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="aa3b2-417">V tomto příkladu tímto se nainstalují pro konkrétní projekt cílí:</span><span class="sxs-lookup"><span data-stu-id="aa3b2-417">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="aa3b2-418">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="aa3b2-418">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="aa3b2-419">. NET4 -> Client Profile `System.Net`</span><span class="sxs-lookup"><span data-stu-id="aa3b2-419">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="aa3b2-420">-> Silverlight 3 `System.Json`</span><span class="sxs-lookup"><span data-stu-id="aa3b2-420">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="aa3b2-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="aa3b2-421">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="aa3b2-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="aa3b2-422">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
