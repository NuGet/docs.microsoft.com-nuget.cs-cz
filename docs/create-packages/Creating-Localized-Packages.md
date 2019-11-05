---
title: Postup vytvoření lokalizovaného balíčku NuGet
description: Podrobnosti o dvou způsobech vytvoření lokalizovaných balíčků NuGet, a to buď zahrnutím všech sestavení do jednoho balíčku, nebo publikováním samostatných sestavení.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610943"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="9e6de-103">Vytváření lokalizovaných balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="9e6de-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="9e6de-104">Existují dva způsoby, jak vytvořit lokalizované verze knihovny:</span><span class="sxs-lookup"><span data-stu-id="9e6de-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="9e6de-105">Zahrňte všechna lokalizovaná sestavení prostředků do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e6de-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="9e6de-106">Pomocí striktní sady konvencí vytvořte samostatné lokalizované satelitní balíčky.</span><span class="sxs-lookup"><span data-stu-id="9e6de-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="9e6de-107">Obě metody mají své výhody a nevýhody, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="9e6de-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="9e6de-108">Lokalizovaná sestavení prostředků v jednom balíčku</span><span class="sxs-lookup"><span data-stu-id="9e6de-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="9e6de-109">Zahrnutí lokalizovaných sestavení prostředků do jednoho balíčku je obvykle nejjednodušší přístup.</span><span class="sxs-lookup"><span data-stu-id="9e6de-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="9e6de-110">Chcete-li to provést, vytvořte složky v rámci `lib` pro jiný podporovaný jazyk, Kromě výchozího balíčku (předpokládá se en-us).</span><span class="sxs-lookup"><span data-stu-id="9e6de-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="9e6de-111">V těchto složkách můžete umístit sestavení prostředků a lokalizované soubory XML technologie IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="9e6de-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="9e6de-112">Například následující struktura složek podporuje, němčina (de), italština (IT), japonština (Japonsko), ruština (ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="9e6de-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="9e6de-113">Můžete vidět, že jsou všechny jazyky uvedené pod složkou `net40` Target Framework.</span><span class="sxs-lookup"><span data-stu-id="9e6de-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="9e6de-114">Pokud [podporujete více platforem](../create-packages/supporting-multiple-target-frameworks.md), máte složku pod `lib` pro každou variantu.</span><span class="sxs-lookup"><span data-stu-id="9e6de-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="9e6de-115">V případě, že tyto složky jsou na místě, odkázat na všechny soubory v `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="9e6de-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="9e6de-116">Jedním z ukázkových balíčků, které používají tento přístup, je [Microsoft. data. OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="9e6de-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="9e6de-117">Výhody a nevýhody (lokalizovaná sestavení prostředků)</span><span class="sxs-lookup"><span data-stu-id="9e6de-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="9e6de-118">Sdružování všech jazyků v jednom balíčku má několik nevýhody:</span><span class="sxs-lookup"><span data-stu-id="9e6de-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="9e6de-119">**Sdílená metadata**: vzhledem k tomu, že balíček NuGet může obsahovat jenom jeden soubor `.nuspec`, můžete zadat metadata jenom pro jeden jazyk.</span><span class="sxs-lookup"><span data-stu-id="9e6de-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="9e6de-120">To znamená, že NuGet nepodporuje lokalizovaná metadata.</span><span class="sxs-lookup"><span data-stu-id="9e6de-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="9e6de-121">**Velikost balíčku**: v závislosti na počtu jazyků, které podporujete, může být knihovna výrazně velká, což zpomaluje instalaci a obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e6de-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="9e6de-122">**Současná vydání**: sdružování lokalizovaných souborů do jednoho balíčku vyžaduje, abyste všechny prostředky v tomto balíčku uvolnili současně, ale nedokázali uvolnit každou lokalizaci samostatně.</span><span class="sxs-lookup"><span data-stu-id="9e6de-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="9e6de-123">Kromě toho jakákoli aktualizace na jednu lokalizaci vyžaduje novou verzi celého balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e6de-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="9e6de-124">Má ale také několik výhod:</span><span class="sxs-lookup"><span data-stu-id="9e6de-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="9e6de-125">**Jednoduchost**: spotřebitelé balíčku získají všechny podporované jazyky v jediné instalaci, ale nemusíte instalovat jednotlivé jazyky samostatně.</span><span class="sxs-lookup"><span data-stu-id="9e6de-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="9e6de-126">Jeden balíček je také snazší najít na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9e6de-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="9e6de-127">Spárované **verze**: vzhledem k tomu, že všechna sestavení prostředků jsou ve stejném balíčku jako primární sestavení, všichni sdílejí stejné číslo verze a nespouštějí riziko chybného odložení.</span><span class="sxs-lookup"><span data-stu-id="9e6de-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="9e6de-128">Lokalizované satelitní balíčky</span><span class="sxs-lookup"><span data-stu-id="9e6de-128">Localized satellite packages</span></span>

<span data-ttu-id="9e6de-129">Podobně jako .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory XML technologie IntelliSense do satelitních balíčků.</span><span class="sxs-lookup"><span data-stu-id="9e6de-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="9e6de-130">K tomu váš primární balíček používá konvenci pojmenování `{identifier}.{version}.nupkg` a obsahuje sestavení pro výchozí jazyk (například en-US).</span><span class="sxs-lookup"><span data-stu-id="9e6de-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="9e6de-131">`ContosoUtilities.1.0.0.nupkg` by například obsahoval následující strukturu:</span><span class="sxs-lookup"><span data-stu-id="9e6de-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="9e6de-132">Satelitní sestavení potom používá konvenci pojmenování `{identifier}.{language}.{version}.nupkg`, například `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="9e6de-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="9e6de-133">Identifikátor **musí** přesně odpovídat primárnímu balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e6de-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="9e6de-134">Vzhledem k tomu, že se jedná o samostatný balíček, má vlastní `.nuspec` soubor, který obsahuje lokalizovaná metadata.</span><span class="sxs-lookup"><span data-stu-id="9e6de-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="9e6de-135">Je třeba mít na vědomí, že jazyk v `.nuspec` **musí** odpovídat názvu použitému v souboru filename.</span><span class="sxs-lookup"><span data-stu-id="9e6de-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="9e6de-136">Satelitní sestavení **musí** také deklarovat přesnou verzi primárního balíčku jako závislost pomocí zápisu verze [] (viz [Správa verzí balíčku](../concepts/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="9e6de-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="9e6de-137">Například `ContosoUtilities.de.1.0.0.nupkg` musí deklarovat závislost na `ContosoUtilities.1.0.0.nupkg` pomocí zápisu `[1.0.0]`.</span><span class="sxs-lookup"><span data-stu-id="9e6de-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="9e6de-138">Satelitní balíček může samozřejmě mít jiné číslo verze než primární balíček.</span><span class="sxs-lookup"><span data-stu-id="9e6de-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="9e6de-139">Struktura satelitního balíčku musí poté zahrnovat sestavení prostředků a soubor XML IntelliSense do podsložky, která odpovídá `{language}` v souboru názvu balíčku:</span><span class="sxs-lookup"><span data-stu-id="9e6de-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="9e6de-140">**Poznámka**: Pokud nejsou nutné konkrétní subkultury jako `ja-JP`, vždy používejte identifikátor jazyka vyšší úrovně, například `ja`.</span><span class="sxs-lookup"><span data-stu-id="9e6de-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="9e6de-141">V satelitním sestavení NuGet rozpozná **pouze** soubory ve složce, které odpovídají `{language}` v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9e6de-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="9e6de-142">Všechny ostatní jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="9e6de-142">All others are ignored.</span></span>

<span data-ttu-id="9e6de-143">Když jsou splněné všechny tyto konvence, NuGet rozpozná balíček jako satelitní balíček a nainstaluje lokalizované soubory do `lib` složky primárního balíčku, jako kdyby byly původně zabalené.</span><span class="sxs-lookup"><span data-stu-id="9e6de-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="9e6de-144">Odinstalováním satelitního balíčku dojde k odebrání souborů ze stejné složky.</span><span class="sxs-lookup"><span data-stu-id="9e6de-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="9e6de-145">Vytvořili byste Další satelitní sestavení stejným způsobem pro každý podporovaný jazyk.</span><span class="sxs-lookup"><span data-stu-id="9e6de-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="9e6de-146">Podívejte se například na sadu balíčků ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="9e6de-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="9e6de-147">[Microsoft. ASPNET. Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (angličtina – primární)</span><span class="sxs-lookup"><span data-stu-id="9e6de-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="9e6de-148">[Microsoft.ASPNET.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (němčina)</span><span class="sxs-lookup"><span data-stu-id="9e6de-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="9e6de-149">[Microsoft. ASPNET. Mvc. ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonština)</span><span class="sxs-lookup"><span data-stu-id="9e6de-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="9e6de-150">[Microsoft. ASPNET. Mvc. zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (čínština (zjednodušená))</span><span class="sxs-lookup"><span data-stu-id="9e6de-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="9e6de-151">[Microsoft. ASPNET. Mvc. zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (čínština (tradiční))</span><span class="sxs-lookup"><span data-stu-id="9e6de-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="9e6de-152">Shrnutí požadovaných konvencí</span><span class="sxs-lookup"><span data-stu-id="9e6de-152">Summary of required conventions</span></span>

- <span data-ttu-id="9e6de-153">Primární balíček musí mít název `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="9e6de-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="9e6de-154">Satelitní balíček musí mít název `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="9e6de-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="9e6de-155">`.nuspec` satelitního balíčku musí určit svůj jazyk tak, aby odpovídal názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9e6de-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="9e6de-156">Satelitní balíček musí deklarovat závislost na přesnou verzi primárního objektu pomocí zápisu [] v souboru `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9e6de-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="9e6de-157">Rozsahy nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="9e6de-157">Ranges are not supported.</span></span>
- <span data-ttu-id="9e6de-158">Satelitní balíček musí umístit soubory do složky `lib\[{framework}\]{language}`, který přesně odpovídá `{language}` v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9e6de-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="9e6de-159">Výhody a nevýhody (satelitní balíčky)</span><span class="sxs-lookup"><span data-stu-id="9e6de-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="9e6de-160">Použití satelitních balíčků má několik výhod:</span><span class="sxs-lookup"><span data-stu-id="9e6de-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="9e6de-161">**Velikost balíčku**: celkové nároky na primární balíček se minimalizují a spotřebitelé účtují jenom náklady na jednotlivé jazyky, které chtějí používat.</span><span class="sxs-lookup"><span data-stu-id="9e6de-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="9e6de-162">**Samostatná metadata**: každý satelitní balíček má vlastní soubor `.nuspec` a tedy vlastní lokalizovaná metadata, protože.</span><span class="sxs-lookup"><span data-stu-id="9e6de-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="9e6de-163">To může některým spotřebitelům dovolit snazší hledání balíčků tím, že prohledají nuget.org s lokalizovanými podmínkami.</span><span class="sxs-lookup"><span data-stu-id="9e6de-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="9e6de-164">**Oddělitelné verze**: satelitní sestavení lze uvolnit v průběhu času, nikoli všechny najednou, což vám umožní rozložit vaše lokalizace.</span><span class="sxs-lookup"><span data-stu-id="9e6de-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="9e6de-165">Nicméně satelitní balíčky mají svou vlastní sadu nevýhod:</span><span class="sxs-lookup"><span data-stu-id="9e6de-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="9e6de-166">**Zbytečných**: místo jednoho balíčku máte mnoho balíčků, které mohou vést k zbytečnému vyhledávání výsledků hledání v NuGet.org a dlouhému seznamu odkazů v projektu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e6de-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="9e6de-167">**Striktní konvence**.</span><span class="sxs-lookup"><span data-stu-id="9e6de-167">**Strict conventions**.</span></span> <span data-ttu-id="9e6de-168">Satelitní balíčky musí přesně splňovat konvence nebo lokalizované verze nebudou správně vyzvednuty.</span><span class="sxs-lookup"><span data-stu-id="9e6de-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="9e6de-169">**Správa verzí**: každý satelitní balíček musí mít přesnou závislost verze v primárním balíčku.</span><span class="sxs-lookup"><span data-stu-id="9e6de-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="9e6de-170">To znamená, že aktualizace primárního balíčku může vyžadovat aktualizaci všech satelitních balíčků i v případě, že se prostředky nezměnily.</span><span class="sxs-lookup"><span data-stu-id="9e6de-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
