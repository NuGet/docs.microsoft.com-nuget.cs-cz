---
title: NuGet – nejčastější dotazy
description: Běžné otázky a odpovědi pro pomocí nástroje NuGet na příkazovém řádku a v sadě Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8bc6af90638408847af6e97cebcbf428f1d5d886
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467754"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="6c0b4-103">NuGet – nejčastější dotazy</span><span class="sxs-lookup"><span data-stu-id="6c0b4-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="6c0b4-104">**Co je potřeba spuštěním rozšíření NuGet?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="6c0b4-105">Všechny informace týkající se uživatelského rozhraní a nástroje příkazového řádku jsou k dispozici v [Instalační příručka](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="6c0b4-106">**Podporuje NuGet Mono?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="6c0b4-107">Nástroj příkazového řádku `nuget.exe`, sestavení a běží pod Mono 3.2 + a můžete vytvořit balíčky v Mono.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="6c0b4-108">I když `nuget.exe` funguje plně na Windows, dochází ke známým problémům v Linuxu a OS X. naleznete [Mono vydá](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na Githubu.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="6c0b4-109">A [grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="6c0b4-110">**Jak zjistím obsah balíčku a zda je stabilní a užitečné pro mé aplikace?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="6c0b4-111">Primární zdroj informací o balíčku je její stránce na nuget.org (nebo jiný privátní kanál).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="6c0b4-112">Každou stránku balíčků na nuget.org obsahuje popis balíčku, historie verzí a statistiky o využití.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="6c0b4-113">**Informace** oddíl na stránce balíček pro také obsahuje odkaz projekt webové stránky, kdy obvykle najít mnoho příkladů a další dokumentaci, která vám pomůže se naučit, jak se používá balíček.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="6c0b4-114">Další informace najdete v tématu [hledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="6c0b4-115">NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6c0b4-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="6c0b4-116">**Jak se v různých produktů Visual Studio podporuje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="6c0b4-117">Visual Studio na Windows podporuje [uživatelské rozhraní Správce balíčků](../tools/package-manager-ui.md) a [Konzola správce balíčků](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="6c0b4-118">Visual Studio for Mac obsahuje integrované funkce NuGet, jak je popsáno na [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="6c0b4-119">Visual Studio Code (všechny platformy) nemá žádné přímé integraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="6c0b4-120">Použití [rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md) nebo [rozhraní příkazového řádku dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="6c0b4-121">Poskytuje Azure DevOps [kroku sestavení pro obnovování balíčků NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="6c0b4-122">Můžete také [privátní balíček NuGet hostitele kanálů na Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="6c0b4-123">**Jak můžu ověřit přesnou verzi, které jsou nainstalované nástroje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="6c0b4-124">V sadě Visual Studio, použijte **Nápověda > o Microsoft Visual Studio** příkazů a podívejte se na verzi vedle položky **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="6c0b4-125">Alternativně spusťte konzolu Správce balíčků (**nástroje > Správce balíčků NuGet > Konzola správce balíčků**) a zadejte `$host` zobrazíte informace o systému NuGet, včetně verze.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="6c0b4-126">**Jaké programovací jazyky podporují NuGet?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="6c0b4-127">NuGet obecně se dá použít pro jazyky .NET a je určený pro přenesení do projektu knihovny .NET.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="6c0b4-128">Vzhledem k tomu, že v některých typech projektů podporuje také automatizaci MSBuild a sadě Visual Studio, podporuje také dalších projektů a jazyky na různých úrovních.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="6c0b4-129">Podporuje nejnovější verzi balíčku nuget C#, Visual Basic, F#, WiX a C++.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="6c0b4-130">**Jaké šablony projektů podporuje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="6c0b4-131">NuGet má plnou podporu pro širokou škálu šablony projektu, jako je Windows, Web, Cloud, SharePoint, Wix a tak dále.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="6c0b4-132">**Jak můžu aktualizovat balíčky, které jsou součástí šablony sady Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="6c0b4-133">Přejděte na **aktualizace** kartu v Uživatelském rozhraní Správce balíčků a vyberte **Aktualizovat vše**, nebo použijte [ `Update-Package` příkaz](../tools/ps-ref-update-package.md) z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="6c0b4-134">Pokud chcete aktualizovat samotné šablony, budete muset ručně aktualizovat úložiště šablon.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="6c0b4-135">Zobrazit [Xavier Decoster blogu](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) k tomuto tématu.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="6c0b4-136">Protože ruční aktualizace může dojít k poškození šablony Pokud nejnovější verze všechny závislosti nejsou navzájem kompatibilní, mějte na paměti, že to se provádí na vaše vlastní nebezpečí.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="6c0b4-137">**Můžete použít balíček NuGet mimo sadu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="6c0b4-138">Ano, NuGet pracuje přímo z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="6c0b4-139">Zobrazit [Instalační příručka](../install-nuget-client-tools.md) a [odkaz na rozhraní příkazového řádku](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="6c0b4-140">NuGet příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="6c0b4-140">NuGet command line</span></span>

<span data-ttu-id="6c0b4-141">**Jak získat nejnovější verzi nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="6c0b4-142">Zobrazit [Instalační příručka](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="6c0b4-143">**Co je licence pro nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="6c0b4-144">Jste oprávněni nuget.exe podle podmínek licence MIT znovu distribuovat.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="6c0b4-145">Zodpovídáte za aktualizace a údržba všechny kopie nuget.exe, které chcete znovu distribuovat.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="6c0b4-146">**Je možné rozšířit nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="6c0b4-147">Ano, je možné přidat vlastní příkazy `nuget.exe`, jak je popsáno v [Rob Reynold příspěvek](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="6c0b4-148">Konzola správce balíčků NuGet (Visual Studio na Windows)</span><span class="sxs-lookup"><span data-stu-id="6c0b4-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="6c0b4-149">**Jak získat přístup k objektu DTE v konzole Správce balíčků**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="6c0b4-150">Objekt nejvyšší úrovně v objektovém modelu automatizace sady Visual Studio se nazývá objekt DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="6c0b4-151">Konzole vám tohle všechno poskytuje prostřednictvím proměnné s názvem `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="6c0b4-152">Další informace najdete v tématu [přehled modelu automatizace](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci k rozšiřitelnosti sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="6c0b4-153">**Můžu zkusit přetypovat $DTE proměnnou typu DTE2, ale se zobrazí chyba: Nelze převést hodnotu "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" typ "EnvDTE80.DTE2". Co je?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="6c0b4-154">Jde o známý problém s interakci Powershellu pomocí objektu COM.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="6c0b4-155">Vyzkoušejte následující postup:</span><span class="sxs-lookup"><span data-stu-id="6c0b4-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="6c0b4-156">`Get-Interface` pomocná funkce přidal hostitele prostředí NuGet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="6c0b4-157">Vytvoření a publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="6c0b4-157">Creating and publishing packages</span></span>

<span data-ttu-id="6c0b4-158">**Jak se seznam Můj balíček v informačním kanálu?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="6c0b4-159">Zobrazit [vytváření a publikování balíčku](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="6c0b4-160">**Mám k dispozici více verzí knihovny, které cílí různé verze rozhraní .NET Framework. Jak vytvořit jeden balíček, který to podporuje?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="6c0b4-161">Zobrazit [podporuje více verzí rozhraní .NET Framework a profily](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="6c0b4-162">**Nastavení vlastní úložiště nebo informačního kanálu**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="6c0b4-163">Zobrazit [hostování balíčků přehled](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="6c0b4-164">**Jak můžete nahrát balíčky do mé NuGet kanálu hromadně?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="6c0b4-165">Zobrazit [hromadně publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="6c0b4-166">Práce s balíčky</span><span class="sxs-lookup"><span data-stu-id="6c0b4-166">Working with packages</span></span>

<span data-ttu-id="6c0b4-167">**Jaký je rozdíl mezi balíčkem na úrovni projektu a balíček řešení úrovni?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="6c0b4-168">Balíček řešení úrovni (NuGet 3.x+) se nainstaluje pouze jednou v řešení a je pak k dispozici pro všechny projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="6c0b4-169">Na úrovni projektu balíček je nainstalován v každém projektu, která ji používá.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="6c0b4-170">Balíček úrovni řešení může být také nainstalovat nové příkazy, které může být volána z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="6c0b4-171">**Je možné nainstalovat balíčky NuGet bez připojení k Internetu?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="6c0b4-172">Ano, najdete v příspěvku blogu Scotta Hanselmana [jak získat přístup k NuGet, když nuget.org je mimo provoz (nebo jste palubě)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="6c0b4-173">**Jak nainstalovat balíčky v jiném umístění z výchozí složku balíčků?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="6c0b4-174">Nastavte [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` pomocí `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="6c0b4-175">**Jak se můžu vyhnout přidávání složce balíčků NuGet do správy zdrojových kódů?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="6c0b4-176">Nastavte [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) v `Nuget.Config` k `true`.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="6c0b4-177">Tento klíč funguje v řešení úrovni a proto je potřeba přidat do `$(Solutiondir)\.nuget\Nuget.Config` souboru.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="6c0b4-178">Povolení obnovení balíčku ze sady Visual Studio automaticky vytvoří tento soubor.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="6c0b4-179">**Jak můžu vypnout obnovení balíčků?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="6c0b4-180">Zobrazit [povolení a zákaz obnovení balíčku](../consume-packages/package-restore.md#enable-and-disable-package-restore).</span><span class="sxs-lookup"><span data-stu-id="6c0b4-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore).</span></span>

<span data-ttu-id="6c0b4-181">**Proč se zobrazí zpráva "Nelze přeložit došlo k chybě závislosti" při instalaci místního balíčku se vzdálených závislostí?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="6c0b4-182">Je nutné vybrat **všechny** zdroje při instalaci místního balíčku do projektu.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="6c0b4-183">To agreguje všechny kanály místo jen jeden.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="6c0b4-184">Důvod se zobrazí tato chyba je, že uživatelé z místního úložiště se často chcete zabránit náhodnému instalace vzdálených balíčků z důvodu firemní zásady.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="6c0b4-185">**Mám několik projektů ve stejné složce, jak můžete použít soubory samostatného souboru packages.config pro každý projekt?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="6c0b4-186">Ve většině projektů, ve kterém live samostatné projekty do samostatné složky, to není problém protože identifikuje NuGet `packages.config` soubory v každém projektu.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="6c0b4-187">Nuget 3.3 + a více projektů ve stejné složce, můžete vložit název projektu do `packages.config` názvy souborů použijte vzor `packages.{project-name}.config`, a tento soubor používá NuGet.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="6c0b4-188">To není problém při používání PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="6c0b4-189">**Nevidím v seznamu úložišť v nuget.org, jak to můžu získat zpátky?**</span><span class="sxs-lookup"><span data-stu-id="6c0b4-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="6c0b4-190">Přidat `https://api.nuget.org/v3/index.json` do seznamu zdrojů, nebo</span><span class="sxs-lookup"><span data-stu-id="6c0b4-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="6c0b4-191">Odstranit `%appdata%\.nuget\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a nechat NuGet znovu vytvořit.</span><span class="sxs-lookup"><span data-stu-id="6c0b4-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
