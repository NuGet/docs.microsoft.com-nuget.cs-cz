---
title: NuGet – nejčastější dotazy
description: Běžné otázky a odpovědi na příkazovém řádku a v sadě Visual Studio pomocí nástroje NuGet a práci v galerii NuGet.
author: karann-msft
ms.author: karann
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 8c63abc9971623e0732ae8d973fafcd04c5d9f48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548801"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="b7342-103">NuGet – nejčastější dotazy</span><span class="sxs-lookup"><span data-stu-id="b7342-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="b7342-104">**Co je potřeba spuštěním rozšíření NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b7342-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="b7342-105">Všechny informace týkající se uživatelského rozhraní a nástroje příkazového řádku jsou k dispozici v [Instalační příručka](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="b7342-106">**Podporuje NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="b7342-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="b7342-107">Nástroj příkazového řádku `nuget.exe`, sestavení a běží pod Mono 3.2 + a můžete vytvořit balíčky v Mono.</span><span class="sxs-lookup"><span data-stu-id="b7342-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="b7342-108">I když `nuget.exe` funguje plně na Windows, dochází ke známým problémům v Linuxu a OS X. naleznete [Mono vydá](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na Githubu.</span><span class="sxs-lookup"><span data-stu-id="b7342-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="b7342-109">A [grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="b7342-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="b7342-110">**Jak zjistím obsah balíčku a zda je stabilní a užitečné pro mé aplikace?**</span><span class="sxs-lookup"><span data-stu-id="b7342-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="b7342-111">Primární zdroj informací o balíčku je její stránce na nuget.org (nebo jiný privátní kanál).</span><span class="sxs-lookup"><span data-stu-id="b7342-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="b7342-112">Každou stránku balíčků na nuget.org obsahuje popis balíčku, historie verzí a statistiky o využití.</span><span class="sxs-lookup"><span data-stu-id="b7342-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="b7342-113">**Informace** oddíl na stránce balíček pro také obsahuje odkaz projekt webové stránky, kdy obvykle najít mnoho příkladů a další dokumentaci, která vám pomůže se naučit, jak se používá balíček.</span><span class="sxs-lookup"><span data-stu-id="b7342-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="b7342-114">Další informace najdete v tématu [hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="b7342-115">NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7342-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="b7342-116">**Jak se v různých produktů Visual Studio podporuje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b7342-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="b7342-117">Visual Studio na Windows podporuje [uživatelské rozhraní Správce balíčků](../tools/package-manager-ui.md) a [Konzola správce balíčků](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="b7342-118">Visual Studio for Mac obsahuje integrované funkce NuGet, jak je popsáno na [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b7342-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="b7342-119">Visual Studio Code (všechny platformy) nemá žádné přímé integraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="b7342-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="b7342-120">Použití [rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md) nebo [rozhraní příkazového řádku dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="b7342-121">Visual Studio Team Services poskytuje [kroku sestavení pro obnovování balíčků NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="b7342-121">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="b7342-122">Můžete také [privátní balíček NuGet hostitele informační kanály ve službě Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="b7342-122">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="b7342-123">**Jak můžu ověřit přesnou verzi, které jsou nainstalované nástroje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b7342-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="b7342-124">V sadě Visual Studio, použijte **Nápověda > o Microsoft Visual Studio** příkazů a podívejte se na verzi vedle položky **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b7342-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="b7342-125">Alternativně spusťte konzolu Správce balíčků (**nástroje > Správce balíčků NuGet > Konzola správce balíčků**) a zadejte `$host` zobrazíte informace o systému NuGet, včetně verze.</span><span class="sxs-lookup"><span data-stu-id="b7342-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="b7342-126">**Jaké programovací jazyky podporují NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b7342-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="b7342-127">NuGet obecně se dá použít pro jazyky .NET a je určený pro přenesení do projektu knihovny .NET.</span><span class="sxs-lookup"><span data-stu-id="b7342-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="b7342-128">Vzhledem k tomu, že v některých typech projektů podporuje také automatizaci MSBuild a sadě Visual Studio, podporuje také dalších projektů a jazyky na různých úrovních.</span><span class="sxs-lookup"><span data-stu-id="b7342-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="b7342-129">Nejnovější verzi balíčku nuget podporuje C#, Visual Basic, F #, WiX a C++.</span><span class="sxs-lookup"><span data-stu-id="b7342-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="b7342-130">**Jaké šablony projektů podporuje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b7342-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="b7342-131">NuGet má plnou podporu pro širokou škálu šablony projektu, jako je Windows, Web, Cloud, SharePoint, Wix a tak dále.</span><span class="sxs-lookup"><span data-stu-id="b7342-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="b7342-132">**Jak můžu aktualizovat balíčky, které jsou součástí šablony sady Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="b7342-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="b7342-133">Přejděte na **aktualizace** kartu v Uživatelském rozhraní Správce balíčků a vyberte **Aktualizovat vše**, nebo použijte [ `Update-Package` příkaz](../tools/ps-ref-update-package.md) z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b7342-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="b7342-134">Pokud chcete aktualizovat samotné šablony, budete muset ručně aktualizovat úložiště šablon.</span><span class="sxs-lookup"><span data-stu-id="b7342-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="b7342-135">Zobrazit [Xavier Decoster blogu](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) k tomuto tématu.</span><span class="sxs-lookup"><span data-stu-id="b7342-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="b7342-136">Protože ruční aktualizace může dojít k poškození šablony Pokud nejnovější verze všechny závislosti nejsou navzájem kompatibilní, mějte na paměti, že to se provádí na vaše vlastní nebezpečí.</span><span class="sxs-lookup"><span data-stu-id="b7342-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="b7342-137">**Můžete použít balíček NuGet mimo sadu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="b7342-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="b7342-138">Ano, NuGet pracuje přímo z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="b7342-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="b7342-139">Zobrazit [Instalační příručka](../install-nuget-client-tools.md) a [odkaz na rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="b7342-140">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="b7342-140">NuGet command line</span></span>

<span data-ttu-id="b7342-141">**Jak získat nejnovější verzi nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b7342-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="b7342-142">Zobrazit [Instalační příručka](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="b7342-143">**Co je licence pro nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="b7342-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="b7342-144">Jste oprávněni nuget.exe podle podmínek licence MIT znovu distribuovat.</span><span class="sxs-lookup"><span data-stu-id="b7342-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="b7342-145">Zodpovídáte za aktualizace a údržba všechny kopie nuget.exe, které chcete znovu distribuovat.</span><span class="sxs-lookup"><span data-stu-id="b7342-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="b7342-146">**Je možné rozšířit nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="b7342-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="b7342-147">Ano, je možné přidat vlastní příkazy `nuget.exe`, jak je popsáno v [Rob Reynold příspěvek](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7342-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="b7342-148">Konzola správce balíčků NuGet (Visual Studio na Windows)</span><span class="sxs-lookup"><span data-stu-id="b7342-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="b7342-149">**Jak získat přístup k objektu DTE v konzole Správce balíčků**</span><span class="sxs-lookup"><span data-stu-id="b7342-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="b7342-150">Objekt nejvyšší úrovně v objektovém modelu automatizace sady Visual Studio se nazývá objekt DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="b7342-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="b7342-151">Konzole vám tohle všechno poskytuje prostřednictvím proměnné s názvem `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="b7342-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="b7342-152">Další informace najdete v tématu [přehled modelu automatizace](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7342-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="b7342-153">**Můžu zkusit přetypovat $DTE proměnnou typu DTE2, ale se zobrazí chyba: nelze převést hodnotu "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" typ "EnvDTE80.DTE2". Co je?**</span><span class="sxs-lookup"><span data-stu-id="b7342-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="b7342-154">Jde o známý problém s interakci Powershellu pomocí objektu COM.</span><span class="sxs-lookup"><span data-stu-id="b7342-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="b7342-155">Vyzkoušejte následující postup:</span><span class="sxs-lookup"><span data-stu-id="b7342-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="b7342-156">`Get-Interface` pomocná funkce přidal hostitele prostředí NuGet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7342-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="b7342-157">Vytvoření a publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="b7342-157">Creating and publishing packages</span></span>

<span data-ttu-id="b7342-158">**Jak se seznam Můj balíček v informačním kanálu?**</span><span class="sxs-lookup"><span data-stu-id="b7342-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="b7342-159">Zobrazit [vytváření a publikování balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="b7342-160">**Mám k dispozici více verzí knihovny, které cílí různé verze rozhraní .NET Framework. Jak vytvořit jeden balíček, který to podporuje?**</span><span class="sxs-lookup"><span data-stu-id="b7342-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="b7342-161">Zobrazit [podporuje více verzí rozhraní .NET Framework a profily](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="b7342-162">**Nastavení vlastní úložiště nebo informačního kanálu**</span><span class="sxs-lookup"><span data-stu-id="b7342-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="b7342-163">Zobrazit [hostování balíčků přehled](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7342-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="b7342-164">**Jak můžete nahrát balíčky do mé NuGet kanálu hromadně?**</span><span class="sxs-lookup"><span data-stu-id="b7342-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="b7342-165">Zobrazit [hromadně publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="b7342-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="b7342-166">Práce s balíčky</span><span class="sxs-lookup"><span data-stu-id="b7342-166">Working with packages</span></span>

<span data-ttu-id="b7342-167">**Jaký je rozdíl mezi balíčkem na úrovni projektu a balíček řešení úrovni?**</span><span class="sxs-lookup"><span data-stu-id="b7342-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="b7342-168">Balíček řešení úrovni (NuGet 3.x+) se nainstaluje pouze jednou v řešení a je pak k dispozici pro všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="b7342-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="b7342-169">Na úrovni projektu balíček je nainstalován v každém projektu, která ji používá.</span><span class="sxs-lookup"><span data-stu-id="b7342-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="b7342-170">Balíček úrovni řešení může být také nainstalovat nové příkazy, které může být volána z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b7342-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="b7342-171">**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**</span><span class="sxs-lookup"><span data-stu-id="b7342-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="b7342-172">Ano, najdete v příspěvku blogu Scotta Hanselmana [jak získat přístup k NuGet, když nuget.org je mimo provoz (nebo jste palubě)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="b7342-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="b7342-173">**Jak nainstalovat balíčky v jiném umístění z výchozí složku balíčků?**</span><span class="sxs-lookup"><span data-stu-id="b7342-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="b7342-174">Nastavte [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` pomocí `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="b7342-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="b7342-175">**Jak se můžu vyhnout přidávání složce balíčků NuGet do správy zdrojových kódů?**</span><span class="sxs-lookup"><span data-stu-id="b7342-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="b7342-176">Nastavte [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) v `Nuget.Config` k `true`.</span><span class="sxs-lookup"><span data-stu-id="b7342-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="b7342-177">Tento klíč funguje v řešení úrovni a proto je potřeba přidat do `$(Solutiondir)\.nuget\Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="b7342-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="b7342-178">Povolení obnovení balíčku ze sady Visual Studio automaticky vytvoří tento soubor.</span><span class="sxs-lookup"><span data-stu-id="b7342-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="b7342-179">**Jak můžu vypnout obnovení balíčků?**</span><span class="sxs-lookup"><span data-stu-id="b7342-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="b7342-180">Zobrazit [povolení a zákaz obnovení balíčku](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="b7342-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="b7342-181">**Proč se zobrazí zpráva "Nelze přeložit došlo k chybě závislosti" při instalaci místního balíčku se vzdálených závislostí?**</span><span class="sxs-lookup"><span data-stu-id="b7342-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="b7342-182">Je nutné vybrat **všechny** zdroje při instalaci místního balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="b7342-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="b7342-183">To agreguje všechny kanály místo jen jeden.</span><span class="sxs-lookup"><span data-stu-id="b7342-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="b7342-184">Důvod se zobrazí tato chyba je, že uživatelé z místního úložiště se často chcete zabránit náhodnému instalace vzdálených balíčků z důvodu firemní zásady.</span><span class="sxs-lookup"><span data-stu-id="b7342-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="b7342-185">**Mám několik projektů ve stejné složce, jak můžete použít soubory samostatného souboru packages.config pro každý projekt?**</span><span class="sxs-lookup"><span data-stu-id="b7342-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="b7342-186">Ve většině projektů, ve kterém live samostatné projekty do samostatné složky, to není problém protože identifikuje NuGet `packages.config` soubory v každém projektu.</span><span class="sxs-lookup"><span data-stu-id="b7342-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="b7342-187">Nuget 3.3 + a více projektů ve stejné složce, můžete vložit název projektu do `packages.config` názvy souborů použijte vzor `packages.{project-name}.config`, a tento soubor používá NuGet.</span><span class="sxs-lookup"><span data-stu-id="b7342-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="b7342-188">To není problém při používání PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="b7342-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="b7342-189">**Nevidím v seznamu úložišť v nuget.org, jak to můžu získat zpátky?**</span><span class="sxs-lookup"><span data-stu-id="b7342-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="b7342-190">Přidat `https://api.nuget.org/v3/index.json` do seznamu zdrojů, nebo</span><span class="sxs-lookup"><span data-stu-id="b7342-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="b7342-191">Odstranit `%appdata%\.nuget\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a nechat NuGet znovu vytvořit.</span><span class="sxs-lookup"><span data-stu-id="b7342-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="b7342-192">**Co jsou výchozí licenční podmínky Pokud balíček neobsahuje konkrétní informace o licencích?**</span><span class="sxs-lookup"><span data-stu-id="b7342-192">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="b7342-193">Každý balíček se řídí podmínkami, které jsou součástí balíčku.</span><span class="sxs-lookup"><span data-stu-id="b7342-193">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="b7342-194">Přečtěte si před přístupem k, stahování nebo získání všechny balíčky, které příslušné podmínky.</span><span class="sxs-lookup"><span data-stu-id="b7342-194">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="b7342-195">Na nuget.org, použijte **informace o licenci** odkaz na stránce balíček.</span><span class="sxs-lookup"><span data-stu-id="b7342-195">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="b7342-196">Pokud balíček neurčuje licenční podmínky, obraťte se přímo pomocí vlastníka balíčku **obraťte se na vlastníky** odkazu na stránce balíček pro nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b7342-196">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="b7342-197">Společnost Microsoft není licence duševního vlastnictví, od poskytovatelů třetích stran balíček a neodpovídá za informace, které jsou poskytovány třetími stranami.</span><span class="sxs-lookup"><span data-stu-id="b7342-197">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="b7342-198">Správa balíčků na nuget.org</span><span class="sxs-lookup"><span data-stu-id="b7342-198">Managing packages on nuget.org</span></span>

<span data-ttu-id="b7342-199">**Můžete upravit po je nahraná metadata balíčků?**</span><span class="sxs-lookup"><span data-stu-id="b7342-199">**Can I edit package metadata after it's been uploaded?**</span></span>

<span data-ttu-id="b7342-200">NuGet doporučuje podepsat všechny balíčky.</span><span class="sxs-lookup"><span data-stu-id="b7342-200">NuGet recommends all packages to be signed.</span></span> <span data-ttu-id="b7342-201">Princip návrhu podpisu balíčku je, že je podepsaný balíček obsahu neměnný, což zahrnuje soubor nuspec.</span><span class="sxs-lookup"><span data-stu-id="b7342-201">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="b7342-202">Úpravy metadat balíčku výsledkem změny do souboru nuspec, proto už není platná existující podpisy.</span><span class="sxs-lookup"><span data-stu-id="b7342-202">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="b7342-203">Doporučujeme, abyste úpravy stávajících pracovních postupů, aby nebyl vyžadován upravovat metadata balíčku po vytvoření balíčku.</span><span class="sxs-lookup"><span data-stu-id="b7342-203">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="b7342-204">Všimněte si, že závislostí uvedených pro váš balíček se generují automaticky z balíčku samotného a nelze jej upravit.</span><span class="sxs-lookup"><span data-stu-id="b7342-204">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="b7342-205">Kromě toho nahrání balíčků [staging.nuget.org](http://staging.nuget.org) je skvělý způsob, jak otestovat a ověřit váš balíček přitom balíček k dispozici ve veřejné galerii.</span><span class="sxs-lookup"><span data-stu-id="b7342-205">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="b7342-206">**Je možné rezervovat názvy balíčků, které se publikují v budoucnosti?**</span><span class="sxs-lookup"><span data-stu-id="b7342-206">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="b7342-207">Ano.</span><span class="sxs-lookup"><span data-stu-id="b7342-207">Yes.</span></span> <span data-ttu-id="b7342-208">ID můžete vyhradit pro balíčky na [nuget.org](https://www.nuget.org/) vyžádáním předponu ID balíčku pro váš účet.</span><span class="sxs-lookup"><span data-stu-id="b7342-208">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="b7342-209">Aby bylo možné požádat o předponu ID balíčku, postupujte podle pokynů [dokumentaci](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span><span class="sxs-lookup"><span data-stu-id="b7342-209">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="b7342-210">**Jak uplatním nárok na vlastnictví pro balíčky?**</span><span class="sxs-lookup"><span data-stu-id="b7342-210">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="b7342-211">Zobrazit [vlastníky Správa balíčků na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="b7342-211">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="b7342-212">**Jak zacházet s vlastníka balíčku, který porušuje licence na software**</span><span class="sxs-lookup"><span data-stu-id="b7342-212">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="b7342-213">Doporučujeme komunity NuGet spolupráce řešení všech sporů, které mohou vzniknout mezi vlastníky balíčku a vlastníci dalšího softwaru.</span><span class="sxs-lookup"><span data-stu-id="b7342-213">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="b7342-214">Jsme vytvořený [spor proces překladu](../policies/dispute-resolution.md) dodržovat před položením správcům nuget.org intercede.</span><span class="sxs-lookup"><span data-stu-id="b7342-214">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="b7342-215">**Je doporučeno uložit Moje testovací balíčky nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="b7342-215">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="b7342-216">Pro účely testování můžete použít [staging.nuget.org](http://staging.nuget.org), nebo jako alternativní veřejné servery NuGet [webu myget.org](https://myget.org) nebo [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="b7342-216">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="b7342-217">Všimněte si, že nemusí být zachována balíčky nahráli do staging.nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b7342-217">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="b7342-218">Zobrazit [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="b7342-218">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="b7342-219">**Jaká je maximální velikost balíčky, které můžu nahrát do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="b7342-219">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="b7342-220">nuget.org umožňuje balíčky až 250MB, ale My doporučujeme udržování balíčky v části 1MB. Pokud je to možné a používání závislosti, které balíčky se propojují.</span><span class="sxs-lookup"><span data-stu-id="b7342-220">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="b7342-221">Balíčky jako říci, obsahovat pouze jedno sestavení pro zabránění kolizím.</span><span class="sxs-lookup"><span data-stu-id="b7342-221">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="b7342-222">Stáhnout balíčky, takže větší balíčky mají vyšší pravděpodobnost selhání instalace, než menších NuGet pomocí protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b7342-222">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="b7342-223">Je možné sdílet závislosti mezi více balíčků zmenšit celková stahovaná velikost spotřebitelé vaše balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="b7342-223">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="b7342-224">Závislosti jsou většinou statická a nikdy změnit.</span><span class="sxs-lookup"><span data-stu-id="b7342-224">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="b7342-225">Pokud opravujete chybu v kódu, závislosti nemusí aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="b7342-225">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="b7342-226">Pokud seskupíte závislosti, skončíte reshipping pokaždé, když větší balíčky.</span><span class="sxs-lookup"><span data-stu-id="b7342-226">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="b7342-227">Rozdělením balíčky NuGet na související závislosti jsou mnohem podrobnějšího pro spotřebitele balíčku upgradu.</span><span class="sxs-lookup"><span data-stu-id="b7342-227">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="b7342-228">není k dispozici nuget.org</span><span class="sxs-lookup"><span data-stu-id="b7342-228">nuget.org not accessible</span></span>

<span data-ttu-id="b7342-229">**Proč nejde stáhnout balíčky z nebo nahrání balíčků na nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="b7342-229">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="b7342-230">Nejprve ujistěte se, že používáte nejnovější verze nugetu.</span><span class="sxs-lookup"><span data-stu-id="b7342-230">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="b7342-231">Pokud tuto verzi ani potom nedaří, [obraťte se na podporu](https://www.nuget.org/policies/Contact) a poskytují další připojení, řešení potíží s informací, včetně:</span><span class="sxs-lookup"><span data-stu-id="b7342-231">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="b7342-232">Verze balíčku nuget, které používáte</span><span class="sxs-lookup"><span data-stu-id="b7342-232">The version of NuGet you're using</span></span>
- <span data-ttu-id="b7342-233">Zdroje balíčků, které používáte</span><span class="sxs-lookup"><span data-stu-id="b7342-233">The package sources you're using</span></span>
- <span data-ttu-id="b7342-234">Obnovení protokolu s podrobnou úroveň podrobností</span><span class="sxs-lookup"><span data-stu-id="b7342-234">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="b7342-235">MTR nebo trasování Fiddler (viz níže)</span><span class="sxs-lookup"><span data-stu-id="b7342-235">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="b7342-236">Zeměpisné oblasti</span><span class="sxs-lookup"><span data-stu-id="b7342-236">Your geographical area</span></span>
- <span data-ttu-id="b7342-237">Verze vašeho operačního systému</span><span class="sxs-lookup"><span data-stu-id="b7342-237">Your operating system version</span></span>
- <span data-ttu-id="b7342-238">Konfigurace počítače (procesor, síť, pevný disk)</span><span class="sxs-lookup"><span data-stu-id="b7342-238">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="b7342-239">Určuje, zda váš počítač není za proxy nebo brány firewall</span><span class="sxs-lookup"><span data-stu-id="b7342-239">Whether your machine is behind a proxy or firewall</span></span>
- <span data-ttu-id="b7342-240">Verze rozhraní .NET, které jsou nainstalované na počítači</span><span class="sxs-lookup"><span data-stu-id="b7342-240">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="b7342-241">Verze nástrojů pro různé platformy jako .NET CLI nebo dnů, které používáte</span><span class="sxs-lookup"><span data-stu-id="b7342-241">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="b7342-242">*K zachycení MTR:*</span><span class="sxs-lookup"><span data-stu-id="b7342-242">*To capture MTR:*</span></span>

- <span data-ttu-id="b7342-243">Stáhněte si WinMTR z [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="b7342-243">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="b7342-244">Zadejte `api.nuget.org` jako název hostitele a klikněte na **Start**.</span><span class="sxs-lookup"><span data-stu-id="b7342-244">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="b7342-245">Počkejte, dokud **odeslané** je sloupec > = 100.</span><span class="sxs-lookup"><span data-stu-id="b7342-245">Wait until the **Sent** column is >= 100.</span></span>

    ![Zachytávání MTR](media/mtr.png)

- <span data-ttu-id="b7342-247">Zkopírování textu do schránky.</span><span class="sxs-lookup"><span data-stu-id="b7342-247">Copy text to clipboard.</span></span>

<span data-ttu-id="b7342-248">*K zachycení Fiddleru:*</span><span class="sxs-lookup"><span data-stu-id="b7342-248">*To capture Fiddler:*</span></span>

- <span data-ttu-id="b7342-249">Nainstalujte nejnovější verzi [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="b7342-249">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="b7342-250">Spusťte aplikaci Fiddler a zakázat zachytávání provozu pomocí **soubor > Capture Traffic** nabídky.</span><span class="sxs-lookup"><span data-stu-id="b7342-250">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="b7342-251">Odebrat všechny relace (vybrat všechny položky v seznamu, stiskněte **odstranit** klíč).</span><span class="sxs-lookup"><span data-stu-id="b7342-251">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="b7342-252">Konfigurace aplikace Fiddler k zachycení přenosy HTTPS tak, že zkontrolujete **přenosy HTTPS dešifrovat** v **HTTPS** karty **nástroje > Možnosti Fiddleru...**  nabídky.</span><span class="sxs-lookup"><span data-stu-id="b7342-252">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="b7342-253">Zavřete Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7342-253">Close Visual Studio.</span></span>
- <span data-ttu-id="b7342-254">Povolit **soubor > Capture Traffic** nabídky.</span><span class="sxs-lookup"><span data-stu-id="b7342-254">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="b7342-255">Spusťte Visual Studio nebo nuget.exe .exe a provádět akce, které nefungují.</span><span class="sxs-lookup"><span data-stu-id="b7342-255">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="b7342-256">Přenosy generované tyto akce by měla objevoval ve Fiddleru.</span><span class="sxs-lookup"><span data-stu-id="b7342-256">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="b7342-257">Po spuštění akce, které mají používat **soubor > Uložit > všechny relace** k uložení zaznamenané relace.</span><span class="sxs-lookup"><span data-stu-id="b7342-257">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="b7342-258">Poznámka: to může být nutné nastavit `HTTP_PROXY` proměnnou prostředí, aby `http://127.0.0.1:8888` za směrování přenosů NuGet pomocí Fiddleru.</span><span class="sxs-lookup"><span data-stu-id="b7342-258">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="b7342-259">Pokud se to nepodaří, zkuste [tipy uvedených v tomto příspěvku na StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="b7342-259">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="b7342-260">**Jaké jsou koncové body rozhraní API pro nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="b7342-260">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="b7342-261">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Všimněte si, že rozhraní API verze 2 je zastaralý a nefunguje s NuGet 4 +.)</span><span class="sxs-lookup"><span data-stu-id="b7342-261">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
