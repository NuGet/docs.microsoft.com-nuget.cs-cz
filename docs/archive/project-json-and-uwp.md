---
title: project.jsNuGet na soubor s projekty UWP
description: Popis způsobu, jakým se project.jspro soubor používá ke sledování závislostí NuGet v projektech Univerzální platforma Windows (UWP).
author: JonDouglas
ms.author: jodou
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 30e2272aafb5d2ea8d932e3cb0209d97c30b3209
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773803"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="029be-103">project.json a UPW</span><span class="sxs-lookup"><span data-stu-id="029be-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="029be-104">Tento obsah je zastaralý.</span><span class="sxs-lookup"><span data-stu-id="029be-104">This content is deprecated.</span></span> <span data-ttu-id="029be-105">Projekty by měly používat buď `packages.config` formáty PackageReference nebo.</span><span class="sxs-lookup"><span data-stu-id="029be-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="029be-106">Tento dokument popisuje strukturu balíčku, která využívá funkce v NuGet 3 + (Visual Studio 2015 a novější).</span><span class="sxs-lookup"><span data-stu-id="029be-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="029be-107">`minClientVersion`Vlastnost `.nuspec` , kterou jste si popsali, můžete použít k určení, že budete potřebovat funkce popsané tady, a to tak, že ji nastavíte na 3,1.</span><span class="sxs-lookup"><span data-stu-id="029be-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="029be-108">Přidání podpory UWP do existujícího balíčku</span><span class="sxs-lookup"><span data-stu-id="029be-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="029be-109">Pokud máte existující balíček a chcete přidat podporu pro aplikace pro UWP, pak nemusíte v takovém případě popsaný formát balíčku přijmout.</span><span class="sxs-lookup"><span data-stu-id="029be-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="029be-110">Tento formát je potřeba přijmout jenom v případě, že vyžadujete funkce, které popisuje, a jsou ochotní pracovat jenom s klienty, kteří se aktualizovaly na verzi 3 + klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="029be-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="029be-111">Již jsem cílí na netcore45</span><span class="sxs-lookup"><span data-stu-id="029be-111">I already target netcore45</span></span>

<span data-ttu-id="029be-112">Pokud už cílíte na cíl `netcore45` a nemusíte používat tyto funkce, není nutné provádět žádnou akci.</span><span class="sxs-lookup"><span data-stu-id="029be-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="029be-113">`netcore45` balíčky můžou využívat aplikace UWP.</span><span class="sxs-lookup"><span data-stu-id="029be-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="029be-114">Chci využít výhod specifických rozhraní API pro Windows 10</span><span class="sxs-lookup"><span data-stu-id="029be-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="029be-115">V takovém případě musíte `uap10.0` do balíčku přidat moniker cílového rozhraní (TFM nebo TxM).</span><span class="sxs-lookup"><span data-stu-id="029be-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="029be-116">Vytvořte ve svém balíčku novou složku a přidejte sestavení, které bylo zkompilováno pro práci s Windows 10, do této složky.</span><span class="sxs-lookup"><span data-stu-id="029be-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="029be-117">Nepotřebujem rozhraní API specifická pro Windows 10, ale chcete, aby už nové funkce .NET nebo netcore45 ještě neexistují.</span><span class="sxs-lookup"><span data-stu-id="029be-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="029be-118">V takovém případě byste přidali `dotnet` TxM do balíčku.</span><span class="sxs-lookup"><span data-stu-id="029be-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="029be-119">Na rozdíl od jiných TxMs `dotnet` neznamená oblast povrchu nebo platformu.</span><span class="sxs-lookup"><span data-stu-id="029be-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="029be-120">Uvádí, že váš balíček funguje na jakékoli platformě, na které fungují závislosti.</span><span class="sxs-lookup"><span data-stu-id="029be-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="029be-121">Při sestavování balíčku s `dotnet` TxM pravděpodobně máte mnoho dalších závislostí specifických pro TxM `.nuspec` , protože potřebujete definovat balíčky BCL, na kterých jste závislí, například, `System.Text` `System.Xml` atd. Umístění, na kterých tyto závislosti pracují, definují, kde váš balíček funguje.</span><span class="sxs-lookup"><span data-stu-id="029be-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="029be-122">Návody zjistit moje závislosti</span><span class="sxs-lookup"><span data-stu-id="029be-122">How do I find out my dependencies</span></span>

<span data-ttu-id="029be-123">Existují dva způsoby, jak zjistit, které závislosti se mají zobrazit:</span><span class="sxs-lookup"><span data-stu-id="029be-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="029be-124">Použijte nástroj [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) od **třetí strany** .</span><span class="sxs-lookup"><span data-stu-id="029be-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="029be-125">Nástroj automatizuje proces a aktualizuje `.nuspec` soubor pomocí závislých balíčků při sestavování.</span><span class="sxs-lookup"><span data-stu-id="029be-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="029be-126">Je k dispozici prostřednictvím balíčku NuGet [NuSpec. ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="029be-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="029be-127">(Pevným způsobem) Použijte `ILDasm` k `.dll` zobrazení informací o tom, jaká sestavení skutečně potřebují za běhu.</span><span class="sxs-lookup"><span data-stu-id="029be-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="029be-128">Pak určete, ze kterého balíčku NuGet pocházejí.</span><span class="sxs-lookup"><span data-stu-id="029be-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="029be-129">[`project.json`](project-json.md)Podrobnosti o funkcích, které vám pomůžou při vytváření balíčku, který podporuje TxM, najdete v tématu `dotnet` .</span><span class="sxs-lookup"><span data-stu-id="029be-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="029be-130">Pokud má váš balíček sloužit k práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složku, aby se předešlo varování a potenciálním problémům s kompatibilitou.</span><span class="sxs-lookup"><span data-stu-id="029be-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="029be-131">Adresářová struktura</span><span class="sxs-lookup"><span data-stu-id="029be-131">Directory structure</span></span>

<span data-ttu-id="029be-132">Balíčky NuGet v tomto formátu mají následující dobře známou složku a chování:</span><span class="sxs-lookup"><span data-stu-id="029be-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="029be-133">Složka</span><span class="sxs-lookup"><span data-stu-id="029be-133">Folder</span></span> | <span data-ttu-id="029be-134">Chování</span><span class="sxs-lookup"><span data-stu-id="029be-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="029be-135">Sestavení</span><span class="sxs-lookup"><span data-stu-id="029be-135">Build</span></span> | <span data-ttu-id="029be-136">Obsahuje cíle a soubory props nástroje MSBuild v této složce jsou v projektu integrovány jinak, ale v opačném případě nedojde ke změně.</span><span class="sxs-lookup"><span data-stu-id="029be-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="029be-137">Nástroje</span><span class="sxs-lookup"><span data-stu-id="029be-137">Tools</span></span> | <span data-ttu-id="029be-138">`install.ps1` a `uninstall.ps1` nejsou spuštěny.</span><span class="sxs-lookup"><span data-stu-id="029be-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="029be-139">`init.ps1` funguje stejně jako vždy.</span><span class="sxs-lookup"><span data-stu-id="029be-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="029be-140">Content</span><span class="sxs-lookup"><span data-stu-id="029be-140">Content</span></span> | <span data-ttu-id="029be-141">Obsah není automaticky zkopírován do projektu uživatele.</span><span class="sxs-lookup"><span data-stu-id="029be-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="029be-142">Podpora pro zahrnutí obsahu v projektu je plánována pro pozdější verzi.</span><span class="sxs-lookup"><span data-stu-id="029be-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="029be-143">Knihovna</span><span class="sxs-lookup"><span data-stu-id="029be-143">Lib</span></span> | <span data-ttu-id="029be-144">Pro mnoho balíčků `lib` funguje stejným způsobem jako v NuGet 2. x, ale s rozšířenými možnostmi, které je možné použít v ní, a lepší logikou pro vybírání správné podsložky při využívání balíčků.</span><span class="sxs-lookup"><span data-stu-id="029be-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="029be-145">Nicméně při použití ve spojení s `ref` , `lib` Složka obsahuje sestavení, která implementují plochu určenou v sestaveních ve `ref` složce.</span><span class="sxs-lookup"><span data-stu-id="029be-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="029be-146">Odkazů</span><span class="sxs-lookup"><span data-stu-id="029be-146">Ref</span></span> | <span data-ttu-id="029be-147">`ref` je volitelná složka, která obsahuje sestavení .NET, která definují veřejnou plochu (veřejné typy a metody) pro aplikaci, která má být zkompilována.</span><span class="sxs-lookup"><span data-stu-id="029be-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="029be-148">Sestavení v této složce nemusí mít žádnou implementaci, jsou čistě použita k definování oblasti povrchu pro kompilátor.</span><span class="sxs-lookup"><span data-stu-id="029be-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="029be-149">Pokud balíček nemá `ref` složku, pak `lib` je referenční sestavení i sestavení implementace.</span><span class="sxs-lookup"><span data-stu-id="029be-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="029be-150">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="029be-150">Runtimes</span></span> | <span data-ttu-id="029be-151">`runtimes` je volitelná složka, která obsahuje kód specifický pro operační systém, jako je například architektura procesoru a specifické pro operační systém nebo jiné binární soubory závislé na platformě.</span><span class="sxs-lookup"><span data-stu-id="029be-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="029be-152">Cíle a soubory props nástroje MSBuild v balíčcích</span><span class="sxs-lookup"><span data-stu-id="029be-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="029be-153">Balíčky NuGet mohou obsahovat `.targets` `.props` soubory a, které jsou importovány do jakéhokoli projektu MSBuild, do kterého je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="029be-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="029be-154">V NuGet 2. x to bylo provedeno vložením `<Import>` příkazů do `.csproj` souboru, v NuGet 3,0 neexistuje žádná konkrétní akce "instalace do projektu".</span><span class="sxs-lookup"><span data-stu-id="029be-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="029be-155">Proces obnovení balíčku místo toho zapisuje dva soubory `[projectname].nuget.props` a `[projectname].NuGet.targets` .</span><span class="sxs-lookup"><span data-stu-id="029be-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="029be-156">Nástroj MSBuild ví, že tyto dva soubory budou hledat, a automaticky je naimportuje poblíž začátku a blízko konce procesu sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="029be-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="029be-157">To poskytuje velmi podobné chování jako NuGet 2. x, ale s jedním významným rozdílem: *v tomto případě není nijak zaručeno pořadí souborů targets/props*.</span><span class="sxs-lookup"><span data-stu-id="029be-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="029be-158">Nástroj MSBuild však poskytuje možnosti pro seřazení cílů pomocí `BeforeTargets` atributů a `AfterTargets` `<Target>` definice (viz [element Target (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="029be-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="029be-159">Lib a ref</span><span class="sxs-lookup"><span data-stu-id="029be-159">Lib and Ref</span></span>

<span data-ttu-id="029be-160">Chování `lib` složky se v NuGet V3 významně nezměnilo.</span><span class="sxs-lookup"><span data-stu-id="029be-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="029be-161">Nicméně všechna sestavení musí být v podsložkách s názvem po TxM a nelze je nadále umístit přímo do `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="029be-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="029be-162">TxM je název platformy, pro kterou má daný Asset v balíčku fungovat.</span><span class="sxs-lookup"><span data-stu-id="029be-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="029be-163">Logicky jsou toto rozšíření monikerů cílového rozhraní (TFM), například,, `net45` `net46` `netcore50` a `dnxcore50` jsou všechny příklady TxMs (viz [cílové architektury](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="029be-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="029be-164">TxM může odkazovat na rozhraní Framework (TFM) a také na jiné oblasti Surface specifické pro platformu.</span><span class="sxs-lookup"><span data-stu-id="029be-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="029be-165">Například UWP TxM ( `uap10.0` ) představuje oblast povrchu rozhraní .NET a také plochu Windows pro aplikace UWP.</span><span class="sxs-lookup"><span data-stu-id="029be-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="029be-166">Ukázková struktura lib:</span><span class="sxs-lookup"><span data-stu-id="029be-166">An example lib structure:</span></span>

```
lib
├───net40
│       MyLibrary.dll
└───wp81
        MyLibrary.dll
```

<span data-ttu-id="029be-167">`lib`Složka obsahuje sestavení, která se používají za běhu.</span><span class="sxs-lookup"><span data-stu-id="029be-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="029be-168">Pro většinu balíčků `lib` je všechny požadované složky pro každý cílový TxMs.</span><span class="sxs-lookup"><span data-stu-id="029be-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="029be-169">Odkazů</span><span class="sxs-lookup"><span data-stu-id="029be-169">Ref</span></span>

<span data-ttu-id="029be-170">V některých případech se v průběhu kompilace mají použít jiné sestavení (referenční sestavení .NET to udělá dnes).</span><span class="sxs-lookup"><span data-stu-id="029be-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="029be-171">V takových případech použijte složku na nejvyšší úrovni s názvem `ref` (krátká pro "referenční sestavení").</span><span class="sxs-lookup"><span data-stu-id="029be-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="029be-172">Většina tvůrců balíčků nevyžaduje `ref` složku.</span><span class="sxs-lookup"><span data-stu-id="029be-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="029be-173">Je užitečné pro balíčky, které musí poskytovat konzistentní plochu pro kompilaci a IntelliSense, ale pak mají odlišnou implementaci pro různé TxMs.</span><span class="sxs-lookup"><span data-stu-id="029be-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="029be-174">Největším případem použití tohoto jsou `System.*` balíčky, které se vytvářejí jako součást přenosu .NET Core na NuGet.</span><span class="sxs-lookup"><span data-stu-id="029be-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="029be-175">Tyto balíčky mají různé implementace, které jsou sjednocené konzistentní sadou referenčních sestavení.</span><span class="sxs-lookup"><span data-stu-id="029be-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="029be-176">Mechanicky jsou sestavení obsažená ve `ref` složce referenční sestavení, která jsou předávána kompilátoru.</span><span class="sxs-lookup"><span data-stu-id="029be-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="029be-177">Pro ty, které jste použili csc.exe jsou ta sestavení, která jsou předávána přepínači [možnosti jazyka C#/Reference](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) .</span><span class="sxs-lookup"><span data-stu-id="029be-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="029be-178">Struktura `ref` složky je stejná jako například `lib` :</span><span class="sxs-lookup"><span data-stu-id="029be-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

```
└───MyImageProcessingLib
        ├───lib
        │   ├───net40
        │   │       MyImageProcessingLibrary.dll
        │   │
        │   ├───net451
        │   │       MyImageProcessingLibrary.dll
        │   │
        │   └───win81
        │           MyImageProcessingLibrary.dll
        │
        └───ref
            ├───net40
            │       MyImageProcessingLibrary.dll
            │
            └───portable-net451-win81
                    MyImageProcessingLibrary.dll
```

<span data-ttu-id="029be-179">V tomto příkladu jsou všechna sestavení v `ref` adresářích identická.</span><span class="sxs-lookup"><span data-stu-id="029be-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="029be-180">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="029be-180">Runtimes</span></span>

<span data-ttu-id="029be-181">Složka runtime obsahuje sestavení a nativní knihovny, které jsou nutné ke spuštění v konkrétních "modulech runtime", které jsou obecně definovány operačním systémem a architekturou procesoru.</span><span class="sxs-lookup"><span data-stu-id="029be-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="029be-182">Tyto moduly runtime jsou identifikovány pomocí [identifikátorů modulu runtime (identifikátorů RID)](/dotnet/core/rid-catalog) , jako jsou,,, atd `win` `win-x86` `win7-x86` `win8-64` .</span><span class="sxs-lookup"><span data-stu-id="029be-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="029be-183">Nativní pomocníky pro použití rozhraní API specifických pro konkrétní platformu</span><span class="sxs-lookup"><span data-stu-id="029be-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="029be-184">Následující příklad ukazuje balíček, který má čistě spravovanou implementaci pro několik platforem, ale používá nativní pomocníky v systému Windows 8, kde může volat nativní rozhraní API specifická pro systém Windows 8.</span><span class="sxs-lookup"><span data-stu-id="029be-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

```
└───MyLibrary
        ├───lib
        │   └───net40
        │           MyLibrary.dll
        │
        └───runtimes
            ├───win8-x64
            │   ├───lib
            │   │   └───net40
            │   │           MyLibrary.dll
            │   │
            │   └───native
            │           MyNativeLibrary.dll
            │
            └───win8-x86
                ├───lib
                │   └───net40
                │           MyLibrary.dll
                │
                └───native
                        MyNativeLibrary.dll
```

<span data-ttu-id="029be-185">S ohledem na výše uvedený balíček dojde k následujícím akcím:</span><span class="sxs-lookup"><span data-stu-id="029be-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="029be-186">Pokud není ve Windows 8, `lib/net40/MyLibrary.dll` používá se sestavení.</span><span class="sxs-lookup"><span data-stu-id="029be-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="029be-187">Při použití v systému Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` je použit a `native/MyNativeHelper.dll` zkopírován do výstupu sestavení.</span><span class="sxs-lookup"><span data-stu-id="029be-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="029be-188">V příkladu výše `lib/net40` sestavení je čistě spravovaný kód, zatímco sestavení ve složce runtime budou p/Invoke do nativního sestavení pomocníka pro volání rozhraní API specifická pro systém Windows 8.</span><span class="sxs-lookup"><span data-stu-id="029be-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="029be-189">`lib`Je možné vybrat pouze jednu složku, takže pokud je složka specifická pro modul runtime, která je zvolena pouze pro konkrétní nemodul runtime `lib` .</span><span class="sxs-lookup"><span data-stu-id="029be-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="029be-190">Nativní složka je aditivní, pokud existuje, je zkopírována do výstupu sestavení.</span><span class="sxs-lookup"><span data-stu-id="029be-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="029be-191">Spravovaná obálka</span><span class="sxs-lookup"><span data-stu-id="029be-191">Managed wrapper</span></span>

<span data-ttu-id="029be-192">Dalším způsobem, jak použít modul runtime, je dodávat balíček, který je čistě spravovanou obálkou prostřednictvím nativního sestavení.</span><span class="sxs-lookup"><span data-stu-id="029be-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="029be-193">V tomto scénáři vytvoříte balíček podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="029be-193">In this scenario you create a package like the following:</span></span>

```
└───MyLibrary
        └───runtimes
            ├───win8-x64
            │   ├───lib
            │   │   └───net451
            │   │           MyLibrary.dll
            │   │
            │   └───native
            │           MyImplementation.dll
            │
            └───win8-x86
                ├───lib
                │   └───net451
                │           MyLibrary.dll
                │
                └───native
                        MyImplementation.dll
```

<span data-ttu-id="029be-194">V takovém případě neexistuje složka nejvyšší úrovně `lib` jako tato složka, protože není k dispozici žádná implementace tohoto balíčku, která nespoléhá na příslušné nativní sestavení.</span><span class="sxs-lookup"><span data-stu-id="029be-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="029be-195">Pokud bylo spravované sestavení `MyLibrary.dll` přesně stejné v obou těchto případech, můžeme ho umístit do složky na nejvyšší úrovni `lib` , ale vzhledem k tomu, že chybějící nativní sestavení nezpůsobí selhání balíčku, pokud byl nainstalován na platformu, která se nenainstalovala-x86 nebo Win-x64, bude použita knihovna lib nejvyšší úrovně, ale nezkopírovalo se žádné nativní sestavení.</span><span class="sxs-lookup"><span data-stu-id="029be-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="029be-196">Vytváření balíčků pro NuGet 2 a NuGet 3</span><span class="sxs-lookup"><span data-stu-id="029be-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="029be-197">Chcete-li vytvořit balíček, který mohou být spotřebovány projekty používajícími `packages.config` i balíčky, použijte `project.json` následující postup:</span><span class="sxs-lookup"><span data-stu-id="029be-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="029be-198">Pouze referenční a běhové moduly fungují pouze na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029be-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="029be-199">Obě tyto parametry ignorují aplikace NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="029be-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="029be-200">Nemůžete spoléhat `install.ps1` na `uninstall.ps1` funkce nebo na funkci.</span><span class="sxs-lookup"><span data-stu-id="029be-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="029be-201">Tyto soubory jsou spouštěny při použití `packages.config` , ale jsou ignorovány v `project.json` .</span><span class="sxs-lookup"><span data-stu-id="029be-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="029be-202">Takže váš balíček musí být použitelný bez spuštění.</span><span class="sxs-lookup"><span data-stu-id="029be-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="029be-203">`init.ps1` pořád běží na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029be-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="029be-204">Instalace cílů a vlastností se liší, takže se ujistěte, že váš balíček funguje na obou klientech podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="029be-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="029be-205">Podadresáře lib musí být TxM v NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029be-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="029be-206">Knihovny nelze umístit do kořenového adresáře `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="029be-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="029be-207">Obsah se nekopíruje automaticky s NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029be-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="029be-208">Příjemci vašeho balíčku by mohli sami zkopírovat soubory nebo použít nástroj jako Spouštěč úloh k automatizaci kopírování souborů.</span><span class="sxs-lookup"><span data-stu-id="029be-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="029be-209">Transformace zdrojového a konfiguračního souboru nejsou spouštěny NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="029be-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="029be-210">Pokud podporujete NuGet 2 a 3 `minClientVersion` , měla by se jednat o nejnižší verzi klienta NuGet 2, na které váš balíček funguje.</span><span class="sxs-lookup"><span data-stu-id="029be-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="029be-211">V případě existujícího balíčku by neměl být nutné ho změnit.</span><span class="sxs-lookup"><span data-stu-id="029be-211">In the case of an existing package it shouldn't need to change.</span></span>
