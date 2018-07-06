---
title: Odkaz na soubor souboru .nuspec pro NuGet
description: Souboru .nuspec soubor obsahuje metadata balíčků používat při vytváření balíčku a zadejte informace pro spotřebitele balíčku.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 142f82386395b8ab2ed1d57218db9bc1d2e98638
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843443"
---
# <a name="nuspec-reference"></a><span data-ttu-id="8950e-103">odkaz na souboru .nuspec</span><span class="sxs-lookup"><span data-stu-id="8950e-103">.nuspec reference</span></span>

<span data-ttu-id="8950e-104">A `.nuspec` je soubor manifestu XML, který obsahuje metadata balíčků.</span><span class="sxs-lookup"><span data-stu-id="8950e-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="8950e-105">Tento manifest slouží k vytvoření balíčku a zadejte informace pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="8950e-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="8950e-106">Manifest je vždy součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="8950e-107">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="8950e-107">In this topic:</span></span>

- [<span data-ttu-id="8950e-108">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="8950e-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="8950e-109">[Nahrazení tokeny](#replacement-tokens) (při použití s projektu sady Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="8950e-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="8950e-110">Závislosti</span><span class="sxs-lookup"><span data-stu-id="8950e-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="8950e-111">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="8950e-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="8950e-112">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="8950e-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="8950e-113">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="8950e-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="8950e-114">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="8950e-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="8950e-115">Příklady</span><span class="sxs-lookup"><span data-stu-id="8950e-115">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="8950e-116">Obecný tvar a schématu</span><span class="sxs-lookup"><span data-stu-id="8950e-116">General form and schema</span></span>

<span data-ttu-id="8950e-117">Aktuální `nuspec.xsd` soubor schématu najdete v [úložiště NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="8950e-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="8950e-118">V tomto schématu `.nuspec` soubor má následující Obecné formuláře:</span><span class="sxs-lookup"><span data-stu-id="8950e-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="8950e-119">Vizuální znázornění schématu, otevřete soubor schématu v sadě Visual Studio v režimu návrhu a klikněte **Průzkumníka schémat XML** odkaz.</span><span class="sxs-lookup"><span data-stu-id="8950e-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="8950e-120">Alternativně otevřete soubor jako kód, klikněte v editoru pravým tlačítkem myši a vyberte **zobrazení Průzkumníka schémat XML**.</span><span class="sxs-lookup"><span data-stu-id="8950e-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="8950e-121">V obou případech, které získáte zobrazení jako na následující (v rozbaleném většinou):</span><span class="sxs-lookup"><span data-stu-id="8950e-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio Průzkumníka schémat s nuspec.xsd otevřít](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="8950e-123">Metadata atributů</span><span class="sxs-lookup"><span data-stu-id="8950e-123">Metadata attributes</span></span>

<span data-ttu-id="8950e-124">`<metadata>` Prvek podporuje atributy jsou popsané v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="8950e-124">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="8950e-125">Atribut</span><span class="sxs-lookup"><span data-stu-id="8950e-125">Attribute</span></span> | <span data-ttu-id="8950e-126">Požadováno</span><span class="sxs-lookup"><span data-stu-id="8950e-126">Required</span></span> | <span data-ttu-id="8950e-127">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-127">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="8950e-128">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="8950e-128">**minClientVersion**</span></span> | <span data-ttu-id="8950e-129">Ne</span><span class="sxs-lookup"><span data-stu-id="8950e-129">No</span></span> | <span data-ttu-id="8950e-130">Určuje minimální verzi klienta NuGet, který můžete nainstalovat tento balíček, vynucuje nuget.exe a Správce balíčků sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8950e-130">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="8950e-131">Používá se pokaždé, když se balíček závisí na konkrétních funkcí služby `.nuspec` souborů, které byly přidány v konkrétní verzi klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="8950e-131">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="8950e-132">Třeba balíček pomocí `developmentDependency` atribut by měl určovat "2.8" pro `minClientVersion`.</span><span class="sxs-lookup"><span data-stu-id="8950e-132">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="8950e-133">Obdobně balíček pomocí `contentFiles` – element (viz další části) by měl nastavit `minClientVersion` na "3.3".</span><span class="sxs-lookup"><span data-stu-id="8950e-133">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="8950e-134">Upozorňujeme také, že klienti NuGet před 2.5 nedokáže rozpoznat tento příznak jsou *vždy* odmítnout instalace balíčku bez ohledu na to, co `minClientVersion` obsahuje.</span><span class="sxs-lookup"><span data-stu-id="8950e-134">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="8950e-135">Prvky požadovaná metadata</span><span class="sxs-lookup"><span data-stu-id="8950e-135">Required metadata elements</span></span>

<span data-ttu-id="8950e-136">I když tyto prvky jsou minimální požadavky pro balíček, měli byste zvážit přidání [volitelná metadata prvky](#optional-metadata-elements) zlepšit celkové prostředí mají vývojáři součástí vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-136">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="8950e-137">Tyto prvky musí být uvedena v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="8950e-137">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="8950e-138">Prvek</span><span class="sxs-lookup"><span data-stu-id="8950e-138">Element</span></span> | <span data-ttu-id="8950e-139">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8950e-140">**id**</span><span class="sxs-lookup"><span data-stu-id="8950e-140">**id**</span></span> | <span data-ttu-id="8950e-141">Identifikátor balíčku velká a malá písmena, která musí být jedinečný v rámci nuget.org nebo cokoli jiného balíčku se nachází v galerii.</span><span class="sxs-lookup"><span data-stu-id="8950e-141">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="8950e-142">ID nemůže obsahovat mezery nebo znaky, které nejsou platné pro adresu URL a obvykle postupují podle pravidla oboru názvů .NET.</span><span class="sxs-lookup"><span data-stu-id="8950e-142">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="8950e-143">Zobrazit [výběr balíčku jedinečný identifikátor](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) pokyny.</span><span class="sxs-lookup"><span data-stu-id="8950e-143">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="8950e-144">**verze**</span><span class="sxs-lookup"><span data-stu-id="8950e-144">**version**</span></span> | <span data-ttu-id="8950e-145">Verze balíčku, následující *hlavníverze.podverze.oprava* vzor.</span><span class="sxs-lookup"><span data-stu-id="8950e-145">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="8950e-146">Čísla verzí může obsahovat příponu předběžné verze, jak je popsáno v [Správa verzí balíčků](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="8950e-146">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="8950e-147">**Popis**</span><span class="sxs-lookup"><span data-stu-id="8950e-147">**description**</span></span> | <span data-ttu-id="8950e-148">Dlouhý popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="8950e-148">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="8950e-149">**Autoři**</span><span class="sxs-lookup"><span data-stu-id="8950e-149">**authors**</span></span> | <span data-ttu-id="8950e-150">Čárkou oddělený seznam autorů balíčků, odpovídající názvy profilů na nuget.org. Tyto jsou zobrazeny v galerii NuGet na nuget.org a slouží k křížový odkaz balíčky stejné autory.</span><span class="sxs-lookup"><span data-stu-id="8950e-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="8950e-151">Volitelná metadata elementy</span><span class="sxs-lookup"><span data-stu-id="8950e-151">Optional metadata elements</span></span>

<span data-ttu-id="8950e-152">Tyto prvky může být zobrazen v rámci `<metadata>` elementu.</span><span class="sxs-lookup"><span data-stu-id="8950e-152">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="8950e-153">Jednotlivé prvky</span><span class="sxs-lookup"><span data-stu-id="8950e-153">Single elements</span></span>

| <span data-ttu-id="8950e-154">Prvek</span><span class="sxs-lookup"><span data-stu-id="8950e-154">Element</span></span> | <span data-ttu-id="8950e-155">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-155">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8950e-156">**Název**</span><span class="sxs-lookup"><span data-stu-id="8950e-156">**title**</span></span> | <span data-ttu-id="8950e-157">Lidské popisný název balíčku, obvykle používaných v uživatelském rozhraní na webech nuget.org a Správce balíčků v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8950e-157">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="8950e-158">Pokud není zadán, použije se ID balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-158">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="8950e-159">**Vlastníci**</span><span class="sxs-lookup"><span data-stu-id="8950e-159">**owners**</span></span> | <span data-ttu-id="8950e-160">Čárkou oddělený seznam Tvůrce balíčku pomocí názvy profilů na nuget.org. To je často seznamu stejné jako v `authors`a je ignorován při nahrávání balíčku do nuget.org. Zobrazit [vlastníky Správa balíčků na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="8950e-160">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="8950e-161">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="8950e-161">**projectUrl**</span></span> | <span data-ttu-id="8950e-162">Adresa URL domovské stránky balíčku, často zobrazuje v uživatelském rozhraní nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8950e-162">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="8950e-163">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="8950e-163">**licenseUrl**</span></span> | <span data-ttu-id="8950e-164">Adresa URL licence balíčku, často zobrazuje v uživatelském rozhraní nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8950e-164">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="8950e-165">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="8950e-165">**iconUrl**</span></span> | <span data-ttu-id="8950e-166">Adresa URL pro bitovou kopii 64 x 64 s průhlednost pozadí použít jako ikona pro balíček zobrazená v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="8950e-166">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="8950e-167">Ujistěte se, obsahuje tento element *přímá adresa URL obrázku* nikoli adresa URL webové stránky, který obsahuje bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="8950e-167">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="8950e-168">Například pokud chcete použít některou image z Githubu, použijte soubor raw, jako je adresa URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="8950e-168">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> |
| <span data-ttu-id="8950e-169">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="8950e-169">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="8950e-170">Logická hodnota určující, zda klient musí požádat spotřebitele o přijetí licence balíčku před instalací balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-170">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="8950e-171">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="8950e-171">**developmentDependency**</span></span> | <span data-ttu-id="8950e-172">*(2.8 +)*  Logická hodnota určující, jestli tento balíček představuje označit jako vývoj – jen závislost, což zabrání balíčku nebudou zahrnuty v závislosti na dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="8950e-172">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="8950e-173">**Souhrn**</span><span class="sxs-lookup"><span data-stu-id="8950e-173">**summary**</span></span> | <span data-ttu-id="8950e-174">Krátký popis balíčku zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="8950e-174">A short description of the package for UI display.</span></span> <span data-ttu-id="8950e-175">Pokud tento parametr vynechán, zkrácená verze `description` se používá.</span><span class="sxs-lookup"><span data-stu-id="8950e-175">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="8950e-176">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="8950e-176">**releaseNotes**</span></span> | <span data-ttu-id="8950e-177">*(1.5 +)*  Popis změn provedených v této verzi balíčku, často používají v uživatelském rozhraní, jako **aktualizace** kartu z Visual Studio Správce balíčků namísto popisu balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-177">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="8950e-178">**Copyright**</span><span class="sxs-lookup"><span data-stu-id="8950e-178">**copyright**</span></span> | <span data-ttu-id="8950e-179">*(1.5 +)*  Copyright podrobnosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-179">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="8950e-180">**Jazyk**</span><span class="sxs-lookup"><span data-stu-id="8950e-180">**language**</span></span> | <span data-ttu-id="8950e-181">ID národního prostředí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="8950e-181">The locale ID for the package.</span></span> <span data-ttu-id="8950e-182">Zobrazit [vytvoření lokalizovaných balíčků](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8950e-182">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="8950e-183">**značky**</span><span class="sxs-lookup"><span data-stu-id="8950e-183">**tags**</span></span>  | <span data-ttu-id="8950e-184">Mezerami oddělený seznam značek a klíčových slov, které popisují balíček a podpora zjistitelnost balíčků prostřednictvím vyhledávání a filtrování.</span><span class="sxs-lookup"><span data-stu-id="8950e-184">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="8950e-185">**možnost změny**</span><span class="sxs-lookup"><span data-stu-id="8950e-185">**serviceable**</span></span> | <span data-ttu-id="8950e-186">*(3.3 +)*  Pouze pro interní NuGet použít.</span><span class="sxs-lookup"><span data-stu-id="8950e-186">*(3.3+)* For internal NuGet use only.</span></span> |
| <span data-ttu-id="8950e-187">**úložiště**</span><span class="sxs-lookup"><span data-stu-id="8950e-187">**repository**</span></span> | <span data-ttu-id="8950e-188">Metadata úložiště, skládající se z čtyři volitelné atributy: *typ* a *url* *(4.0 +)*, a *větev* a  *potvrzení* *(4.6 +)*.</span><span class="sxs-lookup"><span data-stu-id="8950e-188">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="8950e-189">Tyto atributy umožňují namapovat .nupkg do úložiště, který sestavilo, má potenciál, chcete-li získat podrobné jako jednotlivé větev nebo potvrzení změn, které sestaven balíček.</span><span class="sxs-lookup"><span data-stu-id="8950e-189">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="8950e-190">Elementy v kolekci</span><span class="sxs-lookup"><span data-stu-id="8950e-190">Collection elements</span></span>

| <span data-ttu-id="8950e-191">Prvek</span><span class="sxs-lookup"><span data-stu-id="8950e-191">Element</span></span> | <span data-ttu-id="8950e-192">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-192">Description</span></span> |
| --- | --- |
<span data-ttu-id="8950e-193">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="8950e-193">**packageTypes**</span></span> | <span data-ttu-id="8950e-194">*(3.5 +)*  Kolekce nula nebo více `<packageType>` elementy typu balíčku Pokud než tradiční závislost balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-194">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="8950e-195">Každý packageType má atributy *název* a *verze*.</span><span class="sxs-lookup"><span data-stu-id="8950e-195">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="8950e-196">Zobrazit [nastavení typ balíčku](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="8950e-196">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="8950e-197">**závislosti**</span><span class="sxs-lookup"><span data-stu-id="8950e-197">**dependencies**</span></span> | <span data-ttu-id="8950e-198">Kolekce nula nebo více `<dependency>` prvky určení závislostí pro balíček.</span><span class="sxs-lookup"><span data-stu-id="8950e-198">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="8950e-199">Každá závislost má atributy *id*, *verze*, *zahrnují* (3.x+), a *vyloučit* (3.x+).</span><span class="sxs-lookup"><span data-stu-id="8950e-199">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="8950e-200">Zobrazit [závislosti](#dependencies) níže.</span><span class="sxs-lookup"><span data-stu-id="8950e-200">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="8950e-201">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="8950e-201">**frameworkAssemblies**</span></span> | <span data-ttu-id="8950e-202">*(1.2 +)*  Kolekce nula nebo více `<frameworkAssembly>` prvků identifikace odkazy na sestavení rozhraní .NET Framework, které vyžaduje tento balíček, které zajišťuje, že jsou přidány odkazy na projekty využívající balíček.</span><span class="sxs-lookup"><span data-stu-id="8950e-202">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="8950e-203">Má každý frameworkAssembly *assemblyName* a *targetFramework* atributy.</span><span class="sxs-lookup"><span data-stu-id="8950e-203">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="8950e-204">Zobrazit [zadání framework sestavení odkazuje na globální mezipaměti](#specifying-framework-assembly-references-gac) níže.</span><span class="sxs-lookup"><span data-stu-id="8950e-204">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="8950e-205">**odkazy**</span><span class="sxs-lookup"><span data-stu-id="8950e-205">**references**</span></span> | <span data-ttu-id="8950e-206">*(1.5 +)*  Kolekce nula nebo více `<reference>` prvky názvy sestavení v balíčku `lib` složku, která jsou přidány jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="8950e-206">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="8950e-207">Každý odkaz má *souboru* atribut.</span><span class="sxs-lookup"><span data-stu-id="8950e-207">Each reference has a *file* attribute.</span></span> <span data-ttu-id="8950e-208">`<references>` může také obsahovat `<group>` element s *targetFramework* atribut, pak obsahující `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="8950e-208">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="8950e-209">Pokud tento parametr vynechán, všechny odkazy v `lib` jsou zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="8950e-209">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="8950e-210">Zobrazit [odkazy na sestavení explicitní určení](#specifying-explicit-assembly-references) níže.</span><span class="sxs-lookup"><span data-stu-id="8950e-210">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="8950e-211">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="8950e-211">**contentFiles**</span></span> | <span data-ttu-id="8950e-212">*(3.3 +)*  Kolekce `<files>` prvky, které identifikují soubory obsahu, které mají být zahrnuty náročné projektu.</span><span class="sxs-lookup"><span data-stu-id="8950e-212">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="8950e-213">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů.</span><span class="sxs-lookup"><span data-stu-id="8950e-213">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="8950e-214">Zobrazit [určující soubory, které chcete zahrnout do balíčku](#specifying-files-to-include-in-the-package) níže.</span><span class="sxs-lookup"><span data-stu-id="8950e-214">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="8950e-215">Files – element</span><span class="sxs-lookup"><span data-stu-id="8950e-215">Files element</span></span>

<span data-ttu-id="8950e-216">`<package>` Uzel může obsahovat `<files>` uzel na stejné úrovni k `<metadata>`a nebo `<contentFiles>` dítě `<metadata>`, určete, jaké soubory sestavení a obsah zahrnout do balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-216">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="8950e-217">Zobrazit [včetně souborů sestavení](#including-assembly-files) a [včetně soubory obsahu](#including-content-files) dále v tomto tématu podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="8950e-217">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="8950e-218">Nahrazování tokenů</span><span class="sxs-lookup"><span data-stu-id="8950e-218">Replacement tokens</span></span>

<span data-ttu-id="8950e-219">Při vytváření balíčku, [ `nuget pack` příkaz](../tools/cli-ref-pack.md) nahradí $oddělených tokenů v `.nuspec` souboru `<metadata>` uzlu s hodnotami, které pocházejí ze souboru projektu nebo `pack` příkazu `-properties`přepínat.</span><span class="sxs-lookup"><span data-stu-id="8950e-219">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="8950e-220">Na příkazovém řádku zadáte hodnoty tokenu s `nuget pack -properties <name>=<value>;<name>=<value>`.</span><span class="sxs-lookup"><span data-stu-id="8950e-220">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="8950e-221">Například můžete použít token jako `$owners$` a `$desc$` v `.nuspec` a zadejte hodnoty v následujícím způsobem balení čas:</span><span class="sxs-lookup"><span data-stu-id="8950e-221">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="8950e-222">Chcete-li hodnoty z projektu, zadat tokenů popsané v následující tabulce (AssemblyInfo odkazuje na soubor v `Properties` například `AssemblyInfo.cs` nebo `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="8950e-222">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="8950e-223">Pokud chcete použít tyto tokeny, spusťte `nuget pack` do souboru projektu namísto pouze `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="8950e-223">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="8950e-224">Například, když pomocí následujícího příkazu `$id$` a `$version$` tokeny v `.nuspec` souboru jsou nahrazeny projektu `AssemblyName` a `AssemblyVersion` hodnoty:</span><span class="sxs-lookup"><span data-stu-id="8950e-224">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="8950e-225">Obvykle, když máte projekt, vytvoříte `.nuspec` zpočátku pomocí `nuget spec MyProject.csproj` což automaticky zahrnuje některé z těchto standardních tokenů.</span><span class="sxs-lookup"><span data-stu-id="8950e-225">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="8950e-226">Nicméně, pokud projekt neobsahuje hodnoty pro požadované `.nuspec` prvky, pak `nuget pack` selže.</span><span class="sxs-lookup"><span data-stu-id="8950e-226">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="8950e-227">Navíc pokud můžete změnit hodnoty projektu, je nutné znovu sestavit před vytvořením balíčku. To můžete udělat jednoduše pomocí příkazu pack `build` přepnout.</span><span class="sxs-lookup"><span data-stu-id="8950e-227">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="8950e-228">S výjimkou produktů `$configuration$`, jsou hodnoty v projektu použít preferenci pro libovolné přiřazen stejný token v příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="8950e-228">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="8950e-229">Token</span><span class="sxs-lookup"><span data-stu-id="8950e-229">Token</span></span> | <span data-ttu-id="8950e-230">Hodnota zdroje</span><span class="sxs-lookup"><span data-stu-id="8950e-230">Value source</span></span> | <span data-ttu-id="8950e-231">Hodnota</span><span class="sxs-lookup"><span data-stu-id="8950e-231">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="8950e-232">**$id$**</span><span class="sxs-lookup"><span data-stu-id="8950e-232">**$id$**</span></span> | <span data-ttu-id="8950e-233">Soubor projektu</span><span class="sxs-lookup"><span data-stu-id="8950e-233">Project file</span></span> | <span data-ttu-id="8950e-234">AssemblyName (název) ze souboru projektu</span><span class="sxs-lookup"><span data-stu-id="8950e-234">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="8950e-235">**$version$**</span><span class="sxs-lookup"><span data-stu-id="8950e-235">**$version$**</span></span> | <span data-ttu-id="8950e-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8950e-236">AssemblyInfo</span></span> | <span data-ttu-id="8950e-237">AssemblyInformationalVersion, pokud jsou k dispozici, jinak AssemblyVersion</span><span class="sxs-lookup"><span data-stu-id="8950e-237">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="8950e-238">**$author$**</span><span class="sxs-lookup"><span data-stu-id="8950e-238">**$author$**</span></span> | <span data-ttu-id="8950e-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8950e-239">AssemblyInfo</span></span> | <span data-ttu-id="8950e-240">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="8950e-240">AssemblyCompany</span></span> |
| <span data-ttu-id="8950e-241">**$title$**</span><span class="sxs-lookup"><span data-stu-id="8950e-241">**$title$**</span></span> | <span data-ttu-id="8950e-242">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8950e-242">AssemblyInfo</span></span> | <span data-ttu-id="8950e-243">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="8950e-243">AssemblyTitle</span></span> |
| <span data-ttu-id="8950e-244">**$description$**</span><span class="sxs-lookup"><span data-stu-id="8950e-244">**$description$**</span></span> | <span data-ttu-id="8950e-245">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8950e-245">AssemblyInfo</span></span> | <span data-ttu-id="8950e-246">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="8950e-246">AssemblyDescription</span></span> |
| <span data-ttu-id="8950e-247">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="8950e-247">**$copyright$**</span></span> | <span data-ttu-id="8950e-248">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8950e-248">AssemblyInfo</span></span> | <span data-ttu-id="8950e-249">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="8950e-249">AssemblyCopyright</span></span> |
| <span data-ttu-id="8950e-250">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="8950e-250">**$configuration$**</span></span> | <span data-ttu-id="8950e-251">Sestavení knihovny DLL</span><span class="sxs-lookup"><span data-stu-id="8950e-251">Assembly DLL</span></span> | <span data-ttu-id="8950e-252">Konfigurace použitý k vytvoření sestavení, jako výchozí se použije k ladění.</span><span class="sxs-lookup"><span data-stu-id="8950e-252">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="8950e-253">Všimněte si, že pokud chcete vytvořit balíček pomocí konfiguraci vydané verze, vždy používáte `-properties Configuration=Release` na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="8950e-253">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="8950e-254">Tokeny je také možné přeložit cesty, jakmile zahrnete [soubory sestavení](#including-assembly-files) a [obsah souborů](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="8950e-254">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="8950e-255">Tokeny mají stejné názvy jako vlastnosti nástroje MSBuild, což umožňuje vyberte soubory, které mají být zahrnuty v závislosti na aktuální konfiguraci sestavení.</span><span class="sxs-lookup"><span data-stu-id="8950e-255">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="8950e-256">Například, pokud použijete následující klíčová slova v `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="8950e-256">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="8950e-257">A vytvoření sestavení jehož `AssemblyName` je `LoggingLibrary` s `Release` konfigurace v nástroji MSBuild, výsledný vstupující `.nuspec` souborů v balíčku je následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="8950e-257">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="8950e-258">Závislosti</span><span class="sxs-lookup"><span data-stu-id="8950e-258">Dependencies</span></span>

<span data-ttu-id="8950e-259">`<dependencies>` Element v rámci `<metadata>` obsahuje libovolný počet `<dependency>` prvky, které určují další balíčky, na kterých závisí balíček nejvyšší úrovně.</span><span class="sxs-lookup"><span data-stu-id="8950e-259">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="8950e-260">Atributy pro každý `<dependency>` jsou následující:</span><span class="sxs-lookup"><span data-stu-id="8950e-260">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="8950e-261">Atribut</span><span class="sxs-lookup"><span data-stu-id="8950e-261">Attribute</span></span> | <span data-ttu-id="8950e-262">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-262">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="8950e-263">(Povinné) Ukazuje, na stránce balíček pro ID balíčku závislosti, jako je například "EntityFramework" a "NUnit", což je název balíčku nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8950e-263">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="8950e-264">(Povinné) Rozsah verzí přijatelné jako závislost.</span><span class="sxs-lookup"><span data-stu-id="8950e-264">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="8950e-265">Zobrazit [Správa verzí balíčků](../reference/package-versioning.md#version-ranges-and-wildcards) přesnou syntaxi.</span><span class="sxs-lookup"><span data-stu-id="8950e-265">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="8950e-266">include</span><span class="sxs-lookup"><span data-stu-id="8950e-266">include</span></span> | <span data-ttu-id="8950e-267">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti, které mají být zahrnuty do koncového balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-267">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="8950e-268">Výchozí hodnota je `none`.</span><span class="sxs-lookup"><span data-stu-id="8950e-268">The default value is `none`.</span></span> |
| <span data-ttu-id="8950e-269">exclude</span><span class="sxs-lookup"><span data-stu-id="8950e-269">exclude</span></span> | <span data-ttu-id="8950e-270">Čárkami oddělený seznam zahrnutí a vyloučení značek (viz níže) označující závislosti pro vyloučení ve finálním balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-270">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="8950e-271">Výchozí hodnota je `all`.</span><span class="sxs-lookup"><span data-stu-id="8950e-271">The  default value is `all`.</span></span> <span data-ttu-id="8950e-272">Značky s `exclude` přednost zadaným `include`.</span><span class="sxs-lookup"><span data-stu-id="8950e-272">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="8950e-273">Například `include="runtime, compile" exclude="compile"` je stejný jako `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="8950e-273">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="8950e-274">Zahrnutí a vyloučení značek</span><span class="sxs-lookup"><span data-stu-id="8950e-274">Include/Exclude tag</span></span> | <span data-ttu-id="8950e-275">Ovlivněné složky cíle</span><span class="sxs-lookup"><span data-stu-id="8950e-275">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="8950e-276">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8950e-276">contentFiles</span></span> | <span data-ttu-id="8950e-277">Obsah</span><span class="sxs-lookup"><span data-stu-id="8950e-277">Content</span></span> |
| <span data-ttu-id="8950e-278">modul runtime</span><span class="sxs-lookup"><span data-stu-id="8950e-278">runtime</span></span> | <span data-ttu-id="8950e-279">Modul runtime, prostředky a FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="8950e-279">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="8950e-280">kompilace</span><span class="sxs-lookup"><span data-stu-id="8950e-280">compile</span></span> | <span data-ttu-id="8950e-281">lib</span><span class="sxs-lookup"><span data-stu-id="8950e-281">lib</span></span> |
| <span data-ttu-id="8950e-282">sestavení</span><span class="sxs-lookup"><span data-stu-id="8950e-282">build</span></span> | <span data-ttu-id="8950e-283">sestavení (cíle a vlastnosti nástroje MSBuild)</span><span class="sxs-lookup"><span data-stu-id="8950e-283">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="8950e-284">nativní</span><span class="sxs-lookup"><span data-stu-id="8950e-284">native</span></span> | <span data-ttu-id="8950e-285">nativní</span><span class="sxs-lookup"><span data-stu-id="8950e-285">native</span></span> |
| <span data-ttu-id="8950e-286">žádná</span><span class="sxs-lookup"><span data-stu-id="8950e-286">none</span></span> | <span data-ttu-id="8950e-287">Žádné složky</span><span class="sxs-lookup"><span data-stu-id="8950e-287">No folders</span></span> |
| <span data-ttu-id="8950e-288">všechny</span><span class="sxs-lookup"><span data-stu-id="8950e-288">all</span></span> | <span data-ttu-id="8950e-289">Všechny složky</span><span class="sxs-lookup"><span data-stu-id="8950e-289">All folders</span></span> |

<span data-ttu-id="8950e-290">Například následující řádky signalizovat závislosti na `PackageA` verze 1.1.0 nebo vyšší, a `PackageB` verzi 1.x.</span><span class="sxs-lookup"><span data-stu-id="8950e-290">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="8950e-291">Následující řádky označují závislostí na stejné balíčky, ale zadané k vložení `contentFiles` a `build` složky `PackageA` a všechno, co ale `native` a `compile` složky `PackageB`"</span><span class="sxs-lookup"><span data-stu-id="8950e-291">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="8950e-292">Poznámka: Při vytváření `.nuspec` z projektu pomocí `nuget spec`, závislosti, které existují v tomto projektu jsou automaticky obsažené ve výsledné `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="8950e-292">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="8950e-293">Závislostí skupin</span><span class="sxs-lookup"><span data-stu-id="8950e-293">Dependency groups</span></span>

<span data-ttu-id="8950e-294">*Verze 2.0 +*</span><span class="sxs-lookup"><span data-stu-id="8950e-294">*Version 2.0+*</span></span>

<span data-ttu-id="8950e-295">Jako alternativu k jednomu seznamu bez stromové struktury, se dá nastavit závislosti podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<dependencies>`.</span><span class="sxs-lookup"><span data-stu-id="8950e-295">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="8950e-296">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<dependency>` elementy.</span><span class="sxs-lookup"><span data-stu-id="8950e-296">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="8950e-297">Tyto závislosti jsou nainstalovány společně, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="8950e-297">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="8950e-298">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="8950e-298">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="8950e-299">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="8950e-299">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="8950e-300">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="8950e-300">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="8950e-301">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="8950e-301">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="8950e-302">Odkazy na explicitní sestavení</span><span class="sxs-lookup"><span data-stu-id="8950e-302">Explicit assembly references</span></span>

<span data-ttu-id="8950e-303">`<references>` Prvek explicitně určuje sestavení, které by měly odkazovat na cílový projekt, při použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-303">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="8950e-304">Pokud tento prvek je k dispozici, NuGet přidat odkazy pouze na uvedené sestavení; nepřidá odkazy pro jiná sestavení v balíčku `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="8950e-304">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="8950e-305">Například následující `<references>` element dává pokyn NuGet pro přidání odkazů na pouze `xunit.dll` a `xunit.extensions.dll` i v případě, že existují další sestavení v balíčku:</span><span class="sxs-lookup"><span data-stu-id="8950e-305">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="8950e-306">Explicitní odkazy se obvykle používají pro pouze na sestavení doby návrhu.</span><span class="sxs-lookup"><span data-stu-id="8950e-306">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="8950e-307">Při použití [kontrakty kódu](/dotnet/framework/debug-trace-profile/code-contracts), například sestavení kontraktu musí být vedle sestavení modulu runtime, které se rozšiřují, aby Visual Studio můžete najít, ale kontrakt sestavení nemusí být odkazuje projekt nebo zkopírovat do projektu `bin` složky.</span><span class="sxs-lookup"><span data-stu-id="8950e-307">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="8950e-308">Podobně je možné explicitní odkazy pro rozhraní pro testování částí, jako jsou XUnit, která potřebuje jeho nástroje pro sestavení vedle sestavení modulu runtime, ale nemá potřebovat, který je zahrnutý jako odkazy na projekt.</span><span class="sxs-lookup"><span data-stu-id="8950e-308">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="8950e-309">Referenční skupiny</span><span class="sxs-lookup"><span data-stu-id="8950e-309">Reference groups</span></span>

<span data-ttu-id="8950e-310">Jako alternativu k jednomu plochého seznamu lze upravit odkazy podle profilu framework cílový projekt pomocí `<group>` elementů v rámci `<references>`.</span><span class="sxs-lookup"><span data-stu-id="8950e-310">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="8950e-311">Každá skupina obsahuje atribut s názvem `targetFramework` a obsahuje nulu nebo více `<reference>` elementy.</span><span class="sxs-lookup"><span data-stu-id="8950e-311">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="8950e-312">Tyto odkazy jsou přidány do projektu, když Cílová architektura, která je kompatibilní s profilem rozhraní framework projektu.</span><span class="sxs-lookup"><span data-stu-id="8950e-312">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="8950e-313">`<group>` Element bez `targetFramework` atribut se používá jako výchozí nebo záložní seznamu odkazů.</span><span class="sxs-lookup"><span data-stu-id="8950e-313">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="8950e-314">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="8950e-314">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="8950e-315">Formát skupiny nelze smíšeného s nestrukturovaného seznamu.</span><span class="sxs-lookup"><span data-stu-id="8950e-315">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="8950e-316">Následující příklad ukazuje různé varianty `<group>` element:</span><span class="sxs-lookup"><span data-stu-id="8950e-316">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="8950e-317">Odkazy na sestavení rozhraní</span><span class="sxs-lookup"><span data-stu-id="8950e-317">Framework assembly references</span></span>

<span data-ttu-id="8950e-318">Sestavení rozhraní jsou ty, které jsou součástí rozhraní .NET framework a by už měla být v globální mezipaměti sestavení (GAC) pro libovolný daný počítač.</span><span class="sxs-lookup"><span data-stu-id="8950e-318">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="8950e-319">Určením těchto sestavení v rámci `<frameworkAssemblies>` elementu balíčku můžete zajistit, že požadované odkazy jsou přidány do projektu, v případě, že projekt již nemá tyto odkazy.</span><span class="sxs-lookup"><span data-stu-id="8950e-319">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="8950e-320">Takové sestavení, samozřejmě, nejsou obsažené v balíčku přímo.</span><span class="sxs-lookup"><span data-stu-id="8950e-320">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="8950e-321">`<frameworkAssemblies>` Prvek obsahuje nula nebo více `<frameworkAssembly>` prvky, z nichž každý určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="8950e-321">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="8950e-322">Atribut</span><span class="sxs-lookup"><span data-stu-id="8950e-322">Attribute</span></span> | <span data-ttu-id="8950e-323">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-323">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8950e-324">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="8950e-324">**assemblyName**</span></span> | <span data-ttu-id="8950e-325">(Povinné) Plně kvalifikovaný název.</span><span class="sxs-lookup"><span data-stu-id="8950e-325">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="8950e-326">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="8950e-326">**targetFramework**</span></span> | <span data-ttu-id="8950e-327">(Volitelné) Určuje cílovou architekturu, pro který platí tento odkaz.</span><span class="sxs-lookup"><span data-stu-id="8950e-327">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="8950e-328">Pokud tento parametr vynechán, označuje, že odkaz použije pro všechny platformy.</span><span class="sxs-lookup"><span data-stu-id="8950e-328">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="8950e-329">Zobrazit [platforem](../reference/target-frameworks.md) pro identifikátory přesné framework.</span><span class="sxs-lookup"><span data-stu-id="8950e-329">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="8950e-330">Následující příklad ukazuje odkaz na `System.Net` pro všechny cílové platformy a odkaz na `System.ServiceModel` pro pouze rozhraní .NET Framework 4.0:</span><span class="sxs-lookup"><span data-stu-id="8950e-330">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="8950e-331">Včetně souborů sestavení</span><span class="sxs-lookup"><span data-stu-id="8950e-331">Including assembly files</span></span>

<span data-ttu-id="8950e-332">Pokud budete postupovat podle konvence je popsáno v [vytvoření balíčku](../create-packages/creating-a-package.md), není potřeba explicitně zadat seznam souborů v `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="8950e-332">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="8950e-333">`nuget pack` Příkaz automaticky převezme potřebné soubory.</span><span class="sxs-lookup"><span data-stu-id="8950e-333">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="8950e-334">Při instalaci do projektu balíček NuGet automaticky přidá odkazy na sestavení knihovny DLL balíčku, *s výjimkou* ty, které jsou pojmenovány `.resources.dll` vzhledem k tomu, že se budou považovat za lokalizovaná satelitní sestavení.</span><span class="sxs-lookup"><span data-stu-id="8950e-334">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="8950e-335">Z tohoto důvodu se vyhněte se použití `.resources.dll` pro soubory, které jinak obsahují základní balíček kódu.</span><span class="sxs-lookup"><span data-stu-id="8950e-335">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="8950e-336">Toto automatické chování obejít a explicitně kontrolovat soubory, které jsou obsažené v balíčku, umístěte `<files>` jako podřízený element `<package>` (a na stejné úrovni `<metadata>`), identifikuje každý soubor se samostatným `<file>` element.</span><span class="sxs-lookup"><span data-stu-id="8950e-336">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="8950e-337">Příklad:</span><span class="sxs-lookup"><span data-stu-id="8950e-337">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="8950e-338">Nuget 2.x a dřívějších verzí a projekty pomocí `packages.config`, `<files>` element slouží také k neměnné obsahu soubory k zahrnutí při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="8950e-338">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="8950e-339">S NuGet 3.3 + i na PackageReference `<contentFiles>` elementu je použita.</span><span class="sxs-lookup"><span data-stu-id="8950e-339">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="8950e-340">Zobrazit [včetně soubory obsahu](#including-content-files) níže podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="8950e-340">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="8950e-341">Atributy souboru</span><span class="sxs-lookup"><span data-stu-id="8950e-341">File element attributes</span></span>

<span data-ttu-id="8950e-342">Každý `<file>` prvek určuje následující atributy:</span><span class="sxs-lookup"><span data-stu-id="8950e-342">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="8950e-343">Atribut</span><span class="sxs-lookup"><span data-stu-id="8950e-343">Attribute</span></span> | <span data-ttu-id="8950e-344">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-344">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8950e-345">**src**</span><span class="sxs-lookup"><span data-stu-id="8950e-345">**src**</span></span> | <span data-ttu-id="8950e-346">Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="8950e-346">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="8950e-347">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="8950e-347">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="8950e-348">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="8950e-348">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8950e-349">**cíl**</span><span class="sxs-lookup"><span data-stu-id="8950e-349">**target**</span></span> | <span data-ttu-id="8950e-350">Relativní cesta ke složce v rámci balíčku, kde jsou umístěny zdrojové soubory, které musí začínat `lib`, `content`, `build`, nebo `tools`.</span><span class="sxs-lookup"><span data-stu-id="8950e-350">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="8950e-351">Zobrazit [vytváření souboru .nuspec z pracovního adresáře podle úmluvy](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="8950e-351">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="8950e-352">**vyloučení**</span><span class="sxs-lookup"><span data-stu-id="8950e-352">**exclude**</span></span> | <span data-ttu-id="8950e-353">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="8950e-353">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="8950e-354">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="8950e-354">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="8950e-355">Příklady</span><span class="sxs-lookup"><span data-stu-id="8950e-355">Examples</span></span>

<span data-ttu-id="8950e-356">**Jediné sestavení**</span><span class="sxs-lookup"><span data-stu-id="8950e-356">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="8950e-357">**Jediné sestavení specifická pro rozhraní .NET framework**</span><span class="sxs-lookup"><span data-stu-id="8950e-357">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="8950e-358">**Sada knihovny DLL pomocí zástupného znaku**</span><span class="sxs-lookup"><span data-stu-id="8950e-358">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="8950e-359">**Knihovny DLL pro různá rozhraní**</span><span class="sxs-lookup"><span data-stu-id="8950e-359">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="8950e-360">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="8950e-360">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="8950e-361">Včetně souborů obsahu</span><span class="sxs-lookup"><span data-stu-id="8950e-361">Including content files</span></span>

<span data-ttu-id="8950e-362">Soubory obsahu jsou neměnné soubory, které je potřeba zahrnout do projektu balíček.</span><span class="sxs-lookup"><span data-stu-id="8950e-362">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="8950e-363">Je neměnný, nejsou určeny k používání projektu změnit.</span><span class="sxs-lookup"><span data-stu-id="8950e-363">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="8950e-364">Příklad obsahu souborů patří:</span><span class="sxs-lookup"><span data-stu-id="8950e-364">Example content files include:</span></span>

- <span data-ttu-id="8950e-365">Bitové kopie, které jsou vloženy jako prostředky</span><span class="sxs-lookup"><span data-stu-id="8950e-365">Images that are embedded as resources</span></span>
- <span data-ttu-id="8950e-366">Zdrojové soubory, které jsou již kompilován</span><span class="sxs-lookup"><span data-stu-id="8950e-366">Source files that are already compiled</span></span>
- <span data-ttu-id="8950e-367">Skripty, které musí být součástí výstupu sestavení projektu</span><span class="sxs-lookup"><span data-stu-id="8950e-367">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="8950e-368">Konfigurační soubory pro balíček, který mají být zahrnuti do projektu, ale není třeba žádné změny specifické pro projekt</span><span class="sxs-lookup"><span data-stu-id="8950e-368">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="8950e-369">Obsahu souborů jsou součástí balíčku pomocí `<files>` elementu, určení `content` složky `target` atribut.</span><span class="sxs-lookup"><span data-stu-id="8950e-369">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="8950e-370">Ale tyto soubory jsou ignorovány při instalaci balíčku v projektu pomocí PackageReference, který používá místo toho `<contentFiles>` elementu.</span><span class="sxs-lookup"><span data-stu-id="8950e-370">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="8950e-371">Balíček pro maximální kompatibility s využívání projektů v ideálním případě Určuje soubory obsahu v obou elementech.</span><span class="sxs-lookup"><span data-stu-id="8950e-371">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="8950e-372">Pomocí elementu souborů pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="8950e-372">Using the files element for content files</span></span>

<span data-ttu-id="8950e-373">Pro soubory obsahu, stačí použít stejný formát jako soubory sestavení, ale zadat `content` jako základní složka v `target` atributu, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="8950e-373">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="8950e-374">**Soubory základního obsahu**</span><span class="sxs-lookup"><span data-stu-id="8950e-374">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="8950e-375">**Soubory obsahu s adresářovou strukturu**</span><span class="sxs-lookup"><span data-stu-id="8950e-375">**Content files with directory structure**</span></span>

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

<span data-ttu-id="8950e-376">**Soubor s obsahem specifické pro cílové prostředí**</span><span class="sxs-lookup"><span data-stu-id="8950e-376">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="8950e-377">**Zkopírovat do složky s tečkou v názvu souboru obsahu**</span><span class="sxs-lookup"><span data-stu-id="8950e-377">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="8950e-378">V takovém případě se zobrazí NuGet, který rozšíření v `target` se neshoduje s příponou v `src` a proto zpracovává tuto část názvu v `target` jako složka:</span><span class="sxs-lookup"><span data-stu-id="8950e-378">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="8950e-379">**Soubory obsahu bez přípony**</span><span class="sxs-lookup"><span data-stu-id="8950e-379">**Content files without extensions**</span></span>

<span data-ttu-id="8950e-380">Chcete-li zahrnout soubory bez přípony, použijte `*` nebo `**` zástupné znaky:</span><span class="sxs-lookup"><span data-stu-id="8950e-380">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="8950e-381">**Soubory obsahu se hloubkové cesty a hloubkové cílem**</span><span class="sxs-lookup"><span data-stu-id="8950e-381">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="8950e-382">V takovém případě protože přípony zdrojovou a cílovou odpovídají, NuGet předpokládá, že cíl je název souboru a nikoliv složka:</span><span class="sxs-lookup"><span data-stu-id="8950e-382">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="8950e-383">**Přejmenování souboru obsahu v balíčku**</span><span class="sxs-lookup"><span data-stu-id="8950e-383">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="8950e-384">**Vyloučení souborů**</span><span class="sxs-lookup"><span data-stu-id="8950e-384">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="8950e-385">Pomocí elementu contentFiles pro soubory obsahu</span><span class="sxs-lookup"><span data-stu-id="8950e-385">Using the contentFiles element for content files</span></span>

<span data-ttu-id="8950e-386">*NuGet 4.0 + s PackageReference*</span><span class="sxs-lookup"><span data-stu-id="8950e-386">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="8950e-387">Ve výchozím nastavení, umístí balíček obsahu `contentFiles` složky (viz níže) a `nuget pack` zahrnuty všechny soubory ve složce pomocí výchozí atributy.</span><span class="sxs-lookup"><span data-stu-id="8950e-387">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="8950e-388">V tomto případě není nutné zahrnout `contentFiles` uzlu `.nuspec` vůbec.</span><span class="sxs-lookup"><span data-stu-id="8950e-388">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="8950e-389">K řízení souborů, které jsou zahrnuty `<contentFiles>` prvek určuje je kolekce `<files>` mezi prvky, které identifikují přesné soubory patří.</span><span class="sxs-lookup"><span data-stu-id="8950e-389">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="8950e-390">Tyto soubory jsou určené sadu atributů, které popisují, jak mají být použity v rámci systému projektů:</span><span class="sxs-lookup"><span data-stu-id="8950e-390">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="8950e-391">Atribut</span><span class="sxs-lookup"><span data-stu-id="8950e-391">Attribute</span></span> | <span data-ttu-id="8950e-392">Popis</span><span class="sxs-lookup"><span data-stu-id="8950e-392">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8950e-393">**Zahrnout**</span><span class="sxs-lookup"><span data-stu-id="8950e-393">**include**</span></span> | <span data-ttu-id="8950e-394">(Povinné) Umístění souboru nebo souborů zahrnout v souladu s vyloučení určené `exclude` atribut.</span><span class="sxs-lookup"><span data-stu-id="8950e-394">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="8950e-395">Cesta je vzhledem k `.nuspec` souboru není určena absolutní cestu.</span><span class="sxs-lookup"><span data-stu-id="8950e-395">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="8950e-396">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="8950e-396">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8950e-397">**vyloučení**</span><span class="sxs-lookup"><span data-stu-id="8950e-397">**exclude**</span></span> | <span data-ttu-id="8950e-398">Středníkem oddělený seznam soubory nebo vzory souborů, které chcete vyloučit z `src` umístění.</span><span class="sxs-lookup"><span data-stu-id="8950e-398">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="8950e-399">Zástupný znak `*` je povolený nebo double zástupné `**` znamená rekurzivní hledání složky.</span><span class="sxs-lookup"><span data-stu-id="8950e-399">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8950e-400">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="8950e-400">**buildAction**</span></span> | <span data-ttu-id="8950e-401">Akce sestavení zařadit do obsahu položky nástroje MSBuild, jako například `Content`, `None`, `Embedded Resource`, `Compile`atd. Výchozí hodnota je `Compile`.</span><span class="sxs-lookup"><span data-stu-id="8950e-401">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="8950e-402">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="8950e-402">**copyToOutput**</span></span> | <span data-ttu-id="8950e-403">Logická hodnota označující, jestli se má kopírovat položky obsahu pro sestavení (nebo publikovat) výstupní složka.</span><span class="sxs-lookup"><span data-stu-id="8950e-403">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="8950e-404">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="8950e-404">The default is false.</span></span> |
| <span data-ttu-id="8950e-405">**Sloučit**</span><span class="sxs-lookup"><span data-stu-id="8950e-405">**flatten**</span></span> | <span data-ttu-id="8950e-406">Logická hodnota označující, zda se můžete kopírovat položky obsahu na jedinou složku ve výstupu sestavení (pravda), nebo zachovat strukturu složek v balíčku (false).</span><span class="sxs-lookup"><span data-stu-id="8950e-406">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="8950e-407">Tento příznak funguje pouze v případě copyToOutput příznak je nastaven na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="8950e-407">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="8950e-408">Výchozí hodnota je false.</span><span class="sxs-lookup"><span data-stu-id="8950e-408">The default is false.</span></span> |

<span data-ttu-id="8950e-409">Při instalaci balíčku NuGet platí podřízených elementů `<contentFiles>` shora dolů.</span><span class="sxs-lookup"><span data-stu-id="8950e-409">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="8950e-410">Pokud se shodují na stejný soubor několik záznamů se použijí všechny položky.</span><span class="sxs-lookup"><span data-stu-id="8950e-410">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="8950e-411">Položky navrchu přepíše nižší položky dojde ke konfliktu pro stejný atribut.</span><span class="sxs-lookup"><span data-stu-id="8950e-411">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="8950e-412">Struktura složky balíčku</span><span class="sxs-lookup"><span data-stu-id="8950e-412">Package folder structure</span></span>

<span data-ttu-id="8950e-413">Projekt balíčku strukturovat obsahu pomocí následujícímu vzoru:</span><span class="sxs-lookup"><span data-stu-id="8950e-413">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="8950e-414">`codeLanguages` může být `cs`, `vb`, `fs`, `any`, nebo malým ekvivalentem znaku danou `$(ProjectLanguage)`</span><span class="sxs-lookup"><span data-stu-id="8950e-414">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="8950e-415">`TxM` je všechny moniker právní cílového rozhraní, která podporuje NuGet (viz [platforem](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="8950e-415">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="8950e-416">Složky libovolné struktury složek může připojen na konec této syntaxe.</span><span class="sxs-lookup"><span data-stu-id="8950e-416">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="8950e-417">Příklad:</span><span class="sxs-lookup"><span data-stu-id="8950e-417">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="8950e-418">Můžete použít prázdné složky `.` chcete vyjádřit výslovný nesouhlas poskytnutí obsahu pro určité kombinace jazyka a TxM, například:</span><span class="sxs-lookup"><span data-stu-id="8950e-418">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="8950e-419">Vzorový oddíl contentFiles</span><span class="sxs-lookup"><span data-stu-id="8950e-419">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="8950e-420">Příklad souboru .nuspec soubory</span><span class="sxs-lookup"><span data-stu-id="8950e-420">Example .nuspec files</span></span>

<span data-ttu-id="8950e-421">**Jednoduchý `.nuspec` , která neurčuje závislosti nebo souborů**</span><span class="sxs-lookup"><span data-stu-id="8950e-421">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="8950e-422">**A `.nuspec` se závislostmi**</span><span class="sxs-lookup"><span data-stu-id="8950e-422">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="8950e-423">**A `.nuspec` se soubory**</span><span class="sxs-lookup"><span data-stu-id="8950e-423">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="8950e-424">**A `.nuspec` se sestaveními rozhraní framework**</span><span class="sxs-lookup"><span data-stu-id="8950e-424">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="8950e-425">V tomto příkladu tímto se nainstalují pro konkrétní projekt cílí:</span><span class="sxs-lookup"><span data-stu-id="8950e-425">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="8950e-426">.NET4 -> `System.Web`, `System.Net`</span><span class="sxs-lookup"><span data-stu-id="8950e-426">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="8950e-427">. NET4 -> Client Profile `System.Net`</span><span class="sxs-lookup"><span data-stu-id="8950e-427">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="8950e-428">-> Silverlight 3 `System.Json`</span><span class="sxs-lookup"><span data-stu-id="8950e-428">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="8950e-429">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="8950e-429">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="8950e-430">WindowsPhone -> `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="8950e-430">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
