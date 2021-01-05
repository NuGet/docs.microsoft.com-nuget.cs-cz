---
title: Instalace a Správa balíčků NuGet pomocí konzoly nástroje v aplikaci Visual Studio
description: Pokyny k použití konzoly Správce balíčků NuGet v aplikaci Visual Studio pro práci s balíčky.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 31fa51bc017eaaf9306d5f267e5d4b0d7a15ec9c
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699835"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="8f68f-103">Instalace a Správa balíčků pomocí konzoly Správce balíčků v aplikaci Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8f68f-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="8f68f-104">Konzola správce balíčků NuGet umožňuje používat [příkazy NuGet PowerShellu](../reference/powershell-reference.md) k vyhledání, instalaci, odinstalaci a aktualizaci balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f68f-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="8f68f-105">V případech, kdy uživatelské rozhraní Správce balíčků neposkytuje způsob provedení operace, je nutné použít konzolu.</span><span class="sxs-lookup"><span data-stu-id="8f68f-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="8f68f-106">Chcete-li použít `nuget.exe` příkazy rozhraní příkazového řádku v konzole nástroje, přečtěte si téma [použití nuget.exe CLI v konzole](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="8f68f-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="8f68f-107">Konzola je integrována do sady Visual Studio ve Windows.</span><span class="sxs-lookup"><span data-stu-id="8f68f-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="8f68f-108">Není součástí Visual Studio pro Mac ani Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8f68f-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

> [!Important]
> <span data-ttu-id="8f68f-109">Níže uvedené příkazy jsou specifické pro konzolu Správce balíčků v aplikaci Visual Studio a liší se od [příkazů modulu Správa balíčků](/powershell/module/packagemanagement/) , které jsou k dispozici v obecném prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f68f-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="8f68f-110">Konkrétně každé prostředí obsahuje příkazy, které nejsou k dispozici v druhém a příkazy se stejným názvem se mohou v jejich specifických argumentech také lišit.</span><span class="sxs-lookup"><span data-stu-id="8f68f-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="8f68f-111">Při použití konzoly Správa balíčků v aplikaci Visual Studio platí příkazy a argumenty popsané v tomto stávajícím tématu.</span><span class="sxs-lookup"><span data-stu-id="8f68f-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="8f68f-112">Vyhledání a instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="8f68f-112">Find and install a package</span></span>

<span data-ttu-id="8f68f-113">Například vyhledání a instalace balíčku se provádí pomocí tří snadných kroků:</span><span class="sxs-lookup"><span data-stu-id="8f68f-113">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="8f68f-114">Otevřete projekt nebo řešení v aplikaci Visual Studio a otevřete konzolu pomocí **nástrojů > správce balíčků NuGet > příkaz konzoly Správce balíčků** .</span><span class="sxs-lookup"><span data-stu-id="8f68f-114">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="8f68f-115">Najděte balíček, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="8f68f-115">Find the package you want to install.</span></span> <span data-ttu-id="8f68f-116">Pokud už to znáte, přejděte ke kroku 3.</span><span class="sxs-lookup"><span data-stu-id="8f68f-116">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="8f68f-117">Spusťte příkaz instalace:</span><span class="sxs-lookup"><span data-stu-id="8f68f-117">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="8f68f-118">Všechny operace, které jsou k dispozici v konzole nástroje, lze také provést pomocí rozhraní příkazového [řádku NuGet](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8f68f-118">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="8f68f-119">Nicméně příkazy konzoly fungují v kontextu aplikace Visual Studio a uloženého projektu nebo řešení a často doplní více než ekvivalentní příkazy rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="8f68f-119">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="8f68f-120">Například instalace balíčku prostřednictvím konzoly přidá odkaz na projekt, zatímco příkaz CLI neprovede.</span><span class="sxs-lookup"><span data-stu-id="8f68f-120">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="8f68f-121">Z tohoto důvodu vývojáři pracující v aplikaci Visual Studio obvykle upřednostňují použití konzoly pro rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="8f68f-121">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="8f68f-122">Mnoho operací konzoly závisí na tom, že se řešení otevřelo v aplikaci Visual Studio se známým názvem cesty.</span><span class="sxs-lookup"><span data-stu-id="8f68f-122">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="8f68f-123">Pokud máte neuložené řešení nebo žádné řešení, zobrazí se tato chyba: řešení není otevřeno nebo není uloženo.</span><span class="sxs-lookup"><span data-stu-id="8f68f-123">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="8f68f-124">Ujistěte se prosím, že máte otevřené a uložené řešení.</span><span class="sxs-lookup"><span data-stu-id="8f68f-124">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="8f68f-125">To znamená, že konzola nemůže určit složku řešení.</span><span class="sxs-lookup"><span data-stu-id="8f68f-125">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="8f68f-126">Uložení neuloženého řešení nebo vytvoření a uložení řešení, pokud ho ještě nemáte, by mělo chybu opravit.</span><span class="sxs-lookup"><span data-stu-id="8f68f-126">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="8f68f-127">Otevření konzoly a ovládacích prvků konzoly</span><span class="sxs-lookup"><span data-stu-id="8f68f-127">Opening the console and console controls</span></span>

1. <span data-ttu-id="8f68f-128">Otevřete konzolu v aplikaci Visual Studio pomocí **nástrojů > správce balíčků NuGet > příkaz konzoly Správce balíčků** .</span><span class="sxs-lookup"><span data-stu-id="8f68f-128">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="8f68f-129">Konzola je okno aplikace Visual Studio, které lze uspořádat a umístit (viz [přizpůsobení rozložení oken v aplikaci Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="8f68f-129">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="8f68f-130">Ve výchozím nastavení fungují příkazy konzoly s konkrétním zdrojem a projektem balíčku jako nastavené v ovládacím prvku v horní části okna:</span><span class="sxs-lookup"><span data-stu-id="8f68f-130">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projekt](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="8f68f-132">Výběr jiného zdroje balíčků nebo projektu změní tato výchozí nastavení pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="8f68f-132">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="8f68f-133">Pokud chcete tato nastavení overrride beze změny výchozích nastavení, je většina příkazů podporována `-Source` a `-ProjectName` Možnosti.</span><span class="sxs-lookup"><span data-stu-id="8f68f-133">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="8f68f-134">Pokud chcete spravovat zdroje balíčků, vyberte ikonu ozubeného kolečka.</span><span class="sxs-lookup"><span data-stu-id="8f68f-134">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="8f68f-135">Jedná se o zástupce **nástrojů > možností > správce balíčků NuGet > dialogové okno zdroje balíčků** , jak je popsáno na stránce [uživatelského rozhraní Správce balíčků](install-use-packages-visual-studio.md#package-sources) .</span><span class="sxs-lookup"><span data-stu-id="8f68f-135">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="8f68f-136">Ovládací prvek napravo od výběru projektu také vymaže obsah konzoly:</span><span class="sxs-lookup"><span data-stu-id="8f68f-136">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Nastavení konzoly Správce balíčků a zrušení ovládacích prvků](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="8f68f-138">Tlačítko vpravo přerušuje dlouho běžící příkaz.</span><span class="sxs-lookup"><span data-stu-id="8f68f-138">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="8f68f-139">Například při spuštění se `Get-Package -ListAvailable -PageSize 500` zobrazí seznam prvních 500 balíčků na výchozím zdroji (například NuGet.org), což může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="8f68f-139">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Řízení ukončení konzoly Správce balíčků](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="8f68f-141">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="8f68f-141">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="8f68f-142">Viz [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="8f68f-142">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="8f68f-143">Instalace balíčku v konzole nástroje provádí stejný postup, jak je popsáno v tématu [co se stane, když se nainstaluje balíček](../concepts/package-installation-process.md), a to s následujícími přídavky:</span><span class="sxs-lookup"><span data-stu-id="8f68f-143">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="8f68f-144">Konzola zobrazuje příslušné licenční podmínky v okně s předpokládanou smlouvou.</span><span class="sxs-lookup"><span data-stu-id="8f68f-144">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="8f68f-145">Pokud s podmínkami nesouhlasíte, měli byste balíček hned odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="8f68f-145">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="8f68f-146">Také odkaz na balíček je přidán do souboru projektu a zobrazí se v **Průzkumník řešení** pod uzlem **odkazy** , je nutné projekt uložit, aby se změny v souboru projektu zobrazily přímo.</span><span class="sxs-lookup"><span data-stu-id="8f68f-146">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="8f68f-147">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="8f68f-147">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="8f68f-148">Viz [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="8f68f-148">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="8f68f-149">Pokud potřebujete najít identifikátor, použijte [Get-Package](../reference/ps-reference/ps-ref-get-package.md) pro zobrazení všech balíčků aktuálně nainstalovaných ve výchozím projektu.</span><span class="sxs-lookup"><span data-stu-id="8f68f-149">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="8f68f-150">Odinstalace balíčku provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="8f68f-150">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="8f68f-151">Odstraní odkazy na balíček z projektu (a jakýkoli formát správy se používá).</span><span class="sxs-lookup"><span data-stu-id="8f68f-151">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="8f68f-152">Odkazy se již nezobrazují v **Průzkumník řešení**.</span><span class="sxs-lookup"><span data-stu-id="8f68f-152">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="8f68f-153">(Projekt bude pravděpodobně nutné znovu sestavit, aby se zobrazila jeho odebraný ze složky **bin** .)</span><span class="sxs-lookup"><span data-stu-id="8f68f-153">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="8f68f-154">Vrátí všechny změny provedené `app.config` `web.config` v nebo při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="8f68f-154">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="8f68f-155">Odebere dříve nainstalované závislosti, pokud žádné zbývající balíčky nepoužívají tyto závislosti.</span><span class="sxs-lookup"><span data-stu-id="8f68f-155">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="8f68f-156">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="8f68f-156">Update a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="8f68f-157">Viz [Get-Package](../reference/ps-reference/ps-ref-get-package.md) a [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="8f68f-157">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="8f68f-158">Nalezení balíčku</span><span class="sxs-lookup"><span data-stu-id="8f68f-158">Find a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="8f68f-159">Viz [Najít-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="8f68f-159">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="8f68f-160">V Visual Studio 2013 a starších verzích použijte [příkaz Get-Package](../reference/ps-reference/ps-ref-get-package.md) .</span><span class="sxs-lookup"><span data-stu-id="8f68f-160">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="8f68f-161">Dostupnost konzoly</span><span class="sxs-lookup"><span data-stu-id="8f68f-161">Availability of the console</span></span>

<span data-ttu-id="8f68f-162">Od sady Visual Studio 2017 se NuGet a správce balíčků NuGet automaticky nainstalují, když vyberete libovolnou možnost. Úlohy s ČISTÝM vztahem; můžete ji také nainstalovat jednotlivě tím, že v instalačním programu sady Visual Studio zkontrolujete **jednotlivé součásti > nástroj Code tools > správce balíčků NuGet** .</span><span class="sxs-lookup"><span data-stu-id="8f68f-162">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="8f68f-163">Pokud ve Visual Studiu 2015 a starších verzích chybí správce balíčků NuGet, podívejte se na **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f68f-163">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="8f68f-164">Pokud nemůžete použít instalační program rozšíření v aplikaci Visual Studio, můžete si rozšíření stáhnout přímo z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) .</span><span class="sxs-lookup"><span data-stu-id="8f68f-164">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="8f68f-165">Konzola správce balíčků není v Visual Studio pro Mac v současnosti k dispozici.</span><span class="sxs-lookup"><span data-stu-id="8f68f-165">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="8f68f-166">Ekvivalentní příkazy jsou však k dispozici prostřednictvím rozhraní příkazového [řádku NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8f68f-166">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="8f68f-167">Visual Studio pro Mac má uživatelské rozhraní pro správu balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f68f-167">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="8f68f-168">Viz [zahrnutí balíčku NuGet do projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="8f68f-168">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="8f68f-169">Konzola správce balíčků není součástí Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8f68f-169">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="8f68f-170">Rozšiřování konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="8f68f-170">Extend the Package Manager Console</span></span>

<span data-ttu-id="8f68f-171">Některé balíčky instalují nové příkazy pro konzolu nástroje.</span><span class="sxs-lookup"><span data-stu-id="8f68f-171">Some packages install new commands for the console.</span></span> <span data-ttu-id="8f68f-172">Například `MvcScaffolding` vytvoří příkazy `Scaffold` , jako jsou zobrazené níže, které generují řadiče a zobrazení ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="8f68f-172">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalace a použití MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="8f68f-174">Nastavení profilu PowerShellu NuGet</span><span class="sxs-lookup"><span data-stu-id="8f68f-174">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="8f68f-175">Profil PowerShellu umožňuje, aby byly běžně používané příkazy dostupné bez ohledu na to, kde používáte PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f68f-175">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="8f68f-176">NuGet podporuje profil specifický pro NuGet, který se obvykle nachází v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="8f68f-176">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="8f68f-177">Profil najdete tak, že do `$profile` konzoly zadáte:</span><span class="sxs-lookup"><span data-stu-id="8f68f-177">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="8f68f-178">Další podrobnosti najdete v tématu [profily Windows PowerShellu](/previous-versions//bb613488(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="8f68f-178">For more details, refer to [Windows PowerShell Profiles](/previous-versions//bb613488(v=vs.85)).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="8f68f-179">Použití rozhraní příkazového řádku nuget.exe v konzole nástroje</span><span class="sxs-lookup"><span data-stu-id="8f68f-179">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="8f68f-180">Chcete-li zpřístupnit rozhraní příkazového [ `nuget.exe` řádku](../reference/nuget-exe-cli-reference.md) v konzole správce balíčků, nainstalujte balíček [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) z konzoly:</span><span class="sxs-lookup"><span data-stu-id="8f68f-180">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
