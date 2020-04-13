---
title: Soubor NuGet project.json s projekty UPW
description: Popis způsobu, jakým se soubor project.json používá ke sledování závislostí NuGet v projektech univerzální platformy Windows (UPW).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494378"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="ea053-103">project.json a UPW</span><span class="sxs-lookup"><span data-stu-id="ea053-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="ea053-104">Tento obsah je zastaralé.</span><span class="sxs-lookup"><span data-stu-id="ea053-104">This content is deprecated.</span></span> <span data-ttu-id="ea053-105">Projekty by `packages.config` měly používat formáty nebo PackageReference.</span><span class="sxs-lookup"><span data-stu-id="ea053-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="ea053-106">Tento dokument popisuje strukturu balíčku, která využívá funkce v NuGet 3 + (Visual Studio 2015 a novější).</span><span class="sxs-lookup"><span data-stu-id="ea053-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="ea053-107">Vlastnost `minClientVersion` vašeho `.nuspec` můžete uvést, že budete potřebovat funkce popsané zde nastavením na 3.1.</span><span class="sxs-lookup"><span data-stu-id="ea053-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="ea053-108">Přidání podpory UPW do existujícího balíčku</span><span class="sxs-lookup"><span data-stu-id="ea053-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="ea053-109">Pokud máte existující balíček a chcete přidat podporu pro aplikace UPW, pak nemusíte přijmout formát balení popsané zde.</span><span class="sxs-lookup"><span data-stu-id="ea053-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="ea053-110">Tento formát je třeba přijmout pouze v případě, že potřebujete funkce, které popisuje a jsou ochotni pracovat pouze s klienty, které byly aktualizovány na verzi 3 + klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="ea053-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="ea053-111">Už jsem cíl netcore45</span><span class="sxs-lookup"><span data-stu-id="ea053-111">I already target netcore45</span></span>

<span data-ttu-id="ea053-112">Pokud již `netcore45` cílíte a nemusíte využívat funkce zde, není nutná žádná akce.</span><span class="sxs-lookup"><span data-stu-id="ea053-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="ea053-113">`netcore45`balíčky mohou být spotřebovány aplikacemi UPW.</span><span class="sxs-lookup"><span data-stu-id="ea053-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="ea053-114">Chci využít výhod specifických api windows 10</span><span class="sxs-lookup"><span data-stu-id="ea053-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="ea053-115">V takovém případě je `uap10.0` třeba přidat zástupný název cílové ho rozhraní (TFM nebo TxM) do balíčku.</span><span class="sxs-lookup"><span data-stu-id="ea053-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="ea053-116">Vytvořte novou složku v balíčku a přidejte sestavení, které bylo zkompilováno pro práci s Windows 10 do této složky.</span><span class="sxs-lookup"><span data-stu-id="ea053-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="ea053-117">Nepotřebuji windows 10 konkrétní rozhraní API, ale chcete nové .NET funkce nebo nemají netcore45 již</span><span class="sxs-lookup"><span data-stu-id="ea053-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="ea053-118">V takovém případě byste `dotnet` do balíčku přidali TxM.</span><span class="sxs-lookup"><span data-stu-id="ea053-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="ea053-119">Na rozdíl od jiných `dotnet` TxMs, neznamená plochu nebo platformu.</span><span class="sxs-lookup"><span data-stu-id="ea053-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="ea053-120">Uvádí, že váš balíček funguje na libovolné platformě, na které pracují vaše závislosti.</span><span class="sxs-lookup"><span data-stu-id="ea053-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="ea053-121">Při vytváření balíčku `dotnet` s TxM, budete pravděpodobně mít mnohem více TxM `.nuspec`specifické závislosti ve vašem , jak je `System.Text`třeba `System.Xml`definovat Balíčky BCL, na kterých jste závislí, jako , , atd. Umístění, která tyto závislosti pracují na definovat, kde váš balíček funguje.</span><span class="sxs-lookup"><span data-stu-id="ea053-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="ea053-122">Jak zjistím své závislosti</span><span class="sxs-lookup"><span data-stu-id="ea053-122">How do I find out my dependencies</span></span>

<span data-ttu-id="ea053-123">Existují dva způsoby, jak zjistit, které závislosti chcete uvést:</span><span class="sxs-lookup"><span data-stu-id="ea053-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="ea053-124">Použijte nástroj [NuSpec Dependency Generator třetí strany.](https://github.com/onovotny/ReferenceGenerator) **3rd party**</span><span class="sxs-lookup"><span data-stu-id="ea053-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="ea053-125">Nástroj automatizuje proces a `.nuspec` aktualizuje soubor s závislé balíčky na sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea053-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="ea053-126">Je k dispozici prostřednictvím balíčku NuGet, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="ea053-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="ea053-127">(Tvrdá cesta) Pomocí `ILDasm` zobrazení na `.dll` vaše zobrazíte, jaké sestavení jsou skutečně potřeba za běhu.</span><span class="sxs-lookup"><span data-stu-id="ea053-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="ea053-128">Pak určete, ze kterého balíčku NuGet pocházejí.</span><span class="sxs-lookup"><span data-stu-id="ea053-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="ea053-129">[`project.json`](project-json.md) Podrobnosti o funkcích, které pomáhají při vytváření balíčku, který podporuje TxM, najdete v tématu. `dotnet`</span><span class="sxs-lookup"><span data-stu-id="ea053-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="ea053-130">Pokud je váš balíček určen pro práci s projekty PCL, důrazně doporučujeme vytvořit `dotnet` složku, aby se zabránilo upozornění a potenciální problémy s kompatibilitou.</span><span class="sxs-lookup"><span data-stu-id="ea053-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="ea053-131">Adresářová struktura</span><span class="sxs-lookup"><span data-stu-id="ea053-131">Directory structure</span></span>

<span data-ttu-id="ea053-132">Balíčky NuGet používající tento formát mají následující dobře známou složku a chování:</span><span class="sxs-lookup"><span data-stu-id="ea053-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="ea053-133">Složka</span><span class="sxs-lookup"><span data-stu-id="ea053-133">Folder</span></span> | <span data-ttu-id="ea053-134">Chování</span><span class="sxs-lookup"><span data-stu-id="ea053-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="ea053-135">Sestavení</span><span class="sxs-lookup"><span data-stu-id="ea053-135">Build</span></span> | <span data-ttu-id="ea053-136">Obsahuje MSBuild cíle a rekvizity soubory v této složce jsou integrovány odlišně do projektu, ale jinak neexistuje žádná změna.</span><span class="sxs-lookup"><span data-stu-id="ea053-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="ea053-137">nástroje</span><span class="sxs-lookup"><span data-stu-id="ea053-137">Tools</span></span> | <span data-ttu-id="ea053-138">`install.ps1`a `uninstall.ps1` nejsou spuštěny.</span><span class="sxs-lookup"><span data-stu-id="ea053-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="ea053-139">`init.ps1`funguje jako vždy.</span><span class="sxs-lookup"><span data-stu-id="ea053-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="ea053-140">Obsah</span><span class="sxs-lookup"><span data-stu-id="ea053-140">Content</span></span> | <span data-ttu-id="ea053-141">Obsah není automaticky zkopírován do projektu uživatele.</span><span class="sxs-lookup"><span data-stu-id="ea053-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="ea053-142">Podpora pro zahrnutí obsahu do projektu je plánována na pozdější vydání.</span><span class="sxs-lookup"><span data-stu-id="ea053-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="ea053-143">Lib</span><span class="sxs-lookup"><span data-stu-id="ea053-143">Lib</span></span> | <span data-ttu-id="ea053-144">Pro mnoho `lib` balíčků funguje stejným způsobem jako v NuGet 2.x, ale s rozšířenými možnostmi pro jaké názvy lze použít uvnitř a lepší logiku pro výběr správné podsložky při náročné balíčky.</span><span class="sxs-lookup"><span data-stu-id="ea053-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="ea053-145">Pokud je však `ref`složka `lib` použita ve spojení s , obsahuje sestavy, `ref` které implementují plochu vymezenou sestaveními ve složce.</span><span class="sxs-lookup"><span data-stu-id="ea053-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="ea053-146">Ref</span><span class="sxs-lookup"><span data-stu-id="ea053-146">Ref</span></span> | <span data-ttu-id="ea053-147">`ref`je volitelná složka, která obsahuje sestavení rozhraní .NET definující veřejný povrch (veřejné typy a metody) pro kompilování aplikace.</span><span class="sxs-lookup"><span data-stu-id="ea053-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="ea053-148">Sestavení v této složce může mít žádnou implementaci, jsou použity výhradně k definování plochy pro kompilátor.</span><span class="sxs-lookup"><span data-stu-id="ea053-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="ea053-149">Pokud balíček `ref` nemá žádnou `lib` složku, pak je sestavení odkazu a sestavení implementace.</span><span class="sxs-lookup"><span data-stu-id="ea053-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="ea053-150">Runtime</span><span class="sxs-lookup"><span data-stu-id="ea053-150">Runtimes</span></span> | <span data-ttu-id="ea053-151">`runtimes`je volitelná složka, která obsahuje kód specifický pro operační režim, například architekturu procesoru a binární soubory specifické pro operační službu nebo jinak závislé na platformě.</span><span class="sxs-lookup"><span data-stu-id="ea053-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="ea053-152">MSBuild cíle a rekvizity soubory v balíčcích</span><span class="sxs-lookup"><span data-stu-id="ea053-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="ea053-153">Balíčky NuGet `.targets` `.props` mohou obsahovat a soubory, které jsou importovány do libovolného projektu MSBuild, do kterého je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="ea053-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="ea053-154">V NuGet 2.x to bylo `<Import>` provedeno vložením příkazy do souboru, `.csproj` v NuGet 3.0 neexistuje žádná konkrétní akce "instalace k projektu".</span><span class="sxs-lookup"><span data-stu-id="ea053-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="ea053-155">Místo toho proces obnovení `[projectname].nuget.props` balíčku `[projectname].NuGet.targets`zapíše dva soubory a .</span><span class="sxs-lookup"><span data-stu-id="ea053-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="ea053-156">MSBuild ví, že má hledat tyto dva soubory a automaticky je importuje v blízkosti začátku a na konci procesu sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="ea053-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="ea053-157">To poskytuje velmi podobné chování NuGet 2.x, ale s jedním velkým rozdílem: *neexistuje žádné zaručené pořadí cílů / rekvizity soubory v tomto případě*.</span><span class="sxs-lookup"><span data-stu-id="ea053-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="ea053-158">MSBuild však poskytuje způsoby, `BeforeTargets` jak `AfterTargets` objednat cíle `<Target>` prostřednictvím atributy a definice (viz [Cílový prvek (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="ea053-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="ea053-159">Lib a odkaz</span><span class="sxs-lookup"><span data-stu-id="ea053-159">Lib and Ref</span></span>

<span data-ttu-id="ea053-160">Chování `lib` složky se výrazně nezměnila v NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="ea053-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="ea053-161">Všechna sestavení však musí být v rámci podsložek pojmenovaný chrápl txm a již nemůže být umístěn přímo do `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="ea053-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="ea053-162">TxM je název platformy, pro kterou má daný prostředek v balíčku pracovat.</span><span class="sxs-lookup"><span data-stu-id="ea053-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="ea053-163">Logicky se jedná o rozšíření názvů názvů target frameworku (TFM), `net45`například , `net46` `netcore50`, a `dnxcore50` jsou všechny příklady TxM (viz Cílové [rámce](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ea053-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="ea053-164">TxM může odkazovat na rámec (TFM) stejně jako jiné plochy specifické pro platformu.</span><span class="sxs-lookup"><span data-stu-id="ea053-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="ea053-165">Například UWP TxM`uap10.0`( ) představuje plochu .NET, stejně jako plochu windows pro aplikace UPW.</span><span class="sxs-lookup"><span data-stu-id="ea053-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="ea053-166">Příklad lib struktura:</span><span class="sxs-lookup"><span data-stu-id="ea053-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="ea053-167">Složka `lib` obsahuje sestavení, která se používají za běhu.</span><span class="sxs-lookup"><span data-stu-id="ea053-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="ea053-168">Pro většinu balíčků `lib` je potřeba složka pod pro každý z cílových TxMs.</span><span class="sxs-lookup"><span data-stu-id="ea053-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="ea053-169">Ref</span><span class="sxs-lookup"><span data-stu-id="ea053-169">Ref</span></span>

<span data-ttu-id="ea053-170">Někdy existují případy, kdy by měl být použit jiný sestavení během kompilace (.NET reference sestavení to dnes).</span><span class="sxs-lookup"><span data-stu-id="ea053-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="ea053-171">V těchto případech použijte složku nejvyšší `ref` úrovně s názvem (zkratka pro "Referenční sestavení").</span><span class="sxs-lookup"><span data-stu-id="ea053-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="ea053-172">Většina autorů balíčků nepožaduje `ref` složku.</span><span class="sxs-lookup"><span data-stu-id="ea053-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="ea053-173">Je užitečné pro balíčky, které potřebují poskytnout konzistentní plochu pro kompilaci a IntelliSense, ale pak mají různé implementace pro různé TxMs.</span><span class="sxs-lookup"><span data-stu-id="ea053-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="ea053-174">Největší případ použití tohoto `System.*` jsou balíčky, které jsou vyráběny jako součást odesílání .NET Core na NuGet.</span><span class="sxs-lookup"><span data-stu-id="ea053-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="ea053-175">Tyto balíčky mají různé implementace, které jsou jednotné konzistentní sadu sestavení ref.</span><span class="sxs-lookup"><span data-stu-id="ea053-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="ea053-176">Mechanicky sestavení zahrnutá ve `ref` složce jsou referenční sestavení předávaná kompilátoru.</span><span class="sxs-lookup"><span data-stu-id="ea053-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="ea053-177">Pro ty z vás, kteří používají csc.exe to jsou sestavení jsme předávání [C# /reference přepínač možnosti.](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option)</span><span class="sxs-lookup"><span data-stu-id="ea053-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="ea053-178">Struktura `ref` složky je stejná `lib`jako například:</span><span class="sxs-lookup"><span data-stu-id="ea053-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

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

<span data-ttu-id="ea053-179">V tomto příkladu sestavení `ref` v adresářích by všechny identické.</span><span class="sxs-lookup"><span data-stu-id="ea053-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="ea053-180">Runtime</span><span class="sxs-lookup"><span data-stu-id="ea053-180">Runtimes</span></span>

<span data-ttu-id="ea053-181">Složka runtimes obsahuje sestavení a nativní knihovny potřebné ke spuštění na konkrétní "runtimes", které jsou obecně definovány architekturou operačního systému a procesoru.</span><span class="sxs-lookup"><span data-stu-id="ea053-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="ea053-182">Tyto runtime jsou identifikovány pomocí [identifikátorů runtime (ID),](/dotnet/core/rid-catalog) jako `win`jsou , `win-x86`, `win7-x86` `win8-64`, atd.</span><span class="sxs-lookup"><span data-stu-id="ea053-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="ea053-183">Nativní pomocníci pro použití api specifická pro platformu</span><span class="sxs-lookup"><span data-stu-id="ea053-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="ea053-184">Následující příklad ukazuje balíček, který má čistě spravovanou implementaci pro několik platforem, ale používá nativní pomocníky v systému Windows 8, kde může volat do nativních api pro Windows 8.</span><span class="sxs-lookup"><span data-stu-id="ea053-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

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

<span data-ttu-id="ea053-185">Vzhledem k výše uvedenému balíčku se dějí následující věci:</span><span class="sxs-lookup"><span data-stu-id="ea053-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="ea053-186">Pokud není v `lib/net40/MyLibrary.dll` systému Windows 8 sestavení se používá.</span><span class="sxs-lookup"><span data-stu-id="ea053-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="ea053-187">Když na Windows `runtimes/win8-<architecture>/lib/MyLibrary.dll` 8 se `native/MyNativeHelper.dll` používá a zkopíruje se do výstupu sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea053-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="ea053-188">Ve výše uvedeném příkladu `lib/net40` sestavení je čistě spravovaný kód, zatímco sestavení ve složce runtimes bude p/invoke do nativního pomocného sestavení volat api specifické pro Windows 8.</span><span class="sxs-lookup"><span data-stu-id="ea053-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="ea053-189">Je někdy `lib` vybrána pouze jedna složka, takže pokud existuje složka specifická pro běh `lib`za běhu, je vybrána přes nezaběhu .</span><span class="sxs-lookup"><span data-stu-id="ea053-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="ea053-190">Nativní složka je aditivní, pokud existuje, je zkopírována do výstupu sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea053-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="ea053-191">Spravovaný obálka</span><span class="sxs-lookup"><span data-stu-id="ea053-191">Managed wrapper</span></span>

<span data-ttu-id="ea053-192">Dalším způsobem použití runtimes je doložit balíček, který je čistě spravované obálky přes nativní sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea053-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="ea053-193">V tomto scénáři vytvoříte balíček, jako je následující:</span><span class="sxs-lookup"><span data-stu-id="ea053-193">In this scenario you create a package like the following:</span></span>

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

<span data-ttu-id="ea053-194">V tomto případě neexistuje žádná `lib` složka nejvyšší úrovně, protože neexistuje žádná implementace tohoto balíčku, který nespoléhá na odpovídající nativní sestavení.</span><span class="sxs-lookup"><span data-stu-id="ea053-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="ea053-195">Pokud spravované sestavení, , byl přesně stejný v obou těchto případech pak `lib` bychom mohli dát do složky nejvyšší úrovně, ale protože nedostatek nativní sestavení nezpůsobí balíček nezdaří instalaci, `MyLibrary.dll`pokud byl nainstalován na platformě, která nebyla win-x86 nebo win-x64 pak nejvyšší úroveň lib by být použity, ale žádné nativní sestavení by být zkopírovány.</span><span class="sxs-lookup"><span data-stu-id="ea053-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="ea053-196">Vytváření balíčků pro NuGet 2 a NuGet 3</span><span class="sxs-lookup"><span data-stu-id="ea053-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="ea053-197">Pokud chcete vytvořit balíček, který může `packages.config` být spotřebován projekty pomocí, stejně jako balíčky pomocí `project.json` pak platí následující:</span><span class="sxs-lookup"><span data-stu-id="ea053-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="ea053-198">Ref a runtimes pracovat pouze na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="ea053-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="ea053-199">Oba jsou ignorovány NuGet 2.</span><span class="sxs-lookup"><span data-stu-id="ea053-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="ea053-200">Nemůžete se `install.ps1` spoléhat ani `uninstall.ps1` fungovat.</span><span class="sxs-lookup"><span data-stu-id="ea053-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="ea053-201">Tyto soubory se `packages.config`spouštějí při `project.json`použití , ale jsou ignorovány pomocí .</span><span class="sxs-lookup"><span data-stu-id="ea053-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="ea053-202">Takže váš balíček musí být použitelný, aniž by běželi.</span><span class="sxs-lookup"><span data-stu-id="ea053-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="ea053-203">`init.ps1`stále běží na NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="ea053-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="ea053-204">Cíle a rekvizity instalace se liší, takže se ujistěte, že váš balíček funguje podle očekávání na obou klientech.</span><span class="sxs-lookup"><span data-stu-id="ea053-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="ea053-205">Podadresáře lib musí být TxM v NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="ea053-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="ea053-206">Knihovny nelze umístit do kořenového adresáře `lib` složky.</span><span class="sxs-lookup"><span data-stu-id="ea053-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="ea053-207">Obsah není automaticky zkopírován pomocí NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="ea053-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="ea053-208">Spotřebitelé vašeho balíčku mohou zkopírovat soubory sami nebo použít nástroj jako posuč úkolu k automatizaci kopírování souborů.</span><span class="sxs-lookup"><span data-stu-id="ea053-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="ea053-209">Transformace zdrojového a konfiguračního souboru nejsou spuštěny společností NuGet 3.</span><span class="sxs-lookup"><span data-stu-id="ea053-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="ea053-210">Pokud podporujete NuGet 2 a `minClientVersion` 3 pak vaše by měla být nejnižší verze klienta NuGet 2, který váš balíček funguje.</span><span class="sxs-lookup"><span data-stu-id="ea053-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="ea053-211">V případě existujícího balíčku by se nemělo měnit.</span><span class="sxs-lookup"><span data-stu-id="ea053-211">In the case of an existing package it shouldn't need to change.</span></span>
