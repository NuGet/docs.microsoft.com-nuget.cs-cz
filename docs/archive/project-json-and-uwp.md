---
title: Soubor project.json NuGet s projekty UPW
description: Popis, jak soubor project.json slouží ke sledování závislostí NuGet v projektech univerzální platformy Windows (UPW).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548661"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="20594-103">Project.JSON a UPW</span><span class="sxs-lookup"><span data-stu-id="20594-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="20594-104">Tento obsah je zastaralý.</span><span class="sxs-lookup"><span data-stu-id="20594-104">This content is deprecated.</span></span> <span data-ttu-id="20594-105">Projekty by měl použít buď `packages.config` nebo PackageReference formátů.</span><span class="sxs-lookup"><span data-stu-id="20594-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="20594-106">Tento dokument popisuje strukturu balíček, který využívá funkce ve Správci NuGet 3 + (Visual Studio 2015 a novější).</span><span class="sxs-lookup"><span data-stu-id="20594-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="20594-107">`minClientVersion` Vlastnictví vaší `.nuspec` je možné stanovit, zda vyžadujete funkce popsané tady nastavením na 3.1.</span><span class="sxs-lookup"><span data-stu-id="20594-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="20594-108">Přidání podpory pro UPW do existujícího balíčku</span><span class="sxs-lookup"><span data-stu-id="20594-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="20594-109">Pokud máte existující balíček a chcete přidat podporu pro aplikace UPW, pak není nutné přijmout balení formátu popsaném tady.</span><span class="sxs-lookup"><span data-stu-id="20594-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="20594-110">Stačí přijmout tento formát, pokud vyžadujete funkce popisuje a jste ochotni pracovat pouze s klienty, kteří mají aktualizována na verzi 3 + klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="20594-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="20594-111">Už mám cílit netcore45</span><span class="sxs-lookup"><span data-stu-id="20594-111">I already target netcore45</span></span>

<span data-ttu-id="20594-112">Pokud je cílem `netcore45` již a nemusíte využít výhod funkce tady, není vyžadována žádná akce.</span><span class="sxs-lookup"><span data-stu-id="20594-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="20594-113">`netcore45` balíčky mohou být spotřebovány aplikacemi UWP.</span><span class="sxs-lookup"><span data-stu-id="20594-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="20594-114">Budu chtít využívat výhod určitých rozhraní API Windows 10</span><span class="sxs-lookup"><span data-stu-id="20594-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="20594-115">V tomto případě budete muset přidat `uap10.0` cílit na moniker rozhraní (TFM nebo TxM) do balíčku.</span><span class="sxs-lookup"><span data-stu-id="20594-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="20594-116">Vytvoření nové složky v balíčku a přidejte sestavení, která byla zkompilována pro práci s Windows 10 do této složky.</span><span class="sxs-lookup"><span data-stu-id="20594-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="20594-117">Nepotřebuji konkrétní rozhraní API Windows 10, ale má nové funkce rozhraní .NET nebo již nemáte netcore45</span><span class="sxs-lookup"><span data-stu-id="20594-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="20594-118">V tomto případě přidáte `dotnet` TxM do vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="20594-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="20594-119">Na rozdíl od jiných TxMs `dotnet` není určeno styčné plochy nebo platformu.</span><span class="sxs-lookup"><span data-stu-id="20594-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="20594-120">Je s informacemi o tom, které váš balíček funguje na libovolné platformě, která závislostí pracovat.</span><span class="sxs-lookup"><span data-stu-id="20594-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="20594-121">Při vytváření balíčku s `dotnet` TxM, budete pravděpodobně mají mnoho další TxM specifické závislosti vašich `.nuspec`, jako je třeba definovat závisí na tyto balíčky BCL `System.Text`, `System.Xml`atd. Umístění, které tyto závislosti fungují na definovat, pracuje, jak váš balíček.</span><span class="sxs-lookup"><span data-stu-id="20594-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="20594-122">Jak zjistím volání závislostí</span><span class="sxs-lookup"><span data-stu-id="20594-122">How do I find out my dependencies</span></span>

<span data-ttu-id="20594-123">Existují dva způsoby, jak zjistit, jaké závislosti na seznamu:</span><span class="sxs-lookup"><span data-stu-id="20594-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="20594-124">Použití [generátor závislostí souboru NuSpec](https://github.com/onovotny/ReferenceGenerator) **3. stran** nástroj.</span><span class="sxs-lookup"><span data-stu-id="20594-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="20594-125">Nástroj automatizuje proces a aktualizace vašich `.nuspec` soubor se závislé balíčky v sestavení.</span><span class="sxs-lookup"><span data-stu-id="20594-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="20594-126">Je k dispozici prostřednictvím balíčku NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="20594-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="20594-127">(Přiznejme) Použití `ILDasm` podívat se na vaše `.dll` zobrazíte, jaké sestavení jsou skutečně potřeba za běhu.</span><span class="sxs-lookup"><span data-stu-id="20594-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="20594-128">Pak zjistěte balíčky NuGet, které každá pocházejí.</span><span class="sxs-lookup"><span data-stu-id="20594-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="20594-129">Zobrazit [ `project.json` ](project-json.md) tématu informace o funkcích, které pomáhají při vytváření balíčku, který podporuje `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="20594-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="20594-130">Pokud váš balíček je určená pro práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složky, aby se zabránilo upozornění a potenciální problémy s kompatibilitou.</span><span class="sxs-lookup"><span data-stu-id="20594-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="20594-131">Adresářová struktura</span><span class="sxs-lookup"><span data-stu-id="20594-131">Directory structure</span></span>

<span data-ttu-id="20594-132">Balíčky NuGet pomocí tohoto formátu mají následující dobře známou složku a chování:</span><span class="sxs-lookup"><span data-stu-id="20594-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="20594-133">Folder</span><span class="sxs-lookup"><span data-stu-id="20594-133">Folder</span></span> | <span data-ttu-id="20594-134">Chování</span><span class="sxs-lookup"><span data-stu-id="20594-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="20594-135">Sestavení</span><span class="sxs-lookup"><span data-stu-id="20594-135">Build</span></span> | <span data-ttu-id="20594-136">Obsahuje nástroje MSBuild cíle a soubory vlastností v této složce jsou jinak integrované do projektu, ale jinak není žádná změna.</span><span class="sxs-lookup"><span data-stu-id="20594-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="20594-137">Nástroje</span><span class="sxs-lookup"><span data-stu-id="20594-137">Tools</span></span> | <span data-ttu-id="20594-138">`install.ps1` a `uninstall.ps1` se nespustí.</span><span class="sxs-lookup"><span data-stu-id="20594-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="20594-139">`init.ps1` funguje jako má vždy.</span><span class="sxs-lookup"><span data-stu-id="20594-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="20594-140">Obsah</span><span class="sxs-lookup"><span data-stu-id="20594-140">Content</span></span> | <span data-ttu-id="20594-141">Obsah není automaticky zkopíruje do projektu uživatele.</span><span class="sxs-lookup"><span data-stu-id="20594-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="20594-142">Podpora pro zařazení obsahu v projektu je naplánovaná pro novější verzi.</span><span class="sxs-lookup"><span data-stu-id="20594-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="20594-143">lib</span><span class="sxs-lookup"><span data-stu-id="20594-143">Lib</span></span> | <span data-ttu-id="20594-144">Pro mnoho balíčků `lib` funguje stejně v NuGet 2.x, ale rozšířené možnosti, které názvů může být použit uvnitř ho a lépe logiku pro výběr správné dílčí složky při využívání balíčků.</span><span class="sxs-lookup"><span data-stu-id="20594-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="20594-145">Ale při použití ve spojení s `ref`, `lib` složka obsahuje sestavení, které implementují styčné plochy definované v sestavení `ref` složky.</span><span class="sxs-lookup"><span data-stu-id="20594-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="20594-146">REF</span><span class="sxs-lookup"><span data-stu-id="20594-146">Ref</span></span> | <span data-ttu-id="20594-147">`ref` je volitelný složku, která obsahuje sestavení .NET definování veřejného surface (veřejné typy a metody) pro aplikaci kompilovat proti.</span><span class="sxs-lookup"><span data-stu-id="20594-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="20594-148">Sestavení v této složce mohou nemají implementaci, čistě se používají k definování povrchu pro kompilátor.</span><span class="sxs-lookup"><span data-stu-id="20594-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="20594-149">Pokud balíček nemá žádné `ref` složku, pak bude `lib` se referenční sestavení a sestavení implementace.</span><span class="sxs-lookup"><span data-stu-id="20594-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="20594-150">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="20594-150">Runtimes</span></span> | <span data-ttu-id="20594-151">`runtimes` je volitelný složku, která obsahuje určitý kód operačního systému, jako je architektura procesoru a konkrétního nebo jinak závislého na platformě binární soubory.</span><span class="sxs-lookup"><span data-stu-id="20594-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="20594-152">Nástroj MSBuild cíle a soubory vlastností v balíčcích</span><span class="sxs-lookup"><span data-stu-id="20594-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="20594-153">Může obsahovat balíčky NuGet `.targets` a `.props` soubory, které jsou importovány do jakékoli projektu nástroje MSBuild, který je nainstalován balíček do.</span><span class="sxs-lookup"><span data-stu-id="20594-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="20594-154">Ve Správci NuGet 2.x, to se provádí vkládání `<Import>` příkazy do `.csproj` souboru, ale NuGet 3.0 není nic konkrétní "instalace do projektu".</span><span class="sxs-lookup"><span data-stu-id="20594-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="20594-155">Místo toho proces obnovení balíčku zapíše dva soubory `[projectname].nuget.props` a `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="20594-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="20594-156">Nástroj MSBuild ví těchto dvou souborů a automaticky importuje poblíž začátku a na konci procesu sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="20594-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="20594-157">To poskytuje velmi podobné chování NuGet 2.x, ale s jedním z hlavních rozdílů: *není zaručeno pořadí cíle/props soubory v tomto případě*.</span><span class="sxs-lookup"><span data-stu-id="20594-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="20594-158">Nástroj MSBuild poskytuje však způsoby, jak pořadí cíle prostřednictvím `BeforeTargets` a `AfterTargets` atributy `<Target>` definice (naleznete v tématu [Target – Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="20594-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="20594-159">LIB a Ref</span><span class="sxs-lookup"><span data-stu-id="20594-159">Lib and Ref</span></span>

<span data-ttu-id="20594-160">Chování `lib` složky významně nezměnila ve verzi 3 NuGet.</span><span class="sxs-lookup"><span data-stu-id="20594-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="20594-161">Však musí spadat do podsložky s názvem po TxM všechna sestavení a můžete už umístit přímo pod `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="20594-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="20594-162">TxM je název platformy, která daný prostředek v balíčku by měla fungovat.</span><span class="sxs-lookup"><span data-stu-id="20594-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="20594-163">Logicky Toto jsou rozšíření cílové rozhraní Framework Monikery (TFM), třeba `net45`, `net46`, `netcore50`, a `dnxcore50` jsou všechny příklady TxMs (naleznete v tématu [cílové architektury](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="20594-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="20594-164">TxM mohou odkazovat na rozhraní (TFM) a také další specifické pro platformu plochy.</span><span class="sxs-lookup"><span data-stu-id="20594-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="20594-165">Například TxM UPW (`uap10.0`) představuje útoku na rozhraní .NET, jakož i plochy Windows pro aplikace UPW.</span><span class="sxs-lookup"><span data-stu-id="20594-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="20594-166">Příklad lib struktury:</span><span class="sxs-lookup"><span data-stu-id="20594-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="20594-167">`lib` Složka obsahuje sestavení, které se používají v době běhu.</span><span class="sxs-lookup"><span data-stu-id="20594-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="20594-168">Pro většinu balíčků složku ve složce `lib` pro každý cíl TxMs je vše, co je povinný.</span><span class="sxs-lookup"><span data-stu-id="20594-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="20594-169">REF</span><span class="sxs-lookup"><span data-stu-id="20594-169">Ref</span></span>

<span data-ttu-id="20594-170">Někdy existují případy, kdy jiné sestavení by měla sloužit během kompilace (odkaz na sestavení .NET do této dnes).</span><span class="sxs-lookup"><span data-stu-id="20594-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="20594-171">Pro tyto případy použijte složku nejvyšší úrovně s názvem `ref` (zkratka "odkaz na sestavení").</span><span class="sxs-lookup"><span data-stu-id="20594-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="20594-172">Většina autory balíčku nevyžadují `ref` složky.</span><span class="sxs-lookup"><span data-stu-id="20594-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="20594-173">To je užitečné pro balíčky, které je potřeba poskytnout konzistentní styčné plochy pro kompilaci a technologie IntelliSense, ale pak je mít jinou implementaci pro různé TxMs.</span><span class="sxs-lookup"><span data-stu-id="20594-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="20594-174">Největší případ použití jsou `System.*` balíčky, které jsou vytvořených jako součást přenosů .NET Core na webu NuGet.</span><span class="sxs-lookup"><span data-stu-id="20594-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="20594-175">Tyto balíčky obsahují různé implementace, které jsou právě sjednocené konzistentní sada referenční sestavení.</span><span class="sxs-lookup"><span data-stu-id="20594-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="20594-176">Mechanicky, sestavení součástí `ref` složky jsou referenční sestavení, jsou předány kompilátoru.</span><span class="sxs-lookup"><span data-stu-id="20594-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="20594-177">Pro ty z vás, kteří použili csc.exe jde o sestavení jsme jsou předány [možnosti/reference jazyka C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) přepnout.</span><span class="sxs-lookup"><span data-stu-id="20594-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="20594-178">Struktura `ref` složka je stejná jako `lib`, například:</span><span class="sxs-lookup"><span data-stu-id="20594-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

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

<span data-ttu-id="20594-179">V tomto příkladu sestavení v `ref` adresáře by být identické.</span><span class="sxs-lookup"><span data-stu-id="20594-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="20594-180">Moduly runtime</span><span class="sxs-lookup"><span data-stu-id="20594-180">Runtimes</span></span>

<span data-ttu-id="20594-181">Složka moduly runtime obsahuje sestavení a nativních knihoven, které jsou potřeba ke spouštění na konkrétní "moduly runtime", které jsou obvykle definovány pomocí Architektura operačního systému a procesoru.</span><span class="sxs-lookup"><span data-stu-id="20594-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="20594-182">Tyto moduly runtime jsou označeny pomocí [Runtime identifikátorů (RID)](/dotnet/core/rid-catalog) například `win`, `win-x86`, `win7-x86`, `win8-64`atd.</span><span class="sxs-lookup"><span data-stu-id="20594-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="20594-183">Nativní Pomocné rutiny používat rozhraní API pro konkrétní platformu</span><span class="sxs-lookup"><span data-stu-id="20594-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="20594-184">Následující příklad ukazuje balíček, který má plně spravovanou implementaci pro několik platforem, ale používá nativní Pomocné rutiny ve Windows 8, ve kterém může volat do systému Windows 8 specifických nativních rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="20594-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

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

<span data-ttu-id="20594-185">Zadaný balíček výše následující situace:</span><span class="sxs-lookup"><span data-stu-id="20594-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="20594-186">Pokud není v systému Windows 8 `lib/net40/MyLibrary.dll` sestavení používá.</span><span class="sxs-lookup"><span data-stu-id="20594-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="20594-187">Pokud je na Windows 8 `runtimes/win8-<architecture>/lib/MyLibrary.dll` se používá a `native/MyNativeHelper.dll` je zkopírován do výstupního sestavení.</span><span class="sxs-lookup"><span data-stu-id="20594-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="20594-188">Ve výše uvedeném příkladu `lib/net40` sestavení je čistě spravovaném kódu, zatímco sestavení ve složce modulů runtime bude nespravovaného kódu do nativních pomocné rutiny sestavení pro volání rozhraní API specifická pro systém Windows 8.</span><span class="sxs-lookup"><span data-stu-id="20594-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="20594-189">Pouze jeden `lib` složky je někdy má vybrat, takže pokud je konkrétní složka modulu runtime je vybrán přes konkrétní – modul runtime `lib`.</span><span class="sxs-lookup"><span data-stu-id="20594-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="20594-190">Nativní složka je additive, pokud existuje, je zkopírován do výstupního sestavení.</span><span class="sxs-lookup"><span data-stu-id="20594-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="20594-191">Spravovaná obálka</span><span class="sxs-lookup"><span data-stu-id="20594-191">Managed wrapper</span></span>

<span data-ttu-id="20594-192">Dalším způsobem, jak používat moduly runtime je k odeslání balíčku, který je čistě spravovaná obálka nad nativní sestavení.</span><span class="sxs-lookup"><span data-stu-id="20594-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="20594-193">V tomto scénáři vytvoříte balíček vypadat asi takto:</span><span class="sxs-lookup"><span data-stu-id="20594-193">In this scenario you create a package like the following:</span></span>

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

<span data-ttu-id="20594-194">V tomto případě není již nejvyšší úrovně `lib` implementaci tohoto balíčku, který se nemusí spoléhat na odpovídající nativní sestavení je složka jako této složky, protože došlo.</span><span class="sxs-lookup"><span data-stu-id="20594-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="20594-195">Pokud spravované sestavení `MyLibrary.dll`, byla přesně stejné v obou těchto případech potom jsme mohli uvolnit ji v nejvyšší úrovni `lib` složky, ale protože chybějící nativní sestavení nezpůsobí balíček k selhání instalace, pokud byla nainstalovaná na platformě, která nebyl win-x86 nebo win-x64 pak by se použily lib nejvyšší úrovně, ale má být zkopírováno žádné nativní sestavení.</span><span class="sxs-lookup"><span data-stu-id="20594-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="20594-196">Vytváření balíčků pro NuGet 2 a NuGet 3</span><span class="sxs-lookup"><span data-stu-id="20594-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="20594-197">Pokud chcete vytvořit balíček, který mohou být spotřebovány projektů s použitím `packages.config` stejně jako balíčky pomocí `project.json` následujících podmínek:</span><span class="sxs-lookup"><span data-stu-id="20594-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="20594-198">REF a moduly runtime funguje jenom u NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="20594-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="20594-199">Obě jsou ignorovány NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="20594-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="20594-200">Nelze spoléhat na `install.ps1` nebo `uninstall.ps1` funkce.</span><span class="sxs-lookup"><span data-stu-id="20594-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="20594-201">Tyto soubory provést při použití `packages.config`, ale jsou ignorovány s `project.json`.</span><span class="sxs-lookup"><span data-stu-id="20594-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="20594-202">Aby váš balíček musí být možné bez jejich spuštění.</span><span class="sxs-lookup"><span data-stu-id="20594-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="20594-203">`init.ps1` sice dál běží na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="20594-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="20594-204">Cíle a vlastnosti instalace se liší, proto se ujistěte, že váš balíček funguje podle očekávání na obou klientských počítačích.</span><span class="sxs-lookup"><span data-stu-id="20594-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="20594-205">Podadresáře lib musí být TxM NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="20594-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="20594-206">Knihovny nelze umístit v kořenovém adresáři `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="20594-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="20594-207">Obsah není zkopírován automaticky s NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="20594-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="20594-208">Příjemci balíčku může kopírovat soubory sami nebo použít nástroje, jako je Spouštěč úloh k automatizaci kopírování souborů.</span><span class="sxs-lookup"><span data-stu-id="20594-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="20594-209">Transformace zdrojových a konfiguračních souborů nejsou spustit NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="20594-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="20594-210">Pokud podporujete NuGet 2 a 3 vaše `minClientVersion` by měla mít nejnižší verzi klienta NuGet 2, který váš balíček funguje na.</span><span class="sxs-lookup"><span data-stu-id="20594-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="20594-211">V případě existující balíček ho nebylo potřeba měnit.</span><span class="sxs-lookup"><span data-stu-id="20594-211">In the case of an existing package it shouldn't need to change.</span></span>
