---
title: Jak vytvořit lokalizovaný balíček NuGet
description: Podrobnosti o dvou způsobech vytvoření lokalizovaných balíčků NuGet, buď zahrnutím všech sestavení do jednoho balíčku nebo publikováním samostatných sestavení.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610943"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="d7068-103">Vytváření lokalizovaných balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="d7068-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="d7068-104">Existují dva způsoby, jak vytvořit lokalizované verze knihovny:</span><span class="sxs-lookup"><span data-stu-id="d7068-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="d7068-105">Zahrnout všechna sestavení lokalizovaných prostředků do jednoho balíčku.</span><span class="sxs-lookup"><span data-stu-id="d7068-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="d7068-106">Vytvořte samostatné lokalizované satelitní balíčky podle přísné sady konvencí.</span><span class="sxs-lookup"><span data-stu-id="d7068-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="d7068-107">Obě metody mají své výhody a nevýhody, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="d7068-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="d7068-108">Lokalizovaná sestavení prostředků v jednom balíčku</span><span class="sxs-lookup"><span data-stu-id="d7068-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="d7068-109">Zahrnutí lokalizovaných sestavení prostředků do jednoho balíčku je obvykle nejjednodušší přístup.</span><span class="sxs-lookup"><span data-stu-id="d7068-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="d7068-110">Chcete-li to provést, vytvořte složky v rámci `lib` podporovaného jazyka než výchozího balíčku (předpokládá se en-us).</span><span class="sxs-lookup"><span data-stu-id="d7068-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="d7068-111">V těchto složkách můžete umístit sestavení prostředků a lokalizované soubory XML Technologie IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="d7068-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="d7068-112">Například následující struktura složek podporuje, němčina (de), italština (it), japonština (ja), ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="d7068-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="d7068-113">Můžete vidět, že všechny jazyky `net40` jsou uvedeny pod složky cílové architektury.</span><span class="sxs-lookup"><span data-stu-id="d7068-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="d7068-114">Pokud [podporujete více architektur](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku `lib` pod pro každou variantu.</span><span class="sxs-lookup"><span data-stu-id="d7068-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="d7068-115">S těmito složkami na místě, pak `.nuspec`odkazovat na všechny soubory v :</span><span class="sxs-lookup"><span data-stu-id="d7068-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="d7068-116">Jeden příklad balíček, který používá tento přístup je [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="d7068-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="d7068-117">Výhody a nevýhody (lokalizovaná sestavení prostředků)</span><span class="sxs-lookup"><span data-stu-id="d7068-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="d7068-118">Sdružování všech jazyků do jednoho balíčku má několik nevýhod:</span><span class="sxs-lookup"><span data-stu-id="d7068-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="d7068-119">**Sdílená metadata**: Vzhledem k tomu, že balíček NuGet může obsahovat pouze jeden `.nuspec` soubor, můžete poskytnout metadata pouze pro jeden jazyk.</span><span class="sxs-lookup"><span data-stu-id="d7068-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="d7068-120">To znamená NuGet nepředstavuje podporu lokalizovaných metadat.</span><span class="sxs-lookup"><span data-stu-id="d7068-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="d7068-121">**Velikost balíčku**: V závislosti na počtu jazyků, které podporujete, může být knihovna značně velká, což zpomaluje instalaci a obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="d7068-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="d7068-122">**Simultánní verze**: Sdružování lokalizovaných souborů do jednoho balíčku vyžaduje, abyste uvolnili všechny datové zdroje v tomto balíčku současně, místo toho, abyste mohli uvolnit každou lokalizaci samostatně.</span><span class="sxs-lookup"><span data-stu-id="d7068-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="d7068-123">Kromě toho každá aktualizace jedné lokalizace vyžaduje novou verzi celého balíčku.</span><span class="sxs-lookup"><span data-stu-id="d7068-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="d7068-124">Má však také několik výhod:</span><span class="sxs-lookup"><span data-stu-id="d7068-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="d7068-125">**Jednoduchost**: Spotřebitelé balíčku získat všechny podporované jazyky v jedné instalaci, spíše než nutnost instalovat každý jazyk samostatně.</span><span class="sxs-lookup"><span data-stu-id="d7068-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="d7068-126">Jeden balíček je také snazší najít na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d7068-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="d7068-127">**Vázané verze**: Vzhledem k tomu, že všechna sestavení prostředků jsou ve stejném balíčku jako primární sestavení, všechny sdílejí stejné číslo verze a nepředstavují riziko chybného oddělení.</span><span class="sxs-lookup"><span data-stu-id="d7068-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="d7068-128">Lokalizované satelitní balíčky</span><span class="sxs-lookup"><span data-stu-id="d7068-128">Localized satellite packages</span></span>

<span data-ttu-id="d7068-129">Podobně jako rozhraní .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory IntelliSense XML do satelitních balíčků.</span><span class="sxs-lookup"><span data-stu-id="d7068-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="d7068-130">Proveďte to, primární balíček `{identifier}.{version}.nupkg` používá konvence pojmenování a obsahuje sestavení pro výchozí jazyk (například en US).</span><span class="sxs-lookup"><span data-stu-id="d7068-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="d7068-131">Například `ContosoUtilities.1.0.0.nupkg` by obsahovat následující strukturu:</span><span class="sxs-lookup"><span data-stu-id="d7068-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="d7068-132">Satelitní sestavení pak používá `{identifier}.{language}.{version}.nupkg`konvence pojmenování , například `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="d7068-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="d7068-133">Identifikátor **se musí** přesně shodovat s primárním balíčkem.</span><span class="sxs-lookup"><span data-stu-id="d7068-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="d7068-134">Protože se jedná o samostatný balíček, má vlastní `.nuspec` soubor, který obsahuje lokalizovaná metadata.</span><span class="sxs-lookup"><span data-stu-id="d7068-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="d7068-135">Mějte na paměti, `.nuspec` že jazyk v **musí** odpovídat jazyk u použitého v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="d7068-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="d7068-136">Satelitní sestavení **musí** také deklarovat přesnou verzi primárního balíčku jako závislost pomocí zápisu verze [] (viz [Správa verzí balíčku).](../concepts/package-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="d7068-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="d7068-137">Například `ContosoUtilities.de.1.0.0.nupkg` musí deklarovat `ContosoUtilities.1.0.0.nupkg` závislost `[1.0.0]` na použití zápisu.</span><span class="sxs-lookup"><span data-stu-id="d7068-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="d7068-138">Satelitní balíček může mít samozřejmě jiné číslo verze než primární balíček.</span><span class="sxs-lookup"><span data-stu-id="d7068-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="d7068-139">Struktura satelitního balíčku pak musí obsahovat sestavení prostředků a soubor Xml IntelliSense v podsložce, která odpovídá `{language}` názvu souboru balíčku:</span><span class="sxs-lookup"><span data-stu-id="d7068-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="d7068-140">**Poznámka**: Pokud `ja-JP` jsou nezbytné určité subkultury, vždy používejte `ja`identifikátor jazyka vyšší úrovně, například .</span><span class="sxs-lookup"><span data-stu-id="d7068-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="d7068-141">V satelitním sestavení NuGet rozpozná **pouze** ty soubory `{language}` ve složce, která odpovídá v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="d7068-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="d7068-142">Všechny ostatní jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="d7068-142">All others are ignored.</span></span>

<span data-ttu-id="d7068-143">Při splnění všech těchto konvencí, NuGet rozpozná balíček jako satelitní balíček a `lib` nainstaluje lokalizované soubory do složky primárního balíčku, jako by byly původně svázaný.</span><span class="sxs-lookup"><span data-stu-id="d7068-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="d7068-144">Odinstalováním satelitního balíčku odeberete jeho soubory ze stejné složky.</span><span class="sxs-lookup"><span data-stu-id="d7068-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="d7068-145">Pro každý podporovaný jazyk byste vytvořili další satelitní sestavení stejným způsobem.</span><span class="sxs-lookup"><span data-stu-id="d7068-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="d7068-146">Například zkontrolujte sadu ASP.NET balíčků MVC:</span><span class="sxs-lookup"><span data-stu-id="d7068-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="d7068-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (angličtina primární)</span><span class="sxs-lookup"><span data-stu-id="d7068-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="d7068-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (něm.)</span><span class="sxs-lookup"><span data-stu-id="d7068-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="d7068-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonština)</span><span class="sxs-lookup"><span data-stu-id="d7068-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="d7068-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (zjednodušená čínština))</span><span class="sxs-lookup"><span data-stu-id="d7068-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="d7068-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (čínština (tradiční))</span><span class="sxs-lookup"><span data-stu-id="d7068-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="d7068-152">Shrnutí požadovaných konvencí</span><span class="sxs-lookup"><span data-stu-id="d7068-152">Summary of required conventions</span></span>

- <span data-ttu-id="d7068-153">Primární balíček musí být pojmenován.`{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="d7068-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="d7068-154">Satelitní balíček musí být pojmenován`{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="d7068-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="d7068-155">Satelitní balíček `.nuspec` musí zadat svůj jazyk tak, aby odpovídal názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="d7068-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="d7068-156">Satelitní balíček musí deklarovat závislost na přesné verzi primární pomocí `.nuspec` [] zápisu v jeho souboru.</span><span class="sxs-lookup"><span data-stu-id="d7068-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="d7068-157">Rozsahy nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="d7068-157">Ranges are not supported.</span></span>
- <span data-ttu-id="d7068-158">Satelitní balíček musí umístit `lib\[{framework}\]{language}` soubory do `{language}` složky, která přesně odpovídá názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="d7068-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="d7068-159">Výhody a nevýhody (satelitní balíčky)</span><span class="sxs-lookup"><span data-stu-id="d7068-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="d7068-160">Použití satelitních balíčků má několik výhod:</span><span class="sxs-lookup"><span data-stu-id="d7068-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="d7068-161">**Velikost balíčku**: Celková stopa primárního balíčku je minimalizována a spotřebitelům vznikají pouze náklady na každý jazyk, který chtějí používat.</span><span class="sxs-lookup"><span data-stu-id="d7068-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="d7068-162">**Samostatná metadata**: Každý `.nuspec` satelitní balíček má svůj vlastní soubor a tím i vlastní lokalizovaná metadata, protože.</span><span class="sxs-lookup"><span data-stu-id="d7068-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="d7068-163">To může umožnit některým spotřebitelům snadněji najít balíčky vyhledáním nuget.org s lokalizovanými termíny.</span><span class="sxs-lookup"><span data-stu-id="d7068-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="d7068-164">**Oddělené verze**: Satelitní sestavení mohou být uvolněna v průběhu času, nikoli všechny najednou, což vám umožní rozložit vaše lokalizační úsilí.</span><span class="sxs-lookup"><span data-stu-id="d7068-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="d7068-165">Nicméně, satelitní balíčky mají své vlastní sady nevýhod:</span><span class="sxs-lookup"><span data-stu-id="d7068-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="d7068-166">**Nepořádek**: Namísto jednoho balíčku máte mnoho balíčků, které mohou vést k přeplněným výsledkům hledání na nuget.org a dlouhý seznam odkazů v projektu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7068-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="d7068-167">**Přísné konvence**.</span><span class="sxs-lookup"><span data-stu-id="d7068-167">**Strict conventions**.</span></span> <span data-ttu-id="d7068-168">Satelitní balíčky musí přesně dodržovat konvence, jinak lokalizované verze nebudou správně vyzvednuty.</span><span class="sxs-lookup"><span data-stu-id="d7068-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="d7068-169">**Správa verzí**: Každý satelitní balíček musí mít přesnou závislost verze na primárním balíčku.</span><span class="sxs-lookup"><span data-stu-id="d7068-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="d7068-170">To znamená, že aktualizace primárního balíčku může vyžadovat také aktualizaci všech satelitních balíčků, a to i v případě, že se prostředky nezměnily.</span><span class="sxs-lookup"><span data-stu-id="d7068-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
