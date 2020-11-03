---
title: Zpráva k vydání verze NuGet 2,5
description: Poznámky k verzi pro NuGet 2,5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237077"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="eafcf-103">Zpráva k vydání verze NuGet 2,5</span><span class="sxs-lookup"><span data-stu-id="eafcf-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="eafcf-104">Poznámky k verzi [NuGet 2.2.1](../release-notes/nuget-2.2.1.md)  |  Zpráva k [vydání verze NuGet 2,6](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="eafcf-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="eafcf-105">NuGet 2,5 byl vydán 25. dubna 2013.</span><span class="sxs-lookup"><span data-stu-id="eafcf-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="eafcf-106">Tato verze byla tak velká, budeme nuceni proto přeskočit verze 2,3 a 2,4!</span><span class="sxs-lookup"><span data-stu-id="eafcf-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="eafcf-107">To je největší vydání, které jsme měli pro NuGet, s více než [160 pracovními položkami](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) v této verzi.</span><span class="sxs-lookup"><span data-stu-id="eafcf-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="eafcf-108">Poděkování</span><span class="sxs-lookup"><span data-stu-id="eafcf-108">Acknowledgements</span></span>

<span data-ttu-id="eafcf-109">Rádi bychom pro své významné příspěvky k NuGet 2,5 měli Děkujeme za tyto externí přispěvatele:</span><span class="sxs-lookup"><span data-stu-id="eafcf-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="eafcf-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="eafcf-111">[#2847](https://nuget.codeplex.com/workitem/2847) – přidejte MonoAndroid, MonoTouch a MonoMac do seznamu známých identifikátorů cílových rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="eafcf-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="eafcf-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="eafcf-113">[#2865](https://nuget.codeplex.com/workitem/2865) – Oprava pravopisu `NuGet.targets` pro operační systém s rozlišováním velkých a malých písmen</span><span class="sxs-lookup"><span data-stu-id="eafcf-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="eafcf-114">[David Fowlera](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="eafcf-115">Zpřístupněte řešení na mono.</span><span class="sxs-lookup"><span data-stu-id="eafcf-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="eafcf-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="eafcf-117">Opravte selhání testů jednotek mono.</span><span class="sxs-lookup"><span data-stu-id="eafcf-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="eafcf-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="eafcf-119">příkaz [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack nešíří vlastnosti do nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="eafcf-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="eafcf-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="eafcf-121">[#1511](https://nuget.codeplex.com/workitem/1511) – upravený kód pro zpracování XML pro zachování formátování.</span><span class="sxs-lookup"><span data-stu-id="eafcf-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="eafcf-122">[Adam petrpo](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="eafcf-123">Do vlastního slovníku byla přidána rozpoznaná slova, která umožňují úspěšné sestavení. cmd.</span><span class="sxs-lookup"><span data-stu-id="eafcf-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="eafcf-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="eafcf-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="eafcf-125">Opravte testy jednotek při spuštění v lokalizovaných VS.</span><span class="sxs-lookup"><span data-stu-id="eafcf-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="eafcf-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="eafcf-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="eafcf-127">Rozhraní extrahované z PackageService</span><span class="sxs-lookup"><span data-stu-id="eafcf-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="eafcf-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="eafcf-129">[#936](https://nuget.codeplex.com/workitem/936) – zpracovat závislosti projektu při balení</span><span class="sxs-lookup"><span data-stu-id="eafcf-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="eafcf-130">[Xavier denákler](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="eafcf-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) – při ukládání přihlašovacích údajů ke zdroji balíčků do souborů NuGet. cofig se nepodporuje heslo pro nešifrovaný text.</span><span class="sxs-lookup"><span data-stu-id="eafcf-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="eafcf-132">[James obsazení](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="eafcf-133">[#3190](http://nuget.codeplex.com/workitem/3190)popis #3190 [#3191](http://nuget.codeplex.com/workitem/3191) opravy Get-Package</span><span class="sxs-lookup"><span data-stu-id="eafcf-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="eafcf-134">Oceňujeme také následující jednotlivce pro vyhledávání chyb s NuGet 2,5 beta/RC, které byly schváleny a opraveny před poslední verzí:</span><span class="sxs-lookup"><span data-stu-id="eafcf-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="eafcf-135">[Adam zeď](https://www.codeplex.com/site/users/view/CodeChief) ( [@CodeChief](https://twitter.com/codechief) )</span><span class="sxs-lookup"><span data-stu-id="eafcf-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="eafcf-136">[#3200](https://nuget.codeplex.com/workitem/3200) – MSTest se přerušila s posledními sestaveními NuGet 2,4 a 2,5.</span><span class="sxs-lookup"><span data-stu-id="eafcf-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="eafcf-137">Významné funkce v této verzi</span><span class="sxs-lookup"><span data-stu-id="eafcf-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="eafcf-138">Umožní uživatelům přepsat soubory obsahu, které už existují.</span><span class="sxs-lookup"><span data-stu-id="eafcf-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="eafcf-139">Jednou z nejvíce požadovaných funkcí všech možností je možnost přepsat soubory obsahu, které už na disku existují, když jsou zahrnuté v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="eafcf-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="eafcf-140">Počínaje verzí NuGet 2,5 se tyto konflikty identifikují a budete vyzváni k přepsání souborů, zatímco předchozí soubory byly vždycky přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="eafcf-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Přepsat soubory obsahu](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="eafcf-142">nuget.exe Update a Install-Package teď mají novou možnost-FileConflictAction pro nastavení některých výchozích možností pro scénáře příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="eafcf-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="eafcf-143">Nastaví výchozí akci, když soubor z balíčku již v cílovém projektu existuje.</span><span class="sxs-lookup"><span data-stu-id="eafcf-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="eafcf-144">Pokud chcete soubory vždycky přepsat, nastavte na overwrite.</span><span class="sxs-lookup"><span data-stu-id="eafcf-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="eafcf-145">Pokud chcete přeskočit soubory, nastavte na Ignore.</span><span class="sxs-lookup"><span data-stu-id="eafcf-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="eafcf-146">Pokud není zadaný, zobrazí se výzva k zadání každého kolidujícího souboru.</span><span class="sxs-lookup"><span data-stu-id="eafcf-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="eafcf-147">Automatický import cílů a souborů props nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="eafcf-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="eafcf-148">Na nejvyšší úrovni balíčku NuGet se vytvořila nová konvenční složka.</span><span class="sxs-lookup"><span data-stu-id="eafcf-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="eafcf-149">Jako partner `\lib` , `\content` a `\tools` můžete teď do `\build` balíčku přidat složku.</span><span class="sxs-lookup"><span data-stu-id="eafcf-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="eafcf-150">V rámci této složky můžete umístit dva soubory s pevnými názvy `{packageid}.targets` nebo `{packageid}.props` .</span><span class="sxs-lookup"><span data-stu-id="eafcf-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="eafcf-151">Tyto dva soubory mohou být buď přímo pod, `build` nebo pod rámec rozhraní specifického pro rozhraní, stejně jako ostatní složky.</span><span class="sxs-lookup"><span data-stu-id="eafcf-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="eafcf-152">Pravidlo pro vybírání složky rozhraní, které nejlépe odpovídá, je přesně stejné jako v těchto.</span><span class="sxs-lookup"><span data-stu-id="eafcf-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="eafcf-153">Když NuGet nainstaluje balíček se soubory \Build, přidá `<Import>` do souboru projektu element MSBuild, který odkazuje na `.targets` `.props` soubory a.</span><span class="sxs-lookup"><span data-stu-id="eafcf-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="eafcf-154">`.props`Soubor se přidá v horní části, zatímco `.targets` soubor se přidá do dolní části.</span><span class="sxs-lookup"><span data-stu-id="eafcf-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="eafcf-155">Zadejte různé odkazy na platformu pomocí `<References/>` elementu.</span><span class="sxs-lookup"><span data-stu-id="eafcf-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="eafcf-156">Před 2,5, v `.nuspec` souboru může uživatel určit pouze referenční soubory, které mají být přidány pro všechna rozhraní.</span><span class="sxs-lookup"><span data-stu-id="eafcf-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="eafcf-157">Nyní s touto novou funkcí v 2,5 může uživatel vytvořit `<reference/>` element pro každou podporovanou platformu, například:</span><span class="sxs-lookup"><span data-stu-id="eafcf-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="eafcf-158">Tady je postup, jak NuGet přidává odkazy na projekty založené na `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="eafcf-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="eafcf-159">Vyhledejte `lib` složku, která je vhodná pro cílovou architekturu a získejte seznam sestavení z této složky.</span><span class="sxs-lookup"><span data-stu-id="eafcf-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="eafcf-160">Samostatně najít skupinu odkazů, která je vhodná pro cílovou architekturu a získat seznam sestavení z této skupiny.</span><span class="sxs-lookup"><span data-stu-id="eafcf-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="eafcf-161">Referenční skupina bez cílového rozhraní je určená pro záložní skupinu.</span><span class="sxs-lookup"><span data-stu-id="eafcf-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="eafcf-162">Vyhledejte průnik dvou seznamů a použijte je jako odkazy na přidání.</span><span class="sxs-lookup"><span data-stu-id="eafcf-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="eafcf-163">Tato nová funkce umožní autorům balíčků použít funkci References k použití dílčích sad sestavení v různých rozhraních, pokud by jinak musela přenášet duplicitní sestavení ve více `lib` složkách.</span><span class="sxs-lookup"><span data-stu-id="eafcf-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="eafcf-164">Poznámka: k použití této funkce je nutné, abyste používali sadu nuget.exe Pack. Průzkumník balíčků NuGet ho ještě nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="eafcf-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="eafcf-165">Tlačítko Aktualizovat vše, aby bylo možné aktualizovat všechny balíčky najednou</span><span class="sxs-lookup"><span data-stu-id="eafcf-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="eafcf-166">Spousta informací o rutině Update-Package prostředí PowerShell pro aktualizaci všech balíčků; Teď je to snadný způsob, jak to provést také v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="eafcf-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="eafcf-167">Tuto funkci můžete vyzkoušet takto:</span><span class="sxs-lookup"><span data-stu-id="eafcf-167">To try this feature out:</span></span>

1. <span data-ttu-id="eafcf-168">Vytvoření nové aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="eafcf-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="eafcf-169">Spuštění dialogového okna spravovat balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="eafcf-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="eafcf-170">Vybrat aktualizace</span><span class="sxs-lookup"><span data-stu-id="eafcf-170">Select 'Updates'</span></span>
1. <span data-ttu-id="eafcf-171">Klikněte na tlačítko Aktualizovat vše.</span><span class="sxs-lookup"><span data-stu-id="eafcf-171">Click the 'Update All' button</span></span>

![Tlačítko Aktualizovat vše v dialogovém okně](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="eafcf-173">Vylepšená podpora odkazů na projekt pro sadu nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="eafcf-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="eafcf-174">Nyní nuget.exe procesy příkazu Pack na odkazované projekty s následujícími pravidly:</span><span class="sxs-lookup"><span data-stu-id="eafcf-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="eafcf-175">Pokud má odkazovaný projekt odpovídající `.nuspec` soubor, například soubor `proj1.nuspec` s názvem ve stejné složce jako `proj1.csproj` , pak je tento projekt přidán jako závislost k balíčku pomocí ID a verze načtené ze `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="eafcf-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="eafcf-176">V opačném případě jsou soubory odkazovaného projektu seskupeny do balíčku.</span><span class="sxs-lookup"><span data-stu-id="eafcf-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="eafcf-177">Projekty, na které se odkazuje tento projekt, budou zpracovávány pomocí rekurzivních pravidel.</span><span class="sxs-lookup"><span data-stu-id="eafcf-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="eafcf-178">`.pdb`Jsou přidány všechny soubory DLL, a `.exe` .</span><span class="sxs-lookup"><span data-stu-id="eafcf-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="eafcf-179">Všechny ostatní soubory obsahu jsou přidány.</span><span class="sxs-lookup"><span data-stu-id="eafcf-179">All other content files are added.</span></span>
1. <span data-ttu-id="eafcf-180">Všechny závislosti jsou sloučeny.</span><span class="sxs-lookup"><span data-stu-id="eafcf-180">All dependencies are merged.</span></span>

<span data-ttu-id="eafcf-181">To umožňuje, aby odkazovaný projekt byl považován za závislost, pokud je `.nuspec` soubor, v opačném případě se jedná o součást balíčku.</span><span class="sxs-lookup"><span data-stu-id="eafcf-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="eafcf-182">Další podrobnosti najdete tady: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="eafcf-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="eafcf-183">Přidejte do balíčků vlastnost minimální verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="eafcf-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="eafcf-184">Nový atribut metadat nazvaný "minClientVersion" teď může indikovat minimální verzi klienta NuGet, která se vyžaduje ke spotřebování balíčku.</span><span class="sxs-lookup"><span data-stu-id="eafcf-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="eafcf-185">Tato funkce pomáhá autorovi balíčku určit, že balíček bude fungovat až po konkrétní verzi NuGetu.</span><span class="sxs-lookup"><span data-stu-id="eafcf-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="eafcf-186">`.nuspec`Po přidání nových funkcí po NuGet 2,5 budou balíčky schopné vyžádat si minimální verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="eafcf-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="eafcf-187">Pokud má uživatel nainstalovanou NuGet 2,5 a balíček je identifikovaný jako vyžadování 2,6, budou se uživatelům, kteří budou k balíčku instalovat, přidávat vizuální pomůcky.</span><span class="sxs-lookup"><span data-stu-id="eafcf-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="eafcf-188">Uživatel pak bude s asistencí aktualizovat verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="eafcf-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="eafcf-189">Tím se vylepšit existující prostředí, ve kterém se balíčky začnou instalovat, ale pak selže, což znamená, že byla zjištěna Nerozpoznaná verze schématu.</span><span class="sxs-lookup"><span data-stu-id="eafcf-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="eafcf-190">Závislosti se už nemusejí aktualizovat při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="eafcf-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="eafcf-191">Po instalaci balíčku NuGet 2,5, který je závislý na balíčku, který už je v projektu nainstalovaný, by se závislost aktualizovala jako součást nové instalace, i když existující verze splnila závislost.</span><span class="sxs-lookup"><span data-stu-id="eafcf-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="eafcf-192">Počínaje verzí NuGet 2,5, pokud je už verze závislosti splněná, závislost se během dalších instalací balíčku neaktualizuje.</span><span class="sxs-lookup"><span data-stu-id="eafcf-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="eafcf-193">**Scénář:**</span><span class="sxs-lookup"><span data-stu-id="eafcf-193">**The scenario:**</span></span>

1. <span data-ttu-id="eafcf-194">Zdrojové úložiště obsahuje balíček B s verzí 1.0.0 a 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="eafcf-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="eafcf-195">Obsahuje také balíček A, který má závislost na B (>= 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="eafcf-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="eafcf-196">Předpokládejme, že aktuální projekt již má nainstalován balíček B verze 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="eafcf-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="eafcf-197">Nyní chcete nainstalovat balíček A.</span><span class="sxs-lookup"><span data-stu-id="eafcf-197">Now you want to install package A.</span></span>

<span data-ttu-id="eafcf-198">**V NuGet 2,2 a starší:**</span><span class="sxs-lookup"><span data-stu-id="eafcf-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="eafcf-199">Při instalaci balíčku A se NuGet automaticky aktualizuje B na 1.0.2, i když existující verze 1.0.0 už splňuje omezení verze závislosti, což je >= 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="eafcf-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="eafcf-200">**V NuGet 2,5 a novějších verzích:**</span><span class="sxs-lookup"><span data-stu-id="eafcf-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="eafcf-201">NuGet už nebude aktualizovat B, protože detekuje, že stávající verze 1.0.0 splňuje omezení verze závislosti.</span><span class="sxs-lookup"><span data-stu-id="eafcf-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="eafcf-202">Pro další informace o této změně si přečtěte podrobnou [pracovní položku](http://nuget.codeplex.com/workitem/1681) a související [diskusní vlákno](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="eafcf-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="eafcf-203">nuget.exe výstup požadavků HTTP s detailní podrobností</span><span class="sxs-lookup"><span data-stu-id="eafcf-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="eafcf-204">Pokud řešíte řešení potíží nuget.exe nebo stačí zajímá, jaké požadavky HTTP jsou během operací provedeny, přepínač "-detailed Details" nyní vypíše všechny provedené požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="eafcf-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Výstup HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="eafcf-206">nuget.exe push teď podporuje zdroje ve formátu UNC a složky</span><span class="sxs-lookup"><span data-stu-id="eafcf-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="eafcf-207">Pokud se při pokusu o spuštění příkazu ' nuget.exe push ' do zdroje balíčku na základě cesty UNC nebo místní složky pokusíte spustit příkaz ' push ', nabízená oznámení selže. 2,5</span><span class="sxs-lookup"><span data-stu-id="eafcf-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="eafcf-208">Díky funkci nedávno přidané hierarchické konfigurace se stala společná nuget.exe, aby bylo potřeba cílit buď na zdroj UNC nebo složku, nebo na galerii NuGet založenou na protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="eafcf-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="eafcf-209">Pokud nuget.exe identifikuje zdroj UNC nebo složky, počínaje verzí NuGet 2,5, provede kopírování souborů do zdroje.</span><span class="sxs-lookup"><span data-stu-id="eafcf-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="eafcf-210">Nyní bude fungovat následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="eafcf-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="eafcf-211">nuget.exe podporuje explicitně zadané konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="eafcf-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="eafcf-212">nuget.exe příkazy, které přistupují ke konfiguraci (vše kromě "spec" a "Pack"), teď podporují novou možnost-ConfigFile, která vynutí použití konkrétního konfiguračního souboru místo výchozího konfiguračního souboru v% data% \nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="eafcf-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="eafcf-213">Příklad:</span><span class="sxs-lookup"><span data-stu-id="eafcf-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="eafcf-214">Podpora pro nativní projekty</span><span class="sxs-lookup"><span data-stu-id="eafcf-214">Support for Native projects</span></span>

<span data-ttu-id="eafcf-215">S NuGet 2,5 je teď k dispozici nástroj NuGet pro nativní projekty v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eafcf-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="eafcf-216">Očekáváme, že většina nativních balíčků bude používat funkci importu MSBuild výše, a to pomocí nástroje vytvořeného [projektem CoApp](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="eafcf-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="eafcf-217">Další informace najdete v [podrobnostech o nástroji](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na webu coapp.org.</span><span class="sxs-lookup"><span data-stu-id="eafcf-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="eafcf-218">V případě, že se balíček nainstaluje do nativního projektu, zavádí se pro balíčky, které obsahují soubory v \Build, \Content a \Tools, název cílového rozhraní Framework "Native".</span><span class="sxs-lookup"><span data-stu-id="eafcf-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="eafcf-219">\`Složka lib se nepoužívá pro nativní projekty.</span><span class="sxs-lookup"><span data-stu-id="eafcf-219">The \`lib\` folder is not used for native projects.</span></span>
