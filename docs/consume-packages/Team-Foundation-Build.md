---
title: Návod k obnovení balíčků NuGet s aplikací Team Foundation Build
description: Návod, jak se balíček NuGet restore s pomocí procesu Team Foundation Build (TFS a Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549882"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="9a11e-103">Nastavení obnovení balíčku s Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="9a11e-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="9a11e-104">Tento článek poskytuje podrobný návod k obnovení balíčků v rámci [sestavení Team Services](/vsts/build-release/index) i pro Git a správy verzí produktu Team Services.</span><span class="sxs-lookup"><span data-stu-id="9a11e-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="9a11e-105">I když Tento názorný postup je specifické pro scénář, jak pomocí služby Visual Studio Team Services, koncepty také použít další správu verzí a sestavení systémy.</span><span class="sxs-lookup"><span data-stu-id="9a11e-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="9a11e-106">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="9a11e-106">Applies To:</span></span>

- <span data-ttu-id="9a11e-107">Vlastní projekty MSBuild běží na libovolné verzi sady TFS</span><span class="sxs-lookup"><span data-stu-id="9a11e-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="9a11e-108">Team Foundation Server 2012 nebo starší</span><span class="sxs-lookup"><span data-stu-id="9a11e-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="9a11e-109">Migrovat vlastní Team Foundation sestavení šablony procesu TFS 2013 nebo novější</span><span class="sxs-lookup"><span data-stu-id="9a11e-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="9a11e-110">Šablony procesu sestavení odebrat funkce obnovení Nuget</span><span class="sxs-lookup"><span data-stu-id="9a11e-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="9a11e-111">Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 s jeho šablony procesu sestavení, balíček automatické obnovení se stane jako součást procesu sestavení.</span><span class="sxs-lookup"><span data-stu-id="9a11e-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="9a11e-112">Je obecný přístup</span><span class="sxs-lookup"><span data-stu-id="9a11e-112">The general approach</span></span>

<span data-ttu-id="9a11e-113">Výhodou použití NuGet je, že vám pomůže se vyhněte se vracení binárních souborů do systému správy verzí.</span><span class="sxs-lookup"><span data-stu-id="9a11e-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="9a11e-114">To je obzvláště zajímavé, pokud používáte [distribuovanou správu verzí](http://en.wikipedia.org/wiki/Distributed_revision_control) systému, jako je git vzhledem k tomu, že vývojáři potřebují klonovat celé úložiště, včetně úplné historie, než mohou začít pracovat místně.</span><span class="sxs-lookup"><span data-stu-id="9a11e-114">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="9a11e-115">Vracení binárních souborů může způsobit významné úložiště determinističtější jako binární soubory jsou obvykle uložená bez komprese delta.</span><span class="sxs-lookup"><span data-stu-id="9a11e-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="9a11e-116">NuGet má podporované [obnovují se balíčky](../consume-packages/package-restore.md) jako součást sestavení pro dlouho dobou.</span><span class="sxs-lookup"><span data-stu-id="9a11e-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="9a11e-117">Předchozí provádění došlo k potížím kuřecí egg pro balíčky, které chcete rozšíření procesu sestavení, protože NuGet obnovit balíčky při vytváření projektu.</span><span class="sxs-lookup"><span data-stu-id="9a11e-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="9a11e-118">Však MSBuild neumožňuje rozšíření sestavení během sestavování; jeden může tvrdí, že tento problém v nástroji MSBuild, ale I by tvrdí, že se jedná o problém s vlastní.</span><span class="sxs-lookup"><span data-stu-id="9a11e-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="9a11e-119">V závislosti na tom, se kterými aspekty, které potřebujete k rozšiřování může být příliš pozdě pro registraci v době, kdy váš balíček se obnoví.</span><span class="sxs-lookup"><span data-stu-id="9a11e-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="9a11e-120">Léčba tohoto problému je zajistit, že prvním krokem v procesu sestavení obnovení balíčků:</span><span class="sxs-lookup"><span data-stu-id="9a11e-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="9a11e-121">Pokud váš proces sestavení obnoví balíčky před vytvořením kódu, není nutné k vrácení se změnami `.targets` soubory</span><span class="sxs-lookup"><span data-stu-id="9a11e-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="9a11e-122">Balíčky musí být vytvořen umožňuje načítání v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9a11e-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="9a11e-123">V opačném případě může stále chcete vrátit se změnami `.targets` soubory tak, aby ostatní vývojáři mohou jednoduše otevřete řešení aniž byste museli nejdřív obnovit balíčky.</span><span class="sxs-lookup"><span data-stu-id="9a11e-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="9a11e-124">Následující ukázkový projekt ukazuje, jak nastavit sestavení takovým způsobem, který `packages` složky a `.targets` soubory nemusí být vrácené se změnami.</span><span class="sxs-lookup"><span data-stu-id="9a11e-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="9a11e-125">Také ukazuje, jak nastavit automatické sestavení ve službě Team Foundation Service pro tento ukázkový projekt.</span><span class="sxs-lookup"><span data-stu-id="9a11e-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="9a11e-126">Struktura úložiště</span><span class="sxs-lookup"><span data-stu-id="9a11e-126">Repository structure</span></span>

<span data-ttu-id="9a11e-127">Náš ukázkový projekt je jednoduchý příkazového řádku nástroj, který používá argument příkazového řádku pro dotaz Bingu.</span><span class="sxs-lookup"><span data-stu-id="9a11e-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="9a11e-128">Cílí na rozhraní .NET Framework 4 a používá mnoho [BCL balíčky](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), a [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="9a11e-128">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="9a11e-129">Struktury úložiště by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="9a11e-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="9a11e-130">Uvidíte, že jsme nejsou vrácené se změnami `packages` složky ani žádné `.targets` soubory.</span><span class="sxs-lookup"><span data-stu-id="9a11e-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="9a11e-131">Budeme mít, ale vrácené se změnami `nuget.exe` potřeby během sestavení.</span><span class="sxs-lookup"><span data-stu-id="9a11e-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="9a11e-132">Následující často používá konvence jsme jsme vrátili ho se změnami v rámci sdílené `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="9a11e-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="9a11e-133">Zdrojový kód je v části `src` složky.</span><span class="sxs-lookup"><span data-stu-id="9a11e-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="9a11e-134">I když naše Ukázka používá pouze jedno řešení, snadno dokážete představit, že tato složka obsahuje více než jednoho řešení.</span><span class="sxs-lookup"><span data-stu-id="9a11e-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="9a11e-135">Ignorování souborů</span><span class="sxs-lookup"><span data-stu-id="9a11e-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="9a11e-136">Aktuálně nejsou k dispozici [známého problému nástroje klienta NuGet](https://nuget.codeplex.com/workitem/4072) , který způsobí, že klient přesto přidat `packages` složky do správy verzí.</span><span class="sxs-lookup"><span data-stu-id="9a11e-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="9a11e-137">Alternativní řešení je zakázat integraci správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="9a11e-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="9a11e-138">Chcete-li to mohli udělat, musíte `Nuget.Config ` soubor `.nuget` složku, která je paralelní do vašeho řešení.</span><span class="sxs-lookup"><span data-stu-id="9a11e-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="9a11e-139">Pokud tato složka ještě neexistuje, musíte ji vytvořit.</span><span class="sxs-lookup"><span data-stu-id="9a11e-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="9a11e-140">V [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), přidejte následující obsah:</span><span class="sxs-lookup"><span data-stu-id="9a11e-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="9a11e-141">Ke komunikaci do správy verzí, že není cílem je vrácení se změnami **balíčky** složek, přidali jsme také ignorovat soubory pro obě git (`.gitignore`) i správa verzí TF (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="9a11e-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="9a11e-142">Tyto soubory popisují vzory souborů, které nechcete, aby k vrácení se změnami.</span><span class="sxs-lookup"><span data-stu-id="9a11e-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="9a11e-143">`.gitignore` Soubor bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="9a11e-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="9a11e-144">`.gitignore` Soubor [poměrně efektivní](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="9a11e-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="9a11e-145">Například, pokud chcete obecně není vrácení se změnami obsah `packages` složka ale chcete přejít s předchozím pokyny k vrácení se změnami `.targets` souborů může mít následující pravidlo místo:</span><span class="sxs-lookup"><span data-stu-id="9a11e-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="9a11e-146">To se vyřadit všechny `packages` složky bude znovu zahrnout všechny `.targets` soubory.</span><span class="sxs-lookup"><span data-stu-id="9a11e-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="9a11e-147">Tím, jak můžete najít šablonu pro `.gitignore` soubory, které specificky přizpůsobit pro potřeby Visual Studio získávají vývojáři [tady](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="9a11e-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="9a11e-148">Správa verzí TF podporuje plní podobné funkce jako mechanismus prostřednictvím [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) souboru.</span><span class="sxs-lookup"><span data-stu-id="9a11e-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="9a11e-149">Syntaxe je v podstatě stejný:</span><span class="sxs-lookup"><span data-stu-id="9a11e-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="9a11e-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="9a11e-150">build.proj</span></span>

<span data-ttu-id="9a11e-151">Pro naši ukázku uchováváme proces sestavení poměrně jednoduché.</span><span class="sxs-lookup"><span data-stu-id="9a11e-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="9a11e-152">Vytvoříme projektu MSBuild, který vytváří všechna řešení, přičemž zajistěte, že se balíčky neobnoví před sestavením řešení.</span><span class="sxs-lookup"><span data-stu-id="9a11e-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="9a11e-153">Tento projekt bude mít tři konvenční cíle `Clean`, `Build` a `Rebuild` i nový cíl `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="9a11e-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="9a11e-154">`Build` a `Rebuild` cíle i závisí na `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="9a11e-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="9a11e-155">Tím je zajištěno, že oba spustíte `Build` a `Rebuild` a Spolehněte se na balíčky, který se má obnovit.</span><span class="sxs-lookup"><span data-stu-id="9a11e-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="9a11e-156">`Clean`, `Build` a `Rebuild` vyvolání odpovídající cíle MSBuild na všechny soubory řešení.</span><span class="sxs-lookup"><span data-stu-id="9a11e-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="9a11e-157">`RestorePackages` Vyvolá cíl `nuget.exe` pro každý soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="9a11e-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="9a11e-158">To lze provést pomocí [funkce v dávkování nástroje MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="9a11e-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="9a11e-159">Výsledek by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="9a11e-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="9a11e-160">Konfigurace týmového sestavení</span><span class="sxs-lookup"><span data-stu-id="9a11e-160">Configuring Team Build</span></span>

<span data-ttu-id="9a11e-161">Týmový Build nabízí různé šablony procesu.</span><span class="sxs-lookup"><span data-stu-id="9a11e-161">Team Build offers various process templates.</span></span> <span data-ttu-id="9a11e-162">Pro tuto ukázku jsme používáte Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="9a11e-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="9a11e-163">I když bude velmi podobně jako na místní instalace TFS.</span><span class="sxs-lookup"><span data-stu-id="9a11e-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="9a11e-164">Git a správa verzí TF mají různé šablony služby Team Build, takže takto se budou lišit v závislosti na tom, který systém správy verzí, kterou používáte.</span><span class="sxs-lookup"><span data-stu-id="9a11e-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="9a11e-165">V obou případech se vše, co potřebujete je výběr build.proj jako projekt, který má být sestaveno.</span><span class="sxs-lookup"><span data-stu-id="9a11e-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="9a11e-166">Nejprve Podívejme se na šablonu procesu pro git.</span><span class="sxs-lookup"><span data-stu-id="9a11e-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="9a11e-167">V šabloně git na základě výběru sestavení prostřednictvím vlastnosti `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="9a11e-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces sestavení pro git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="9a11e-169">Všimněte si, že je tato vlastnost umístění v úložišti.</span><span class="sxs-lookup"><span data-stu-id="9a11e-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="9a11e-170">Protože naše `build.proj` je v kořenovém adresáři, můžeme jednoduše použít `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="9a11e-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="9a11e-171">Pokud byste umístit soubor sestavení v rámci složky s názvem `tools`, bude hodnota `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="9a11e-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="9a11e-172">V šabloně ovládacího prvku verze TF je projekt určen prostřednictvím vlastnosti `Projects`:</span><span class="sxs-lookup"><span data-stu-id="9a11e-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="9a11e-174">Na rozdíl od TF git na základě šablony Správa verzí podporuje výběrech (tlačítko na pravé straně se třemi tečkami).</span><span class="sxs-lookup"><span data-stu-id="9a11e-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="9a11e-175">Proto pokud se chcete vyhnout chybám psaní doporučujeme, že pomocí kterých lze vyberte projekt.</span><span class="sxs-lookup"><span data-stu-id="9a11e-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
