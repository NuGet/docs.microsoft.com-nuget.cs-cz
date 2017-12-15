---
title: "Instalace nástrojů klienta NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Pokyny k instalaci klienta nástroje, rozhraní příkazového řádku (CLI) a Správce balíčků pro sadu Visual Studio."
keywords: "nuget.exe rozhraní příkazového řádku, nástrojích klienta NuGet, Správce balíčků NuGet, konzoly Správce balíčků NuGet, NuGet pro Visual Studio, NuGet beta kanálu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="b181e-104">Instalace nástrojů klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="b181e-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="b181e-105">**Hledáte nainstalovat balíček? V tématu [rychlý start - použití balíček](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="b181e-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="b181e-106">Existují dvě primární nástroje, které vám pomůžou vytvářet, publikovat a využívat balíčky NuGet:</span><span class="sxs-lookup"><span data-stu-id="b181e-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="b181e-107">[ **NuGet CLI** ](#nuget-cli) je nástroj příkazového řádku pro Windows, který nabízí všechny funkce NuGet; může být spuštěn také na Mac OSX a Linux pomocí Mono nebo prostřednictvím rozhraní příkazového řádku .NET Core (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="b181e-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="b181e-108">[ **Správce balíčků NuGet v sadě Visual Studio** ](#nuget-package-manager-in-visual-studio) (jenom Windows) je nástroj grafického uživatelského rozhraní pro správu balíčků a zahrnuje konzole prostředí PowerShell, pomocí kterého můžete určité příkazy pro balíčky NuGet přímo v rámci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b181e-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="b181e-109">Uživatelské rozhraní Správce balíčků a konzoly jsou obě zahrnutá v sadě Visual Studio (v systému Windows) 2012 a novější a může být nainstalován ručně pro starší verze.</span><span class="sxs-lookup"><span data-stu-id="b181e-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="b181e-110">Pomocí sady Visual Studio pro Mac NuGet možnosti jsou součástí přímo.</span><span class="sxs-lookup"><span data-stu-id="b181e-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="b181e-111">V tématu [balíček včetně NuGet ve vašem projektu](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) návod.</span><span class="sxs-lookup"><span data-stu-id="b181e-111">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="b181e-112">Visual Studio Code v současnosti nemá žádné integrovanou podporu NuGet.</span><span class="sxs-lookup"><span data-stu-id="b181e-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="b181e-113">Pomocí rozhraní příkazového řádku NuGet nebo [dotnet rozhraní příkazového řádku](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="b181e-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="b181e-114">Rozhraní příkazového řádku NuGet a Správce balíčků podporují následující operace:</span><span class="sxs-lookup"><span data-stu-id="b181e-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="b181e-115">Hledání balíčků</span><span class="sxs-lookup"><span data-stu-id="b181e-115">Search packages</span></span>
- <span data-ttu-id="b181e-116">Instalovat balíčky</span><span class="sxs-lookup"><span data-stu-id="b181e-116">Install packages</span></span>
- <span data-ttu-id="b181e-117">Balíčky aktualizací</span><span class="sxs-lookup"><span data-stu-id="b181e-117">Update packages</span></span>
- <span data-ttu-id="b181e-118">Odinstalaci balíčků</span><span class="sxs-lookup"><span data-stu-id="b181e-118">Uninstall packages</span></span>
- <span data-ttu-id="b181e-119">Obnovení balíčků (uživatelského rozhraní pouze v Správce balíčků)</span><span class="sxs-lookup"><span data-stu-id="b181e-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="b181e-120">Spravovat zdroje NuGet</span><span class="sxs-lookup"><span data-stu-id="b181e-120">Manage NuGet sources</span></span>

<span data-ttu-id="b181e-121">Následující funkce jsou podporovány pouze v rozhraní příkazového řádku NuGet:</span><span class="sxs-lookup"><span data-stu-id="b181e-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="b181e-122">Správa balíčků (nuget.org nebo privátní informační kanál)</span><span class="sxs-lookup"><span data-stu-id="b181e-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="b181e-123">Vytvoření balíčků</span><span class="sxs-lookup"><span data-stu-id="b181e-123">Create packages</span></span> 
- <span data-ttu-id="b181e-124">Publikování balíčků</span><span class="sxs-lookup"><span data-stu-id="b181e-124">Publish packages</span></span>
- <span data-ttu-id="b181e-125">Spravovat soubor nuget.config.</span><span class="sxs-lookup"><span data-stu-id="b181e-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="b181e-126">Správě ukládání do mezipaměti NuGet</span><span class="sxs-lookup"><span data-stu-id="b181e-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="b181e-127">Replikace balíčku</span><span class="sxs-lookup"><span data-stu-id="b181e-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="b181e-128">Dobrý dalším nástrojem je [Explorer balíček NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), nástroj na open source, samostatné vizuálně zkoumat, vytvořit a upravit balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="b181e-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="b181e-129">Je třeba velmi užitečné, změnit experimentální struktura balíček bez nutnosti znovu sestavte balíček pokaždé, když.</span><span class="sxs-lookup"><span data-stu-id="b181e-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="b181e-130">Napříč platformami [.NET Core rozhraní příkazového řádku](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) nástrojů, použít pro vývoj aplikací .NET Core podporuje několik příkazy pro balíčky NuGet, například odstranit, místní hodnoty, push, aktualizací Service pack a obnovení.</span><span class="sxs-lookup"><span data-stu-id="b181e-130">The cross-platform [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="b181e-131">Rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="b181e-131">NuGet CLI</span></span>

<span data-ttu-id="b181e-132">Rozhraní příkazového řádku NuGet poskytuje přístup k všechny možnosti NuGet a lze spustit ve Windows, Mac OSX a Linux, jak je popsáno v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="b181e-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="b181e-133">Windows</span><span class="sxs-lookup"><span data-stu-id="b181e-133">Windows</span></span>

<span data-ttu-id="b181e-134">**Přímé stahování:**</span><span class="sxs-lookup"><span data-stu-id="b181e-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="b181e-135">U balíčku NuGet 1.4 +, můžete použít `nuget update -self` aktualizovat vaše stávající nuget.exe na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="b181e-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="b181e-136">**Ostatní metody:**</span><span class="sxs-lookup"><span data-stu-id="b181e-136">**Other methods:**</span></span>

- <span data-ttu-id="b181e-137">**Chocolatey**: Nainstalujte [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey balíčku pomocí [Chocolatey](http://chocolatey.org) klienta.</span><span class="sxs-lookup"><span data-stu-id="b181e-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="b181e-138">**Visual Studio**: Nainstalujte [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) balíček z konzoly Správce balíčků v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b181e-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="b181e-139">**Pro uživatele 2.x NuGet**: z důvodu nejnovější změny zavedené v NuGet 3.2 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) body na nejnovější stabilní verze 2.x NuGet aby průběžnou integraci systémů z potenciálně ukončování řádků.</span><span class="sxs-lookup"><span data-stu-id="b181e-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="b181e-140">Mac OSX a Linux</span><span class="sxs-lookup"><span data-stu-id="b181e-140">Mac OSX and Linux</span></span>

<span data-ttu-id="b181e-141">Na Mac OSX a Linux existují dva způsoby, jak spustit rozhraní NuGet příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="b181e-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="b181e-142">Nainstalujte [.NET Core SDK](https://www.microsoft.com/net/download/core), což zahrnuje základních možností NuGet.</span><span class="sxs-lookup"><span data-stu-id="b181e-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="b181e-143">Soubory ke stažení jsou také uvedeny na [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="b181e-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="b181e-144">Pokud potřebujete úplnější možnosti, použijte druhý níže uvedenou možnost používat `nuget.exe` s Mono.</span><span class="sxs-lookup"><span data-stu-id="b181e-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="b181e-145">Nainstalujte [Mono](http://www.mono-project.com/docs/getting-started/install/) a potom pomocí `nuget.exe` spustitelného souboru příkazového řádku pro Windows (verze 3.2 a novější) z [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="b181e-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="b181e-146">Systémem NuGet Mono podléhá následující omezení:</span><span class="sxs-lookup"><span data-stu-id="b181e-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="b181e-147">Postup testování příkazy:</span><span class="sxs-lookup"><span data-stu-id="b181e-147">Commands tested to work:</span></span>
        - <span data-ttu-id="b181e-148">Konfigurace</span><span class="sxs-lookup"><span data-stu-id="b181e-148">config</span></span>
        - <span data-ttu-id="b181e-149">Odstranit</span><span class="sxs-lookup"><span data-stu-id="b181e-149">delete</span></span>
        - <span data-ttu-id="b181e-150">Nápověda</span><span class="sxs-lookup"><span data-stu-id="b181e-150">help</span></span>
        - <span data-ttu-id="b181e-151">Instalace</span><span class="sxs-lookup"><span data-stu-id="b181e-151">install</span></span>
        - <span data-ttu-id="b181e-152">list</span><span class="sxs-lookup"><span data-stu-id="b181e-152">list</span></span>
        - <span data-ttu-id="b181e-153">Push</span><span class="sxs-lookup"><span data-stu-id="b181e-153">push</span></span>
        - <span data-ttu-id="b181e-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="b181e-154">setApiKey</span></span>
        - <span data-ttu-id="b181e-155">Zdroje</span><span class="sxs-lookup"><span data-stu-id="b181e-155">sources</span></span>
        - <span data-ttu-id="b181e-156">specifikace</span><span class="sxs-lookup"><span data-stu-id="b181e-156">spec</span></span>

    - <span data-ttu-id="b181e-157">Částečně pracovní příkazy:</span><span class="sxs-lookup"><span data-stu-id="b181e-157">Partially-working commands:</span></span>
        - <span data-ttu-id="b181e-158">Sada: funguje s `.nuspec` soubory, ale ne soubory projektu.</span><span class="sxs-lookup"><span data-stu-id="b181e-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="b181e-159">obnovení: funguje s `packages.config` a `project.json` soubory, ale ne při řešení (`.sln`) soubory.</span><span class="sxs-lookup"><span data-stu-id="b181e-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="b181e-160">Příkazy, které nefungují:</span><span class="sxs-lookup"><span data-stu-id="b181e-160">Commands that do not work:</span></span>
        - <span data-ttu-id="b181e-161">Aktualizace</span><span class="sxs-lookup"><span data-stu-id="b181e-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="b181e-162">Související témata</span><span class="sxs-lookup"><span data-stu-id="b181e-162">Related topics</span></span>

- [<span data-ttu-id="b181e-163">Referenční dokumentace rozhraní příkazového řádku NuGet</span><span class="sxs-lookup"><span data-stu-id="b181e-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="b181e-164">Vytváření balíčku</span><span class="sxs-lookup"><span data-stu-id="b181e-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="b181e-165">Publikování balíčku</span><span class="sxs-lookup"><span data-stu-id="b181e-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="b181e-166">Správce balíčků NuGet v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b181e-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="b181e-167">Správce balíčků NuGet je zahrnuta v každé edici sady Visual Studio v systému Windows 2012 a novější.</span><span class="sxs-lookup"><span data-stu-id="b181e-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="b181e-168">Obsahuje uživatelského rozhraní Správce balíčků ([odkaz](../tools/package-manager-ui.md)) a konzola Správce balíčků, pomocí kterého se dostanete nástroje, které jsou součástí určitých balíčků ([odkaz](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="b181e-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="b181e-169">Instalační program Visual Studio 2017 zahrnuje Správce balíčků NuGet s libovolnou úlohu, kterou využívá rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="b181e-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="b181e-170">Chcete-li instalovat samostatně, nebo ověřte, zda je nainstalován Správce balíčků, spusťte instalační program Visual Studio 2017 a zkontrolujte příslušné možnosti v nabídce **jednotlivých součástí > Code nástroje > Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b181e-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="b181e-171">Konzole vyžaduje [prostředí PowerShell 2.0](http://support.microsoft.com/kb/968929), která již bude nainstalován ve Windows 7 nebo novější a Windows Server 2008 R2 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="b181e-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="b181e-172">Konzola správce balíčků příkazy také fungovat pouze v sadě Visual Studio v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="b181e-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="b181e-173">Pomocí rozhraní příkazového řádku NuGet mimo prostředí, včetně pomocí sady Visual Studio pro Mac a Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b181e-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="b181e-174">Instalace Správce balíčků pro Visual Studio 2010 a starší</span><span class="sxs-lookup"><span data-stu-id="b181e-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="b181e-175">*Tyto kroky nejsou potřebné pro sadu Visual Studio 2012 a novějším, které již obsahují Správce balíčků.*</span><span class="sxs-lookup"><span data-stu-id="b181e-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="b181e-176">V sadě Visual Studio 2010 a starší, klikněte na tlačítko **nástroje > rozšíření a aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="b181e-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="b181e-177">Přejděte na **Online**, vyhledejte "NuGet balíček správce pro Visual Studio" a klikněte na **Stáhnout**.</span><span class="sxs-lookup"><span data-stu-id="b181e-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="b181e-178">V dialogovém okně instalačního programu klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="b181e-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="b181e-179">Po dokončení instalace restartujte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b181e-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="b181e-180">Pokud nelze použít **rozšíření a aktualizace** dialogové okno v sadě Visual Studio (například jeho blokován bránou proxy serveru), si můžete stáhnout rozšíření pro Visual Studio 2013 a 2015 přímo na [https://dist.nuget.org/ index.HTML](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="b181e-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="b181e-181">Aktualizace Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="b181e-181">Updating the Package Manager</span></span>

<span data-ttu-id="b181e-182">Pro Visual Studio 2015 Update 2 nebo novější správce balíčku se automaticky aktualizují na nejnovější stabilní verze.</span><span class="sxs-lookup"><span data-stu-id="b181e-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="b181e-183">Pro Visual Studio 2015 Update 1 a starší, vyberte **nástroje > rozšíření a aktualizace** příkaz a klikněte na **aktualizace** a zda je k dispozici nová verze Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="b181e-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="b181e-184">Verze Preview NuGet</span><span class="sxs-lookup"><span data-stu-id="b181e-184">NuGet previews</span></span>

<span data-ttu-id="b181e-185">Pokud chcete zobrazit náhled chystaných funkcí NuGet, nainstalujte [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), který funguje souběžného s stabilní verze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b181e-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="b181e-186">Všimněte si, že předchozí Beta NuGet kanálu (`https://dotnet.myget.org/F/nuget-beta/vsix/`) pro Visual Studio 2015 se už používá.</span><span class="sxs-lookup"><span data-stu-id="b181e-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="b181e-187">Chcete odesílat zprávy o problémech s libovolnou verzi aplikace NuGet nebo sdílet nápady, otevřete na problém [úložiště NuGet GitHub](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="b181e-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="b181e-188">Související témata</span><span class="sxs-lookup"><span data-stu-id="b181e-188">Related topics</span></span>

- [<span data-ttu-id="b181e-189">Odkaz uživatelského rozhraní Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="b181e-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="b181e-190">Konzola správce balíčků odkaz</span><span class="sxs-lookup"><span data-stu-id="b181e-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="b181e-191">Referenční informace prostředí PowerShell konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="b181e-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)