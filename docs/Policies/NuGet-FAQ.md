---
title: "NuGet – nejčastější dotazy | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "Běžné otázky a odpovědi na příkazovém řádku a v sadě Visual Studio pomocí nástroje NuGet a práce s galerii NuGet."
keywords: "Verze balíčku NuGet otázek a odpovědí, otázky a odpovědi, běžné problémy, verze NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 105fa6e1cad3d163b673376c74ce9c835a0b5059
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="cb170-104">Nejčastější dotazy NuGet</span><span class="sxs-lookup"><span data-stu-id="cb170-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="cb170-105">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="cb170-105">In this topic:</span></span>

- [<span data-ttu-id="cb170-106">Začínáme</span><span class="sxs-lookup"><span data-stu-id="cb170-106">Getting started</span></span>](#getting-started)
- [<span data-ttu-id="cb170-107">NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb170-107">NuGet in Visual Studio</span></span>](#nuget-in-visual-studio)
- [<span data-ttu-id="cb170-108">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="cb170-108">NuGet command line</span></span>](#nuget-command-line)
- [<span data-ttu-id="cb170-109">Konzola správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="cb170-109">NuGet Package Manager Console</span></span>](#nuget-package-manager-console)
- [<span data-ttu-id="cb170-110">Vytváření a publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="cb170-110">Creating and publishing packages</span></span>](#creating-and-publishing-packages)
- [<span data-ttu-id="cb170-111">Práce s balíčky</span><span class="sxs-lookup"><span data-stu-id="cb170-111">Working with packages</span></span>](#working-with-packages)
- [<span data-ttu-id="cb170-112">Spravovat balíčky v nuget.org</span><span class="sxs-lookup"><span data-stu-id="cb170-112">Managing packages on nuget.org</span></span>](#managing-packages-on-nugetorg)
- [<span data-ttu-id="cb170-113">není k dispozici nuget.org</span><span class="sxs-lookup"><span data-stu-id="cb170-113">nuget.org not accessible</span></span>](#nugetorg-not-accessible)

## <a name="getting-started"></a><span data-ttu-id="cb170-114">Začínáme</span><span class="sxs-lookup"><span data-stu-id="cb170-114">Getting started</span></span>

<span data-ttu-id="cb170-115">**Co je potřeba spustit NuGet?**</span><span class="sxs-lookup"><span data-stu-id="cb170-115">**What is required to run NuGet?**</span></span>

<span data-ttu-id="cb170-116">Všechny informace ohledně uživatelského rozhraní a nástroje příkazového řádku je k dispozici v [instalace Průvodce](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-116">All the information around both UI and command-line tools is available in the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="cb170-117">**Podporuje NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="cb170-117">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="cb170-118">Nástroj příkazového řádku `nuget.exe`, sestavení a běží pod Mono 3.2 + a balíčky lze vytvořit mono.</span><span class="sxs-lookup"><span data-stu-id="cb170-118">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="cb170-119">I když `nuget.exe` funguje plně v systému Windows, existují známé problémy na Linuxu a OS X. najdete [Mono problémy](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na Githubu.</span><span class="sxs-lookup"><span data-stu-id="cb170-119">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="cb170-120">A [grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="cb170-120">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="cb170-121">**Jak mohu zjistit, co balíček obsahuje a zda je stabilní a užitečné pro Moje aplikace?**</span><span class="sxs-lookup"><span data-stu-id="cb170-121">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="cb170-122">Primární zdroj informací o balíčku je stránka výpis na nuget.org (nebo jiného privátního kanálu).</span><span class="sxs-lookup"><span data-stu-id="cb170-122">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="cb170-123">Každý balíček stránky na nuget.org obsahuje popis balíčku, jeho historie verzí a Statistika využití.</span><span class="sxs-lookup"><span data-stu-id="cb170-123">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="cb170-124">**Informace** části na stránce balíček také obsahuje odkaz na projektu webové stránky, kde je obvykle najít mnoho příklady a další dokumentaci, která vás se způsobu použití balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb170-124">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="cb170-125">Další informace najdete v tématu [vyhledání a výběr balíčků](../Consume-Packages/Finding-and-Choosing-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-125">For more information, see [Finding and choosing packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="cb170-126">NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb170-126">NuGet in Visual Studio</span></span>

<span data-ttu-id="cb170-127">**Jak se podporuje NuGet v různých produktů Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="cb170-127">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="cb170-128">Visual Studio v systému Windows podporuje [uživatelského rozhraní Správce balíčků](../tools/Package-Manager-UI.md) a [Konzola správce balíčků](../tools/Package-Manager-Console.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-128">Visual Studio on Windows supports the [Package Manager UI](../tools/Package-Manager-UI.md) and the [Package Manager Console](../tools/Package-Manager-Console.md).</span></span>
- <span data-ttu-id="cb170-129">Visual Studio pro Mac obsahuje integrované funkce NuGet, jak je popsáno na [balíček včetně NuGet ve vašem projektu](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="cb170-129">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="cb170-130">Visual Studio Code (všechny platformy) nemá žádné přímé integrace NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb170-130">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="cb170-131">Použití [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) nebo [dotnet rozhraní příkazového řádku](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-131">Use the [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="cb170-132">Visual Studio Team Services poskytuje [krok sestavení pro obnovování balíčků NuGet](https://docs.microsoft.com/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="cb170-132">Visual Studio Team Services provides [a build step to restore NuGet packages](https://docs.microsoft.com/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="cb170-133">Můžete také [privátní balíček NuGet hostitele kanály na Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="cb170-133">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="cb170-134">**Jak zkontrolovat přesnou verzi systému NuGet nástroje, které jsou nainstalovány?**</span><span class="sxs-lookup"><span data-stu-id="cb170-134">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="cb170-135">V sadě Visual Studio, použijte **pomoci > o sadě Microsoft Visual Studio** příkazů a podívejte se na verzi zobrazí vedle možnosti **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cb170-135">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="cb170-136">Alternativně spusťte konzolu nástroje Správce balíčků (**nástroje > Správce balíčků NuGet > Konzola správce balíčků**) a zadejte `$host` zobrazíte informace o systému NuGet, včetně verze.</span><span class="sxs-lookup"><span data-stu-id="cb170-136">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="cb170-137">**Jaké programovací jazyky jsou podporované systémem NuGet?**</span><span class="sxs-lookup"><span data-stu-id="cb170-137">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="cb170-138">NuGet obecně se dá použít pro jazyky rozhraní .NET a je navržená tak, aby knihovny .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="cb170-138">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="cb170-139">Vzhledem k tomu, že podporuje také MSBuild a Visual Studio automatizace v některé typy projektů, podporuje také další projekty a jazyky do různých stupňů.</span><span class="sxs-lookup"><span data-stu-id="cb170-139">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="cb170-140">Nejnovější verzi NuGet podporuje C#, Visual Basic, F #, WiX a C++.</span><span class="sxs-lookup"><span data-stu-id="cb170-140">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="cb170-141">**Jaké šablony projektů jsou podporované systémem NuGet?**</span><span class="sxs-lookup"><span data-stu-id="cb170-141">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="cb170-142">NuGet má plnou podporu pro celou řadu šablon projektu, například Windows, webové, Cloud, SharePoint, Wix a tak dále.</span><span class="sxs-lookup"><span data-stu-id="cb170-142">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="cb170-143">**Jak aktualizovat balíčky, které jsou součástí šablony sady Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="cb170-143">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="cb170-144">Přejděte na **aktualizace** v uživatelském rozhraní Správce balíčků a vyberte **Aktualizovat vše**, nebo použijte [ `Update-Package` příkaz](../Tools/ps-ref-update-package.md) z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="cb170-144">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../Tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="cb170-145">Aktualizovat šablonu sám sebe, musíte ručně aktualizovat úložiště šablon.</span><span class="sxs-lookup"><span data-stu-id="cb170-145">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="cb170-146">V tématu [Xavier Decoster blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na toto téma.</span><span class="sxs-lookup"><span data-stu-id="cb170-146">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="cb170-147">Všimněte si, že to se provádí na vlastní nebezpečí, protože ruční aktualizace může dojít k poškození šablony Pokud nejnovější verzi všechny závislosti nejsou vzájemně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="cb170-147">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="cb170-148">**Můžete použít balíček NuGet mimo Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="cb170-148">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="cb170-149">Ano, NuGet pracuje přímo z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="cb170-149">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="cb170-150">Najdete v článku [instalace Průvodce](../guides/install-nuget.md) a [referenční dokumentace rozhraní příkazového řádku](../tools/nuget-exe-CLI-Reference.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-150">See the [Install guide](../guides/install-nuget.md) and the [CLI reference](../tools/nuget-exe-CLI-Reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="cb170-151">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="cb170-151">NuGet command line</span></span>

<span data-ttu-id="cb170-152">**Jak lze získat nejnovější verzi nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="cb170-152">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="cb170-153">Najdete v článku [instalace Průvodce](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-153">See the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="cb170-154">**Je možné rozšířit nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="cb170-154">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="cb170-155">Ano, je možné přidat vlastní příkazy `nuget.exe`, jak je popsáno v [post Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb170-155">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="cb170-156">Konzola správce balíčků NuGet (Visual Studio v systému Windows)</span><span class="sxs-lookup"><span data-stu-id="cb170-156">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="cb170-157">**Jak získat přístup k objektu DTE v konzole Správce balíčků**</span><span class="sxs-lookup"><span data-stu-id="cb170-157">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="cb170-158">Objekt nejvyšší úrovně v sadě Visual Studio automatizace objektový model se nazývá objekt prostředí DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="cb170-158">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="cb170-159">To konzole poskytuje prostřednictvím proměnné s názvem `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="cb170-159">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="cb170-160">Další informace najdete v tématu [Přehled automatizace modelu](https://docs.microsoft.com/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb170-160">For more information, see [Automation Model Overview](https://docs.microsoft.com/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="cb170-161">**Pokusu převést proměnnou $DTE typu DTE2, ale zobrazí chybová zpráva: nelze převést hodnotu "EnvDTE.DTEClass" typ "EnvDTE.DTEClass" typ "EnvDTE80.DTE2". Co je?**</span><span class="sxs-lookup"><span data-stu-id="cb170-161">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="cb170-162">Jde o známý problém s jak prostředí PowerShell komunikuje s objektem COM.</span><span class="sxs-lookup"><span data-stu-id="cb170-162">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="cb170-163">Zkuste následující postup:</span><span class="sxs-lookup"><span data-stu-id="cb170-163">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="cb170-164">`Get-Interface`Přidat hostitele NuGet PowerShell pomocné funkce.</span><span class="sxs-lookup"><span data-stu-id="cb170-164">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="cb170-165">Vytváření a publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="cb170-165">Creating and publishing packages</span></span>

<span data-ttu-id="cb170-166">**Jak seznamu Moje balíčku v informačním kanálu?**</span><span class="sxs-lookup"><span data-stu-id="cb170-166">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="cb170-167">V tématu [vytváření a publikování balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-167">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="cb170-168">**Mám několik verzí mé knihovny, které jiné cílové verze rozhraní .NET Framework. Jak lze vytvořit jeden balíček, který to podporuje?**</span><span class="sxs-lookup"><span data-stu-id="cb170-168">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="cb170-169">V tématu [podpora více verzí rozhraní .NET Framework a profily](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-169">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="cb170-170">**Jak mám nastavit vlastní úložiště nebo informační kanál?**</span><span class="sxs-lookup"><span data-stu-id="cb170-170">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="cb170-171">Najdete v článku [hostování balíčků přehled](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="cb170-171">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="cb170-172">**Jak můžete nahrát balíčky pro moje NuGet kanálu hromadně?**</span><span class="sxs-lookup"><span data-stu-id="cb170-172">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="cb170-173">V tématu [hromadné publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="cb170-173">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="cb170-174">Práce s balíčky</span><span class="sxs-lookup"><span data-stu-id="cb170-174">Working with packages</span></span>

<span data-ttu-id="cb170-175">**Jaký je rozdíl mezi balíčkem úrovni projektu a řešení úrovni balíčku?**</span><span class="sxs-lookup"><span data-stu-id="cb170-175">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="cb170-176">Balíček úrovni řešení (NuGet 3.x+) se nainstaluje pouze jednou v řešení a pak je k dispozici pro všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="cb170-176">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="cb170-177">Balíček úrovni projektu je nainstalována v každém projektu, který používá je.</span><span class="sxs-lookup"><span data-stu-id="cb170-177">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="cb170-178">Balíček úrovni řešení může také nainstalovat nové příkazy, které lze volat z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="cb170-178">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="cb170-179">**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**</span><span class="sxs-lookup"><span data-stu-id="cb170-179">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="cb170-180">Ano, najdete v příspěvku blogu Scott Hanselman [postup při nuget.org je dolů (nebo jste do roviny) získat přístup k NuGet](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="cb170-180">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="cb170-181">**Jak instalovat balíčky v jiném umístění z výchozí složku balíčků?**</span><span class="sxs-lookup"><span data-stu-id="cb170-181">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="cb170-182">Nastavte [ `repositoryPath` ](../Schema/nuget-config-file.md#config-section) nastavení v `Nuget.Config` pomocí `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="cb170-182">Set the [`repositoryPath`](../Schema/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="cb170-183">**Jak vyhnout, přidání složky balíčků NuGet do do správy zdrojového kódu?**</span><span class="sxs-lookup"><span data-stu-id="cb170-183">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="cb170-184">Nastavte [ `disableSourceControlIntegration` ](../Schema/nuget-config-file.md#solution-section) v `Nuget.Config` k `true`.</span><span class="sxs-lookup"><span data-stu-id="cb170-184">Set the [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="cb170-185">Tento klíč funguje v řešení úroveň a proto musí být přidán do `$(Solutiondir)\.nuget\Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="cb170-185">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="cb170-186">Povolení obnovení balíčku ze sady Visual Studio automaticky vytvoří tento soubor.</span><span class="sxs-lookup"><span data-stu-id="cb170-186">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="cb170-187">**Jak lze vypnout obnovení balíčků?**</span><span class="sxs-lookup"><span data-stu-id="cb170-187">**How do I turn off package restore?**</span></span>

<span data-ttu-id="cb170-188">V tématu [povolení a zákaz obnovení balíčků](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="cb170-188">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="cb170-189">**Proč se zobrazila "Nelze přeložit došlo k chybě závislosti" při instalaci balíčku, místní vzdálené závislosti?**</span><span class="sxs-lookup"><span data-stu-id="cb170-189">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="cb170-190">Je nutné vybrat **všechny** zdroje při instalaci místní balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="cb170-190">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="cb170-191">To agreguje informační kanály místo použití pouze jeden.</span><span class="sxs-lookup"><span data-stu-id="cb170-191">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="cb170-192">Tato chyba se zobrazí důvodem je, že uživatelé místní úložiště se často chtít vyhnout omylem instalaci vzdálených balíčků z důvodu podnikové zásady.</span><span class="sxs-lookup"><span data-stu-id="cb170-192">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="cb170-193">**Je nutné více projektů ve stejné složce, jak můžete použít samostatné packages.config soubory pro každý projekt?**</span><span class="sxs-lookup"><span data-stu-id="cb170-193">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="cb170-194">Ve většině projekty bydlišti samostatné projekty v samostatné složky, to není problém jako NuGet identifikuje `packages.config` soubory do každého projektu.</span><span class="sxs-lookup"><span data-stu-id="cb170-194">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="cb170-195">U balíčku NuGet 3.3 + a více projektů ve stejné složce, můžete vložit název projektu do `packages.config` názvy souborů pomocí vzoru `packages.{project-name}.config`, a NuGet použije tento soubor.</span><span class="sxs-lookup"><span data-stu-id="cb170-195">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="cb170-196">To není problém při použití PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislosti.</span><span class="sxs-lookup"><span data-stu-id="cb170-196">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="cb170-197">**Nuget.org se nezobrazí v seznamu úložišť, jak lze získat ho zpátky?**</span><span class="sxs-lookup"><span data-stu-id="cb170-197">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="cb170-198">Přidat `https://api.nuget.org/v3/index.json` si na seznam zdrojů, nebo</span><span class="sxs-lookup"><span data-stu-id="cb170-198">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="cb170-199">Odstranit `%appdata%\.nuget\NuGet.Config` a nechat NuGet znovu vytvořit.</span><span class="sxs-lookup"><span data-stu-id="cb170-199">Delete the `%appdata%\.nuget\NuGet.Config` and let NuGet re-create it.</span></span>

<span data-ttu-id="cb170-200">**Jaké jsou výchozí licenční podmínky Pokud balíček neposkytuje konkrétní informace o licencích?**</span><span class="sxs-lookup"><span data-stu-id="cb170-200">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="cb170-201">Každý balíček se řídí podmínkami, které jsou součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb170-201">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="cb170-202">Přečtěte si podmínky použít před přístup, stahování nebo získávání všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="cb170-202">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="cb170-203">Na nuget.org, použijte **licenční informace** odkaz na stránce balíček.</span><span class="sxs-lookup"><span data-stu-id="cb170-203">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="cb170-204">Pokud balíček neurčuje licenční podmínky, obraťte se na vlastníka balíčku přímo pomocí **obraťte se na vlastníky** odkaz na stránce balíček nuget.org.</span><span class="sxs-lookup"><span data-stu-id="cb170-204">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="cb170-205">Společnost Microsoft není licence duševního vlastnictví vám ze zprostředkovatelů balíček třetích stran a není zodpovědná za informace třetích stran.</span><span class="sxs-lookup"><span data-stu-id="cb170-205">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>


## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="cb170-206">Spravovat balíčky v nuget.org</span><span class="sxs-lookup"><span data-stu-id="cb170-206">Managing packages on nuget.org</span></span>

<span data-ttu-id="cb170-207">**Můžete upravit metadata balíčků, až se nahrají? Proč vám doporučujeme upravit soubor nuspec a odesílání nový balíček pro provádění změn do balíčku metadata?**</span><span class="sxs-lookup"><span data-stu-id="cb170-207">**Can I edit package metadata after it's been uploaded? Why do you recommend editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="cb170-208">NuGet bude implementace podpis balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb170-208">NuGet will be implementing package signing.</span></span> <span data-ttu-id="cb170-209">Princip návrhu podepisování balíčku je, že podepsaný balíček obsahu musí být neměnné, což zahrnuje soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="cb170-209">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="cb170-210">Úpravy metadata balíčků výsledkem změny pro soubor nuspec, zneplatnění existující podpisy.</span><span class="sxs-lookup"><span data-stu-id="cb170-210">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="cb170-211">Doporučujeme, abyste úprava existující pracovní postupy a nevyžadují úpravy metadata balíčků po vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb170-211">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="cb170-212">Všimněte si, že pro svůj balíček uvedené závislosti jsou automaticky generovány z balíčku sám sebe a nelze jej upravit.</span><span class="sxs-lookup"><span data-stu-id="cb170-212">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="cb170-213">Kromě toho odesílání balíčků [staging.nuget.org](http://staging.nuget.org) je skvělým způsobem, jak testování a ověření vašeho balíčku bez zpřístupnění balíček ve veřejné galerii.</span><span class="sxs-lookup"><span data-stu-id="cb170-213">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="cb170-214">**Je možné rezervovat názvy pro balíčky, které budou publikovány v budoucnosti?**</span><span class="sxs-lookup"><span data-stu-id="cb170-214">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="cb170-215">Ano.</span><span class="sxs-lookup"><span data-stu-id="cb170-215">Yes.</span></span> <span data-ttu-id="cb170-216">ID můžete vyhradit pro balíčky na [nuget.org](https://www.nuget.org/) tím, že požádá předponu ID balíčku pro váš účet.</span><span class="sxs-lookup"><span data-stu-id="cb170-216">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="cb170-217">Chcete-li požádat o předponu ID balíčku, odeslat e-mailu na účet (na) nuget.org s zobrazovaný název vlastníka balíčku a předpona ID požadovaný balíček.</span><span class="sxs-lookup"><span data-stu-id="cb170-217">In order to request a package ID prefix, send mail to account (at) nuget.org with the package owner display name, and the requested package ID prefix.</span></span>  

<span data-ttu-id="cb170-218">**Jak nárokovat vlastnictví pro balíčky?**</span><span class="sxs-lookup"><span data-stu-id="cb170-218">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="cb170-219">V tématu [Správa vlastníků balíčku na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="cb170-219">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="cb170-220">**Řešení s vlastníka balíčku, který je bychom při tom porušili Moje softwarových licencí**</span><span class="sxs-lookup"><span data-stu-id="cb170-220">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="cb170-221">Doporučujeme komunitou NuGet spolupracovat na řešení sporů, které může způsobit mezi balíček vlastníků a vlastníci na ostatní software.</span><span class="sxs-lookup"><span data-stu-id="cb170-221">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="cb170-222">Budeme mít vytvořené [proces řešení sporu](../policies/dispute-resolution.md) dříve, než s dotazem, správcům nuget.org intercede.</span><span class="sxs-lookup"><span data-stu-id="cb170-222">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="cb170-223">**Se doporučuje nahrát Moje testovací balíčky do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="cb170-223">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="cb170-224">Pro účely testování můžete použít [staging.nuget.org](http://staging.nuget.org), nebo jako alternativní veřejné servery NuGet [myget.org](https://myget.org) nebo [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="cb170-224">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="cb170-225">Všimněte si, že balíčky nahrán do staging.nuget.org nelze zachovat.</span><span class="sxs-lookup"><span data-stu-id="cb170-225">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="cb170-226">V tématu [dát sbohem všem preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="cb170-226">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="cb170-227">**Jaká je maximální velikost balíčků, které I můžete uložit do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="cb170-227">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="cb170-228">nuget.org umožňuje balíčky až 250MB, ale nemůžeme doporučujeme zachovat balíčky v části 1MB, pokud je to možné a použití závislosti propojení balíčky současně.</span><span class="sxs-lookup"><span data-stu-id="cb170-228">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="cb170-229">Balíčky jako existuje pravidlo, obsahovat pouze jeden sestavení, aby se zabránilo kolizí.</span><span class="sxs-lookup"><span data-stu-id="cb170-229">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="cb170-230">NuGet stáhnout balíčky, takže větší balíčky mít vyšší pravděpodobnost selhání nainstaluje než menším pomocí protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="cb170-230">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="cb170-231">Je možné sdílet závislosti mezi více balíčků, zmenšit velikost stažených pro příjemci vašich balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb170-231">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="cb170-232">Závislosti jsou většinou statické a nikdy změnit.</span><span class="sxs-lookup"><span data-stu-id="cb170-232">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="cb170-233">Při opravě chyby v kódu, nemusí být závislosti nutné aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="cb170-233">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="cb170-234">Pokud jste sady závislosti, skončili reshipping pokaždé, když větší balíčky.</span><span class="sxs-lookup"><span data-stu-id="cb170-234">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="cb170-235">Rozdělením balíčků NuGet do související závislosti, upgrade je mnohem podrobnějšího pro spotřebitele vašeho balíčku.</span><span class="sxs-lookup"><span data-stu-id="cb170-235">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="cb170-236">není k dispozici nuget.org</span><span class="sxs-lookup"><span data-stu-id="cb170-236">nuget.org not accessible</span></span>

<span data-ttu-id="cb170-237">**Proč nelze stáhnout balíčky nebo balíčky odešlete do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="cb170-237">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="cb170-238">První Ujistěte se, že používáte nejnovější verze NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb170-238">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="cb170-239">Pokud tuto verzi dále nedaří, [obraťte se na podporu](https://www.nuget.org/policies/Contact) a poskytnout další připojení, řešení potíží s informace, včetně:</span><span class="sxs-lookup"><span data-stu-id="cb170-239">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="cb170-240">Verze NuGet používáte</span><span class="sxs-lookup"><span data-stu-id="cb170-240">The version of NuGet you're using</span></span>
- <span data-ttu-id="cb170-241">Zdroje balíčku, kterou používáte</span><span class="sxs-lookup"><span data-stu-id="cb170-241">The package sources you're using</span></span>
- <span data-ttu-id="cb170-242">Obnovení protokolu s podrobné podrobností</span><span class="sxs-lookup"><span data-stu-id="cb170-242">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="cb170-243">MTR nebo Fiddler trasování (viz níže)</span><span class="sxs-lookup"><span data-stu-id="cb170-243">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="cb170-244">Zeměpisná oblast</span><span class="sxs-lookup"><span data-stu-id="cb170-244">Your geographical area</span></span>
- <span data-ttu-id="cb170-245">Verze vašeho operačního systému</span><span class="sxs-lookup"><span data-stu-id="cb170-245">Your operating system version</span></span>
- <span data-ttu-id="cb170-246">Konfigurace počítače (procesor, sítě, pevný disk)</span><span class="sxs-lookup"><span data-stu-id="cb170-246">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="cb170-247">Jestli je váš počítač za proxy nebo brány firewall</span><span class="sxs-lookup"><span data-stu-id="cb170-247">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="cb170-248">Verze rozhraní .NET, které jsou nainstalovány na počítači</span><span class="sxs-lookup"><span data-stu-id="cb170-248">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="cb170-249">Verze nástrojů pro různé platformy jako je rozhraní příkazového řádku .NET nebo dnů, který používáte</span><span class="sxs-lookup"><span data-stu-id="cb170-249">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="cb170-250">*Chcete-li zaznamenat MTR:*</span><span class="sxs-lookup"><span data-stu-id="cb170-250">*To capture MTR:*</span></span>

- <span data-ttu-id="cb170-251">Stáhněte si WinMTR z [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="cb170-251">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="cb170-252">Zadejte `api.nuget.org` jako název hostitele a klikněte na tlačítko **spustit**.</span><span class="sxs-lookup"><span data-stu-id="cb170-252">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="cb170-253">Počkejte **odeslané** sloupec je sloupec > = 100.</span><span class="sxs-lookup"><span data-stu-id="cb170-253">Wait until the **Sent** column is >= 100.</span></span>

    ![Zaznamenání MTR](media/mtr.png)

- <span data-ttu-id="cb170-255">Zkopírujte text do schránky.</span><span class="sxs-lookup"><span data-stu-id="cb170-255">Copy text to clipboard.</span></span>

<span data-ttu-id="cb170-256">*Chcete-li zaznamenat Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="cb170-256">*To capture Fiddler:*</span></span>

- <span data-ttu-id="cb170-257">Nainstalujte nejnovější verzi [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="cb170-257">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="cb170-258">Spusťte aplikaci Fiddler a zakázat pomocí zaznamenávání provoz **soubor > zachycování provozu** nabídky.</span><span class="sxs-lookup"><span data-stu-id="cb170-258">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="cb170-259">Odeberte všechny relace (vyberte všechny položky v seznamu, stiskněte **odstranit** klíč).</span><span class="sxs-lookup"><span data-stu-id="cb170-259">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="cb170-260">Nakonfigurujte aplikaci Fiddler k zachycení provoz HTTPS kontrolou **provoz HTTPS dešifrovat** v **HTTPS** kartě **nástroje > Možnosti Fiddler...**  nabídky.</span><span class="sxs-lookup"><span data-stu-id="cb170-260">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="cb170-261">Zavřete Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb170-261">Close Visual Studio.</span></span>
- <span data-ttu-id="cb170-262">Povolit **soubor > zachycování provozu** nabídky.</span><span class="sxs-lookup"><span data-stu-id="cb170-262">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="cb170-263">Spusťte Visual Studio nebo nuget.exe .exe a provádět akce, které nefungují.</span><span class="sxs-lookup"><span data-stu-id="cb170-263">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="cb170-264">Přenosy dat vytvářené pomocí tyto akce by měl zobrazí v aplikaci Fiddler.</span><span class="sxs-lookup"><span data-stu-id="cb170-264">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="cb170-265">Jakmile akce, které jste spustili, použijte **soubor > Uložit > všechny relace** k uložení zaznamenané relací.</span><span class="sxs-lookup"><span data-stu-id="cb170-265">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="cb170-266">Poznámka: může být nezbytné k nastavení `HTTP_PROXY` proměnnou prostředí `http://127.0.0.1:8888` pro směrování provozu NuGet prostřednictvím aplikaci Fiddler.</span><span class="sxs-lookup"><span data-stu-id="cb170-266">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="cb170-267">Pokud se nezdaří, zkuste [tipy uvedených v tomto blogu StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="cb170-267">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="cb170-268">**Jaké jsou koncové body rozhraní API pro nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="cb170-268">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="cb170-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Všimněte si, že rozhraní API verze 2 je zastaralá a nefunguje s NuGet 4 +.)</span><span class="sxs-lookup"><span data-stu-id="cb170-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
