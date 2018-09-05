---
title: Poznámky k verzi 2.5 NuGet
description: Zpráva k vydání verze pro NuGet 2.5 včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550480"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="55672-103">Poznámky k verzi 2.5 NuGet</span><span class="sxs-lookup"><span data-stu-id="55672-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="55672-104">[Zpráva k vydání verze NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [zpráva k vydání verze NuGet 2.6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="55672-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="55672-105">25. dubna 2013 byla vydána NuGet 2.5.</span><span class="sxs-lookup"><span data-stu-id="55672-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="55672-106">Tato verze byla tak velká, jsme popisovač compelled přeskočit verze 2.3 a 2.4!</span><span class="sxs-lookup"><span data-stu-id="55672-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="55672-107">Do dnešního dne, jedná se o nejvyšší verzi už nějakou dobu NuGet, se přes [160 pracovní položky](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) ve vydané verzi.</span><span class="sxs-lookup"><span data-stu-id="55672-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="55672-108">Potvrzení</span><span class="sxs-lookup"><span data-stu-id="55672-108">Acknowledgements</span></span>

<span data-ttu-id="55672-109">Rádi bychom vám chceme poděkovat následující externí přispěvatele pro své důležité příspěvky na NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="55672-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="55672-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="55672-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="55672-111">[#2847](https://nuget.codeplex.com/workitem/2847) – přidání MonoAndroid MonoTouch a MonoMac do seznamu známých cílové rozhraní framework identifikátory.</span><span class="sxs-lookup"><span data-stu-id="55672-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="55672-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="55672-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="55672-113">[#2865](https://nuget.codeplex.com/workitem/2865) -Opravte pravopis `NuGet.targets` pro velká a malá písmena operačního systému</span><span class="sxs-lookup"><span data-stu-id="55672-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="55672-114">[David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="55672-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="55672-115">Sestavit řešení sestavit v Mono.</span><span class="sxs-lookup"><span data-stu-id="55672-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="55672-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="55672-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="55672-117">Opravte testování částí v Mono.</span><span class="sxs-lookup"><span data-stu-id="55672-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="55672-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="55672-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="55672-119">[#2920](https://nuget.codeplex.com/workitem/2920) -pack příkaz nuget.exe nešíří vlastnosti nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="55672-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="55672-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="55672-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="55672-121">[#1511](https://nuget.codeplex.com/workitem/1511) – upravit XML kód pro zpracování zachovat formátování.</span><span class="sxs-lookup"><span data-stu-id="55672-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="55672-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="55672-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="55672-123">Přidat rozpoznaná slova do vlastního slovníku umožňující build.cmd proběhla úspěšně.</span><span class="sxs-lookup"><span data-stu-id="55672-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="55672-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="55672-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="55672-125">Opravte testů jednotek při spuštění v lokalizovaných VS.</span><span class="sxs-lookup"><span data-stu-id="55672-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="55672-126">Garetha Evans</span><span class="sxs-lookup"><span data-stu-id="55672-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="55672-127">Extrahované rozhraní z PackageService</span><span class="sxs-lookup"><span data-stu-id="55672-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="55672-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="55672-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="55672-129">[#936](https://nuget.codeplex.com/workitem/936) -řešit závislosti projektu při balení</span><span class="sxs-lookup"><span data-stu-id="55672-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="55672-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="55672-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="55672-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) – podpora vymazat Text heslo při ukládání přihlašovacích údajů ke zdroji balíčku v souborech nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="55672-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="55672-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="55672-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="55672-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package opravit Nápověda popis</span><span class="sxs-lookup"><span data-stu-id="55672-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="55672-134">Tyto jednotlivce vážíme také pro hledání chyb s NuGet 2.5 Beta nebo RC, která byla schválena a opravena dříve než ve finální verzi:</span><span class="sxs-lookup"><span data-stu-id="55672-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="55672-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="55672-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="55672-136">[#3200](https://nuget.codeplex.com/workitem/3200) – MSTest vs15.6.0 nejnovější NuGet 2.4 a 2,5 sestavení</span><span class="sxs-lookup"><span data-stu-id="55672-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="55672-137">Důležité funkce ve verzi</span><span class="sxs-lookup"><span data-stu-id="55672-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="55672-138">Povolit uživatelům přepsat soubory obsahu, které již existují.</span><span class="sxs-lookup"><span data-stu-id="55672-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="55672-139">Jedna z nejžádanějších funkcí celou dobu se stále možnost přepsat soubory obsahu, které již existují na disku, obsažen v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="55672-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="55672-140">Od verze NuGet 2.5, jsou označeny tyto konflikty a zobrazí se výzva k přepsání souborů, zatímco dříve byly tyto soubory vždy přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="55672-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Přepsat soubory obsahu](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="55672-142">"nuget.exe aktualizace" a "Install-Package", teď mají novou možnost '-FileConflictAction "můžete nastavit některé výchozí pro scénáře, příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="55672-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="55672-143">Nastavte výchozí akce, soubor z balíčku již existuje v na cílový projekt.</span><span class="sxs-lookup"><span data-stu-id="55672-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="55672-144">Nastavte na "Přepsat" vždy přepsat soubory.</span><span class="sxs-lookup"><span data-stu-id="55672-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="55672-145">Chcete-li přeskočit soubory nastavena na hodnotu 'Ignorovat'.</span><span class="sxs-lookup"><span data-stu-id="55672-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="55672-146">Pokud není zadán, bude zadání jednotlivých konfliktních souborů.</span><span class="sxs-lookup"><span data-stu-id="55672-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="55672-147">Automatický import MSBuild cíle a soubory vlastností</span><span class="sxs-lookup"><span data-stu-id="55672-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="55672-148">Na nejvyšší úrovni balíčku NuGet se vytvořila nová složka konvenční.</span><span class="sxs-lookup"><span data-stu-id="55672-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="55672-149">Jako partnera, který `\lib`, `\content`, a `\tools`, nyní můžete zahrnout `\build` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="55672-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="55672-150">V této složce, můžete umístit dva soubory se přiděleny pevně určené názvy, `{packageid}.targets` nebo `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="55672-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="55672-151">Tyto dva soubory mohou být buď přímo v rámci `build` nebo ve složkách specifické pro architekturu, stejně jako ostatní složky.</span><span class="sxs-lookup"><span data-stu-id="55672-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="55672-152">Pravidlo pro výběr složky nejlépe odpovídající framework je přesně stejné jako ty.</span><span class="sxs-lookup"><span data-stu-id="55672-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="55672-153">Při instalaci balíčku NuGet se soubory \build přidá MSBuild `<Import>` element v souboru projektu, přejdete `.targets` a `.props` soubory.</span><span class="sxs-lookup"><span data-stu-id="55672-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="55672-154">`.props` Přidá soubor v horní části, že `.targets` přidá soubor do dolní části.</span><span class="sxs-lookup"><span data-stu-id="55672-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="55672-155">Zadejte jiné odkazy na platformě pomocí `<References/>` – element</span><span class="sxs-lookup"><span data-stu-id="55672-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="55672-156">Před 2.5 v `.nuspec` souboru, uživatele můžete pouze zadat odkaz na soubory, přidat pro všechna rozhraní.</span><span class="sxs-lookup"><span data-stu-id="55672-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="55672-157">Teď s touto novou funkcí v 2.5, lze vytvářet uživatele `<reference/>` – element pro každou podporovanou platformu, například:</span><span class="sxs-lookup"><span data-stu-id="55672-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="55672-158">Tady je postup jak NuGet přidá odkazy na projekty na základě `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="55672-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="55672-159">Najít `lib` složku, která je vhodné pro cílovou architekturu a získat seznam sestavení z této složky</span><span class="sxs-lookup"><span data-stu-id="55672-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="55672-160">Samostatně najít odkazy na skupinu, která je vhodná pro cílovou architekturu a získat seznam sestavení z dané skupiny.</span><span class="sxs-lookup"><span data-stu-id="55672-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="55672-161">Referenční skupiny bez zadaná Cílová architektura je skupině pro použití náhradní lokality.</span><span class="sxs-lookup"><span data-stu-id="55672-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="55672-162">Zjistí průnik dvou seznamů a použít je jako odkazy pro přidání</span><span class="sxs-lookup"><span data-stu-id="55672-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="55672-163">Tato nová funkce vám umožní autory balíčku používat funkci odkazy na používání podmnožiny sestavení pro různé platformy, když byste jinak potřebovali pro přenesení duplicitní sestavení ve více `lib` složek.</span><span class="sxs-lookup"><span data-stu-id="55672-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="55672-164">Poznámka: musí v současné době používáte nuget.exe pack pro použití této funkce; NuGet – Průzkumník balíčků ještě nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="55672-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="55672-165">Aktualizovat všechny tlačítko pro aktualizaci všech balíčků najednou</span><span class="sxs-lookup"><span data-stu-id="55672-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="55672-166">Řada z vás vědět o rutině prostředí PowerShell "Update-Package" aktualizovat všechny balíčky; Nyní je snadný způsob, jak to provést prostřednictvím uživatelského rozhraní i.</span><span class="sxs-lookup"><span data-stu-id="55672-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="55672-167">Vyzkoušet tuto funkci:</span><span class="sxs-lookup"><span data-stu-id="55672-167">To try this feature out:</span></span>

1. <span data-ttu-id="55672-168">Vytvoření nové aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="55672-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="55672-169">Spuštění dialogového okna spravovat balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="55672-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="55672-170">Vyberte možnost aktualizace.</span><span class="sxs-lookup"><span data-stu-id="55672-170">Select 'Updates'</span></span>
1. <span data-ttu-id="55672-171">Klikněte na tlačítko Aktualizovat vše</span><span class="sxs-lookup"><span data-stu-id="55672-171">Click the 'Update All' button</span></span>

![Aktualizovat všechny tlačítko v dialogovém okně](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="55672-173">Vylepšené projektu odkaz na podporu pro nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="55672-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="55672-174">Nyní nuget.exe pack příkaz procesy odkazované projekty pomocí následujících pravidel:</span><span class="sxs-lookup"><span data-stu-id="55672-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="55672-175">Pokud má odkazovaného projektu odpovídající `.nuspec` souboru, například existuje soubor s názvem `proj1.nuspec` ve stejné složce jako `proj1.csproj`, pak tento projekt je přidán jako závislost pro balíček s použitím id a verze číst z `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="55672-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="55672-176">V opačném případě jsou spojeny soubory odkazovaného projektu do balíčku.</span><span class="sxs-lookup"><span data-stu-id="55672-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="55672-177">Potom projekty odkazuje tento projekt se zpracuje pomocí způsobu rekurzivně sames pravidla.</span><span class="sxs-lookup"><span data-stu-id="55672-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="55672-178">Všechny knihovny DLL, `.pdb`, a `.exe` se přidají soubory.</span><span class="sxs-lookup"><span data-stu-id="55672-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="55672-179">Všechny ostatní soubory obsahu budou přidány.</span><span class="sxs-lookup"><span data-stu-id="55672-179">All other content files are added.</span></span>
1. <span data-ttu-id="55672-180">Všechny závislosti jsou sloučeny.</span><span class="sxs-lookup"><span data-stu-id="55672-180">All dependencies are merged.</span></span>

<span data-ttu-id="55672-181">To umožňuje odkazovaného projektu jsou považovány za závislosti, dojde-li `.nuspec` souboru, v opačném případě se stává součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="55672-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="55672-182">Další podrobnosti tady: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="55672-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="55672-183">Přidání vlastnosti "Minimální verze NuGet" k balíčkům</span><span class="sxs-lookup"><span data-stu-id="55672-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="55672-184">Nový atribut metadat nazývá 'minClientVersion' můžete teď určit minimální verzi klienta NuGet využívat balíček nepotřebujete k tomu.</span><span class="sxs-lookup"><span data-stu-id="55672-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="55672-185">Tato funkce pomáhá autora balíčku k určení, že balíček bude fungovat až po konkrétní verzi balíčku nuget.</span><span class="sxs-lookup"><span data-stu-id="55672-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="55672-186">Jako nové `.nuspec` funkce byly přidány po NuGet 2.5 balíčky budou moci deklarace identity minimální verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="55672-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="55672-187">Pokud má uživatel 2.5 NuGet, nainstalované a balíček je identifikován jako vyžadující 2.6, uživateli zprávu, že nebudou instalovat balíček dostanou vizuální prvky.</span><span class="sxs-lookup"><span data-stu-id="55672-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="55672-188">Uživatel pak by se zobrazil pokyn k aktualizaci jejich verze balíčku nuget.</span><span class="sxs-lookup"><span data-stu-id="55672-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="55672-189">To bude vylepšují existující prostředí, kde začít balíčky nainstalovat, ale dojde k selhání oznamující, že byl identifikován Nerozpoznaná verze schématu.</span><span class="sxs-lookup"><span data-stu-id="55672-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="55672-190">Během instalace balíčku už zbytečně aktualizovat závislosti</span><span class="sxs-lookup"><span data-stu-id="55672-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="55672-191">Před NuGet 2.5 Pokud nainstaloval balíček, který závisí na balíčku již nainstalována v projektu, závislost by aktualizovat jako součást nové instalace i v případě, že stávající verzi vyhověla závislosti.</span><span class="sxs-lookup"><span data-stu-id="55672-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="55672-192">Od verze NuGet 2.5 při splnění závislostí verze se už, nebudou aktualizovány závislost během instalace dalších balíčků.</span><span class="sxs-lookup"><span data-stu-id="55672-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="55672-193">**Scénář:**</span><span class="sxs-lookup"><span data-stu-id="55672-193">**The scenario:**</span></span>

1. <span data-ttu-id="55672-194">Zdrojové úložiště obsahuje balíček B verze 1.0.0 a 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="55672-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="55672-195">Obsahuje také balíček A závislý na B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="55672-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="55672-196">Předpokládejme, že aktuální projekt již obsahuje balíček B verze 1.0.0 nainstalované.</span><span class="sxs-lookup"><span data-stu-id="55672-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="55672-197">Chcete nyní nainstalovat balíček A.</span><span class="sxs-lookup"><span data-stu-id="55672-197">Now you want to install package A.</span></span>

<span data-ttu-id="55672-198">**Ve Správci NuGet 2.2 a starší:**</span><span class="sxs-lookup"><span data-stu-id="55672-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="55672-199">Při instalaci A balíčku NuGet se automatické aktualizace B 1.0.2, i v případě, že stávající verze 1.0.0 již splňuje omezení verze závislosti, což je > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="55672-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="55672-200">**Ve Správci NuGet 2.5 a novější:**</span><span class="sxs-lookup"><span data-stu-id="55672-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="55672-201">NuGet už aktualizuje B, protože rozpozná, že stávající verze 1.0.0 splňuje omezení verze závislosti.</span><span class="sxs-lookup"><span data-stu-id="55672-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="55672-202">Další informace o této změně najdete podrobné [pracovní položku](http://nuget.codeplex.com/workitem/1681) a také související [diskusní vlákna](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="55672-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="55672-203">nuget.exe výstupů požadavky http s podrobnou úroveň podrobností</span><span class="sxs-lookup"><span data-stu-id="55672-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="55672-204">Pokud řešíte nuget.exe nebo právě zvědaví jaké požadavky HTTP jsou prováděny během operace, "-podrobností podrobné" přepínač se teď výstup všechny požadavky HTTP, které jsou vytvořené.</span><span class="sxs-lookup"><span data-stu-id="55672-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Výstup protokolu HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="55672-206">nuget.exe push nyní podporuje UNC a složku zdroje</span><span class="sxs-lookup"><span data-stu-id="55672-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="55672-207">Před NuGet 2.5 Pokud se pokus o spuštění "nuget.exe push" ke zdroji balíčku na základě cesty UNC nebo místní složku, že nasdílení změn selže.</span><span class="sxs-lookup"><span data-stu-id="55672-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="55672-208">Díky funkci naposledy přidané hierarchické konfigurace má stát běžné, že nuget.exe potřebovat cílit na zdroji UNC nebo složku nebo založené na protokolu HTTP Galerie NuGet.</span><span class="sxs-lookup"><span data-stu-id="55672-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="55672-209">Od verze NuGet 2.5, pokud nuget.exe identifikuje zdroj UNC nebo složku, provede kopírování souborů do zdroje.</span><span class="sxs-lookup"><span data-stu-id="55672-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="55672-210">Následující příkaz bude nyní fungovat:</span><span class="sxs-lookup"><span data-stu-id="55672-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="55672-211">nuget.exe podporuje explicitně zadán konfigurační soubory</span><span class="sxs-lookup"><span data-stu-id="55672-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="55672-212">podporují novou nuget.exe příkazy, které teď přístup ke konfiguraci (všechny s výjimkou "specifikace" a "aktualizací Service pack") "-ConfigFile' možnost, která vynutí konkrétní konfigurační soubor, který se má použít místo výchozí konfigurační soubor v umístění % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="55672-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="55672-213">Příklad:</span><span class="sxs-lookup"><span data-stu-id="55672-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="55672-214">Podpora pro nativní projekty</span><span class="sxs-lookup"><span data-stu-id="55672-214">Support for Native projects</span></span>

<span data-ttu-id="55672-215">NuGet 2.5 nástroje NuGet se teď k dispozici u nativních projektů v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55672-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="55672-216">Očekáváme, že většina nativní balíčky budou využívat funkci MSBuild importy výše, pomocí nástroje, vytvořené [CoApp projektu](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="55672-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="55672-217">Další informace najdete v článku [podrobné informace o nástroji](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na webu coapp.org.</span><span class="sxs-lookup"><span data-stu-id="55672-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="55672-218">Název cílového rozhraní framework "nativní" se používá pro balíčky, které mají zahrnout soubory \build \content a \tools při instalaci balíčku do nativního projektu.</span><span class="sxs-lookup"><span data-stu-id="55672-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="55672-219">\`Lib "složky se nepoužívá pro nativní projekty.</span><span class="sxs-lookup"><span data-stu-id="55672-219">The \`lib` folder is not used for native projects.</span></span>
