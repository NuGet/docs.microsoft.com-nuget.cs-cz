---
title: Poznámky k verzi 2,5 NuGet
description: Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 2.5 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: accea5033e44927259537b5047a4a821babc6146
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="674b0-103">Poznámky k verzi 2,5 NuGet</span><span class="sxs-lookup"><span data-stu-id="674b0-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="674b0-104">[Poznámky k verzi NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 poznámky k verzi](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="674b0-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="674b0-105">NuGet 2.5 byla vydána 25. dubna 2013.</span><span class="sxs-lookup"><span data-stu-id="674b0-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="674b0-106">Tato verze byla tak velká, jsme popisovač compelled tak, aby přeskočil verze 2.3 a 2.4!</span><span class="sxs-lookup"><span data-stu-id="674b0-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="674b0-107">Dosud se největší verzi jsme jste měli pro NuGet, se přes [160 pracovní položky](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) ve verzi.</span><span class="sxs-lookup"><span data-stu-id="674b0-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="674b0-108">Potvrzení</span><span class="sxs-lookup"><span data-stu-id="674b0-108">Acknowledgements</span></span>

<span data-ttu-id="674b0-109">Rádi bychom se Děkujeme, že následující externí přispěvatele pro jejich významné příspěvky k NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="674b0-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="674b0-110">[ADAM Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="674b0-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="674b0-111">[#2847](https://nuget.codeplex.com/workitem/2847) -přidat MonoAndroid, MonoTouch a MonoMac do seznamu identifikátorů známé target framework.</span><span class="sxs-lookup"><span data-stu-id="674b0-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="674b0-112">[G. Aragoneses Andresu](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="674b0-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="674b0-113">[#2865](https://nuget.codeplex.com/workitem/2865) -Opravte pravopis `NuGet.targets` pro malá a velká písmena operačního systému</span><span class="sxs-lookup"><span data-stu-id="674b0-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="674b0-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="674b0-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="674b0-115">Ujistěte se, vychází z Mono řešení.</span><span class="sxs-lookup"><span data-stu-id="674b0-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="674b0-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="674b0-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="674b0-117">Testování částí v Mono opravte.</span><span class="sxs-lookup"><span data-stu-id="674b0-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="674b0-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="674b0-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="674b0-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe pack příkaz nešířily vlastností nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="674b0-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="674b0-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="674b0-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="674b0-121">[#1511](https://nuget.codeplex.com/workitem/1511) – upravit XML kód pro zpracování zachovat formátování.</span><span class="sxs-lookup"><span data-stu-id="674b0-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="674b0-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="674b0-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="674b0-123">Přidat rozpoznaný slova slovníku umožňující build.cmd proběhla úspěšně.</span><span class="sxs-lookup"><span data-stu-id="674b0-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="674b0-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="674b0-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="674b0-125">Opravte testů jednotek při spuštění v lokalizovaných VS.</span><span class="sxs-lookup"><span data-stu-id="674b0-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="674b0-126">Zařízení Evans Gareth</span><span class="sxs-lookup"><span data-stu-id="674b0-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="674b0-127">Extrahované rozhraní PackageService</span><span class="sxs-lookup"><span data-stu-id="674b0-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="674b0-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="674b0-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="674b0-129">[#936](https://nuget.codeplex.com/workitem/936) -zpracování závislosti projektu při balení</span><span class="sxs-lookup"><span data-stu-id="674b0-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="674b0-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="674b0-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="674b0-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -podpora vymazat Text heslo při ukládání přihlašovacích údajů zdroje balíčku v souborech nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="674b0-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="674b0-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="674b0-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="674b0-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) – popis opravte Get-Package nápovědy</span><span class="sxs-lookup"><span data-stu-id="674b0-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="674b0-134">Děkujeme také následující jednotlivce pro vyhledání chyby s NuGet 2.5 Beta nebo RC, které byly schválené a opravit dřív, než finální verzi:</span><span class="sxs-lookup"><span data-stu-id="674b0-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="674b0-135">[ADAM Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="674b0-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="674b0-136">[#3200](https://nuget.codeplex.com/workitem/3200) – Mstestu přerušený s nejnovější NuGet 2.4 a 2,5 sestavení</span><span class="sxs-lookup"><span data-stu-id="674b0-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="674b0-137">Upozorňují na důležité funkce ve verzi</span><span class="sxs-lookup"><span data-stu-id="674b0-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="674b0-138">Povolit uživatelům přepsat soubory obsahu, které již existují.</span><span class="sxs-lookup"><span data-stu-id="674b0-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="674b0-139">Jednou z nejžádanějších funkcí celou dobu byla možnost přepsat soubory obsahu, které již existují na disku, obsažen v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="674b0-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="674b0-140">Od verze NuGet 2.5, jsou identifikovány tyto konflikty a zobrazí se výzva k přepsání souborů, zatímco dříve byly tyto soubory vždy přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="674b0-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Přepsat soubory obsahu](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="674b0-142">'nuget.exe aktualizace' a 'Install-Package"teď mají novou možnost '-FileConflictAction, můžete nastavit některé výchozí pro scénáře příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="674b0-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="674b0-143">Nastavte výchozí akce, soubor z balíčku již existuje v cílové projektu.</span><span class="sxs-lookup"><span data-stu-id="674b0-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="674b0-144">Nastavte na "přepsat, aby vždy přepsat soubory.</span><span class="sxs-lookup"><span data-stu-id="674b0-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="674b0-145">Přeskočit soubory nastavena na hodnotu 'Ignorovat'.</span><span class="sxs-lookup"><span data-stu-id="674b0-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="674b0-146">Pokud není zadáno, zobrazí výzvu pro každý konfliktní soubor.</span><span class="sxs-lookup"><span data-stu-id="674b0-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="674b0-147">Automatické import MSBuild cíle a soubory props</span><span class="sxs-lookup"><span data-stu-id="674b0-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="674b0-148">Byla vytvořena konvenční novou složku na nejvyšší úrovni balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="674b0-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="674b0-149">Jako partnera, který `\lib`, `\content`, a `\tools`, teď můžete zahrnout `\build` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="674b0-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="674b0-150">V této složce, můžete umístit dva soubory s pevnou názvy `{packageid}.targets` nebo `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="674b0-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="674b0-151">Tyto dva soubory mohou být buď přímo `build` nebo pod konkrétní rozhraní složky stejně jako jiných složkách.</span><span class="sxs-lookup"><span data-stu-id="674b0-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="674b0-152">Pravidlo pro výběr nejlépe odpovídající složku je přesně stejné jako ty.</span><span class="sxs-lookup"><span data-stu-id="674b0-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="674b0-153">Při instalaci balíčku NuGet se soubory \build přidá MSBuild `<Import>` element v souboru projektu přejdete `.targets` a `.props` soubory.</span><span class="sxs-lookup"><span data-stu-id="674b0-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="674b0-154">`.props` Soubor přidán v horní části, zatímco `.targets` soubor přidán do dolní části.</span><span class="sxs-lookup"><span data-stu-id="674b0-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="674b0-155">Zadejte jiný odkazy na platformě pomocí `<References/>` – element</span><span class="sxs-lookup"><span data-stu-id="674b0-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="674b0-156">Před 2.5 v `.nuspec` souboru uživatele můžete jenom zadat referenčních souborů, který se má přidat pro všechny framework.</span><span class="sxs-lookup"><span data-stu-id="674b0-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="674b0-157">Teď pomocí této nové funkce v 2.5, můžete vytvořit uživatele `<reference/>` element pro každou podporovanou platformu, například:</span><span class="sxs-lookup"><span data-stu-id="674b0-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="674b0-158">Tady je postup pro jak NuGet přidá odkazy na projekty na základě `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="674b0-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="674b0-159">Najít `lib` složku, která je vhodná pro cílové rozhraní a získat seznam sestavení z této složky</span><span class="sxs-lookup"><span data-stu-id="674b0-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="674b0-160">Samostatně najít odkazuje na skupinu, která je vhodná pro cílové rozhraní a získat seznam sestavení z dané skupiny.</span><span class="sxs-lookup"><span data-stu-id="674b0-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="674b0-161">Referenční dokumentace skupina bez cílovém Frameworku, zadaný je záložní skupina.</span><span class="sxs-lookup"><span data-stu-id="674b0-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="674b0-162">Zjistí průnik dva seznamy a použít jej jako odkazy pro přidání</span><span class="sxs-lookup"><span data-stu-id="674b0-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="674b0-163">Tato nová funkce vám umožní použít funkci odkazy na používání podmnožiny sestavení pro různé architektury, když byste jinak potřebovali pro přenos duplicitní sestavení v několika autorům balíček `lib` složek.</span><span class="sxs-lookup"><span data-stu-id="674b0-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="674b0-164">Poznámka: v současné době můžete nuget.exe pack k použití této funkce; Průzkumník balíček NuGet ještě ji nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="674b0-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="674b0-165">Aktualizovat všechny tlačítko umožňující aktualizuje všechny balíčky současně</span><span class="sxs-lookup"><span data-stu-id="674b0-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="674b0-166">Řada z vás vědět o rutiny prostředí PowerShell "Balíček aktualizace" k aktualizaci všech vašich balíčků; Nyní je snadný způsob, jak to provést prostřednictvím uživatelského rozhraní také.</span><span class="sxs-lookup"><span data-stu-id="674b0-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="674b0-167">Můžete vyzkoušet tuto funkci na:</span><span class="sxs-lookup"><span data-stu-id="674b0-167">To try this feature out:</span></span>

1. <span data-ttu-id="674b0-168">Vytvoření nové aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="674b0-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="674b0-169">Spustit dialogové okno Spravovat balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="674b0-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="674b0-170">Vyberte možnost aktualizace.</span><span class="sxs-lookup"><span data-stu-id="674b0-170">Select 'Updates'</span></span>
1. <span data-ttu-id="674b0-171">Klikněte na tlačítko Aktualizovat vše</span><span class="sxs-lookup"><span data-stu-id="674b0-171">Click the 'Update All' button</span></span>

![Aktualizovat všechny tlačítka v dialogovém okně](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="674b0-173">Vylepšené projektu odkaz na podporu pro nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="674b0-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="674b0-174">Nyní nuget.exe pack příkaz procesy odkazuje projekty s následující pravidla:</span><span class="sxs-lookup"><span data-stu-id="674b0-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="674b0-175">Pokud odkazovaný projekt má odpovídající `.nuspec` souboru, například je do souboru s názvem `proj1.nuspec` ve stejné složce jako `proj1.csproj`, pak je tento projekt přidal jako závislost do balíčku, pomocí id a verzi čtení z `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="674b0-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="674b0-176">Soubory odkazované projektu, jinak jsou seskupeny do balíčku.</span><span class="sxs-lookup"><span data-stu-id="674b0-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="674b0-177">Potom projekty odkazuje tento projekt budou zpracovány pomocí rekurzivně pravidla sames.</span><span class="sxs-lookup"><span data-stu-id="674b0-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="674b0-178">Všechny knihovny DLL, `.pdb`, a `.exe` soubory budou přidány.</span><span class="sxs-lookup"><span data-stu-id="674b0-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="674b0-179">Všechny ostatní soubory obsahu budou přidány.</span><span class="sxs-lookup"><span data-stu-id="674b0-179">All other content files are added.</span></span>
1. <span data-ttu-id="674b0-180">Všechny závislosti jsou sloučeny.</span><span class="sxs-lookup"><span data-stu-id="674b0-180">All dependencies are merged.</span></span>

<span data-ttu-id="674b0-181">To umožňuje odkazované projektu jsou považovány za závislost, pokud dojde `.nuspec` souboru, jinak, stane se součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="674b0-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="674b0-182">Další podrobnosti tady: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="674b0-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="674b0-183">Přidat do balíčků vlastnost 'minimální verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="674b0-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="674b0-184">Nový atribut metadat volat 'minClientVersion' můžete teď určit minimální verzi klienta NuGet požadované využívat balíček.</span><span class="sxs-lookup"><span data-stu-id="674b0-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="674b0-185">Tato funkce vám pomůže balíček autorovi určit, že balíček bude fungovat až po konkrétní verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="674b0-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="674b0-186">Nový `.nuspec` funkce jsou přidány po NuGet 2.5 balíčky budou moci deklarace minimální verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="674b0-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="674b0-187">Pokud má uživatel 2.5 NuGet, které jsou nainstalované a balíček je označený jako vyžadující 2.6, bude mu udělená vizuální upozornění na uživatele, což značí, že nebudou instalovat balíček.</span><span class="sxs-lookup"><span data-stu-id="674b0-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="674b0-188">Uživatele se pak řídí k aktualizaci jejich verze balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="674b0-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="674b0-189">Tím se zvyšuje na stávající prostředí balíčky, kde začít instalovat, ale pak neúspěšné, což značí, že byla identifikována ve schématu nerozpoznané verzi.</span><span class="sxs-lookup"><span data-stu-id="674b0-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="674b0-190">Závislosti jsou už zbytečně aktualizován v průběhu instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="674b0-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="674b0-191">Před 2.5 NuGet Pokud byla nainstalována balíček, který závisí na balíčku již nainstalované v projektu, závislost by aktualizovat v rámci nové instalace i v případě, že stávající verze uspokojit závislost.</span><span class="sxs-lookup"><span data-stu-id="674b0-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="674b0-192">Od verze NuGet 2.5, pokud je již splnit verze závislosti, závislost nebude aktualizován v průběhu jiné instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="674b0-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="674b0-193">**Scénář:**</span><span class="sxs-lookup"><span data-stu-id="674b0-193">**The scenario:**</span></span>

1. <span data-ttu-id="674b0-194">Zdrojové úložiště obsahuje balíček B s verzí 1.0.0 a 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="674b0-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="674b0-195">Obsahuje taky balíčku A, který má závislost na B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="674b0-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="674b0-196">Předpokládejme, že aktuální projekt již obsahuje verze balíčku B 1.0.0 nainstalována.</span><span class="sxs-lookup"><span data-stu-id="674b0-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="674b0-197">Teď chcete nainstalovat balíček A.</span><span class="sxs-lookup"><span data-stu-id="674b0-197">Now you want to install package A.</span></span>

<span data-ttu-id="674b0-198">**V NuGet 2.2 nebo starší:**</span><span class="sxs-lookup"><span data-stu-id="674b0-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="674b0-199">Při instalaci balíčku A, NuGet bude automaticky aktualizován B na verzi 1.0.2, i když stávající verzi 1.0.0 již splňuje omezení verze závislosti, což je > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="674b0-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="674b0-200">**V NuGet 2,5 a novější:**</span><span class="sxs-lookup"><span data-stu-id="674b0-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="674b0-201">NuGet už zaktualizuje B, protože zjistí, že stávající verzi 1.0.0 splňuje omezení verze závislosti.</span><span class="sxs-lookup"><span data-stu-id="674b0-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="674b0-202">Další informace o této změně, najdete v podrobné [pracovní položka](http://nuget.codeplex.com/workitem/1681) a také související [diskusní téma](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="674b0-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="674b0-203">nuget.exe výstupy požadavky http s podrobné podrobností</span><span class="sxs-lookup"><span data-stu-id="674b0-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="674b0-204">Pokud jsou řešení potíží s nuget.exe nebo právě zvědaví jaké požadavky HTTP jsou vytvářeny během operací '-podrobností podrobné ' přepínač teď výstup všech požadavků HTTP, které jsou provedeny.</span><span class="sxs-lookup"><span data-stu-id="674b0-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Výstup HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="674b0-206">nuget.exe nabízené teď podporuje UNC a složku zdroje</span><span class="sxs-lookup"><span data-stu-id="674b0-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="674b0-207">Před NuGet 2.5 Pokud jste se pokusili spustit "nuget.exe push" ke zdroji balíčku na základě cesty UNC nebo místní složky nabízeného oznámení skončí s chybou.</span><span class="sxs-lookup"><span data-stu-id="674b0-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="674b0-208">Nedávno přidané hierarchické konfigurace funkce s měl stát běžné nuget.exe potřebovat cílit na zdroji UNC nebo složku nebo Galerie NuGet založené na protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="674b0-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="674b0-209">Od verze NuGet 2.5, pokud nuget.exe identifikuje zdroj UNC nebo složku, provede kopírování souborů do zdroje.</span><span class="sxs-lookup"><span data-stu-id="674b0-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="674b0-210">Nyní bude fungovat následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="674b0-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="674b0-211">nuget.exe podporuje explicitně zadat konfigurační soubory</span><span class="sxs-lookup"><span data-stu-id="674b0-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="674b0-212">podporují novou nuget.exe příkazy, které nyní získat přístup ke konfiguraci, (všechny kromě 'specifikace' a 'pack') '-ConfigFile' možnost, která vynutí konkrétní konfiguračním souboru, který se má použít místo výchozí konfigurační soubor % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="674b0-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="674b0-213">Příklad:</span><span class="sxs-lookup"><span data-stu-id="674b0-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="674b0-214">Podpora pro nativní projekty</span><span class="sxs-lookup"><span data-stu-id="674b0-214">Support for Native projects</span></span>

<span data-ttu-id="674b0-215">S NuGet 2.5 nástrojů NuGet je teď dostupná pro nativní projekty v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="674b0-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="674b0-216">Očekáváme, že většina nativní balíčky budou využívat funkci MSBuild importy výš, pomocí nástroje vytvořené [CoApp projektu](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="674b0-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="674b0-217">Další informace najdete v tématu [podrobné informace o nástroji](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na webu coapp.org.</span><span class="sxs-lookup"><span data-stu-id="674b0-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="674b0-218">Název cílové rozhraní "nativní" byla zavedená pro balíčky vložení souborů do \build, \content a \tools při instalaci balíčku do k nativnímu projektu.</span><span class="sxs-lookup"><span data-stu-id="674b0-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="674b0-219">\`Lib, složky, se nepoužije pro nativní projekty.</span><span class="sxs-lookup"><span data-stu-id="674b0-219">The \`lib` folder is not used for native projects.</span></span>
