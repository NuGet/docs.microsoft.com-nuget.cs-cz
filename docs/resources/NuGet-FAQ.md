---
title: NuGet často kladené otázky
description: Běžné otázky a odpovědi pro použití NuGet na příkazovém řádku a v sadě Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "69999942"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="503b0-103">NuGet nejčastější dotazy</span><span class="sxs-lookup"><span data-stu-id="503b0-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="503b0-104">Nejčastější dotazy týkající se NuGet.org, například NuGet.org otázky k účtu, naleznete [v NuGet.org často kladených otázkách](../nuget-org/nuget-org-faq.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="503b0-105">**Co je nutné ke spuštění NuGet?**</span><span class="sxs-lookup"><span data-stu-id="503b0-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="503b0-106">Všechny informace o nástroji ui i příkazového řádku jsou k dispozici v [průvodci instalací](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="503b0-107">**Podporuje NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="503b0-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="503b0-108">Nástroj příkazového řádku `nuget.exe`, , sestaví a spustí pod Mono 3.2+ a můžete vytvořit balíčky v Mono.</span><span class="sxs-lookup"><span data-stu-id="503b0-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="503b0-109">Ačkoli `nuget.exe` funguje plně na Windows, existují známé problémy na Linuxu a OS X. Viz [Problémy Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="503b0-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="503b0-110">[Grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="503b0-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="503b0-111">**Jak zjistím, co balíček obsahuje a zda je stabilní a užitečný pro mou aplikaci?**</span><span class="sxs-lookup"><span data-stu-id="503b0-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="503b0-112">Primárním zdrojem pro učení o balíčku je jeho výpis stránky na nuget.org (nebo jiný soukromý zdroj).</span><span class="sxs-lookup"><span data-stu-id="503b0-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="503b0-113">Každá stránka balíčku na nuget.org obsahuje popis balíčku, jeho historii verzí a statistiky využití.</span><span class="sxs-lookup"><span data-stu-id="503b0-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="503b0-114">Část **Informace** na stránce balíčku také obsahuje odkaz na web projektu, kde obvykle najdete mnoho příkladů a další dokumentaci, která vám pomůže zjistit, jak se balíček používá.</span><span class="sxs-lookup"><span data-stu-id="503b0-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="503b0-115">Další informace naleznete v [tématu Hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="503b0-116">NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="503b0-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="503b0-117">**Jak je NuGet podporován v různých produktech sady Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="503b0-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="503b0-118">Visual Studio v systému Windows podporuje [ui Správce balíčků](../consume-packages/install-use-packages-visual-studio.md) a [konzolu Správce balíčků](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="503b0-119">Visual Studio pro Mac má integrované funkce NuGet, jak je popsáno na [včetně balíčku NuGet v projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="503b0-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="503b0-120">Visual Studio Code (všechny platformy) nemá žádné přímé NuGet integrace.</span><span class="sxs-lookup"><span data-stu-id="503b0-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="503b0-121">Použijte [rozhraní se konstituce NuGet](../reference/nuget-exe-cli-reference.md) nebo [rozhraní se kontinu pro dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="503b0-122">Azure DevOps poskytuje [krok sestavení k obnovení balíčků NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="503b0-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="503b0-123">Můžete také [hostovat privátní nugetové kanály balíčků v Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="503b0-123">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="503b0-124">**Jak lze zkontrolovat přesnou verzi nástrojů NuGet, které jsou nainstalovány?**</span><span class="sxs-lookup"><span data-stu-id="503b0-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="503b0-125">V sadě Visual Studio použijte příkaz **Nápověda > o aplikaci Microsoft Visual Studio** a podívejte se na verzi zobrazenou vedle **správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="503b0-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="503b0-126">Případně spusťte konzolu Správce balíčků **(Nástroje > NuGet Správce balíčků > konzoli správce balíčků)** a zadejte `$host` informace o NuGet včetně verze.</span><span class="sxs-lookup"><span data-stu-id="503b0-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="503b0-127">**Jaké programovací jazyky jsou podporovány NuGet?**</span><span class="sxs-lookup"><span data-stu-id="503b0-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="503b0-128">NuGet obecně funguje pro jazyky .NET a je navržen tak, aby knihovny .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="503b0-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="503b0-129">Vzhledem k tomu, že také podporuje automatizaci MSBuild a Visual Studio v některých typech projektů, podporuje také jiné projekty a jazyky v různých stupních.</span><span class="sxs-lookup"><span data-stu-id="503b0-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="503b0-130">Nejnovější verze NuGet podporuje C#, Visual Basic, F#, WiX a C++.</span><span class="sxs-lookup"><span data-stu-id="503b0-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="503b0-131">**Jaké šablony projektů jsou podporovány nugetem?**</span><span class="sxs-lookup"><span data-stu-id="503b0-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="503b0-132">NuGet má plnou podporu pro různé šablony projektů, jako jsou Windows, Web, Cloud, SharePoint, Wix a tak dále.</span><span class="sxs-lookup"><span data-stu-id="503b0-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="503b0-133">**Jak lze aktualizovat balíčky, které jsou součástí šablon sady Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="503b0-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="503b0-134">Přejděte na kartu **Aktualizace** v uzdu Správce balíčků a vyberte **Aktualizovat vše**nebo použijte [ `Update-Package` příkaz](../reference/ps-reference/ps-ref-update-package.md) z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="503b0-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="503b0-135">Chcete-li aktualizovat samotnou šablonu, musíte ručně aktualizovat úložiště šablon.</span><span class="sxs-lookup"><span data-stu-id="503b0-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="503b0-136">Viz [Xavier Decoster blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na toto téma.</span><span class="sxs-lookup"><span data-stu-id="503b0-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="503b0-137">Všimněte si, že se to provádí na vlastní nebezpečí, protože ruční aktualizace může poškodit šablonu, pokud nejnovější verze všech závislostí nejsou vzájemně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="503b0-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="503b0-138">**Je možné použít NuGet mimo Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="503b0-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="503b0-139">Ano, NuGet funguje přímo z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="503b0-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="503b0-140">Viz [průvodce instalací](../install-nuget-client-tools.md) a [odkaz na vzpona v nařízení o vyřizování mu sekacího systému](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="503b0-141">Příkazový řádek NuGet</span><span class="sxs-lookup"><span data-stu-id="503b0-141">NuGet command line</span></span>

<span data-ttu-id="503b0-142">**Jak získám nejnovější verzi nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="503b0-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="503b0-143">Viz [průvodce instalací](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="503b0-144">Chcete-li zkontrolovat aktuální nainstalovanou `nuget help`verzi nástroje, použijte .</span><span class="sxs-lookup"><span data-stu-id="503b0-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="503b0-145">**Jaká je licence pro nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="503b0-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="503b0-146">Můžete distribuovat nuget.exe podle podmínek licence MIT.</span><span class="sxs-lookup"><span data-stu-id="503b0-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="503b0-147">Jste zodpovědní za aktualizaci a údržbu všech kopií nuget.exe, které se rozhodnete redistribuovat.</span><span class="sxs-lookup"><span data-stu-id="503b0-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="503b0-148">**Je možné rozšířit nástroj příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="503b0-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="503b0-149">Ano, je možné přidat vlastní příkazy , `nuget.exe`jak je popsáno v [příspěvku Roba Reynolda](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="503b0-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="503b0-150">Konzola Správce balíčků NuGet (Visual Studio v systému Windows)</span><span class="sxs-lookup"><span data-stu-id="503b0-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="503b0-151">**Jak získám přístup k objektu DTE v konzole Správce balíčků?**</span><span class="sxs-lookup"><span data-stu-id="503b0-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="503b0-152">Objekt nejvyšší úrovně v objektovém modelu automatizace sady Visual Studio se nazývá objekt DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="503b0-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="503b0-153">Konzola poskytuje prostřednictvím `$DTE`proměnné s názvem .</span><span class="sxs-lookup"><span data-stu-id="503b0-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="503b0-154">Další informace naleznete v [tématu Přehled modelu automatizace](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="503b0-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="503b0-155">**Snažím se přetypovat proměnnou $DTE na typ DTE2, ale zobrazí se chyba: Nelze převést hodnotu "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co je?**</span><span class="sxs-lookup"><span data-stu-id="503b0-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="503b0-156">Toto je známý problém s tím, jak prostředí PowerShell spolupracuje s objektem COM.</span><span class="sxs-lookup"><span data-stu-id="503b0-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="503b0-157">Vyzkoušejte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="503b0-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="503b0-158">`Get-Interface`je pomocná funkce přidaná hostitelem prostředí NuGet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="503b0-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="503b0-159">Vytváření a publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="503b0-159">Creating and publishing packages</span></span>

<span data-ttu-id="503b0-160">**Jak mohu uvést svůj balíček v informačním kanálu?**</span><span class="sxs-lookup"><span data-stu-id="503b0-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="503b0-161">Viz [Vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="503b0-162">**Mám více verzí knihovny, které cílí na různé verze rozhraní .NET Framework. Jak vytvořím jeden balíček, který to podporuje?**</span><span class="sxs-lookup"><span data-stu-id="503b0-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="503b0-163">Viz [Podpora více verzí a profilů rozhraní .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="503b0-164">**Jak si nastavím vlastní úložiště nebo informační kanál?**</span><span class="sxs-lookup"><span data-stu-id="503b0-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="503b0-165">Podívejte se na [přehled hostingových balíčků](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="503b0-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="503b0-166">**Jak mohu nahrát balíčky do mého NuGet feed hromadně?**</span><span class="sxs-lookup"><span data-stu-id="503b0-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="503b0-167">Viz [Hromadné publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="503b0-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="503b0-168">Práce s balíčky</span><span class="sxs-lookup"><span data-stu-id="503b0-168">Working with packages</span></span>

<span data-ttu-id="503b0-169">**Jaký je rozdíl mezi balíčkem na úrovni projektu a balíčkem na úrovni řešení?**</span><span class="sxs-lookup"><span data-stu-id="503b0-169">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="503b0-170">Balíček na úrovni řešení (NuGet 3.x+) je nainstalován pouze jednou v řešení a je pak k dispozici pro všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="503b0-170">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="503b0-171">Balíček na úrovni projektu je nainstalován v každém projektu, který jej používá.</span><span class="sxs-lookup"><span data-stu-id="503b0-171">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="503b0-172">Balíček na úrovni řešení může také nainstalovat nové příkazy, které lze volat z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="503b0-172">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="503b0-173">**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**</span><span class="sxs-lookup"><span data-stu-id="503b0-173">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="503b0-174">Ano, viz příspěvek blogu Scotta Hanselmana [Jak získat přístup k NuGetu, když je nuget.org vypnutý (nebo jste v letadle)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="503b0-174">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="503b0-175">**Jak nainstaluji balíčky do jiného umístění než výchozí složka balíčků?**</span><span class="sxs-lookup"><span data-stu-id="503b0-175">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="503b0-176">Nastavte [`repositoryPath`](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` v `nuget config -set repositoryPath=<path>`použití .</span><span class="sxs-lookup"><span data-stu-id="503b0-176">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="503b0-177">**Jak se vyhnout přidání složky balíčky NuGet do správy zdrojového kódu?**</span><span class="sxs-lookup"><span data-stu-id="503b0-177">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="503b0-178">Nastavte [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` `true`na .</span><span class="sxs-lookup"><span data-stu-id="503b0-178">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="503b0-179">Tento klíč funguje na úrovni řešení, a `$(Solutiondir)\.nuget\Nuget.Config` proto je třeba přidat do souboru.</span><span class="sxs-lookup"><span data-stu-id="503b0-179">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="503b0-180">Povolení obnovení balíčku z aplikace Visual Studio vytvoří tento soubor automaticky.</span><span class="sxs-lookup"><span data-stu-id="503b0-180">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="503b0-181">**Jak vypnu obnovení balíčku?**</span><span class="sxs-lookup"><span data-stu-id="503b0-181">**How do I turn off package restore?**</span></span>

<span data-ttu-id="503b0-182">Viz [Povolení a zakázání obnovení balíčku](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="503b0-182">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="503b0-183">**Proč se při instalaci místního balíčku se vzdálenými závislostmi zobrazuje chyba "Nelze vyřešit chybu závislostí"?**</span><span class="sxs-lookup"><span data-stu-id="503b0-183">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="503b0-184">Při instalaci místního balíčku do projektu je třeba vybrat zdroj **Vše.**</span><span class="sxs-lookup"><span data-stu-id="503b0-184">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="503b0-185">Tím se agreguje všechny kanály namísto použití pouze jednoho.</span><span class="sxs-lookup"><span data-stu-id="503b0-185">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="503b0-186">Důvodem, proč se tato chyba zobrazuje, je to, že uživatelé místního úložiště se často chtějí vyhnout náhodné instalaci vzdáleného balíčku kvůli firemním vazbám.</span><span class="sxs-lookup"><span data-stu-id="503b0-186">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="503b0-187">**Mám více projektů ve stejné složce, jak mohu použít samostatné packages.config soubory pro každý projekt?**</span><span class="sxs-lookup"><span data-stu-id="503b0-187">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="503b0-188">Ve většině projektů, kde samostatné projekty žijí v samostatných složkách, to není problém jako NuGet identifikuje `packages.config` soubory v každém projektu.</span><span class="sxs-lookup"><span data-stu-id="503b0-188">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="503b0-189">S NuGet 3.3+ a více projektů ve stejné složce, můžete `packages.config` vložit název `packages.{project-name}.config`projektu do názvy souborů použít vzor a NuGet používá tento soubor.</span><span class="sxs-lookup"><span data-stu-id="503b0-189">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="503b0-190">To to není problém při použití PackageReference, jako každý soubor projektu obsahuje vlastní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="503b0-190">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="503b0-191">**V seznamu úložišť nevidím nuget.org, jak je získám zpět?**</span><span class="sxs-lookup"><span data-stu-id="503b0-191">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="503b0-192">Přidejte `https://api.nuget.org/v3/index.json` do seznamu zdrojů nebo</span><span class="sxs-lookup"><span data-stu-id="503b0-192">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="503b0-193">Odstranit `%appdata%\.nuget\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` nebo (Mac/Linux) a nechat NuGet znovu vytvořit.</span><span class="sxs-lookup"><span data-stu-id="503b0-193">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
