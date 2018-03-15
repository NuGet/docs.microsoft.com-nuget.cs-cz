---
title: "NuGet – nejčastější dotazy | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Běžné otázky a odpovědi na příkazovém řádku a v sadě Visual Studio pomocí nástroje NuGet a práce s galerii NuGet."
keywords: "Verze balíčku NuGet otázek a odpovědí, otázky a odpovědi, běžné problémy, verze NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3782fe5dcf8df002d99446aa7548a6eacc62211c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="e9632-104">Nejčastější dotazy NuGet</span><span class="sxs-lookup"><span data-stu-id="e9632-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="e9632-105">**Co je potřeba spustit NuGet?**</span><span class="sxs-lookup"><span data-stu-id="e9632-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="e9632-106">Všechny informace ohledně uživatelského rozhraní a nástroje příkazového řádku je k dispozici v [instalace Průvodce](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="e9632-107">**Podporuje NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="e9632-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="e9632-108">Nástroj příkazového řádku `nuget.exe`, sestavení a běží pod Mono 3.2 + a balíčky lze vytvořit mono.</span><span class="sxs-lookup"><span data-stu-id="e9632-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="e9632-109">I když `nuget.exe` funguje plně v systému Windows, existují známé problémy na Linuxu a OS X. najdete [Mono problémy](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na Githubu.</span><span class="sxs-lookup"><span data-stu-id="e9632-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="e9632-110">A [grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="e9632-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="e9632-111">**Jak mohu zjistit, co balíček obsahuje a zda je stabilní a užitečné pro Moje aplikace?**</span><span class="sxs-lookup"><span data-stu-id="e9632-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="e9632-112">Primární zdroj informací o balíčku je stránka výpis na nuget.org (nebo jiného privátního kanálu).</span><span class="sxs-lookup"><span data-stu-id="e9632-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="e9632-113">Každý balíček stránky na nuget.org obsahuje popis balíčku, jeho historie verzí a Statistika využití.</span><span class="sxs-lookup"><span data-stu-id="e9632-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="e9632-114">**Informace** části na stránce balíček také obsahuje odkaz na projektu webové stránky, kde je obvykle najít mnoho příklady a další dokumentaci, která vás se způsobu použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="e9632-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="e9632-115">Další informace najdete v tématu [vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="e9632-116">NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9632-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="e9632-117">**Jak se podporuje NuGet v různých produktů Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="e9632-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="e9632-118">Visual Studio v systému Windows podporuje [uživatelského rozhraní Správce balíčků](../tools/package-manager-ui.md) a [Konzola správce balíčků](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-118">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="e9632-119">Visual Studio pro Mac obsahuje integrované funkce NuGet, jak je popsáno na [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="e9632-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="e9632-120">Visual Studio Code (všechny platformy) nemá žádné přímé integrace NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9632-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="e9632-121">Použití [NuGet CLI](../tools/nuget-exe-cli-reference.md) nebo [dotnet rozhraní příkazového řádku](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-121">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="e9632-122">Visual Studio Team Services poskytuje [krok sestavení pro obnovování balíčků NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="e9632-122">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="e9632-123">Můžete také [privátní balíček NuGet hostitele kanály na Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="e9632-123">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="e9632-124">**Jak zkontrolovat přesnou verzi systému NuGet nástroje, které jsou nainstalovány?**</span><span class="sxs-lookup"><span data-stu-id="e9632-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="e9632-125">V sadě Visual Studio, použijte **pomoci > o sadě Microsoft Visual Studio** příkazů a podívejte se na verzi zobrazí vedle možnosti **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e9632-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="e9632-126">Alternativně spusťte konzolu nástroje Správce balíčků (**nástroje > Správce balíčků NuGet > Konzola správce balíčků**) a zadejte `$host` zobrazíte informace o systému NuGet, včetně verze.</span><span class="sxs-lookup"><span data-stu-id="e9632-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="e9632-127">**Jaké programovací jazyky jsou podporované systémem NuGet?**</span><span class="sxs-lookup"><span data-stu-id="e9632-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="e9632-128">NuGet obecně se dá použít pro jazyky rozhraní .NET a je navržená tak, aby knihovny .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="e9632-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="e9632-129">Vzhledem k tomu, že podporuje také MSBuild a Visual Studio automatizace v některé typy projektů, podporuje také další projekty a jazyky do různých stupňů.</span><span class="sxs-lookup"><span data-stu-id="e9632-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="e9632-130">Nejnovější verzi NuGet podporuje C#, Visual Basic, F #, WiX a C++.</span><span class="sxs-lookup"><span data-stu-id="e9632-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="e9632-131">**Jaké šablony projektů jsou podporované systémem NuGet?**</span><span class="sxs-lookup"><span data-stu-id="e9632-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="e9632-132">NuGet má plnou podporu pro celou řadu šablon projektu, například Windows, webové, Cloud, SharePoint, Wix a tak dále.</span><span class="sxs-lookup"><span data-stu-id="e9632-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="e9632-133">**Jak aktualizovat balíčky, které jsou součástí šablony sady Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="e9632-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="e9632-134">Přejděte na **aktualizace** v uživatelském rozhraní Správce balíčků a vyberte **Aktualizovat vše**, nebo použijte [ `Update-Package` příkaz](../tools/ps-ref-update-package.md) z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="e9632-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="e9632-135">Aktualizovat šablonu sám sebe, musíte ručně aktualizovat úložiště šablon.</span><span class="sxs-lookup"><span data-stu-id="e9632-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="e9632-136">V tématu [Xavier Decoster blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na toto téma.</span><span class="sxs-lookup"><span data-stu-id="e9632-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="e9632-137">Všimněte si, že to se provádí na vlastní nebezpečí, protože ruční aktualizace může dojít k poškození šablony Pokud nejnovější verzi všechny závislosti nejsou vzájemně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="e9632-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="e9632-138">**Můžete použít balíček NuGet mimo Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="e9632-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="e9632-139">Ano, NuGet pracuje přímo z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="e9632-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="e9632-140">Najdete v článku [instalace Průvodce](../install-nuget-client-tools.md) a [referenční dokumentace rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="e9632-141">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="e9632-141">NuGet command line</span></span>

<span data-ttu-id="e9632-142">**Jak lze získat nejnovější verzi nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="e9632-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="e9632-143">Najdete v článku [instalace Průvodce](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-143">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="e9632-144">**Co je licence k nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="e9632-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="e9632-145">Jsou povoleny nuget.exe v rámci podmínek licencí MIT znovu distribuovat.</span><span class="sxs-lookup"><span data-stu-id="e9632-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="e9632-146">Jste zodpovědní za aktualizace a údržba všechny kopie nuget.exe, které chcete znovu distribuovat.</span><span class="sxs-lookup"><span data-stu-id="e9632-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="e9632-147">**Je možné rozšířit nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="e9632-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="e9632-148">Ano, je možné přidat vlastní příkazy `nuget.exe`, jak je popsáno v [post Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9632-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="e9632-149">Konzola správce balíčků NuGet (Visual Studio v systému Windows)</span><span class="sxs-lookup"><span data-stu-id="e9632-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="e9632-150">**Jak získat přístup k objektu DTE v konzole Správce balíčků**</span><span class="sxs-lookup"><span data-stu-id="e9632-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="e9632-151">Objekt nejvyšší úrovně v sadě Visual Studio automatizace objektový model se nazývá objekt prostředí DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="e9632-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="e9632-152">To konzole poskytuje prostřednictvím proměnné s názvem `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="e9632-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="e9632-153">Další informace najdete v tématu [Přehled automatizace modelu](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9632-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="e9632-154">**Pokusu převést proměnnou $DTE typu DTE2, ale zobrazí chybová zpráva: nelze převést hodnotu "EnvDTE.DTEClass" typ "EnvDTE.DTEClass" typ "EnvDTE80.DTE2". Co je?**</span><span class="sxs-lookup"><span data-stu-id="e9632-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="e9632-155">Jde o známý problém s jak prostředí PowerShell komunikuje s objektem COM.</span><span class="sxs-lookup"><span data-stu-id="e9632-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="e9632-156">Zkuste následující postup:</span><span class="sxs-lookup"><span data-stu-id="e9632-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="e9632-157">`Get-Interface` Přidat hostitele NuGet PowerShell pomocné funkce.</span><span class="sxs-lookup"><span data-stu-id="e9632-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="e9632-158">Vytváření a publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="e9632-158">Creating and publishing packages</span></span>

<span data-ttu-id="e9632-159">**Jak seznamu Moje balíčku v informačním kanálu?**</span><span class="sxs-lookup"><span data-stu-id="e9632-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="e9632-160">V tématu [vytváření a publikování balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="e9632-161">**Mám několik verzí mé knihovny, které jiné cílové verze rozhraní .NET Framework. Jak lze vytvořit jeden balíček, který to podporuje?**</span><span class="sxs-lookup"><span data-stu-id="e9632-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="e9632-162">V tématu [podpora více verzí rozhraní .NET Framework a profily](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="e9632-163">**Jak mám nastavit vlastní úložiště nebo informační kanál?**</span><span class="sxs-lookup"><span data-stu-id="e9632-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="e9632-164">Najdete v článku [hostování balíčků přehled](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9632-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="e9632-165">**Jak můžete nahrát balíčky pro moje NuGet kanálu hromadně?**</span><span class="sxs-lookup"><span data-stu-id="e9632-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="e9632-166">V tématu [hromadné publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="e9632-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="e9632-167">Práce s balíčky</span><span class="sxs-lookup"><span data-stu-id="e9632-167">Working with packages</span></span>

<span data-ttu-id="e9632-168">**Jaký je rozdíl mezi balíčkem úrovni projektu a řešení úrovni balíčku?**</span><span class="sxs-lookup"><span data-stu-id="e9632-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="e9632-169">Balíček úrovni řešení (NuGet 3.x+) se nainstaluje pouze jednou v řešení a pak je k dispozici pro všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="e9632-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="e9632-170">Balíček úrovni projektu je nainstalována v každém projektu, který používá je.</span><span class="sxs-lookup"><span data-stu-id="e9632-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="e9632-171">Balíček úrovni řešení může také nainstalovat nové příkazy, které lze volat z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="e9632-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="e9632-172">**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**</span><span class="sxs-lookup"><span data-stu-id="e9632-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="e9632-173">Ano, najdete v příspěvku blogu Scott Hanselman [postup při nuget.org je dolů (nebo jste do roviny) získat přístup k NuGet](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="e9632-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="e9632-174">**Jak instalovat balíčky v jiném umístění z výchozí složku balíčků?**</span><span class="sxs-lookup"><span data-stu-id="e9632-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="e9632-175">Nastavte [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) nastavení v `Nuget.Config` pomocí `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="e9632-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="e9632-176">**Jak vyhnout, přidání složky balíčků NuGet do do správy zdrojového kódu?**</span><span class="sxs-lookup"><span data-stu-id="e9632-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="e9632-177">Nastavte [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) v `Nuget.Config` k `true`.</span><span class="sxs-lookup"><span data-stu-id="e9632-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="e9632-178">Tento klíč funguje v řešení úroveň a proto musí být přidán do `$(Solutiondir)\.nuget\Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="e9632-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="e9632-179">Povolení obnovení balíčku ze sady Visual Studio automaticky vytvoří tento soubor.</span><span class="sxs-lookup"><span data-stu-id="e9632-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="e9632-180">**Jak lze vypnout obnovení balíčků?**</span><span class="sxs-lookup"><span data-stu-id="e9632-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="e9632-181">V tématu [povolení a zákaz obnovení balíčků](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="e9632-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="e9632-182">**Proč se zobrazila "Nelze přeložit došlo k chybě závislosti" při instalaci balíčku, místní vzdálené závislosti?**</span><span class="sxs-lookup"><span data-stu-id="e9632-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="e9632-183">Je nutné vybrat **všechny** zdroje při instalaci místní balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="e9632-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="e9632-184">To agreguje informační kanály místo použití pouze jeden.</span><span class="sxs-lookup"><span data-stu-id="e9632-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="e9632-185">Tato chyba se zobrazí důvodem je, že uživatelé místní úložiště se často chtít vyhnout omylem instalaci vzdálených balíčků z důvodu podnikové zásady.</span><span class="sxs-lookup"><span data-stu-id="e9632-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="e9632-186">**Je nutné více projektů ve stejné složce, jak můžete použít samostatné packages.config soubory pro každý projekt?**</span><span class="sxs-lookup"><span data-stu-id="e9632-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="e9632-187">Ve většině projekty bydlišti samostatné projekty v samostatné složky, to není problém jako NuGet identifikuje `packages.config` soubory do každého projektu.</span><span class="sxs-lookup"><span data-stu-id="e9632-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="e9632-188">U balíčku NuGet 3.3 + a více projektů ve stejné složce, můžete vložit název projektu do `packages.config` názvy souborů pomocí vzoru `packages.{project-name}.config`, a NuGet použije tento soubor.</span><span class="sxs-lookup"><span data-stu-id="e9632-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="e9632-189">To není problém při použití PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislosti.</span><span class="sxs-lookup"><span data-stu-id="e9632-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="e9632-190">**Nuget.org se nezobrazí v seznamu úložišť, jak lze získat ho zpátky?**</span><span class="sxs-lookup"><span data-stu-id="e9632-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="e9632-191">Přidat `https://api.nuget.org/v3/index.json` si na seznam zdrojů, nebo</span><span class="sxs-lookup"><span data-stu-id="e9632-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="e9632-192">Odstranit `%appdata%\.nuget\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a umožní NuGet znovu vytvořit.</span><span class="sxs-lookup"><span data-stu-id="e9632-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="e9632-193">**Jaké jsou výchozí licenční podmínky Pokud balíček neposkytuje konkrétní informace o licencích?**</span><span class="sxs-lookup"><span data-stu-id="e9632-193">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="e9632-194">Každý balíček se řídí podmínkami, které jsou součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="e9632-194">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="e9632-195">Přečtěte si podmínky použít před přístup, stahování nebo získávání všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="e9632-195">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="e9632-196">Na nuget.org, použijte **licenční informace** odkaz na stránce balíček.</span><span class="sxs-lookup"><span data-stu-id="e9632-196">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="e9632-197">Pokud balíček neurčuje licenční podmínky, obraťte se na vlastníka balíčku přímo pomocí **obraťte se na vlastníky** odkaz na stránce balíček nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e9632-197">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="e9632-198">Společnost Microsoft není licence duševního vlastnictví vám ze zprostředkovatelů balíček třetích stran a není zodpovědná za informace třetích stran.</span><span class="sxs-lookup"><span data-stu-id="e9632-198">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="e9632-199">Spravovat balíčky v nuget.org</span><span class="sxs-lookup"><span data-stu-id="e9632-199">Managing packages on nuget.org</span></span>

<span data-ttu-id="e9632-200">**Můžete upravit metadata balíčků, až se nahrají? Proč požadujete úpravy soubor nuspec a odesílání nový balíček pro provádění změn do balíčku metadata?**</span><span class="sxs-lookup"><span data-stu-id="e9632-200">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="e9632-201">NuGet vyžaduje všechny balíčky k podepsání.</span><span class="sxs-lookup"><span data-stu-id="e9632-201">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="e9632-202">Princip návrhu podepisování balíčku je, že podepsaný balíček obsahu musí být neměnné, což zahrnuje soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="e9632-202">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="e9632-203">Úpravy metadata balíčků výsledkem změny pro soubor nuspec, zneplatnění existující podpisy.</span><span class="sxs-lookup"><span data-stu-id="e9632-203">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="e9632-204">Doporučujeme, abyste úprava existující pracovní postupy a nevyžadují úpravy metadata balíčků po vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="e9632-204">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="e9632-205">Všimněte si, že pro svůj balíček uvedené závislosti jsou automaticky generovány z balíčku sám sebe a nelze jej upravit.</span><span class="sxs-lookup"><span data-stu-id="e9632-205">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="e9632-206">Kromě toho odesílání balíčků [staging.nuget.org](http://staging.nuget.org) je skvělým způsobem, jak testování a ověření vašeho balíčku bez zpřístupnění balíček ve veřejné galerii.</span><span class="sxs-lookup"><span data-stu-id="e9632-206">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="e9632-207">**Je možné rezervovat názvy pro balíčky, které budou publikovány v budoucnosti?**</span><span class="sxs-lookup"><span data-stu-id="e9632-207">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="e9632-208">Ano.</span><span class="sxs-lookup"><span data-stu-id="e9632-208">Yes.</span></span> <span data-ttu-id="e9632-209">ID můžete vyhradit pro balíčky na [nuget.org](https://www.nuget.org/) tím, že požádá předponu ID balíčku pro váš účet.</span><span class="sxs-lookup"><span data-stu-id="e9632-209">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="e9632-210">Chcete-li požádat o předponu ID balíčku, postupujte podle pokynů [dokumentaci](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span><span class="sxs-lookup"><span data-stu-id="e9632-210">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="e9632-211">**Jak nárokovat vlastnictví pro balíčky?**</span><span class="sxs-lookup"><span data-stu-id="e9632-211">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="e9632-212">V tématu [Správa vlastníků balíčku na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="e9632-212">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="e9632-213">**Řešení s vlastníka balíčku, který je bychom při tom porušili Moje softwarových licencí**</span><span class="sxs-lookup"><span data-stu-id="e9632-213">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="e9632-214">Doporučujeme komunitou NuGet spolupracovat na řešení sporů, které může způsobit mezi balíček vlastníků a vlastníci na ostatní software.</span><span class="sxs-lookup"><span data-stu-id="e9632-214">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="e9632-215">Budeme mít vytvořené [proces řešení sporu](../policies/dispute-resolution.md) dříve, než s dotazem, správcům nuget.org intercede.</span><span class="sxs-lookup"><span data-stu-id="e9632-215">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="e9632-216">**Se doporučuje nahrát Moje testovací balíčky do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="e9632-216">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="e9632-217">Pro účely testování můžete použít [staging.nuget.org](http://staging.nuget.org), nebo jako alternativní veřejné servery NuGet [myget.org](https://myget.org) nebo [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="e9632-217">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="e9632-218">Všimněte si, že balíčky nahrán do staging.nuget.org nelze zachovat.</span><span class="sxs-lookup"><span data-stu-id="e9632-218">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="e9632-219">V tématu [dát sbohem všem preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="e9632-219">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="e9632-220">**Jaká je maximální velikost balíčků, které I můžete uložit do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="e9632-220">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="e9632-221">nuget.org umožňuje balíčky až 250MB, ale nemůžeme doporučujeme zachovat balíčky v části 1MB, pokud je to možné a použití závislosti propojení balíčky současně.</span><span class="sxs-lookup"><span data-stu-id="e9632-221">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="e9632-222">Balíčky jako existuje pravidlo, obsahovat pouze jeden sestavení, aby se zabránilo kolizí.</span><span class="sxs-lookup"><span data-stu-id="e9632-222">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="e9632-223">NuGet stáhnout balíčky, takže větší balíčky mít vyšší pravděpodobnost selhání nainstaluje než menším pomocí protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e9632-223">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="e9632-224">Je možné sdílet závislosti mezi více balíčků, zmenšit velikost stažených pro příjemci vašich balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9632-224">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="e9632-225">Závislosti jsou většinou statické a nikdy změnit.</span><span class="sxs-lookup"><span data-stu-id="e9632-225">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="e9632-226">Při opravě chyby v kódu, nemusí být závislosti nutné aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="e9632-226">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="e9632-227">Pokud jste sady závislosti, skončili reshipping pokaždé, když větší balíčky.</span><span class="sxs-lookup"><span data-stu-id="e9632-227">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="e9632-228">Rozdělením balíčků NuGet do související závislosti, upgrade je mnohem podrobnějšího pro spotřebitele vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="e9632-228">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="e9632-229">není k dispozici nuget.org</span><span class="sxs-lookup"><span data-stu-id="e9632-229">nuget.org not accessible</span></span>

<span data-ttu-id="e9632-230">**Proč nelze stáhnout balíčky nebo balíčky odešlete do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="e9632-230">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="e9632-231">První Ujistěte se, že používáte nejnovější verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="e9632-231">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="e9632-232">Pokud tuto verzi dále nedaří, [obraťte se na podporu](https://www.nuget.org/policies/Contact) a poskytnout další připojení, řešení potíží s informace, včetně:</span><span class="sxs-lookup"><span data-stu-id="e9632-232">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="e9632-233">Verze NuGet používáte</span><span class="sxs-lookup"><span data-stu-id="e9632-233">The version of NuGet you're using</span></span>
- <span data-ttu-id="e9632-234">Zdroje balíčku, kterou používáte</span><span class="sxs-lookup"><span data-stu-id="e9632-234">The package sources you're using</span></span>
- <span data-ttu-id="e9632-235">Obnovení protokolu s podrobné podrobností</span><span class="sxs-lookup"><span data-stu-id="e9632-235">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="e9632-236">MTR nebo Fiddler trasování (viz níže)</span><span class="sxs-lookup"><span data-stu-id="e9632-236">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="e9632-237">Zeměpisná oblast</span><span class="sxs-lookup"><span data-stu-id="e9632-237">Your geographical area</span></span>
- <span data-ttu-id="e9632-238">Verze vašeho operačního systému</span><span class="sxs-lookup"><span data-stu-id="e9632-238">Your operating system version</span></span>
- <span data-ttu-id="e9632-239">Konfigurace počítače (procesor, sítě, pevný disk)</span><span class="sxs-lookup"><span data-stu-id="e9632-239">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="e9632-240">Jestli je váš počítač za proxy nebo brány firewall</span><span class="sxs-lookup"><span data-stu-id="e9632-240">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="e9632-241">Verze rozhraní .NET, které jsou nainstalovány na počítači</span><span class="sxs-lookup"><span data-stu-id="e9632-241">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="e9632-242">Verze nástrojů pro různé platformy jako je rozhraní příkazového řádku .NET nebo dnů, který používáte</span><span class="sxs-lookup"><span data-stu-id="e9632-242">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="e9632-243">*Chcete-li zaznamenat MTR:*</span><span class="sxs-lookup"><span data-stu-id="e9632-243">*To capture MTR:*</span></span>

- <span data-ttu-id="e9632-244">Stáhněte si WinMTR z [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="e9632-244">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="e9632-245">Zadejte `api.nuget.org` jako název hostitele a klikněte na tlačítko **spustit**.</span><span class="sxs-lookup"><span data-stu-id="e9632-245">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="e9632-246">Počkejte **odeslané** sloupec je sloupec > = 100.</span><span class="sxs-lookup"><span data-stu-id="e9632-246">Wait until the **Sent** column is >= 100.</span></span>

    ![Zaznamenání MTR](media/mtr.png)

- <span data-ttu-id="e9632-248">Zkopírujte text do schránky.</span><span class="sxs-lookup"><span data-stu-id="e9632-248">Copy text to clipboard.</span></span>

<span data-ttu-id="e9632-249">*Chcete-li zaznamenat Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="e9632-249">*To capture Fiddler:*</span></span>

- <span data-ttu-id="e9632-250">Nainstalujte nejnovější verzi [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="e9632-250">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="e9632-251">Spusťte aplikaci Fiddler a zakázat pomocí zaznamenávání provoz **soubor > zachycování provozu** nabídky.</span><span class="sxs-lookup"><span data-stu-id="e9632-251">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="e9632-252">Odeberte všechny relace (vyberte všechny položky v seznamu, stiskněte **odstranit** klíč).</span><span class="sxs-lookup"><span data-stu-id="e9632-252">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="e9632-253">Nakonfigurujte aplikaci Fiddler k zachycení provoz HTTPS kontrolou **provoz HTTPS dešifrovat** v **HTTPS** kartě **nástroje > Možnosti Fiddler...**  nabídky.</span><span class="sxs-lookup"><span data-stu-id="e9632-253">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="e9632-254">Zavřete Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9632-254">Close Visual Studio.</span></span>
- <span data-ttu-id="e9632-255">Povolit **soubor > zachycování provozu** nabídky.</span><span class="sxs-lookup"><span data-stu-id="e9632-255">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="e9632-256">Spusťte Visual Studio nebo nuget.exe .exe a provádět akce, které nefungují.</span><span class="sxs-lookup"><span data-stu-id="e9632-256">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="e9632-257">Přenosy dat vytvářené pomocí tyto akce by měl zobrazí v aplikaci Fiddler.</span><span class="sxs-lookup"><span data-stu-id="e9632-257">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="e9632-258">Jakmile akce, které jste spustili, použijte **soubor > Uložit > všechny relace** k uložení zaznamenané relací.</span><span class="sxs-lookup"><span data-stu-id="e9632-258">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="e9632-259">Poznámka: může být nezbytné k nastavení `HTTP_PROXY` proměnnou prostředí `http://127.0.0.1:8888` pro směrování provozu NuGet prostřednictvím aplikaci Fiddler.</span><span class="sxs-lookup"><span data-stu-id="e9632-259">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="e9632-260">Pokud se nezdaří, zkuste [tipy uvedených v tomto blogu StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="e9632-260">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="e9632-261">**Jaké jsou koncové body rozhraní API pro nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="e9632-261">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="e9632-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Všimněte si, že rozhraní API verze 2 je zastaralá a nefunguje s NuGet 4 +.)</span><span class="sxs-lookup"><span data-stu-id="e9632-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
