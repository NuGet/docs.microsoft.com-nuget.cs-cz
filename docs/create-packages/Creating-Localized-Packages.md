---
title: Vytvoření lokalizovaných balíčků NuGet
description: Podrobnosti o dva způsoby vytvoření lokalizovaných balíčků NuGet, včetně všechna sestavení v jediném balíčku nebo publikování samostatné sestavení.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: b1c2511c1fbafc7f52029c23521fa55671b0b5c5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546892"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="9b37f-103">Vytvoření lokalizovaných balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="9b37f-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="9b37f-104">Existují dva způsoby vytvoření lokalizované verze knihovny:</span><span class="sxs-lookup"><span data-stu-id="9b37f-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="9b37f-105">Zahrňte všechna sestavení lokalizovaných prostředků v jediném balíčku.</span><span class="sxs-lookup"><span data-stu-id="9b37f-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="9b37f-106">Vytváření balíčků samostatné lokalizované satelitní podle striktní sadu pravidel.</span><span class="sxs-lookup"><span data-stu-id="9b37f-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="9b37f-107">Obě metody mají své výhody a nevýhody, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="9b37f-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="9b37f-108">Sestavení lokalizovaných prostředků v jediném balíčku</span><span class="sxs-lookup"><span data-stu-id="9b37f-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="9b37f-109">Včetně sestavení lokalizovaných prostředků v jediném balíčku je obvykle nejjednodušším přístupem.</span><span class="sxs-lookup"><span data-stu-id="9b37f-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="9b37f-110">K tomuto účelu vytváření složek v rámci `lib` pro podporovaný jazyk jiné než výchozí balíček (předpokládá, že en-us).</span><span class="sxs-lookup"><span data-stu-id="9b37f-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="9b37f-111">V těchto složkách můžete umístit sestavení prostředků a lokalizované soubory XML technologie IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="9b37f-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="9b37f-112">Například následující strukturu složek podporuje, němčina (de), italština (it), japonština (Japonsko), ruština (ru), čínština (zjednodušená) (zh-Hans) a čínština (tradiční) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="9b37f-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="9b37f-113">Uvidíte, že jazyky jsou všechny uvedené pod `net40` cílové rozhraní framework složky.</span><span class="sxs-lookup"><span data-stu-id="9b37f-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="9b37f-114">Pokud jste [podporuje více platforem](../create-packages/supporting-multiple-target-frameworks.md), pak máte složku ve složce `lib` pro každý typ variant.</span><span class="sxs-lookup"><span data-stu-id="9b37f-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="9b37f-115">Pomocí těchto složek na místě můžete odkázat na všechny soubory ve vašich `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="9b37f-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="9b37f-116">Jeden příklad balíčku, který používá tento přístup je [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="9b37f-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="9b37f-117">Výhody a nevýhody (lokalizovaný prostředek sestavení)</span><span class="sxs-lookup"><span data-stu-id="9b37f-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="9b37f-118">Sdružování všechny jazyky v jediném balíčku má několik nevýhody:</span><span class="sxs-lookup"><span data-stu-id="9b37f-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="9b37f-119">**Sdílet metadata**: protože balíčku NuGet může obsahovat jenom jeden `.nuspec` soubor, můžete zadat metadata pouze jeden jazyk.</span><span class="sxs-lookup"><span data-stu-id="9b37f-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="9b37f-120">To znamená NuGet není k dispozici podpora lokalizované metadat.</span><span class="sxs-lookup"><span data-stu-id="9b37f-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="9b37f-121">**Balíček velikost**: v závislosti na počtu podporovaných jazyků, knihovny, může být značně velké, což zpomalí instalace a obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="9b37f-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="9b37f-122">**Souběžných verzí**: sdružování lokalizované soubory do jediného balíčku vyžaduje uvolnit všechny prostředky v tomto balíčku současně, namísto samostatně uvolnit každý lokalizace.</span><span class="sxs-lookup"><span data-stu-id="9b37f-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="9b37f-123">Kromě toho kterákoli aktualizace jakékoli jeden lokalizaci vyžaduje novou verzi celý balíček.</span><span class="sxs-lookup"><span data-stu-id="9b37f-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="9b37f-124">Také má však několik výhod:</span><span class="sxs-lookup"><span data-stu-id="9b37f-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="9b37f-125">**Zjednodušení**: spotřebitele balíčku získat všechny podporované jazyky v jedna instalace, a nemusíte instalovat každý jazyk samostatně.</span><span class="sxs-lookup"><span data-stu-id="9b37f-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="9b37f-126">Jeden balíček je také snazší najít na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9b37f-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="9b37f-127">**Verze s velkou provázaností**: vzhledem k tomu, že všechna sestavení prostředků jsou ve stejném balíčku jako primární sestavení, sdílejí stejné číslo verze a při spuštění riziko získávání chybně oddělení.</span><span class="sxs-lookup"><span data-stu-id="9b37f-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="9b37f-128">Lokalizovaná satelitní balíčky</span><span class="sxs-lookup"><span data-stu-id="9b37f-128">Localized satellite packages</span></span>

<span data-ttu-id="9b37f-129">Podobně jako způsob, jakým rozhraní .NET Framework podporuje satelitní sestavení, tato metoda odděluje lokalizované prostředky a soubory IntelliSense XML do satelitních balíčků.</span><span class="sxs-lookup"><span data-stu-id="9b37f-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="9b37f-130">To, jak, váš primární balíček používá konvence `{identifier}.{version}.nupkg` a obsahuje sestavení pro výchozí jazyk (třeba cs cz).</span><span class="sxs-lookup"><span data-stu-id="9b37f-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="9b37f-131">Například `ContosoUtilities.1.0.0.nupkg` by obsahovala následující strukturu:</span><span class="sxs-lookup"><span data-stu-id="9b37f-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="9b37f-132">Satelitní sestavení pak používá konvence `{identifier}.{language}.{version}.nupkg`, jako například `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="9b37f-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="9b37f-133">Identifikátor **musí** přesně odpovídat primární balíček.</span><span class="sxs-lookup"><span data-stu-id="9b37f-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="9b37f-134">Protože jde o samostatný balíček, má své vlastní `.nuspec` soubor, který obsahuje lokalizované metadat.</span><span class="sxs-lookup"><span data-stu-id="9b37f-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="9b37f-135">Mějte na paměti, který jazyk `.nuspec` **musí** odpovídat tomu použitému v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9b37f-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="9b37f-136">Satelitní sestavení **musí** zároveň deklarovat přesnou verzi primární balíčku jako závislost, pomocí zápisu verze [] \(viz [verze balíčku](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="9b37f-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="9b37f-137">Například `ContosoUtilities.de.1.0.0.nupkg` musí deklarovat závislost na `ContosoUtilities.1.0.0.nupkg` pomocí `[1.0.0]` zápis.</span><span class="sxs-lookup"><span data-stu-id="9b37f-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="9b37f-138">Balíček satelitní může samozřejmě mít jinou verzi číslo než primární balíček.</span><span class="sxs-lookup"><span data-stu-id="9b37f-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="9b37f-139">Struktura balíčku satelitní pak zahrnout sestavení prostředků a soubor XML IntelliSense do podsložky, která odpovídá `{language}` v názvu souboru balíčku:</span><span class="sxs-lookup"><span data-stu-id="9b37f-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="9b37f-140">**Poznámka:**: není-li konkrétní subkultury jako `ja-JP` jsou nezbytné, vždy používejte identifikátor vyšší úrovně jazyka, jako je třeba `ja`.</span><span class="sxs-lookup"><span data-stu-id="9b37f-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="9b37f-141">Do satelitního sestavení NuGet rozpozná **pouze** tyto soubory ve složce, která odpovídá `{language}` v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9b37f-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="9b37f-142">Případné další se ignorují.</span><span class="sxs-lookup"><span data-stu-id="9b37f-142">All others are ignored.</span></span>

<span data-ttu-id="9b37f-143">Pokud se splní všechny tyto konvence, NuGet rozpozná balíčku jako balíček satelitní a lokalizované soubory nainstalovat do primární balíček `lib` složky, jako by se měl byly spojeny původně.</span><span class="sxs-lookup"><span data-stu-id="9b37f-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="9b37f-144">Odinstalovává se balíček satelitní odebere jeho souborů ze stejné složce.</span><span class="sxs-lookup"><span data-stu-id="9b37f-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="9b37f-145">Vytvoříte další satelitní sestavení stejným způsobem pro každý podporovaný jazyk.</span><span class="sxs-lookup"><span data-stu-id="9b37f-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="9b37f-146">Příklad prozkoumejte sadu balíčků ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="9b37f-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="9b37f-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (anglické primární)</span><span class="sxs-lookup"><span data-stu-id="9b37f-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="9b37f-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (němčina)</span><span class="sxs-lookup"><span data-stu-id="9b37f-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="9b37f-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japonština)</span><span class="sxs-lookup"><span data-stu-id="9b37f-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="9b37f-150">[Microsoft.AspNet.Mvc.zh Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (čínština (zjednodušená))</span><span class="sxs-lookup"><span data-stu-id="9b37f-150">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="9b37f-151">[Microsoft.AspNet.Mvc.zh Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (čínština (tradiční))</span><span class="sxs-lookup"><span data-stu-id="9b37f-151">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="9b37f-152">Souhrnné informace o požadované konvence</span><span class="sxs-lookup"><span data-stu-id="9b37f-152">Summary of required conventions</span></span>

- <span data-ttu-id="9b37f-153">Primární balíček musí mít název. `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="9b37f-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="9b37f-154">Satelitní balíčku musí mít název. `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="9b37f-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="9b37f-155">Satelitní balíček `.nuspec` musíte zadat jeho jazyk tak, aby odpovídaly názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9b37f-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="9b37f-156">Satelitní balíčku musí deklarovat závislost na přesnou verzi primární pomocí zápisu []. v jeho `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="9b37f-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="9b37f-157">Rozsahy nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="9b37f-157">Ranges are not supported.</span></span>
- <span data-ttu-id="9b37f-158">Satelitní balíčku musíte umístit soubory `lib\[{framework}\]{language}` složky, který přesně odpovídá `{language}` v názvu souboru.</span><span class="sxs-lookup"><span data-stu-id="9b37f-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="9b37f-159">Výhody a nevýhody (satelitní balíčky)</span><span class="sxs-lookup"><span data-stu-id="9b37f-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="9b37f-160">Použití balíčků satelitní má několik výhod:</span><span class="sxs-lookup"><span data-stu-id="9b37f-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="9b37f-161">**Balíček velikost**: je minimalizován celkový objem primární balíček a spotřebitelé pouze vám být naúčtovány náklady na jednotlivé jazyky, které chtějí používat.</span><span class="sxs-lookup"><span data-stu-id="9b37f-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="9b37f-162">**Samostatné metadat**: každý balíček satelitní má vlastní `.nuspec` soubor a proto lokalizované metadat protože.</span><span class="sxs-lookup"><span data-stu-id="9b37f-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="9b37f-163">To umožňuje některé příjemce snadněji najít balíčků tak, že nuget.org lokalizované podmínek.</span><span class="sxs-lookup"><span data-stu-id="9b37f-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="9b37f-164">**Oddělené verze**: satelitní sestavení mohou být vydány v čase, nikoli všechny najednou, umožňuje rozprostřete vaše úsilí lokalizace.</span><span class="sxs-lookup"><span data-stu-id="9b37f-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="9b37f-165">Satelitní balíčků však mají své vlastní sadu nevýhody:</span><span class="sxs-lookup"><span data-stu-id="9b37f-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="9b37f-166">**Nepořádku**: místo jeden balíček, budete mít mnoho balíčků, které můžou vést k výsledkům nevypadala hledání na webech nuget.org a dlouhý seznam odkazů v projektu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b37f-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="9b37f-167">**Striktní konvence**.</span><span class="sxs-lookup"><span data-stu-id="9b37f-167">**Strict conventions**.</span></span> <span data-ttu-id="9b37f-168">Satelitní balíčky musí konvence přesně nebo lokalizované verze nesmí být nenačítají správně.</span><span class="sxs-lookup"><span data-stu-id="9b37f-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="9b37f-169">**Správa verzí**: každý balíček satelitní musí mít závislost přesnou verzi na primární balíčku.</span><span class="sxs-lookup"><span data-stu-id="9b37f-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="9b37f-170">To znamená, že aktualizace primární balíčku může vyžadovat aktualizaci všechny satelitní balíčky, i v případě, že prostředky nezměnila.</span><span class="sxs-lookup"><span data-stu-id="9b37f-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
