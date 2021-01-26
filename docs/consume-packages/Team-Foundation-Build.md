---
title: Návod k obnovení balíčku NuGet pomocí Team Foundation Build
description: Návod, jak obnovit balíček NuGet pomocí nástroje Team Foundation Build (TFS a Visual Studio Team Services).
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 8b993106d439dc137fbe040b51fda373539de81a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774992"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="be9ab-103">Nastavení obnovení balíčku pomocí Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="be9ab-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="be9ab-104">Tento článek poskytuje podrobný návod k tomu, jak obnovit balíčky v rámci [sestavení Team Services](/vsts/build-release/index) obou pro správu verzí Git i Team Services.</span><span class="sxs-lookup"><span data-stu-id="be9ab-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="be9ab-105">I když je tento návod specifický pro scénář použití Visual Studio Team Services, koncepce se vztahují také na jiné systémy správy verzí a sestavování.</span><span class="sxs-lookup"><span data-stu-id="be9ab-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="be9ab-106">Platí pro:</span><span class="sxs-lookup"><span data-stu-id="be9ab-106">Applies To:</span></span>

- <span data-ttu-id="be9ab-107">Vlastní projekty MSBuild spuštěné v libovolné verzi TFS</span><span class="sxs-lookup"><span data-stu-id="be9ab-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="be9ab-108">Team Foundation Server 2012 nebo starší</span><span class="sxs-lookup"><span data-stu-id="be9ab-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="be9ab-109">Vlastní šablony procesu sestavení Team Foundation migrovány na TFS 2013 nebo novější</span><span class="sxs-lookup"><span data-stu-id="be9ab-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="be9ab-110">Šablony procesu sestavení s odebranými funkcemi obnovení NuGet</span><span class="sxs-lookup"><span data-stu-id="be9ab-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="be9ab-111">Pokud používáte Visual Studio Team Services nebo Team Foundation Server 2013 se svými šablonami procesu sestavení, automatické obnovení balíčků probíhá jako součást procesu sestavení.</span><span class="sxs-lookup"><span data-stu-id="be9ab-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="be9ab-112">Obecný přístup</span><span class="sxs-lookup"><span data-stu-id="be9ab-112">The general approach</span></span>

<span data-ttu-id="be9ab-113">Výhodou použití NuGet je, že ho můžete použít k tomu, abyste se vyhnuli vrácení binárních souborů do systému správy verzí.</span><span class="sxs-lookup"><span data-stu-id="be9ab-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="be9ab-114">To je užitečné hlavně v případě, že používáte [distribuovaný systém správy verzí](https://en.wikipedia.org/wiki/Distributed_revision_control) , jako je git, protože vývojáři potřebují klonovat celé úložiště, včetně úplné historie, aby mohli začít pracovat místně.</span><span class="sxs-lookup"><span data-stu-id="be9ab-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="be9ab-115">Vracení souborů se změnami může způsobit významné dispozici determinističtější úložiště, protože binární soubory jsou obvykle uložené bez rozdílové komprese.</span><span class="sxs-lookup"><span data-stu-id="be9ab-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="be9ab-116">NuGet podporuje [obnovení balíčků](../consume-packages/package-restore.md) v rámci sestavení po dlouhou dobu.</span><span class="sxs-lookup"><span data-stu-id="be9ab-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="be9ab-117">Předchozí implementace obsahovala nevaječný problém pro balíčky, které chtějí tento proces sestavení zvětšit, protože NuGet obnovil balíčky při sestavování projektu.</span><span class="sxs-lookup"><span data-stu-id="be9ab-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="be9ab-118">Nástroj MSBuild ale neumožňuje rozšíření sestavení během sestavení; jedna z nich by mohla tvrdí tento problém v nástroji MSBuild, ale mám tvrdí, že se jedná o podstatný problém.</span><span class="sxs-lookup"><span data-stu-id="be9ab-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="be9ab-119">V závislosti na tom, který aspekt potřebujete roztáhnout, může být příliš pozdě k registraci v době obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="be9ab-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="be9ab-120">K tomuto problému se zajišťují, že se balíčky obnovují jako první krok procesu sestavení:</span><span class="sxs-lookup"><span data-stu-id="be9ab-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="be9ab-121">Když proces sestavení obnoví balíčky před sestavením kódu, nemusíte soubory vracet se změnami `.targets`</span><span class="sxs-lookup"><span data-stu-id="be9ab-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="be9ab-122">Balíčky musí být vytvořeny tak, aby umožňovaly načítání v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be9ab-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="be9ab-123">V opačném případě možná budete chtít soubory vrátit se změnami `.targets` , aby ostatní vývojáři mohli jednoduše otevřít řešení bez nutnosti obnovovat balíčky jako první.</span><span class="sxs-lookup"><span data-stu-id="be9ab-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="be9ab-124">Následující ukázkový projekt ukazuje, jak nastavit sestavení tak, aby `packages` složky a `.targets` soubory nemusely být vráceny se změnami.</span><span class="sxs-lookup"><span data-stu-id="be9ab-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="be9ab-125">Také ukazuje, jak nastavit automatizované sestavení v Team Foundation Service pro tento vzorový projekt.</span><span class="sxs-lookup"><span data-stu-id="be9ab-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="be9ab-126">Struktura úložiště</span><span class="sxs-lookup"><span data-stu-id="be9ab-126">Repository structure</span></span>

<span data-ttu-id="be9ab-127">Náš ukázkový projekt je jednoduchý nástroj příkazového řádku, který používá argument příkazového řádku pro dotazování Bingu.</span><span class="sxs-lookup"><span data-stu-id="be9ab-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="be9ab-128">Cílí na .NET Framework 4 a používá mnoho [balíčků BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.NET. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)a [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="be9ab-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="be9ab-129">Struktura úložiště vypadá následovně:</span><span class="sxs-lookup"><span data-stu-id="be9ab-129">The structure of the repository looks as follows:</span></span>

```
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
```

<span data-ttu-id="be9ab-130">Vidíte, že jsme nevrátili do `packages` složky ani do žádného `.targets` souboru.</span><span class="sxs-lookup"><span data-stu-id="be9ab-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="be9ab-131">V případě, že je `nuget.exe` to v průběhu sestavení potřeba, ale jsme vrátili se změnami.</span><span class="sxs-lookup"><span data-stu-id="be9ab-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="be9ab-132">Tyto široce používané konvence jsme kontrolovali v rámci sdílené `tools` složky.</span><span class="sxs-lookup"><span data-stu-id="be9ab-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="be9ab-133">Zdrojový kód je pod `src` složkou.</span><span class="sxs-lookup"><span data-stu-id="be9ab-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="be9ab-134">I když naše ukázka používá jenom jedno řešení, můžete si snadno představit, že tato složka obsahuje víc než jedno řešení.</span><span class="sxs-lookup"><span data-stu-id="be9ab-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="be9ab-135">Ignorování souborů</span><span class="sxs-lookup"><span data-stu-id="be9ab-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="be9ab-136">[V klientovi NuGet je aktuálně známá chyba](https://nuget.codeplex.com/workitem/4072) , která způsobuje, že klient bude stále přidávat `packages` složku do správy verzí.</span><span class="sxs-lookup"><span data-stu-id="be9ab-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="be9ab-137">Alternativním řešením je zakázat integraci správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="be9ab-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="be9ab-138">Aby to bylo možné, budete potřebovat `Nuget.Config ` soubor ve  `.nuget` složce, která je pro vaše řešení paralelní.</span><span class="sxs-lookup"><span data-stu-id="be9ab-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="be9ab-139">Pokud tato složka ještě neexistuje, je nutné ji vytvořit.</span><span class="sxs-lookup"><span data-stu-id="be9ab-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="be9ab-140">Do [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) přidejte následující obsah:</span><span class="sxs-lookup"><span data-stu-id="be9ab-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="be9ab-141">Pro komunikaci se správou verzí, kterou nezáměrím vracet se změnami složky **balíčků** , jsme také přidali ignorovat soubory pro Git () i pro `.gitignore` správu verzí TF ( `.tfignore` ).</span><span class="sxs-lookup"><span data-stu-id="be9ab-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="be9ab-142">Tyto soubory popisují vzory souborů, které nechcete vrátit se změnami.</span><span class="sxs-lookup"><span data-stu-id="be9ab-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="be9ab-143">`.gitignore`Soubor vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="be9ab-143">The `.gitignore` file looks as follows:</span></span>

```
syntax: glob
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

<span data-ttu-id="be9ab-144">`.gitignore`Soubor je [poměrně výkonný](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="be9ab-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="be9ab-145">Například pokud chcete obecně nevracet obsah složky se změnami, `packages` ale chcete se podívat na předchozí pokyny k vrácení `.targets` souborů, které by mohly mít následující pravidlo:</span><span class="sxs-lookup"><span data-stu-id="be9ab-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

```
packages
!packages/**/*.targets
```

<span data-ttu-id="be9ab-146">Tím se vyloučí všechny `packages` složky, ale znovu se zahrnou všechny obsažené `.targets` soubory.</span><span class="sxs-lookup"><span data-stu-id="be9ab-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="be9ab-147">Způsobem můžete najít šablonu pro `.gitignore` soubory, které jsou speciálně upraveny pro potřeby vývojářů sady Visual Studio. [](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)</span><span class="sxs-lookup"><span data-stu-id="be9ab-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="be9ab-148">Správa verzí TF podporuje velmi podobný mechanismus prostřednictvím souboru [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) .</span><span class="sxs-lookup"><span data-stu-id="be9ab-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="be9ab-149">Syntaxe je prakticky stejná:</span><span class="sxs-lookup"><span data-stu-id="be9ab-149">The syntax is virtually the same:</span></span>

```
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

## <a name="buildproj"></a><span data-ttu-id="be9ab-150">sestavení. proj</span><span class="sxs-lookup"><span data-stu-id="be9ab-150">build.proj</span></span>

<span data-ttu-id="be9ab-151">V naší ukázce udržujeme proces sestavení poměrně jednoduchý.</span><span class="sxs-lookup"><span data-stu-id="be9ab-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="be9ab-152">Vytvoříme projekt MSBuild, který sestaví všechna řešení a zajistěte, aby se balíčky obnovily ještě před sestavením řešení.</span><span class="sxs-lookup"><span data-stu-id="be9ab-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="be9ab-153">Tento projekt bude mít tři konvenční cíle `Clean` `Build` a `Rebuild` také nový cíl `RestorePackages` .</span><span class="sxs-lookup"><span data-stu-id="be9ab-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="be9ab-154">`Build`Cíle a jsou `Rebuild` závislé na `RestorePackages` .</span><span class="sxs-lookup"><span data-stu-id="be9ab-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="be9ab-155">Tím zajistíte, že můžete spouštět i `Build` `Rebuild` a spoléhat na obnovené balíčky.</span><span class="sxs-lookup"><span data-stu-id="be9ab-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="be9ab-156">`Clean``Build`a `Rebuild` vyvolejte odpovídající cíl nástroje MSBuild pro všechny soubory řešení.</span><span class="sxs-lookup"><span data-stu-id="be9ab-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="be9ab-157">`RestorePackages`Cíl vyvolá `nuget.exe` pro každý soubor řešení.</span><span class="sxs-lookup"><span data-stu-id="be9ab-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="be9ab-158">K tomu je možné využít [funkci dávkování MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="be9ab-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="be9ab-159">Výsledek vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="be9ab-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="be9ab-160">Konfigurace týmového sestavení</span><span class="sxs-lookup"><span data-stu-id="be9ab-160">Configuring Team Build</span></span>

<span data-ttu-id="be9ab-161">Týmové sestavení nabízí různé šablony procesů.</span><span class="sxs-lookup"><span data-stu-id="be9ab-161">Team Build offers various process templates.</span></span> <span data-ttu-id="be9ab-162">V této ukázce používáme Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="be9ab-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="be9ab-163">Místní instalace TFS budou velmi podobné, i když.</span><span class="sxs-lookup"><span data-stu-id="be9ab-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="be9ab-164">Správa verzí Gitu a TF mají jiné šablony sestavení týmu, takže následující kroky se budou lišit v závislosti na tom, který systém správy verzí používáte.</span><span class="sxs-lookup"><span data-stu-id="be9ab-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="be9ab-165">V obou případech stačí pouze vybrat sestavit. proj jako projekt, který chcete sestavit.</span><span class="sxs-lookup"><span data-stu-id="be9ab-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="be9ab-166">Nejprve se podívejme na šablonu procesu pro Git.</span><span class="sxs-lookup"><span data-stu-id="be9ab-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="be9ab-167">V šabloně založené na Gitu se sestavení vybere prostřednictvím vlastnosti `Solution to build` :</span><span class="sxs-lookup"><span data-stu-id="be9ab-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces sestavení pro Git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="be9ab-169">Všimněte si, že tato vlastnost je umístění v úložišti.</span><span class="sxs-lookup"><span data-stu-id="be9ab-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="be9ab-170">Vzhledem k tomu `build.proj` , že se nachází v kořenovém adresáři, stačí použít `build.proj` .</span><span class="sxs-lookup"><span data-stu-id="be9ab-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="be9ab-171">Pokud soubor sestavení umístíte do složky s názvem, bude `tools` hodnota `tools\build.proj` .</span><span class="sxs-lookup"><span data-stu-id="be9ab-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="be9ab-172">V šabloně správy verzí TF se projekt vybere prostřednictvím vlastnosti `Projects` :</span><span class="sxs-lookup"><span data-stu-id="be9ab-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces sestavení pro TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="be9ab-174">Na rozdíl od šablony založené na Gitu podporuje Správa verzí TF (tlačítko na pravé straně se třemi tečkami).</span><span class="sxs-lookup"><span data-stu-id="be9ab-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="be9ab-175">Takže pokud chcete zabránit jakýmkoli chybám při psaní, doporučujeme je použít k výběru projektu.</span><span class="sxs-lookup"><span data-stu-id="be9ab-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
