---
title: Otázky Frequently-Asked NuGet
description: Běžné otázky a odpovědi pro používání NuGetu na příkazovém řádku a v aplikaci Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: aae6f0474cc6e8e8aa5c269b79be6fd949d9184c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237994"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="90b6d-103">Nejčastější dotazy k NuGet</span><span class="sxs-lookup"><span data-stu-id="90b6d-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="90b6d-104">Nejčastější dotazy týkající se NuGet.org, například otázky k účtu NuGet.org, najdete v článku [NuGet.org Nejčastější dotazy](../nuget-org/nuget-org-faq.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="90b6d-105">**Co je potřeba ke spuštění NuGet?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="90b6d-106">Všechny informace o uživatelském rozhraní a nástrojích příkazového řádku jsou k dispozici v [instalační příručce](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="90b6d-107">**Podporuje NuGet mono?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="90b6d-108">Nástroj příkazového řádku, `nuget.exe` , vytvoří a spustí v mono 3.2 + a může vytvářet balíčky v mono.</span><span class="sxs-lookup"><span data-stu-id="90b6d-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="90b6d-109">I když `nuget.exe` funguje plně ve Windows, jsou známé problémy v systémech Linux a OS X. Projděte si informace o [problémech mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="90b6d-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="90b6d-110">[Grafický klient](https://github.com/mrward/monodevelop-nuget-addin) je k dispozici jako doplněk pro MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="90b6d-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="90b6d-111">**Jak zjistím, co balíček obsahuje a jestli je pro moji aplikaci stabilní a užitečný?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="90b6d-112">Primární zdroj pro učení o balíčku je jeho stránka se seznamem na nuget.org (nebo jiném privátním informačním kanálu).</span><span class="sxs-lookup"><span data-stu-id="90b6d-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="90b6d-113">Každá stránka balíčku v nuget.org obsahuje popis balíčku, jeho historii verzí a statistiku využití.</span><span class="sxs-lookup"><span data-stu-id="90b6d-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="90b6d-114">Část **informace** na stránce balíček obsahuje také odkaz na web projektu, kde obvykle najdete mnoho příkladů a další dokumentaci, která vám pomůžou zjistit, jak se balíček používá.</span><span class="sxs-lookup"><span data-stu-id="90b6d-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="90b6d-115">Další informace najdete v tématu [vyhledání a výběr balíčků](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="90b6d-116">NuGet v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90b6d-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="90b6d-117">**Jak se podporuje NuGet v různých produktech sady Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="90b6d-118">Sada Visual Studio ve Windows podporuje [uživatelské rozhraní Správce balíčků](../consume-packages/install-use-packages-visual-studio.md) a [konzolu Správce balíčků](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="90b6d-119">Visual Studio pro Mac obsahuje integrované funkce NuGet, jak je popsáno v tématu [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="90b6d-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="90b6d-120">Visual Studio Code (všechny platformy) nemá žádnou přímou integraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="90b6d-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="90b6d-121">Použijte rozhraní příkazového [řádku NuGet](../reference/nuget-exe-cli-reference.md) nebo rozhraní příkazového [řádku dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="90b6d-122">Azure DevOps poskytuje [krok sestavení pro obnovení balíčků NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="90b6d-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="90b6d-123">[V Azure DevOps můžete také hostovat kanály privátního balíčku NuGet](/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="90b6d-123">You can also [host private NuGet package feeds on Azure DevOps](/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="90b6d-124">**Návody ověřit přesnou verzi nástrojů NuGet, které jsou nainstalované?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="90b6d-125">V aplikaci Visual Studio použijte **nápovědu > o Microsoft Visual Studio** příkaz a podívejte se na verzi zobrazenou vedle **Správce balíčků NuGet** .</span><span class="sxs-lookup"><span data-stu-id="90b6d-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager** .</span></span>

<span data-ttu-id="90b6d-126">Případně můžete spustit konzolu Správce balíčků ( **nástroje > správce balíčků NuGet > konzolu Správce balíčků** ) a zadáním `$host` zobrazíte informace o NuGet včetně verze.</span><span class="sxs-lookup"><span data-stu-id="90b6d-126">Alternatively, launch the Package Manager Console ( **Tools > NuGet Package Manager > Package Manager Console** ) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="90b6d-127">**Jaké programovací jazyky podporuje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="90b6d-128">NuGet je obecně funkční pro jazyky .NET a je navržena k převedení knihoven .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="90b6d-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="90b6d-129">Protože podporuje také automatizaci nástroje MSBuild a sady Visual Studio v některých typech projektů, podporuje také jiné projekty a jazyky do různých stupňů.</span><span class="sxs-lookup"><span data-stu-id="90b6d-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="90b6d-130">Nejnovější verze NuGet podporuje jazyky C#, Visual Basic, F #, WiX a C++.</span><span class="sxs-lookup"><span data-stu-id="90b6d-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="90b6d-131">**Jaké šablony projektů podporuje NuGet?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="90b6d-132">NuGet má plnou podporu pro celou řadu šablon projektů, jako jsou Windows, web, Cloud, SharePoint, WIX a tak dále.</span><span class="sxs-lookup"><span data-stu-id="90b6d-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="90b6d-133">**Návody balíčky aktualizací, které jsou součástí šablon sady Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="90b6d-134">V uživatelském rozhraní Správce balíčků otevřete kartu **aktualizace** a vyberte **Aktualizovat vše** nebo použijte [ `Update-Package` příkaz](../reference/ps-reference/ps-ref-update-package.md) z konzoly Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="90b6d-134">Go to the **Updates** tab in the Package Manager UI and select **Update All** , or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="90b6d-135">Chcete-li aktualizovat vlastní šablonu, je nutné ručně aktualizovat úložiště šablon.</span><span class="sxs-lookup"><span data-stu-id="90b6d-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="90b6d-136">Podívejte se na [blog Xavier pro denákle](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na tomto předmětu.</span><span class="sxs-lookup"><span data-stu-id="90b6d-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="90b6d-137">Všimněte si, že se jedná o vlastní riziko, protože ruční aktualizace mohou poškodit šablonu, pokud není nejnovější verze všech závislostí vzájemně kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="90b6d-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="90b6d-138">**Můžu použít NuGet mimo Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="90b6d-139">Ano, NuGet funguje přímo z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="90b6d-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="90b6d-140">Přečtěte si [příručku k instalaci](../install-nuget-client-tools.md) a [odkaz CLI](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="90b6d-141">Příkazový řádek NuGet</span><span class="sxs-lookup"><span data-stu-id="90b6d-141">NuGet command line</span></span>

<span data-ttu-id="90b6d-142">**Návody získat nejnovější verzi nástroje příkazového řádku NuGet?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="90b6d-143">Projděte si [příručku Instalace](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="90b6d-144">Chcete-li zjistit aktuální nainstalovanou verzi nástroje, použijte `nuget help` .</span><span class="sxs-lookup"><span data-stu-id="90b6d-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="90b6d-145">**Jaká je licence pro nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="90b6d-146">V rámci podmínek licence MIT můžete nuget.exe redistribuovat.</span><span class="sxs-lookup"><span data-stu-id="90b6d-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="90b6d-147">Zodpovídáte za aktualizaci a obsluhu všech kopií nuget.exe, které se rozhodnete znovu distribuovat.</span><span class="sxs-lookup"><span data-stu-id="90b6d-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="90b6d-148">**Je možné nástroj příkazového řádku NuGet zvětšit?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="90b6d-149">Ano, do je možné přidat vlastní příkazy `nuget.exe` , jak je popsáno v [příspěvku na Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="90b6d-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="90b6d-150">Konzola správce balíčků NuGet (Visual Studio ve Windows)</span><span class="sxs-lookup"><span data-stu-id="90b6d-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="90b6d-151">**Návody získat přístup k objektu DTE v konzole správce balíčků?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="90b6d-152">Objekt nejvyšší úrovně v objektovém modelu automatizace sady Visual Studio se nazývá objekt DTE (vývojové nástroje prostředí).</span><span class="sxs-lookup"><span data-stu-id="90b6d-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="90b6d-153">Konzola poskytuje tuto proměnnou prostřednictvím proměnné s názvem `$DTE` .</span><span class="sxs-lookup"><span data-stu-id="90b6d-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="90b6d-154">Další informace najdete v tématu [Přehled modelu automatizace](/visualstudio/extensibility/internals/automation-model-overview) v dokumentaci rozšiřitelnosti sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90b6d-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="90b6d-155">**Snažím se přetypovat $DTE proměnnou na typ DTE2, ale zobrazí se chyba: hodnotu EnvDTE. DTEClass typu EnvDTE. DTEClass nejde převést na typ EnvDTE80. DTE2. Co je?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="90b6d-156">Jedná se o známý problém s tím, jak prostředí PowerShell spolupracuje s objektem COM.</span><span class="sxs-lookup"><span data-stu-id="90b6d-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="90b6d-157">Vyzkoušejte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="90b6d-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="90b6d-158">`Get-Interface` je pomocná funkce, kterou přidal hostitel PowerShellu NuGet.</span><span class="sxs-lookup"><span data-stu-id="90b6d-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="90b6d-159">Vytváření a publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="90b6d-159">Creating and publishing packages</span></span>

<span data-ttu-id="90b6d-160">**Návody seznam můj balíček v informačním kanálu?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="90b6d-161">Viz [Vytvoření a publikování balíčku](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="90b6d-162">**Mám více verzí knihovny, která cílí na různé verze .NET Framework. Návody sestavit jeden balíček, který tuto podporu podporuje?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="90b6d-163">Viz [Podpora více .NET Framework verzí a profilů](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="90b6d-164">**Návody nastavit vlastní úložiště nebo informační kanál?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="90b6d-165">Podívejte se na téma [Přehled hostujících balíčků](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="90b6d-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="90b6d-166">**Jak mohu hromadně nahrávat balíčky do svého informačního kanálu NuGet?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="90b6d-167">Viz [hromadné publikování balíčků NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="90b6d-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="90b6d-168">Práce s balíčky</span><span class="sxs-lookup"><span data-stu-id="90b6d-168">Working with packages</span></span>

<span data-ttu-id="90b6d-169">**Je možné balíčky NuGet nainstalovat bez připojení k Internetu?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-169">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="90b6d-170">Ano, další informace [o tom, jak získat přístup k nugetu v případě nedostatku NuGet.org (nebo jste na rovině)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com), najdete v blogovém příspěvku Scott Hanselman.</span><span class="sxs-lookup"><span data-stu-id="90b6d-170">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="90b6d-171">**Návody instalovat balíčky v jiném umístění než výchozí složka balíčků?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-171">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="90b6d-172">Nastavte [`repositoryPath`](../reference/nuget-config-file.md#config-section) nastavení `Nuget.Config` pomocí `nuget config -set repositoryPath=<path>` .</span><span class="sxs-lookup"><span data-stu-id="90b6d-172">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="90b6d-173">**Návody se vyhnout přidání složky balíčků NuGet do správy zdrojového kódu?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-173">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="90b6d-174">Nastavte na [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) `Nuget.Config` `true` .</span><span class="sxs-lookup"><span data-stu-id="90b6d-174">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="90b6d-175">Tento klíč funguje na úrovni řešení, a proto musí být do `$(Solutiondir)\.nuget\Nuget.Config` souboru přidán.</span><span class="sxs-lookup"><span data-stu-id="90b6d-175">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="90b6d-176">Povolením obnovení balíčku ze sady Visual Studio se tento soubor automaticky vytvoří.</span><span class="sxs-lookup"><span data-stu-id="90b6d-176">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="90b6d-177">**Návody vypnout obnovení balíčků?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-177">**How do I turn off package restore?**</span></span>

<span data-ttu-id="90b6d-178">Viz [povolení a zakázání obnovení balíčku](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="90b6d-178">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="90b6d-179">**Proč se při instalaci místního balíčku se vzdálenými závislostmi zobrazí chybová zpráva "nelze vyřešit chybu závislostí?"**</span><span class="sxs-lookup"><span data-stu-id="90b6d-179">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="90b6d-180">Při instalaci místního balíčku do projektu je nutné vybrat možnost **všechny** zdroje.</span><span class="sxs-lookup"><span data-stu-id="90b6d-180">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="90b6d-181">Tato část agreguje všechny informační kanály namísto použití jediného.</span><span class="sxs-lookup"><span data-stu-id="90b6d-181">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="90b6d-182">Důvodem této chyby je, že uživatelé místního úložiště často chtějí vyhnout nechtěné instalaci vzdáleného balíčku kvůli podnikovým zásadám.</span><span class="sxs-lookup"><span data-stu-id="90b6d-182">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="90b6d-183">**Mám ve stejné složce více projektů, jak můžu použít samostatné soubory packages.config pro každý projekt?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-183">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="90b6d-184">Ve většině projektů, kde samostatné projekty jsou v samostatných složkách živé, to není problém, protože NuGet identifikuje `packages.config` soubory v jednotlivých projektech.</span><span class="sxs-lookup"><span data-stu-id="90b6d-184">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="90b6d-185">Pomocí NuGet 3.3 + a více projektů ve stejné složce můžete vložit název projektu do `packages.config` názvů souborů pomocí vzoru `packages.{project-name}.config` a nástroj NuGet tento soubor použije.</span><span class="sxs-lookup"><span data-stu-id="90b6d-185">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="90b6d-186">Nejedná se o problém při použití PackageReference, protože každý soubor projektu obsahuje vlastní seznam závislostí.</span><span class="sxs-lookup"><span data-stu-id="90b6d-186">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="90b6d-187">**V seznamu úložišť nevidím nuget.org, jak se dá získat zpátky?**</span><span class="sxs-lookup"><span data-stu-id="90b6d-187">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="90b6d-188">Přidejte `https://api.nuget.org/v3/index.json` do seznamu zdrojů nebo</span><span class="sxs-lookup"><span data-stu-id="90b6d-188">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="90b6d-189">Odstraňte `%appdata%\.nuget\NuGet.Config` (Windows) nebo `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) a umožněte novému vytvoření NuGet.</span><span class="sxs-lookup"><span data-stu-id="90b6d-189">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>