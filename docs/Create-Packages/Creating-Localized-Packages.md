---
title: "Vytvoření lokalizovaných balíčků NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Podrobnosti o dva způsoby vytvoření lokalizované balíčky NuGet, včetně všech sestaveních ve jeden balíček nebo publikování samostatné sestavení."
keywords: "Lokalizace balíčku NuGet, NuGet satelitní sestavení, vytvoření lokalizovaných balíčků NuGet lokalizace konvence"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1ce8cff07bf629fcdeeaace901a185f2446b077a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="be292-104">Vytvoření lokalizovaných balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="be292-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="be292-105">Existují dva způsoby vytvoření lokalizované verze knihovny:</span><span class="sxs-lookup"><span data-stu-id="be292-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="be292-106">Zahrňte všechna sestavení lokalizované prostředky jeden balíček.</span><span class="sxs-lookup"><span data-stu-id="be292-106">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="be292-107">Vytvořte samostatné lokalizované satelitní balíčky (NuGet 1,8 a novější), pomocí následujících o striktní sadu pravidel.</span><span class="sxs-lookup"><span data-stu-id="be292-107">Create separate localized satellite packages (NuGet 1.8 and later), by following a strict set of conventions.</span></span>

<span data-ttu-id="be292-108">Obě metody mít jejich výhody a nevýhody, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="be292-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="be292-109">Lokalizovaný prostředek sestavení v jeden balíček</span><span class="sxs-lookup"><span data-stu-id="be292-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="be292-110">Včetně lokalizovaný prostředek sestavení v jednom balíčku je obvykle nejjednodušší přístup.</span><span class="sxs-lookup"><span data-stu-id="be292-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="be292-111">K tomuto účelu vytváření složek v rámci `lib` pro podporovaný jazyk jiné než výchozí balíček (předpokládá, že en-us).</span><span class="sxs-lookup"><span data-stu-id="be292-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="be292-112">V uvedených složkách můžete umístit prostředek sestavení a lokalizované soubory IntelliSense XML.</span><span class="sxs-lookup"><span data-stu-id="be292-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="be292-113">Například následující strukturu složek podporuje, němčina (de), italština (it), japonština (ja), ruština (ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="be292-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="be292-114">Uvidíte, že jazyky jsou všechny uvedené pod `net40` cílové složce framework.</span><span class="sxs-lookup"><span data-stu-id="be292-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="be292-115">Pokud jste [podpora více rozhraní](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku ve složce `lib` pro každý typ variant.</span><span class="sxs-lookup"><span data-stu-id="be292-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="be292-116">Pomocí těchto složek na místě, pak odkazovat všechny soubory ve vašem `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="be292-116">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="be292-117">Jeden balíček příklad, který používá tento přístup je [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="be292-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="be292-118">Výhody a nevýhody (lokalizovaný prostředek sestavení)</span><span class="sxs-lookup"><span data-stu-id="be292-118">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="be292-119">Sdružování všechny jazyky do jednoho balíčku má několik nevýhody:</span><span class="sxs-lookup"><span data-stu-id="be292-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="be292-120">**Sdílené metadata**: vzhledem k tomu, že balíček NuGet může obsahovat pouze jeden `.nuspec` souboru, můžete zadat metadata pouze jeden jazyk.</span><span class="sxs-lookup"><span data-stu-id="be292-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="be292-121">To znamená NuGet nemá k dispozici podpora lokalizované metadat.</span><span class="sxs-lookup"><span data-stu-id="be292-121">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="be292-122">**Velikost balíčku**: v závislosti na počet jazyků, které podporujete, knihovně, může být výrazně velký, což zpomalí instalace a obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="be292-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="be292-123">**Souběžné verze**: sdružování lokalizované soubory do jednoho balíčku vyžaduje verzi všechny prostředky v tomto balíčku současně, místo bude možné verze jednotlivých lokalizace samostatně.</span><span class="sxs-lookup"><span data-stu-id="be292-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="be292-124">Kromě toho jakékoliv aktualizace jakékoli jeden lokalizace vyžaduje novou verzi celý balíček.</span><span class="sxs-lookup"><span data-stu-id="be292-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="be292-125">Však také má několik výhod:</span><span class="sxs-lookup"><span data-stu-id="be292-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="be292-126">**Jednoduchost**: příjemci balíčku získat všechny podporované jazyky v jedné instalaci, namísto nutnosti instalovat samostatně jednotlivé jazyky.</span><span class="sxs-lookup"><span data-stu-id="be292-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="be292-127">Snazší najít v nuget.org je také jeden balíček.</span><span class="sxs-lookup"><span data-stu-id="be292-127">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="be292-128">**Doplněná verze**: vzhledem k tomu, že jsou všechny sestavení prostředků ve stejném balíčku jako primární sestavení, všechny sdílet stejné číslo verze a nespouštět riziko získávání chybnou informací odpojené.</span><span class="sxs-lookup"><span data-stu-id="be292-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="be292-129">Lokalizovaná satelitní balíčky</span><span class="sxs-lookup"><span data-stu-id="be292-129">Localized satellite packages</span></span>

<span data-ttu-id="be292-130">Podobně jako na tom, jak rozhraní .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory IntelliSense XML do balíčků satelit.</span><span class="sxs-lookup"><span data-stu-id="be292-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="be292-131">Do tohoto, váš primární balíček použije zásady vytváření názvů `{identifier}.{version}.nupkg` a obsahuje sestavení pro výchozí jazyk (například en US).</span><span class="sxs-lookup"><span data-stu-id="be292-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="be292-132">Například `ContosoUtilities.1.0.0.nupkg` by obsahovat následující strukturou:</span><span class="sxs-lookup"><span data-stu-id="be292-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="be292-133">Satelitní sestavení pak používá zásady vytváření názvů `{identifier}.{language}.{version}.nupkg`, jako například `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="be292-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="be292-134">Identifikátor **musí** přesně shodovat s primární balíčku.</span><span class="sxs-lookup"><span data-stu-id="be292-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="be292-135">Vzhledem k tomu je samostatný balíček, má svou vlastní `.nuspec` soubor, který obsahuje lokalizované metadat.</span><span class="sxs-lookup"><span data-stu-id="be292-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="be292-136">Mějte na paměti, jazyk v `.nuspec` **musí** odpovídat používaný v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="be292-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="be292-137">Satelitní sestavení **musí** zároveň deklarovat přesnou verzi primární balíčku jako závislost, pomocí zápisu verze [] \(viz [verze balíčku](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="be292-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="be292-138">Například `ContosoUtilities.de.1.0.0.nupkg` závislost na musí deklarovat `ContosoUtilities.1.0.0.nupkg` pomocí `[1.0.0]` zápis.</span><span class="sxs-lookup"><span data-stu-id="be292-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="be292-139">Balíček satelitní můžou mít samozřejmě číslo jinou verzi než primární balíček.</span><span class="sxs-lookup"><span data-stu-id="be292-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="be292-140">Struktura satelitní balíček pak zahrnout sestavení prostředků a soubor XML IntelliSense podsložky, která odpovídá `{language}` v názvu souboru balíčku:</span><span class="sxs-lookup"><span data-stu-id="be292-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="be292-141">**Poznámka:**: Pokud konkrétní subkultury jako `ja-JP` nezbytné, vždy použijte identifikátor vyšší úrovně jazyka, jako je třeba `ja`.</span><span class="sxs-lookup"><span data-stu-id="be292-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="be292-142">V satelitní sestavení, NuGet rozpozná **pouze** tyto soubory ve složce, která odpovídá `{language}` v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="be292-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="be292-143">Všechny další se ignorují.</span><span class="sxs-lookup"><span data-stu-id="be292-143">All others are ignored.</span></span>

<span data-ttu-id="be292-144">Pokud jsou splněny všechny tyto konvence, NuGet rozpozná balíček jako balíček satelitní a instalace lokalizované soubory do primární balíčku `lib` složky, jako kdyby měl byla původně sdružit do sady.</span><span class="sxs-lookup"><span data-stu-id="be292-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="be292-145">Odinstalace balíčku satelitní odebere jeho soubory ze stejné složce.</span><span class="sxs-lookup"><span data-stu-id="be292-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="be292-146">Měli byste vytvořit další satelitní sestavení stejným způsobem pro každý podporovaný jazyk.</span><span class="sxs-lookup"><span data-stu-id="be292-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="be292-147">Příklad zkontrolujte sadu rozhraní ASP.NET MVC balíčků:</span><span class="sxs-lookup"><span data-stu-id="be292-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="be292-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (anglické primární)</span><span class="sxs-lookup"><span data-stu-id="be292-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="be292-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span><span class="sxs-lookup"><span data-stu-id="be292-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="be292-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span><span class="sxs-lookup"><span data-stu-id="be292-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="be292-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span><span class="sxs-lookup"><span data-stu-id="be292-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="be292-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span><span class="sxs-lookup"><span data-stu-id="be292-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="be292-153">Souhrn požadované konvence</span><span class="sxs-lookup"><span data-stu-id="be292-153">Summary of required conventions</span></span>

- <span data-ttu-id="be292-154">Primární balíček musí mít název. `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="be292-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="be292-155">Satelitní balíček musí mít název. `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="be292-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="be292-156">Satelitní balíček `.nuspec` musíte zadat jeho jazyk odpovídající název souboru.</span><span class="sxs-lookup"><span data-stu-id="be292-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="be292-157">Satelitní balíčku musí deklarovat závislost na přesnou verzi systému primární notaci [] v jeho `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="be292-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="be292-158">Rozsahy nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="be292-158">Ranges are not supported.</span></span>
- <span data-ttu-id="be292-159">Satelitní balíčku musíte umístit soubory v `lib\[{framework}\]{language}` složky, který přesně odpovídá `{language}` v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="be292-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="be292-160">Výhody a nevýhody (satelitní balíčky)</span><span class="sxs-lookup"><span data-stu-id="be292-160">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="be292-161">Použití balíčků satelitní má několik výhod:</span><span class="sxs-lookup"><span data-stu-id="be292-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="be292-162">**Velikost balíčku**: celkové nároky na primární balíčku je minimalizován, a spotřebitelé pouze vynakládá jednotlivé jazyky, které chtějí používat.</span><span class="sxs-lookup"><span data-stu-id="be292-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="be292-163">**Samostatné metadata**: každý balíček satelitní má svou vlastní `.nuspec` soubor a proto jeho vlastní lokalizované metadata protože.</span><span class="sxs-lookup"><span data-stu-id="be292-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="be292-164">To umožňuje snadno najít balíčků tak, že nuget.org s podmínkami lokalizované některé příjemcům.</span><span class="sxs-lookup"><span data-stu-id="be292-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="be292-165">**Odpojené verze**: satelitní sestavení, se uvolní v čase, nikoli všechny najednou, umožňuje šíření vaše snahy o lokalizaci.</span><span class="sxs-lookup"><span data-stu-id="be292-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="be292-166">Satelitní balíčky však mít vlastní sadu nevýhody:</span><span class="sxs-lookup"><span data-stu-id="be292-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="be292-167">**Zbytečné soubory**: místo jeden balíček, máte velký počet balíčků, které může vést k nepřehlednost výsledků na nuget.org a dlouhý seznam odkazů v projektu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be292-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="be292-168">**Striktní konvence**.</span><span class="sxs-lookup"><span data-stu-id="be292-168">**Strict conventions**.</span></span> <span data-ttu-id="be292-169">Satelitní balíčky musí přesně odpovídat daným nebo lokalizované verze nesmí být zachyceny správně.</span><span class="sxs-lookup"><span data-stu-id="be292-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="be292-170">**Správa verzí**: každý balíček satelitní musí mít přesnou verzi závislostí na primární balíčku.</span><span class="sxs-lookup"><span data-stu-id="be292-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="be292-171">To znamená, že primární balíček aktualizace může vyžadovat aktualizaci všech balíčků satelitní taky i v případě, že prostředky nezměnil.</span><span class="sxs-lookup"><span data-stu-id="be292-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
