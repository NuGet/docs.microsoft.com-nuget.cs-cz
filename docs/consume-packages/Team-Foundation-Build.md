---
title: Návod obnovení balíčku NuGet s sestavením team foundation
description: Návod, jak NuGet balíček obnovit s Team Foundation Build (TFS a Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "73611006"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="14d14-103">Nastavení obnovení balíčku pomocí team foundation buildu</span><span class="sxs-lookup"><span data-stu-id="14d14-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="14d14-104">Tento článek obsahuje podrobný návod, jak obnovit balíčky jako součást [team services sestavení](/vsts/build-release/index) obou, pro Git a Team Services version control.</span><span class="sxs-lookup"><span data-stu-id="14d14-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="14d14-105">Přestože tento návod je specifický pro scénář použití Visual Studio Team Services, koncepty platí také pro jiné verze správy a sestavení systémů.</span><span class="sxs-lookup"><span data-stu-id="14d14-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="14d14-106">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="14d14-106">Applies To:</span></span>

- <span data-ttu-id="14d14-107">Vlastní projekty MSBuild spuštěné v libovolné verzi tfs</span><span class="sxs-lookup"><span data-stu-id="14d14-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="14d14-108">Team Foundation Server 2012 nebo starší</span><span class="sxs-lookup"><span data-stu-id="14d14-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="14d14-109">Šablony procesů sestavení vlastní hospo- základy Team Foundation migrované na TFS 2013 nebo novější</span><span class="sxs-lookup"><span data-stu-id="14d14-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="14d14-110">Vytváření šablon procesů s odebranou funkcí obnovení nugetu</span><span class="sxs-lookup"><span data-stu-id="14d14-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="14d14-111">Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 s jeho šablony procesu sestavení, automatické obnovení balíčků se stane jako součást procesu sestavení.</span><span class="sxs-lookup"><span data-stu-id="14d14-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="14d14-112">Obecný přístup</span><span class="sxs-lookup"><span data-stu-id="14d14-112">The general approach</span></span>

<span data-ttu-id="14d14-113">Výhodou použití NuGet je, že můžete použít, aby se zabránilo vrácení binárních souborů v systému správy verzí.</span><span class="sxs-lookup"><span data-stu-id="14d14-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="14d14-114">To je obzvláště zajímavé, pokud používáte [distribuovaný](https://en.wikipedia.org/wiki/Distributed_revision_control) systém správy verzí, jako je git, protože vývojáři potřebují klonovat celé úložiště, včetně úplné historie, než mohou začít pracovat místně.</span><span class="sxs-lookup"><span data-stu-id="14d14-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="14d14-115">Vrácení binárních souborů se změnami může způsobit významné nafouknutí úložiště, protože binární soubory jsou obvykle uloženy bez rozdílové komprese.</span><span class="sxs-lookup"><span data-stu-id="14d14-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="14d14-116">NuGet podporuje [obnovení balíčků](../consume-packages/package-restore.md) jako součást sestavení po dlouhou dobu.</span><span class="sxs-lookup"><span data-stu-id="14d14-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="14d14-117">Předchozí implementace měla problém kuře a vejce pro balíčky, které chcete rozšířit proces sestavení, protože NuGet obnovené balíčky při vytváření projektu.</span><span class="sxs-lookup"><span data-stu-id="14d14-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="14d14-118">MSBuild však neumožňuje rozšíření sestavení během sestavení; dalo by se tvrdit, že tento problém v MSBuild, ale já bych tvrdit, že se jedná o vlastní problém.</span><span class="sxs-lookup"><span data-stu-id="14d14-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="14d14-119">V závislosti na tom, který aspekt je třeba prodloužit, může být příliš pozdě na registraci v době, kdy je balíček obnoven.</span><span class="sxs-lookup"><span data-stu-id="14d14-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="14d14-120">Lékna tento problém je ujistit se, že balíčky jsou obnoveny jako první krok v procesu sestavení:</span><span class="sxs-lookup"><span data-stu-id="14d14-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="14d14-121">Když proces sestavení obnoví balíčky před vytvořením kódu, nemusíte `.targets` soubory vrácení se změnami</span><span class="sxs-lookup"><span data-stu-id="14d14-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="14d14-122">Balíčky musí být vytvořen, aby bylo možné načítat v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="14d14-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="14d14-123">V opačném případě můžete stále `.targets` chtít vrátit soubory se změnami, aby ostatní vývojáři mohli jednoduše otevřít řešení bez nutnosti nejprve obnovit balíčky.</span><span class="sxs-lookup"><span data-stu-id="14d14-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="14d14-124">Následující ukázkový projekt ukazuje, jak nastavit sestavení tak, aby `packages` složky a `.targets` soubory není nutné se změnami.</span><span class="sxs-lookup"><span data-stu-id="14d14-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="14d14-125">Také ukazuje, jak nastavit automatické sestavení služby Team Foundation pro tento ukázkový projekt.</span><span class="sxs-lookup"><span data-stu-id="14d14-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="14d14-126">Struktura úložiště</span><span class="sxs-lookup"><span data-stu-id="14d14-126">Repository structure</span></span>

<span data-ttu-id="14d14-127">Náš demo projekt je jednoduchý nástroj příkazového řádku, který používá argument příkazového řádku k dotazování Bingu.</span><span class="sxs-lookup"><span data-stu-id="14d14-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="14d14-128">Zaměřuje se na rozhraní .NET Framework 4 a používá mnoho [balíčků BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)a [Microsoft.Bcl.Build).](https://www.nuget.org/packages/Microsoft.Bcl.Build)</span><span class="sxs-lookup"><span data-stu-id="14d14-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="14d14-129">Struktura úložiště vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="14d14-129">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="14d14-130">Můžete vidět, že jsme nezkontrolovali `packages` složku ani `.targets` žádné soubory.</span><span class="sxs-lookup"><span data-stu-id="14d14-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="14d14-131">Máme však zkontrolovat- jak `nuget.exe` je potřeba během sestavení.</span><span class="sxs-lookup"><span data-stu-id="14d14-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="14d14-132">Po široce používaných konvencích jsme je `tools` zkontrolovali ve sdílené složce.</span><span class="sxs-lookup"><span data-stu-id="14d14-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="14d14-133">Zdrojový kód je `src` ve složce.</span><span class="sxs-lookup"><span data-stu-id="14d14-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="14d14-134">Ačkoli naše demo používá pouze jediné řešení, můžete si snadno představit, že tato složka obsahuje více než jedno řešení.</span><span class="sxs-lookup"><span data-stu-id="14d14-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="14d14-135">Ignorování souborů</span><span class="sxs-lookup"><span data-stu-id="14d14-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="14d14-136">V klientovi NuGet je aktuálně [známá chyba,](https://nuget.codeplex.com/workitem/4072) která `packages` způsobí, že klient stále přidá složku do správy verzí.</span><span class="sxs-lookup"><span data-stu-id="14d14-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="14d14-137">Řešení je zakázat integraci správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="14d14-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="14d14-138">Chcete-li to provést, `Nuget.Config ` potřebujete soubor `.nuget` ve složce, která je rovnoběžná s vaším řešením.</span><span class="sxs-lookup"><span data-stu-id="14d14-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="14d14-139">Pokud tato složka ještě neexistuje, musíte ji vytvořit.</span><span class="sxs-lookup"><span data-stu-id="14d14-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="14d14-140">V [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), přidejte následující obsah:</span><span class="sxs-lookup"><span data-stu-id="14d14-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="14d14-141">Chcete-li sdělit správu verzí, že nemáme v úmyslu zařazovat složky balíčků se **změnami,** přidali jsme také soubory ignorování pro git (`.gitignore`) i pro správu verzí TF (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="14d14-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="14d14-142">Tyto soubory popisují vzory souborů, které nechcete se změnami.</span><span class="sxs-lookup"><span data-stu-id="14d14-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="14d14-143">Soubor `.gitignore` vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="14d14-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="14d14-144">Soubor `.gitignore` je [poměrně silný](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="14d14-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="14d14-145">Chcete-li například obecně nevrátit obsah `packages` složky se změnami, ale chcete použít `.targets` předchozí pokyny pro vrácení souborů se změnami, můžete mít místo toho následující pravidlo:</span><span class="sxs-lookup"><span data-stu-id="14d14-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="14d14-146">Tím se `packages` vyloučí všechny složky, ale znovu zahrnete všechny obsažené `.targets` soubory.</span><span class="sxs-lookup"><span data-stu-id="14d14-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="14d14-147">Mimochodem, můžete najít šablonu `.gitignore` pro soubory, která je speciálně přizpůsobena potřebám vývojářů sady Visual Studio [zde](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="14d14-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="14d14-148">Tf verze řízení podporuje velmi podobný mechanismus prostřednictvím souboru [.tfignore.](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control)</span><span class="sxs-lookup"><span data-stu-id="14d14-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="14d14-149">Syntaxe je prakticky stejná:</span><span class="sxs-lookup"><span data-stu-id="14d14-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="14d14-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="14d14-150">build.proj</span></span>

<span data-ttu-id="14d14-151">Pro naše demo, udržujeme proces sestavení poměrně jednoduché.</span><span class="sxs-lookup"><span data-stu-id="14d14-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="14d14-152">Vytvoříme projekt MSBuild, který vytvoří všechna řešení a zároveň zajistí, že balíčky jsou obnoveny před sestavením řešení.</span><span class="sxs-lookup"><span data-stu-id="14d14-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="14d14-153">Tento projekt bude mít `Clean`tři `Build` `Rebuild` konvenční cíle a `RestorePackages`také nový cíl .</span><span class="sxs-lookup"><span data-stu-id="14d14-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="14d14-154">A `Build` `Rebuild` cíle jsou `RestorePackages`závislé na .</span><span class="sxs-lookup"><span data-stu-id="14d14-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="14d14-155">Tím zajistíte, že `Build` můžete `Rebuild` spustit a spoléhat na balíčky, které jsou obnoveny.</span><span class="sxs-lookup"><span data-stu-id="14d14-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="14d14-156">`Clean`a `Build` `Rebuild` vyvolat odpovídající cíl MSBuild ve všech souborech řešení.</span><span class="sxs-lookup"><span data-stu-id="14d14-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="14d14-157">Cíl `RestorePackages` vyvolá `nuget.exe` pro každý soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="14d14-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="14d14-158">Toho lze dosáhnout pomocí [funkce dávkování msbuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="14d14-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="14d14-159">Výsledek vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="14d14-159">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="14d14-160">Konfigurace sestavení týmu</span><span class="sxs-lookup"><span data-stu-id="14d14-160">Configuring Team Build</span></span>

<span data-ttu-id="14d14-161">Team Build nabízí různé šablony procesů.</span><span class="sxs-lookup"><span data-stu-id="14d14-161">Team Build offers various process templates.</span></span> <span data-ttu-id="14d14-162">Pro tuto demonstraci používáme službu Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="14d14-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="14d14-163">Místní instalace TFS bude velmi podobné ačkoli.</span><span class="sxs-lookup"><span data-stu-id="14d14-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="14d14-164">Git a TF Version Control mají různé šablony team buildu, takže následující kroky se budou lišit v závislosti na tom, který systém správy verzí používáte.</span><span class="sxs-lookup"><span data-stu-id="14d14-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="14d14-165">V obou případech vše, co potřebujete, je vybrat build.proj jako projekt, který chcete sestavit.</span><span class="sxs-lookup"><span data-stu-id="14d14-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="14d14-166">Nejprve se podívejme na šablonu procesu pro git.</span><span class="sxs-lookup"><span data-stu-id="14d14-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="14d14-167">V šabloně založené na gitu `Solution to build`je sestavení vybráno pomocí vlastnosti :</span><span class="sxs-lookup"><span data-stu-id="14d14-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces sestavení pro git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="14d14-169">Vezměte prosím na vědomí, že toto zařízení je místem ve vašem úložišti.</span><span class="sxs-lookup"><span data-stu-id="14d14-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="14d14-170">Vzhledem `build.proj` k tomu, naše `build.proj`je v kořeni, jsme prostě použili .</span><span class="sxs-lookup"><span data-stu-id="14d14-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="14d14-171">Pokud umístíte soubor sestavení pod `tools`složku s `tools\build.proj`názvem , bude hodnota .</span><span class="sxs-lookup"><span data-stu-id="14d14-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="14d14-172">V šabloně správy verzí TF je `Projects`projekt vybrán prostřednictvím vlastnosti :</span><span class="sxs-lookup"><span data-stu-id="14d14-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="14d14-174">Na rozdíl od git založené šablony podporuje ovládací prvek verze TF výběr (tlačítko na pravé straně se třemi tečkami).</span><span class="sxs-lookup"><span data-stu-id="14d14-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="14d14-175">Aby chomáč chyb y jejich zadání doporučujeme použít k výběru projektu.</span><span class="sxs-lookup"><span data-stu-id="14d14-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
