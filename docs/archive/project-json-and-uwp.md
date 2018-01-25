---
title: Soubor project.json NuGet s projekty UWP | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Popis použití souboru project.json k sledování závislostí NuGet v projektech pro univerzální platformu Windows (UWP)."
keywords: "NuGet závislosti, NuGet a UPW, UWP a project.json, soubor project.json NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0063c959a6d638d7ba1d579d35ff660dccae282c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="f02ac-104">Project.JSON a UWP</span><span class="sxs-lookup"><span data-stu-id="f02ac-104">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="f02ac-105">Tento obsah je zastaralý.</span><span class="sxs-lookup"><span data-stu-id="f02ac-105">This content is deprecated.</span></span> <span data-ttu-id="f02ac-106">Projekty využít buď `packages.config` nebo PackageReference formáty.</span><span class="sxs-lookup"><span data-stu-id="f02ac-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="f02ac-107">Tento dokument popisuje strukturu balíčku, která využívá funkce v NuGet 3 + (Visual Studio 2015 a novější).</span><span class="sxs-lookup"><span data-stu-id="f02ac-107">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="f02ac-108">`minClientVersion` Vlastnost vaší `.nuspec` slouží k stavu, že potřebujete popsané nastavením na 3.1 funkce.</span><span class="sxs-lookup"><span data-stu-id="f02ac-108">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="f02ac-109">Přidání podpory UPW do existujícího balíčku</span><span class="sxs-lookup"><span data-stu-id="f02ac-109">Adding UWP support to an existing package</span></span>

<span data-ttu-id="f02ac-110">Pokud máte existující balíček a chcete přidat podporu pro aplikace UWP, pak nemusíte přijmout balení formát, který je popsaný v tomto poli.</span><span class="sxs-lookup"><span data-stu-id="f02ac-110">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="f02ac-111">Stačí přijmout tento formát, pokud potřebujete funkce popisuje a chcete-li pracovat pouze s klienty, které byly aktualizovány na verzi 3 + klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="f02ac-111">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="f02ac-112">I již cíle netcore45</span><span class="sxs-lookup"><span data-stu-id="f02ac-112">I already target netcore45</span></span>

<span data-ttu-id="f02ac-113">Pokud cílíte `netcore45` již a nemusíte zde využít výhod funkcí, není vyžadována žádná akce.</span><span class="sxs-lookup"><span data-stu-id="f02ac-113">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="f02ac-114">`netcore45`balíčky mohou být spotřebovávána aplikace UWP.</span><span class="sxs-lookup"><span data-stu-id="f02ac-114">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="f02ac-115">Chcete využít výhod konkrétní rozhraní API systému Windows 10</span><span class="sxs-lookup"><span data-stu-id="f02ac-115">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="f02ac-116">V takovém případě je nutné přidat `uap10.0` cíle Přezdívka framework (TFM nebo TxM) do vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="f02ac-116">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="f02ac-117">Vytvořte novou složku na balíček a přidejte sestavení, která je kompilovaná pro práci s Windows 10 do této složky.</span><span class="sxs-lookup"><span data-stu-id="f02ac-117">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="f02ac-118">Není zapotřebí rozhraní API specifické pro Windows 10, ale mají nové funkce rozhraní .NET nebo již nemáte netcore45</span><span class="sxs-lookup"><span data-stu-id="f02ac-118">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="f02ac-119">V takovém případě byste přidali `dotnet` TxM do vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="f02ac-119">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="f02ac-120">Na rozdíl od jiných TxMs `dotnet` není určeno, útoku na nebo platformu.</span><span class="sxs-lookup"><span data-stu-id="f02ac-120">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="f02ac-121">Je oznamující, že váš balíček funguje na jakékoli platformě, která závislostmi práci.</span><span class="sxs-lookup"><span data-stu-id="f02ac-121">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="f02ac-122">Při vytváření balíčku s `dotnet` TxM, budete pravděpodobně mít mnoho další závislosti konkrétní TxM ve vaší `.nuspec`, jako je třeba definovat BCL balíčky, závisí na, například `System.Text`, `System.Xml`atd. Umístění, které fungují těchto závislostí na definovat, které pracuje vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="f02ac-122">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="f02ac-123">Jak zjistím Moje závislosti</span><span class="sxs-lookup"><span data-stu-id="f02ac-123">How do I find out my dependencies</span></span>

<span data-ttu-id="f02ac-124">Existují dva způsoby, jak zjistit, které závislosti do seznamu:</span><span class="sxs-lookup"><span data-stu-id="f02ac-124">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="f02ac-125">Použití [NuSpec závislostí generátor](https://github.com/onovotny/ReferenceGenerator) **3. stran** nástroj.</span><span class="sxs-lookup"><span data-stu-id="f02ac-125">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="f02ac-126">Nástroj automatizuje proces a aktualizace vašeho `.nuspec` soubor s balíčky závislých na sestavení.</span><span class="sxs-lookup"><span data-stu-id="f02ac-126">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="f02ac-127">Je k dispozici prostřednictvím balíčku NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="f02ac-127">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="f02ac-128">(Podle pevného) Použití `ILDasm` podívat se na vaše `.dll` chcete zobrazit, jaké sestavení jsou skutečně potřeba za běhu.</span><span class="sxs-lookup"><span data-stu-id="f02ac-128">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="f02ac-129">Pak stanovit, který NuGet balíček každá pocházet z.</span><span class="sxs-lookup"><span data-stu-id="f02ac-129">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="f02ac-130">Najdete v článku [ `project.json` ](project-json.md) téma podrobné informace o funkcích, které pomáhají při vytváření balíčku, který podporuje `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="f02ac-130">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="f02ac-131">Pokud váš balíček je určen pro práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složky, aby se zabránilo upozornění a potenciální problémy s kompatibilitou.</span><span class="sxs-lookup"><span data-stu-id="f02ac-131">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="f02ac-132">Struktura adresářů</span><span class="sxs-lookup"><span data-stu-id="f02ac-132">Directory structure</span></span>

<span data-ttu-id="f02ac-133">Balíčky NuGet formátu mají následující dobře známou složku a chování:</span><span class="sxs-lookup"><span data-stu-id="f02ac-133">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="f02ac-134">Folder</span><span class="sxs-lookup"><span data-stu-id="f02ac-134">Folder</span></span> | <span data-ttu-id="f02ac-135">Chování</span><span class="sxs-lookup"><span data-stu-id="f02ac-135">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="f02ac-136">Sestavení</span><span class="sxs-lookup"><span data-stu-id="f02ac-136">Build</span></span> | <span data-ttu-id="f02ac-137">Obsahuje nástroje MSBuild cíle a soubory props v této složce jsou jinak integrované do projektu, ale jinak není žádná změna.</span><span class="sxs-lookup"><span data-stu-id="f02ac-137">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="f02ac-138">Nástroje</span><span class="sxs-lookup"><span data-stu-id="f02ac-138">Tools</span></span> | <span data-ttu-id="f02ac-139">`install.ps1`a `uninstall.ps1` se nespustí.</span><span class="sxs-lookup"><span data-stu-id="f02ac-139">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="f02ac-140">`init.ps1`funguje jako má vždy.</span><span class="sxs-lookup"><span data-stu-id="f02ac-140">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="f02ac-141">Obsah</span><span class="sxs-lookup"><span data-stu-id="f02ac-141">Content</span></span> | <span data-ttu-id="f02ac-142">Obsah není automaticky zkopírují do projektu uživatele.</span><span class="sxs-lookup"><span data-stu-id="f02ac-142">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="f02ac-143">Podpora pro zahrnutí obsahu v projektu je plánovaná pro novější verzi.</span><span class="sxs-lookup"><span data-stu-id="f02ac-143">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="f02ac-144">Lib</span><span class="sxs-lookup"><span data-stu-id="f02ac-144">Lib</span></span> | <span data-ttu-id="f02ac-145">Pro mnoho balíčky `lib` funguje stejným způsobem jako v NuGet 2.x, ale s rozšířené možnosti pro jaké názvy dá se použít uvnitř ho a lepší logiku pro výběr správné podsložky při využívání balíčky.</span><span class="sxs-lookup"><span data-stu-id="f02ac-145">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="f02ac-146">Ale při použití ve spojení s `ref`, `lib` složka obsahuje sestavení, které implementují plochy definované v sestavení `ref` složky.</span><span class="sxs-lookup"><span data-stu-id="f02ac-146">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="f02ac-147">REF</span><span class="sxs-lookup"><span data-stu-id="f02ac-147">Ref</span></span> | <span data-ttu-id="f02ac-148">`ref`je volitelné složka, který obsahuje sestavení .NET definování veřejnosti prostor (veřejné typy a metody) pro aplikaci zkompilovat proti.</span><span class="sxs-lookup"><span data-stu-id="f02ac-148">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="f02ac-149">Sestavení v této složce může mít žádné implementace, se používají výhradně k definování povrchu pro kompilátor.</span><span class="sxs-lookup"><span data-stu-id="f02ac-149">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="f02ac-150">Pokud balíček neobsahuje žádné `ref` složku, pak se `lib` je referenční sestavení a implementace sestavení.</span><span class="sxs-lookup"><span data-stu-id="f02ac-150">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="f02ac-151">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="f02ac-151">Runtimes</span></span> | <span data-ttu-id="f02ac-152">`runtimes`je volitelné složka, která obsahuje konkrétní kódu operačního systému, třeba architektura procesoru a binární soubory závislé na platformu operačního systému konkrétní nebo jinak.</span><span class="sxs-lookup"><span data-stu-id="f02ac-152">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="f02ac-153">MSBuild cíle a soubory props do balíčků</span><span class="sxs-lookup"><span data-stu-id="f02ac-153">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="f02ac-154">Balíčky NuGet může obsahovat `.targets` a `.props` soubory, které jsou importovány do jakékoli projektu nástroje MSBuild, který je balíček nainstalován do.</span><span class="sxs-lookup"><span data-stu-id="f02ac-154">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="f02ac-155">V NuGet 2.x, k tomu bylo potřeba vložením `<Import>` příkazů do `.csproj` souboru, v NuGet 3.0 není k dispozici žádná konkrétní "instalace do projektu" akce.</span><span class="sxs-lookup"><span data-stu-id="f02ac-155">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="f02ac-156">Místo toho v procesu obnovení balíčku zapíše dva soubory `[projectname].nuget.props` a `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="f02ac-156">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="f02ac-157">MSBuild zná hledání tyto dva soubory a automaticky je importuje téměř začátku a konci procesu sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="f02ac-157">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="f02ac-158">To poskytuje velmi podobné chování NuGet 2.x, ale jeden hlavní rozdíl: *neexistuje žádné zaručenou pořadí cíle nebo props souborů v tomto případě*.</span><span class="sxs-lookup"><span data-stu-id="f02ac-158">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="f02ac-159">Však poskytuje způsoby, jak pořadí cíle prostřednictvím nástroje MSBuild `BeforeTargets` a `AfterTargets` atributy `<Target>` definice (najdete v části [Target – Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="f02ac-159">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="f02ac-160">LIB a Ref</span><span class="sxs-lookup"><span data-stu-id="f02ac-160">Lib and Ref</span></span>

<span data-ttu-id="f02ac-161">Chování `lib` složky významně nezměnilo ve NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="f02ac-161">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="f02ac-162">Musí být v rámci dílčí složky s názvem po TxM však ve všech sestaveních a už může být umístěno přímo ve `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="f02ac-162">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="f02ac-163">TxM je název platformu, která by měla fungovat pro daný prostředek v balíčku.</span><span class="sxs-lookup"><span data-stu-id="f02ac-163">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="f02ac-164">Logicky Toto jsou rozšíření z Monikery cílový Framework (TFM), například `net45`, `net46`, `netcore50`, a `dnxcore50` jsou všechny příklady TxMs (najdete v části [cílové rozhraní](../Schema/Target-Frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="f02ac-164">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../Schema/Target-Frameworks.md).</span></span> <span data-ttu-id="f02ac-165">TxM mohou odkazovat na rozhraní (TFM) a také další oblasti povrchu specifické pro platformu.</span><span class="sxs-lookup"><span data-stu-id="f02ac-165">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="f02ac-166">Například TxM UWP (`uap10.0`) představuje možnosti útoku na rozhraní .NET, jakož i prostor oblasti systému Windows pro aplikace UWP.</span><span class="sxs-lookup"><span data-stu-id="f02ac-166">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="f02ac-167">Příklad lib struktury:</span><span class="sxs-lookup"><span data-stu-id="f02ac-167">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="f02ac-168">`lib` Složka obsahuje sestavení, které se používají v době běhu.</span><span class="sxs-lookup"><span data-stu-id="f02ac-168">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="f02ac-169">Pro většinu balíčky složku ve složce `lib` pro každý cíl TxMs je všechno, co je vyžadován.</span><span class="sxs-lookup"><span data-stu-id="f02ac-169">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="f02ac-170">REF</span><span class="sxs-lookup"><span data-stu-id="f02ac-170">Ref</span></span>

<span data-ttu-id="f02ac-171">Jsou někdy případech, kdy by měla být použita jiném sestavení při kompilaci (referenční sestavení .NET do této dnes).</span><span class="sxs-lookup"><span data-stu-id="f02ac-171">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="f02ac-172">Pro případy, použijte složku nejvyšší úrovně s názvem `ref` (zkratka pro "referenční sestavení").</span><span class="sxs-lookup"><span data-stu-id="f02ac-172">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="f02ac-173">Většina autoři balíček nevyžadují `ref` složky.</span><span class="sxs-lookup"><span data-stu-id="f02ac-173">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="f02ac-174">Je vhodné pro balíčky, které potřebují k zajištění konzistentní útoku pro kompilaci a technologii IntelliSense, ale pak mít jinou implementaci pro různé TxMs.</span><span class="sxs-lookup"><span data-stu-id="f02ac-174">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="f02ac-175">Největších případ použití tyto `System.*` balíčky, které vznikají jako součást přenosů .NET Core na NuGet.</span><span class="sxs-lookup"><span data-stu-id="f02ac-175">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="f02ac-176">Tyto balíčky mají různé implementace, které jsou právě unified konzistentní sada ref sestavení.</span><span class="sxs-lookup"><span data-stu-id="f02ac-176">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="f02ac-177">Mechanicky sestavení součástí `ref` složky jsou předávány kompilátoru referenční sestavení.</span><span class="sxs-lookup"><span data-stu-id="f02ac-177">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="f02ac-178">Pro ty z vás, kteří použili csc.exe Toto jsou sestavení jsme jsou předány [možnost/reference jazyka C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) přepínače.</span><span class="sxs-lookup"><span data-stu-id="f02ac-178">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="f02ac-179">Struktura `ref` složky je stejný jako `lib`, například:</span><span class="sxs-lookup"><span data-stu-id="f02ac-179">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

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

<span data-ttu-id="f02ac-180">V tomto příkladu sestavení v `ref` adresáře by být identické.</span><span class="sxs-lookup"><span data-stu-id="f02ac-180">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="f02ac-181">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="f02ac-181">Runtimes</span></span>

<span data-ttu-id="f02ac-182">Moduly runtime složka obsahuje sestavení a nativní knihovny potřebné ke spuštění na konkrétní "moduly runtime", které jsou obvykle definovány Architektura operačního systému a procesoru.</span><span class="sxs-lookup"><span data-stu-id="f02ac-182">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="f02ac-183">Tyto moduly runtime jsou identifikovány pomocí [Runtime identifikátorů (RID)](/dotnet/core/rid-catalog) například `win`, `win-x86`, `win7-x86`, `win8-64`atd.</span><span class="sxs-lookup"><span data-stu-id="f02ac-183">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-light-up"></a><span data-ttu-id="f02ac-184">Nativní lehký up</span><span class="sxs-lookup"><span data-stu-id="f02ac-184">Native light-up</span></span>

<span data-ttu-id="f02ac-185">Následující příklad ukazuje balíček, který má čistě spravované implementace pro několik platforem, ale používá nativní Pomocné rutiny v systému Windows 8, kde můžete volání do nativního rozhraní API systému Windows 8 specifické.</span><span class="sxs-lookup"><span data-stu-id="f02ac-185">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

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

<span data-ttu-id="f02ac-186">Daný balíček výše provedou následující akce:</span><span class="sxs-lookup"><span data-stu-id="f02ac-186">Given the above package the following things happen:</span></span>

- <span data-ttu-id="f02ac-187">Pokud není v systému Windows 8 `lib/net40/MyLibrary.dll` sestavení používá.</span><span class="sxs-lookup"><span data-stu-id="f02ac-187">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="f02ac-188">Když v systému Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` se používá a `native/MyNativeHelper.dll` se zkopíruje na výstup buildu.</span><span class="sxs-lookup"><span data-stu-id="f02ac-188">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="f02ac-189">V příkladu nahoře `lib/net40` sestavení je čistě spravovaného kódu, zatímco sestavení ve složce moduly runtime bude p/invoke do sestavení nativní pomocná k volání rozhraní API specifická pro Windows 8.</span><span class="sxs-lookup"><span data-stu-id="f02ac-189">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="f02ac-190">Jediným `lib` složky je někdy být zachyceny, takže pokud je konkrétní složce runtime je zvolen přes konkrétní – modul runtime `lib`.</span><span class="sxs-lookup"><span data-stu-id="f02ac-190">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="f02ac-191">Nativní složka je aditivní, pokud existuje ho zkopíruje do výstupu sestavení.</span><span class="sxs-lookup"><span data-stu-id="f02ac-191">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="f02ac-192">Spravovaná obálka</span><span class="sxs-lookup"><span data-stu-id="f02ac-192">Managed wrapper</span></span>

<span data-ttu-id="f02ac-193">Pro odeslání balíčku, který je plně spravovaná obálka přes nativní sestavení je další způsob použití moduly runtime.</span><span class="sxs-lookup"><span data-stu-id="f02ac-193">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="f02ac-194">V tomto scénáři vytvoříte balíček, podobně jako tento:</span><span class="sxs-lookup"><span data-stu-id="f02ac-194">In this scenario you create a package like the following:</span></span>

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

<span data-ttu-id="f02ac-195">V takovém případě není žádná nejvyšší úrovně `lib` žádné implementace tohoto balíčku, který není závislý na odpovídající nativní sestavení je složka jako tuto složku jako zde.</span><span class="sxs-lookup"><span data-stu-id="f02ac-195">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="f02ac-196">Pokud spravované sestavení `MyLibrary.dll`, se přesně stejná v obou případech pak jsme může pro něj nejvyšší úrovni `lib` složky, ale protože nedostatečná nativní sestavení nemá způsobit, že balíček k selhání instalace, pokud byla nainstalovaná na platformě, pak se použije lib nejvyšší úrovně, ale žádné nativní sestavení by zkopírují nebyl win-x86 nebo win-x64.</span><span class="sxs-lookup"><span data-stu-id="f02ac-196">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="f02ac-197">Vytváření balíčků NuGet 2 a NuGet 3</span><span class="sxs-lookup"><span data-stu-id="f02ac-197">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="f02ac-198">Pokud chcete vytvořit balíček, který mohou být spotřebovávána projektů pomocí `packages.config` také jako balíčky pomocí `project.json` pak následujících podmínek:</span><span class="sxs-lookup"><span data-stu-id="f02ac-198">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="f02ac-199">REF a moduly runtime fungovat jenom na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="f02ac-199">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="f02ac-200">Obě jsou ignorovány NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="f02ac-200">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="f02ac-201">Nelze spoléhat na `install.ps1` nebo `uninstall.ps1` funkce.</span><span class="sxs-lookup"><span data-stu-id="f02ac-201">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="f02ac-202">Tyto soubory provést při použití `packages.config`, ale jsou ignorovány s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="f02ac-202">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="f02ac-203">Takže vašeho balíčku musí být možné bez je spuštěná.</span><span class="sxs-lookup"><span data-stu-id="f02ac-203">So your package needs to be usable without them running.</span></span> <span data-ttu-id="f02ac-204">`init.ps1`stále běží na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="f02ac-204">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="f02ac-205">Cíle a Props instalace je jiné, proto se ujistěte, že váš balíček funguje podle očekávání na obou klientských počítačích.</span><span class="sxs-lookup"><span data-stu-id="f02ac-205">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="f02ac-206">Podadresáře lib musí být TxM v NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="f02ac-206">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="f02ac-207">Knihovny nelze umístit na nejnižší úrovni `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="f02ac-207">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="f02ac-208">Obsah není automaticky zkopíruje s NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="f02ac-208">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="f02ac-209">Příjemci vašeho balíčku může kopírovat soubory sami nebo pomocí některého nástroje, například Spouštěče úloh k automatizaci kopírování souborů.</span><span class="sxs-lookup"><span data-stu-id="f02ac-209">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="f02ac-210">Zdroj a konfiguračním souboru transformace se nespustí 3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="f02ac-210">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="f02ac-211">Pokud podporujete NuGet 2 a 3 a vaše `minClientVersion` by měla být nejnižší verzi klienta NuGet 2, který na funguje vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="f02ac-211">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="f02ac-212">V případě existující balíček není vhodné měnit.</span><span class="sxs-lookup"><span data-stu-id="f02ac-212">In the case of an existing package it shouldn't need to change.</span></span>