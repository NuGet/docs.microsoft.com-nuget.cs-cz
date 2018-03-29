---
title: Návod balíček NuGet obnovit pomocí aplikace Team Foundation Build | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Návod, jak balíček NuGet obnovení s Team Foundation Build (sady TFS a Visual Studio Team Services).
keywords: Obnovení balíčku NuGet, NuGet a sady TFS, NuGet a služby VSTS, systémy sestavení NuGet, team foundation build, vlastní projektů MSBuild cloudu, nepřetržité integrace sestavení
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f46a7402214bf965918a5195605027913a8c60c2
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="16af6-104">Nastavení obnovení balíčků s Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="16af6-104">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="16af6-105">Tento článek obsahuje podrobný návod k obnovení balíčků jako součást [Team Services Build](/vsts/build-release/index) i pro Git a správě verzí Team Services.</span><span class="sxs-lookup"><span data-stu-id="16af6-105">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="16af6-106">I když Tento názorný postup je specifická pro scénář použití Visual Studio Team Services, koncepty také použít pro další ovládací prvek verze a sestavit systémy.</span><span class="sxs-lookup"><span data-stu-id="16af6-106">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="16af6-107">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="16af6-107">Applies To:</span></span>

- <span data-ttu-id="16af6-108">Vlastní projektů MSBuild spuštěna v libovolné verzi sady TFS</span><span class="sxs-lookup"><span data-stu-id="16af6-108">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="16af6-109">Team Foundation Server 2012 nebo starším</span><span class="sxs-lookup"><span data-stu-id="16af6-109">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="16af6-110">Vlastní Team Foundation sestavení šablony procesů migrovat do sady TFS 2013 nebo novější</span><span class="sxs-lookup"><span data-stu-id="16af6-110">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="16af6-111">Šablony procesu sestavení odebrané funkce obnovení Nuget</span><span class="sxs-lookup"><span data-stu-id="16af6-111">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="16af6-112">Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 s jeho šablony procesu sestavení, se stane balíček automatické obnovení jako součást procesu sestavení.</span><span class="sxs-lookup"><span data-stu-id="16af6-112">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="16af6-113">Obecný přístup</span><span class="sxs-lookup"><span data-stu-id="16af6-113">The general approach</span></span>

<span data-ttu-id="16af6-114">Výhodou použití NuGet je, že jste ji používat předejdete kontrola v binární soubory do systému správy verzí.</span><span class="sxs-lookup"><span data-stu-id="16af6-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="16af6-115">To je zajímavé hlavně, pokud používáte [distribuované verzí](http://en.wikipedia.org/wiki/Distributed_revision_control) systému jako git, protože vývojáři muset klonovat celý úložiště, včetně úplnou historii, před spuštěním lokálně.</span><span class="sxs-lookup"><span data-stu-id="16af6-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="16af6-116">Kontrola v binárních souborech může způsobit významné úložiště tomu, jak binární soubory se obvykle ukládají bez rozdílů komprese.</span><span class="sxs-lookup"><span data-stu-id="16af6-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="16af6-117">Obsahoval podporované NuGet [obnovují se balíčky](../consume-packages/package-restore.md) jako součást sestavení pro typ long čas nyní.</span><span class="sxs-lookup"><span data-stu-id="16af6-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="16af6-118">Předchozí implementace došlo k potížím kuřecí a vaječných pro balíčky, které chcete rozšíření procesu sestavení, protože NuGet při sestavování projektu obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="16af6-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="16af6-119">Ale MSBuild neumožňuje rozšíření sestavení během vytváření sestavení; jeden může uvádějí, které tento problém v nástroji MSBuild, ale I by uvádějí, že se jedná o problém s vyplývajících.</span><span class="sxs-lookup"><span data-stu-id="16af6-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="16af6-120">V závislosti na tom, které aspekt potřebujete rozšířit může být příliš pozdní registrovat, a v době obnovení vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="16af6-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="16af6-121">Vytvrdit tento problém je ubezpečit, že jsou balíčky obnovit jako první krok v procesu sestavení:</span><span class="sxs-lookup"><span data-stu-id="16af6-121">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="16af6-122">Když váš proces sestavení obnoví balíčky před vytvořením kód, nepotřebujete k vrácení se změnami `.targets` soubory</span><span class="sxs-lookup"><span data-stu-id="16af6-122">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="16af6-123">Balíčky musí být vytvořené umožňuje načítání v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16af6-123">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="16af6-124">Jinak, může stále chcete vrátit se změnami `.targets` soubory, aby ostatní vývojáři mohli jednoduše otevřít řešení bez nutnosti nejprve obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="16af6-124">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="16af6-125">Následující ukázkový projekt ukazuje, jak nastavit sestavení takovým způsobem, který `packages` složky a `.targets` soubory nemusí být vráceno se změnami.</span><span class="sxs-lookup"><span data-stu-id="16af6-125">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="16af6-126">Také ukazuje, jak nastavit automatické sestavení na Team Foundation Service pro tento ukázkový projekt.</span><span class="sxs-lookup"><span data-stu-id="16af6-126">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="16af6-127">Struktura úložiště</span><span class="sxs-lookup"><span data-stu-id="16af6-127">Repository structure</span></span>

<span data-ttu-id="16af6-128">Naše ukázkový projekt je nástroj jednoduché příkazového řádku, který používá argument příkazového řádku k dotazu služby Bing.</span><span class="sxs-lookup"><span data-stu-id="16af6-128">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="16af6-129">Jeho cílem rozhraní .NET Framework 4 a používá řadu [BCL balíčky](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), a [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="16af6-129">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="16af6-130">Struktura úložiště vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="16af6-130">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="16af6-131">Uvidíte, že jsme nebyly vráceno se změnami `packages` složku ani žádný `.targets` soubory.</span><span class="sxs-lookup"><span data-stu-id="16af6-131">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="16af6-132">Jsme k dispozici, ale vráceno se změnami `nuget.exe` potřeby během sestavení.</span><span class="sxs-lookup"><span data-stu-id="16af6-132">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="16af6-133">Následující často používají konvence jsme jste změnami ji pod sdílenou `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="16af6-133">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="16af6-134">Zdrojový kód je v části `src` složky.</span><span class="sxs-lookup"><span data-stu-id="16af6-134">The source code is under the `src` folder.</span></span> <span data-ttu-id="16af6-135">I když naše Ukázka používá jenom jedno řešení, můžete snadno představte, že tato složka obsahuje více než jedno řešení.</span><span class="sxs-lookup"><span data-stu-id="16af6-135">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="16af6-136">Ignorování souborů</span><span class="sxs-lookup"><span data-stu-id="16af6-136">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="16af6-137">V současné době není [známého problému v klientovi NuGet](https://nuget.codeplex.com/workitem/4072) který způsobuje, že klient stále přidat `packages` složky do správy verzí.</span><span class="sxs-lookup"><span data-stu-id="16af6-137">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="16af6-138">Alternativní řešení je zakázat integrace ovládacích prvků zdrojového.</span><span class="sxs-lookup"><span data-stu-id="16af6-138">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="16af6-139">Aby bylo možné provést, je nutné `Nuget.Config ` v soubor `.nuget` složky, která je paralelní k řešení.</span><span class="sxs-lookup"><span data-stu-id="16af6-139">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="16af6-140">Pokud tato složka ještě neexistuje, musíte ji vytvořit.</span><span class="sxs-lookup"><span data-stu-id="16af6-140">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="16af6-141">V [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), přidejte do něj následující obsah:</span><span class="sxs-lookup"><span data-stu-id="16af6-141">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="16af6-142">Pro komunikaci se správa verzí, že nepodporujeme záměr vrácení se změnami **balíčky** složek, jsme také doplnili ignorovat soubory pro oba git (`.gitignore`) a také TF správy verzí (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="16af6-142">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="16af6-143">Tyto soubory popisují vzorů souborů, které nechcete použít k vrácení se změnami.</span><span class="sxs-lookup"><span data-stu-id="16af6-143">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="16af6-144">`.gitignore` Souboru vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="16af6-144">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="16af6-145">`.gitignore` Soubor [velmi výkonné](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="16af6-145">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="16af6-146">Například, pokud chcete obecně není vrácení se změnami obsah `packages` složka ale chcete přejít s předchozí pokyny k vrácení se změnami `.targets` soubory můžete mít následující pravidlo místo:</span><span class="sxs-lookup"><span data-stu-id="16af6-146">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="16af6-147">To vyloučí všechny `packages` složky ale bude znovu zahrnout všechny obsažené `.targets` soubory.</span><span class="sxs-lookup"><span data-stu-id="16af6-147">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="16af6-148">Tím, můžete najít šablonu pro `.gitignore` soubory, které je specificky přizpůsobit pro potřeby vývojářů Visual Studio [zde](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="16af6-148">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="16af6-149">Správa verzí TF podporuje velmi podobné mechanismus prostřednictvím [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) souboru.</span><span class="sxs-lookup"><span data-stu-id="16af6-149">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="16af6-150">Syntaxe je v podstatě stejný:</span><span class="sxs-lookup"><span data-stu-id="16af6-150">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="16af6-151">build.proj</span><span class="sxs-lookup"><span data-stu-id="16af6-151">build.proj</span></span>

<span data-ttu-id="16af6-152">Pro naše ukázka jsme zjednodušení procesu sestavení poměrně.</span><span class="sxs-lookup"><span data-stu-id="16af6-152">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="16af6-153">Vytvoříme projektu MSBuild, který sestavuje všechny řešení při a ujistěte se, že jsou balíčky obnovit před vytvořením řešení.</span><span class="sxs-lookup"><span data-stu-id="16af6-153">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="16af6-154">Tento projekt bude mít tři konvenční cíle `Clean`, `Build` a `Rebuild` i nový cíl `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="16af6-154">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="16af6-155">`Build` a `Rebuild` cíle obě závisí na `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="16af6-155">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="16af6-156">Tím je zajištěno, že oba spuštěním `Build` a `Rebuild` a spoléhá na balíčky obnovena.</span><span class="sxs-lookup"><span data-stu-id="16af6-156">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="16af6-157">`Clean`, `Build` a `Rebuild` vyvolání odpovídající cíle MSBuild na všechny soubory řešení.</span><span class="sxs-lookup"><span data-stu-id="16af6-157">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="16af6-158">`RestorePackages` Cíl vyvolá `nuget.exe` pro každý soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="16af6-158">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="16af6-159">To se dá udělat pomocí [je dávkování nástroje MSBuild funkce](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="16af6-159">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="16af6-160">Výsledek vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="16af6-160">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="16af6-161">Konfigurace sestavení Team</span><span class="sxs-lookup"><span data-stu-id="16af6-161">Configuring Team Build</span></span>

<span data-ttu-id="16af6-162">Sestavení Team nabízí různé šablony procesů.</span><span class="sxs-lookup"><span data-stu-id="16af6-162">Team Build offers various process templates.</span></span> <span data-ttu-id="16af6-163">Pro této ukázce používáme Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="16af6-163">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="16af6-164">Když bude velmi podobně jako na místní instalace sady TFS.</span><span class="sxs-lookup"><span data-stu-id="16af6-164">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="16af6-165">Git a správa verzí TF mít různé šablony Team Build, následující postup se bude lišit v závislosti na tom, které systém správy verzí, kterou používáte.</span><span class="sxs-lookup"><span data-stu-id="16af6-165">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="16af6-166">V obou případech je třeba je výběr build.proj jako projekt, který chcete vytvořit.</span><span class="sxs-lookup"><span data-stu-id="16af6-166">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="16af6-167">První Podíváme se na šablony procesu pro git.</span><span class="sxs-lookup"><span data-stu-id="16af6-167">First, let's look at the process template for git.</span></span> <span data-ttu-id="16af6-168">V šabloně git na základě sestavení je vybrána přes vlastnost `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="16af6-168">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces sestavení pro git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="16af6-170">Upozorňujeme, že je tato vlastnost umístění v úložišti.</span><span class="sxs-lookup"><span data-stu-id="16af6-170">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="16af6-171">Protože naše `build.proj` je v kořenovém adresáři, můžeme jednoduše použít `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="16af6-171">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="16af6-172">Pokud umístěte soubor sestavení do složky s názvem `tools`, bude hodnota `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="16af6-172">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="16af6-173">V šabloně TF verze ovládací prvek je vybrán projekt přes vlastnost `Projects`:</span><span class="sxs-lookup"><span data-stu-id="16af6-173">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="16af6-175">Na rozdíl od git na základě šablony TF podporuje Správa verzí ovládacích prvků výběr (tlačítko na pravé straně tři tečky).</span><span class="sxs-lookup"><span data-stu-id="16af6-175">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="16af6-176">Takže aby se zabránilo chybám zadáním doporučujeme že použít vyberte projekt.</span><span class="sxs-lookup"><span data-stu-id="16af6-176">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
