---
title: "Poznámky k verzi NuGet 2.5 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 2.5 NuGet."
keywords: "NuGet 2.5 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4fb696a1f4d76bdd3461df6af461f279f9f0a8b0
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="c8dce-104">Poznámky k verzi 2,5 NuGet</span><span class="sxs-lookup"><span data-stu-id="c8dce-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="c8dce-105">[Poznámky k verzi NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 poznámky k verzi](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="c8dce-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="c8dce-106">NuGet 2.5 byla vydána 25. dubna 2013.</span><span class="sxs-lookup"><span data-stu-id="c8dce-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="c8dce-107">Tato verze byla tak velká, jsme popisovač compelled tak, aby přeskočil verze 2.3 a 2.4!</span><span class="sxs-lookup"><span data-stu-id="c8dce-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="c8dce-108">Dosud se největší verzi jsme jste měli pro NuGet, se přes [160 pracovní položky](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) ve verzi.</span><span class="sxs-lookup"><span data-stu-id="c8dce-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="c8dce-109">Potvrzení</span><span class="sxs-lookup"><span data-stu-id="c8dce-109">Acknowledgements</span></span>

<span data-ttu-id="c8dce-110">Rádi bychom se Děkujeme, že následující externí přispěvatele pro jejich významné příspěvky k NuGet 2.5:</span><span class="sxs-lookup"><span data-stu-id="c8dce-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="c8dce-111">[ADAM Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="c8dce-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="c8dce-112">[#2847](https://nuget.codeplex.com/workitem/2847) -přidat MonoAndroid, MonoTouch a MonoMac do seznamu identifikátorů známé target framework.</span><span class="sxs-lookup"><span data-stu-id="c8dce-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="c8dce-113">[G. Aragoneses Andresu](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="c8dce-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="c8dce-114">[#2865](https://nuget.codeplex.com/workitem/2865) -Opravte pravopis `NuGet.targets` pro malá a velká písmena operačního systému</span><span class="sxs-lookup"><span data-stu-id="c8dce-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="c8dce-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="c8dce-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="c8dce-116">Ujistěte se, vychází z Mono řešení.</span><span class="sxs-lookup"><span data-stu-id="c8dce-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="c8dce-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="c8dce-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="c8dce-118">Testování částí v Mono opravte.</span><span class="sxs-lookup"><span data-stu-id="c8dce-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="c8dce-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="c8dce-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="c8dce-120">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe pack příkaz nešířily vlastností nástroje MSBuild</span><span class="sxs-lookup"><span data-stu-id="c8dce-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="c8dce-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="c8dce-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="c8dce-122">[#1511](https://nuget.codeplex.com/workitem/1511) – upravit XML kód pro zpracování zachovat formátování.</span><span class="sxs-lookup"><span data-stu-id="c8dce-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="c8dce-123">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="c8dce-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="c8dce-124">Přidat rozpoznaný slova slovníku umožňující build.cmd proběhla úspěšně.</span><span class="sxs-lookup"><span data-stu-id="c8dce-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="c8dce-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="c8dce-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="c8dce-126">Opravte testů jednotek při spuštění v lokalizovaných VS.</span><span class="sxs-lookup"><span data-stu-id="c8dce-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="c8dce-127">Zařízení Evans Gareth</span><span class="sxs-lookup"><span data-stu-id="c8dce-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="c8dce-128">Extrahované rozhraní PackageService</span><span class="sxs-lookup"><span data-stu-id="c8dce-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="c8dce-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="c8dce-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="c8dce-130">[#936](https://nuget.codeplex.com/workitem/936) -zpracování závislosti projektu při balení</span><span class="sxs-lookup"><span data-stu-id="c8dce-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="c8dce-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="c8dce-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="c8dce-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -podpora vymazat Text heslo při ukládání přihlašovacích údajů zdroje balíčku v souborech nuget.cofig</span><span class="sxs-lookup"><span data-stu-id="c8dce-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="c8dce-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="c8dce-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="c8dce-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) – popis opravte Get-Package nápovědy</span><span class="sxs-lookup"><span data-stu-id="c8dce-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="c8dce-135">Děkujeme také následující jednotlivce pro vyhledání chyby s NuGet 2.5 Beta nebo RC, které byly schválené a opravit dřív, než finální verzi:</span><span class="sxs-lookup"><span data-stu-id="c8dce-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="c8dce-136">[ADAM Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="c8dce-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="c8dce-137">[#3200](https://nuget.codeplex.com/workitem/3200) – Mstestu přerušený s nejnovější NuGet 2.4 a 2,5 sestavení</span><span class="sxs-lookup"><span data-stu-id="c8dce-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="c8dce-138">Upozorňují na důležité funkce ve verzi</span><span class="sxs-lookup"><span data-stu-id="c8dce-138">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="c8dce-139">Povolit uživatelům přepsat soubory obsahu, které již existují.</span><span class="sxs-lookup"><span data-stu-id="c8dce-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="c8dce-140">Jednou z nejžádanějších funkcí celou dobu byla možnost přepsat soubory obsahu, které již existují na disku, obsažen v balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8dce-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="c8dce-141">Od verze NuGet 2.5, jsou identifikovány tyto konflikty a zobrazí se výzva k přepsání souborů, zatímco dříve byly tyto soubory vždy přeskočeny.</span><span class="sxs-lookup"><span data-stu-id="c8dce-141">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![Přepsat soubory obsahu](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="c8dce-143">'nuget.exe aktualizace' a 'Install-Package"teď mají novou možnost '-FileConflictAction, můžete nastavit některé výchozí pro scénáře příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="c8dce-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="c8dce-144">Nastavte výchozí akce, soubor z balíčku již existuje v cílové projektu.</span><span class="sxs-lookup"><span data-stu-id="c8dce-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="c8dce-145">Nastavte na "přepsat, aby vždy přepsat soubory.</span><span class="sxs-lookup"><span data-stu-id="c8dce-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="c8dce-146">Přeskočit soubory nastavena na hodnotu 'Ignorovat'.</span><span class="sxs-lookup"><span data-stu-id="c8dce-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="c8dce-147">Pokud není zadáno, zobrazí výzvu pro každý konfliktní soubor.</span><span class="sxs-lookup"><span data-stu-id="c8dce-147">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="c8dce-148">Automatické import MSBuild cíle a soubory props</span><span class="sxs-lookup"><span data-stu-id="c8dce-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="c8dce-149">Byla vytvořena konvenční novou složku na nejvyšší úrovni balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8dce-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="c8dce-150">Jako partnera, který `\lib`, `\content`, a `\tools`, teď můžete zahrnout `\build` složky v balíčku.</span><span class="sxs-lookup"><span data-stu-id="c8dce-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="c8dce-151">V této složce, můžete umístit dva soubory s pevnou názvy `{packageid}.targets` nebo `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="c8dce-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="c8dce-152">Tyto dva soubory mohou být buď přímo `build` nebo pod konkrétní rozhraní složky stejně jako jiných složkách.</span><span class="sxs-lookup"><span data-stu-id="c8dce-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="c8dce-153">Pravidlo pro výběr nejlépe odpovídající složku je přesně stejné jako ty.</span><span class="sxs-lookup"><span data-stu-id="c8dce-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="c8dce-154">Při instalaci balíčku NuGet se soubory \build přidá MSBuild `<Import>` element v souboru projektu přejdete `.targets` a `.props` soubory.</span><span class="sxs-lookup"><span data-stu-id="c8dce-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="c8dce-155">`.props` Soubor přidán v horní části, zatímco `.targets` soubor přidán do dolní části.</span><span class="sxs-lookup"><span data-stu-id="c8dce-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="c8dce-156">Zadejte jiný odkazy na platformě pomocí `<References/>` – element</span><span class="sxs-lookup"><span data-stu-id="c8dce-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="c8dce-157">Před 2.5 v `.nuspec` souboru uživatele můžete jenom zadat referenčních souborů, který se má přidat pro všechny framework.</span><span class="sxs-lookup"><span data-stu-id="c8dce-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="c8dce-158">Teď pomocí této nové funkce v 2.5, můžete vytvořit uživatele `<reference/>` element pro každou podporovanou platformu, například:</span><span class="sxs-lookup"><span data-stu-id="c8dce-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="c8dce-159">Tady je postup pro jak NuGet přidá odkazy na projekty na základě `.nuspec` souboru:</span><span class="sxs-lookup"><span data-stu-id="c8dce-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="c8dce-160">Najít `lib` složku, která je vhodná pro cílové rozhraní a získat seznam sestavení z této složky</span><span class="sxs-lookup"><span data-stu-id="c8dce-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="c8dce-161">Samostatně najít odkazuje na skupinu, která je vhodná pro cílové rozhraní a získat seznam sestavení z dané skupiny.</span><span class="sxs-lookup"><span data-stu-id="c8dce-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="c8dce-162">Referenční dokumentace skupina bez cílovém Frameworku, zadaný je záložní skupina.</span><span class="sxs-lookup"><span data-stu-id="c8dce-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="c8dce-163">Zjistí průnik dva seznamy a použít jej jako odkazy pro přidání</span><span class="sxs-lookup"><span data-stu-id="c8dce-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="c8dce-164">Tato nová funkce vám umožní použít funkci odkazy na používání podmnožiny sestavení pro různé architektury, když byste jinak potřebovali pro přenos duplicitní sestavení v několika autorům balíček `lib` složek.</span><span class="sxs-lookup"><span data-stu-id="c8dce-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="c8dce-165">Poznámka: v současné době můžete nuget.exe pack k použití této funkce; Průzkumník balíček NuGet ještě ji nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="c8dce-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="c8dce-166">Aktualizovat všechny tlačítko umožňující aktualizuje všechny balíčky současně</span><span class="sxs-lookup"><span data-stu-id="c8dce-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="c8dce-167">Řada z vás vědět o rutiny prostředí PowerShell "Balíček aktualizace" k aktualizaci všech vašich balíčků; Nyní je snadný způsob, jak to provést prostřednictvím uživatelského rozhraní také.</span><span class="sxs-lookup"><span data-stu-id="c8dce-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="c8dce-168">Můžete vyzkoušet tuto funkci na:</span><span class="sxs-lookup"><span data-stu-id="c8dce-168">To try this feature out:</span></span>

1. <span data-ttu-id="c8dce-169">Vytvoření nové aplikace ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="c8dce-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="c8dce-170">Spustit dialogové okno Spravovat balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="c8dce-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="c8dce-171">Vyberte možnost aktualizace.</span><span class="sxs-lookup"><span data-stu-id="c8dce-171">Select 'Updates'</span></span>
1. <span data-ttu-id="c8dce-172">Klikněte na tlačítko Aktualizovat vše</span><span class="sxs-lookup"><span data-stu-id="c8dce-172">Click the 'Update All' button</span></span>

![Aktualizovat všechny tlačítka v dialogovém okně](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="c8dce-174">Vylepšené projektu odkaz na podporu pro nuget.exe Pack</span><span class="sxs-lookup"><span data-stu-id="c8dce-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="c8dce-175">Nyní nuget.exe pack příkaz procesy odkazuje projekty s následující pravidla:</span><span class="sxs-lookup"><span data-stu-id="c8dce-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="c8dce-176">Pokud odkazovaný projekt má odpovídající `.nuspec` souboru, například je do souboru s názvem `proj1.nuspec` ve stejné složce jako `proj1.csproj`, pak je tento projekt přidal jako závislost do balíčku, pomocí id a verzi čtení z `.nuspec` souboru.</span><span class="sxs-lookup"><span data-stu-id="c8dce-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="c8dce-177">Soubory odkazované projektu, jinak jsou seskupeny do balíčku.</span><span class="sxs-lookup"><span data-stu-id="c8dce-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="c8dce-178">Potom projekty odkazuje tento projekt budou zpracovány pomocí rekurzivně pravidla sames.</span><span class="sxs-lookup"><span data-stu-id="c8dce-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="c8dce-179">Všechny knihovny DLL, `.pdb`, a `.exe` soubory budou přidány.</span><span class="sxs-lookup"><span data-stu-id="c8dce-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="c8dce-180">Všechny ostatní soubory obsahu budou přidány.</span><span class="sxs-lookup"><span data-stu-id="c8dce-180">All other content files are added.</span></span>
1. <span data-ttu-id="c8dce-181">Všechny závislosti jsou sloučeny.</span><span class="sxs-lookup"><span data-stu-id="c8dce-181">All dependencies are merged.</span></span>

<span data-ttu-id="c8dce-182">To umožňuje odkazované projektu jsou považovány za závislost, pokud dojde `.nuspec` souboru, jinak, stane se součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="c8dce-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="c8dce-183">Další podrobnosti zde: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="c8dce-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="c8dce-184">Přidat do balíčků vlastnost 'minimální verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8dce-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="c8dce-185">Nový atribut metadat volat 'minClientVersion' můžete teď určit minimální verzi klienta NuGet požadované využívat balíček.</span><span class="sxs-lookup"><span data-stu-id="c8dce-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="c8dce-186">Tato funkce vám pomůže balíček autorovi určit, že balíček bude fungovat až po konkrétní verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8dce-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="c8dce-187">Nový `.nuspec` funkce jsou přidány po NuGet 2.5 balíčky budou moci deklarace minimální verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8dce-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="c8dce-188">Pokud má uživatel 2.5 NuGet, které jsou nainstalované a balíček je označený jako vyžadující 2.6, bude mu udělená vizuální upozornění na uživatele, což značí, že nebudou instalovat balíček.</span><span class="sxs-lookup"><span data-stu-id="c8dce-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="c8dce-189">Uživatele se pak řídí k aktualizaci jejich verze balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="c8dce-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="c8dce-190">Tím se zvyšuje na stávající prostředí balíčky, kde začít instalovat, ale pak neúspěšné, což značí, že byla identifikována ve schématu nerozpoznané verzi.</span><span class="sxs-lookup"><span data-stu-id="c8dce-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="c8dce-191">Závislosti jsou už zbytečně aktualizován v průběhu instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="c8dce-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="c8dce-192">Před 2.5 NuGet Pokud byla nainstalována balíček, který závisí na balíčku již nainstalované v projektu, závislost by aktualizovat v rámci nové instalace i v případě, že stávající verze uspokojit závislost.</span><span class="sxs-lookup"><span data-stu-id="c8dce-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="c8dce-193">Od verze NuGet 2.5, pokud je již splnit verze závislosti, závislost nebude aktualizován v průběhu jiné instalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="c8dce-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="c8dce-194">**Scénář:**</span><span class="sxs-lookup"><span data-stu-id="c8dce-194">**The scenario:**</span></span>

1. <span data-ttu-id="c8dce-195">Zdrojové úložiště obsahuje balíček B s verzí 1.0.0 a 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="c8dce-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="c8dce-196">Obsahuje taky balíčku A, který má závislost na B (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="c8dce-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="c8dce-197">Předpokládejme, že aktuální projekt již obsahuje verze balíčku B 1.0.0 nainstalována.</span><span class="sxs-lookup"><span data-stu-id="c8dce-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="c8dce-198">Teď chcete nainstalovat balíček A.</span><span class="sxs-lookup"><span data-stu-id="c8dce-198">Now you want to install package A.</span></span>

<span data-ttu-id="c8dce-199">**V NuGet 2.2 nebo starší:**</span><span class="sxs-lookup"><span data-stu-id="c8dce-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="c8dce-200">Při instalaci balíčku A, NuGet bude automaticky aktualizován B na verzi 1.0.2, i když stávající verzi 1.0.0 již splňuje omezení verze závislosti, což je > = 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="c8dce-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="c8dce-201">**V NuGet 2,5 a novější:**</span><span class="sxs-lookup"><span data-stu-id="c8dce-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="c8dce-202">NuGet už zaktualizuje B, protože zjistí, že stávající verzi 1.0.0 splňuje omezení verze závislosti.</span><span class="sxs-lookup"><span data-stu-id="c8dce-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="c8dce-203">Další informace o této změně, najdete v podrobné [pracovní položka](http://nuget.codeplex.com/workitem/1681) a také související [diskusní téma](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="c8dce-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="c8dce-204">nuget.exe výstupy požadavky http s podrobné podrobností</span><span class="sxs-lookup"><span data-stu-id="c8dce-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="c8dce-205">Pokud jsou řešení potíží s nuget.exe nebo právě zvědaví jaké požadavky HTTP jsou vytvářeny během operací '-podrobností podrobné ' přepínač teď výstup všech požadavků HTTP, které jsou provedeny.</span><span class="sxs-lookup"><span data-stu-id="c8dce-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Výstup HTTP z nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="c8dce-207">nuget.exe nabízené teď podporuje UNC a složku zdroje</span><span class="sxs-lookup"><span data-stu-id="c8dce-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="c8dce-208">Před NuGet 2.5 Pokud jste se pokusili spustit "nuget.exe push" ke zdroji balíčku na základě cesty UNC nebo místní složky nabízeného oznámení skončí s chybou.</span><span class="sxs-lookup"><span data-stu-id="c8dce-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="c8dce-209">Nedávno přidané hierarchické konfigurace funkce s měl stát běžné nuget.exe potřebovat cílit na zdroji UNC nebo složku nebo Galerie NuGet založené na protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="c8dce-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="c8dce-210">Od verze NuGet 2.5, pokud nuget.exe identifikuje zdroj UNC nebo složku, provede kopírování souborů do zdroje.</span><span class="sxs-lookup"><span data-stu-id="c8dce-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="c8dce-211">Nyní bude fungovat následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="c8dce-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="c8dce-212">nuget.exe podporuje explicitně zadat konfigurační soubory</span><span class="sxs-lookup"><span data-stu-id="c8dce-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="c8dce-213">podporují novou nuget.exe příkazy, které nyní získat přístup ke konfiguraci, (všechny kromě 'specifikace' a 'pack') '-ConfigFile' možnost, která vynutí konkrétní konfiguračním souboru, který se má použít místo výchozí konfigurační soubor % AppData%\nuget\Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="c8dce-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="c8dce-214">Příklad:</span><span class="sxs-lookup"><span data-stu-id="c8dce-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="c8dce-215">Podpora pro nativní projekty</span><span class="sxs-lookup"><span data-stu-id="c8dce-215">Support for Native projects</span></span>

<span data-ttu-id="c8dce-216">S NuGet 2.5 nástrojů NuGet je teď dostupná pro nativní projekty v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c8dce-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="c8dce-217">Očekáváme, že většina nativní balíčky budou využívat funkci MSBuild importy výš, pomocí nástroje vytvořené [CoApp projektu](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="c8dce-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="c8dce-218">Další informace najdete v tématu [podrobné informace o nástroji](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) na webu coapp.org.</span><span class="sxs-lookup"><span data-stu-id="c8dce-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="c8dce-219">Název cílové rozhraní "nativní" byla zavedená pro balíčky vložení souborů do \build, \content a \tools při instalaci balíčku do k nativnímu projektu.</span><span class="sxs-lookup"><span data-stu-id="c8dce-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="c8dce-220">\`Lib, složky, se nepoužije pro nativní projekty.</span><span class="sxs-lookup"><span data-stu-id="c8dce-220">The \`lib` folder is not used for native projects.</span></span>
