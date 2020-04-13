---
title: Instalace a správa balíčků NuGet pomocí konzoly v sadě Visual Studio
description: Pokyny pro použití konzoly NuGet Package Manager console v sadě Visual Studio pro práci s balíčky.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428952"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="318d9-103">Instalace a správa balíčků pomocí konzoly Správce balíčků v sadě Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="318d9-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="318d9-104">Konzola Správce balíčků NuGet umožňuje pomocí [příkazů NuGet PowerShell](../reference/powershell-reference.md) najít, nainstalovat, odinstalovat a aktualizovat balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="318d9-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="318d9-105">Použití konzoly je nezbytné v případech, kdy ui Správce balíčků neposkytuje způsob, jak provést operaci.</span><span class="sxs-lookup"><span data-stu-id="318d9-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="318d9-106">Informace `nuget.exe` o použití příkazů příkazového příkazu příkazu PŘÍKAZOvého nastavení v konzole naleznete v [tématu Použití příkazového příkazu nuget.exe v konzole](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="318d9-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="318d9-107">Konzole je integrovándo sady Visual Studio v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="318d9-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="318d9-108">Není součástí Visual Studio pro Mac nebo Visual Studio kód.</span><span class="sxs-lookup"><span data-stu-id="318d9-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="318d9-109">Vyhledání a instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="318d9-109">Find and install a package</span></span>

<span data-ttu-id="318d9-110">Například nalezení a instalace balíčku se provádí třemi jednoduchými kroky:</span><span class="sxs-lookup"><span data-stu-id="318d9-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="318d9-111">Otevřete projekt nebo řešení v sadě Visual Studio a otevřete konzolu pomocí **příkazu Nástroje > NuGet Správce balíčků > konzoli správce balíčků.**</span><span class="sxs-lookup"><span data-stu-id="318d9-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="318d9-112">Najděte balíček, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="318d9-112">Find the package you want to install.</span></span> <span data-ttu-id="318d9-113">Pokud již víte, přejděte ke kroku 3.</span><span class="sxs-lookup"><span data-stu-id="318d9-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="318d9-114">Spusťte příkaz instalace:</span><span class="sxs-lookup"><span data-stu-id="318d9-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="318d9-115">Všechny operace, které jsou k dispozici v konzole lze provést také s [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="318d9-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="318d9-116">Příkazy konzoly však pracovat v kontextu sady Visual Studio a uložené projekt/řešení a často dosáhnout více než jejich ekvivalentní příkazy příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="318d9-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="318d9-117">Například instalace balíčku prostřednictvím konzoly přidá odkaz na projekt vzhledem k tomu, že příkaz příkazu příkazu příkazu cli nikoli.</span><span class="sxs-lookup"><span data-stu-id="318d9-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="318d9-118">Z tohoto důvodu vývojáři pracující v sadě Visual Studio obvykle dávají přednost použití konzoly rozhraní cli.</span><span class="sxs-lookup"><span data-stu-id="318d9-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="318d9-119">Mnoho operací konzoly závisí na otevření řešení v sadě Visual Studio se známým názvem cesty.</span><span class="sxs-lookup"><span data-stu-id="318d9-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="318d9-120">Pokud máte neuložené řešení nebo žádné řešení, zobrazí se chyba "Řešení není otevřeno nebo není uloženo.</span><span class="sxs-lookup"><span data-stu-id="318d9-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="318d9-121">Ujistěte se, že máte otevřené a uložené řešení."</span><span class="sxs-lookup"><span data-stu-id="318d9-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="318d9-122">To znamená, že konzola nemůže určit složku řešení.</span><span class="sxs-lookup"><span data-stu-id="318d9-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="318d9-123">Uložení neuloženého řešení nebo vytvoření a uložení řešení, pokud nemáte otevřené, by mělo chybu opravit.</span><span class="sxs-lookup"><span data-stu-id="318d9-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="318d9-124">Otevření ovládacích prvků konzoly a konzoly</span><span class="sxs-lookup"><span data-stu-id="318d9-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="318d9-125">Otevřete konzolu v sadě Visual Studio pomocí příkazu **Nástroje > Správce balíčků > konzola správce balíčků.**</span><span class="sxs-lookup"><span data-stu-id="318d9-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="318d9-126">Konzola je okno sady Visual Studio, které lze uspořádat a umístit však chcete (viz [Přizpůsobení rozložení oken v sadě Visual Studio).](/visualstudio/ide/customizing-window-layouts-in-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="318d9-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="318d9-127">Ve výchozím nastavení konzolové příkazy pracují s určitým zdrojem balíčku a projektem, jak je nastaveno v ovládacím prvku v horní části okna:</span><span class="sxs-lookup"><span data-stu-id="318d9-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projekt](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="318d9-129">Výběrem jiného zdroje balíčku nebo projektu se změní výchozí hodnoty pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="318d9-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="318d9-130">Chcete-li tato nastavení přepsat bez evidenčních hodnot, podporuje většina příkazů `-Source` a `-ProjectName` možností.</span><span class="sxs-lookup"><span data-stu-id="318d9-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="318d9-131">Chcete-li spravovat zdroje balíčků, vyberte ikonu ozubeného kola.</span><span class="sxs-lookup"><span data-stu-id="318d9-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="318d9-132">Toto je zástupce **nástroje > možnosti > NuGet Správce balíčků > zdroje balíčků,** jak je popsáno na stránce [ui Správce balíčků.](install-use-packages-visual-studio.md#package-sources)</span><span class="sxs-lookup"><span data-stu-id="318d9-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="318d9-133">Ovládací prvek vpravo od voliče projektu také vymaže obsah konzoly:</span><span class="sxs-lookup"><span data-stu-id="318d9-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Nastavení konzoly Správce balíčků a jasné ovládací prvky](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="318d9-135">Tlačítko zcela vpravo přeruší dlouhotrvající příkaz.</span><span class="sxs-lookup"><span data-stu-id="318d9-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="318d9-136">Spuštění `Get-Package -ListAvailable -PageSize 500` například uvádí prvních 500 balíčků na výchozím zdroji (například nuget.org), což může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="318d9-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Ovládací prvek zastavení konzoly Správce balíčků](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="318d9-138">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="318d9-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="318d9-139">Viz [Instalační balíček](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="318d9-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="318d9-140">Instalace balíčku v konzole provádí stejné kroky, jaké jsou popsány v části [Co se stane při instalaci balíčku](../concepts/package-installation-process.md), s následujícími dodatky:</span><span class="sxs-lookup"><span data-stu-id="318d9-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="318d9-141">Konzola zobrazí příslušné licenční podmínky ve svém okně s předpokládanou smlouvou.</span><span class="sxs-lookup"><span data-stu-id="318d9-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="318d9-142">Pokud s podmínkami nesouhlasíte, měli byste balíček okamžitě odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="318d9-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="318d9-143">Také odkaz na balíček je přidán do souboru projektu a zobrazí se v **Průzkumníku řešení** v uzlu **Odkazy,** je třeba uložit projekt zobrazíte změny v souboru projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="318d9-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="318d9-144">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="318d9-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="318d9-145">Viz [Odinstalovat-Balíček](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="318d9-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="318d9-146">Pomocí [get-package](../reference/ps-reference/ps-ref-get-package.md) zobrazíte všechny balíčky aktuálně nainstalované ve výchozím projektu, pokud potřebujete najít identifikátor.</span><span class="sxs-lookup"><span data-stu-id="318d9-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="318d9-147">Odinstalování balíčku provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="318d9-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="318d9-148">Odebere odkazy na balíček z projektu (a bez ohledu na formát správy je používán).</span><span class="sxs-lookup"><span data-stu-id="318d9-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="318d9-149">Odkazy se již nezobrazují v **Průzkumníku řešení**.</span><span class="sxs-lookup"><span data-stu-id="318d9-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="318d9-150">(Pravděpodobně bude nutné znovu vytvořit projekt, aby byl odebrán ze složky **Bin.)**</span><span class="sxs-lookup"><span data-stu-id="318d9-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="318d9-151">Vrátí všechny změny `app.config` provedené `web.config` v aplikaci nebo při instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="318d9-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="318d9-152">Odebere dříve nainstalované závislosti, pokud tyto závislosti nepoužívají žádné zbývající balíčky.</span><span class="sxs-lookup"><span data-stu-id="318d9-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="318d9-153">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="318d9-153">Update a package</span></span>

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

<span data-ttu-id="318d9-154">Viz [Get-Package](../reference/ps-reference/ps-ref-get-package.md) a [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="318d9-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="318d9-155">Najít balíček</span><span class="sxs-lookup"><span data-stu-id="318d9-155">Find a package</span></span>

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

<span data-ttu-id="318d9-156">Viz [Najít-balíček](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="318d9-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="318d9-157">V Sadě Visual Studio 2013 a starší, použijte [get-package](../reference/ps-reference/ps-ref-get-package.md) místo.</span><span class="sxs-lookup"><span data-stu-id="318d9-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="318d9-158">Dostupnost konzoly</span><span class="sxs-lookup"><span data-stu-id="318d9-158">Availability of the console</span></span>

<span data-ttu-id="318d9-159">Počínaje Visual Studio 2017 NuGet a NuGet Správce balíčků jsou automaticky nainstalovány, když vyberete libovolné . NET související s úlohami; Můžete jej také nainstalovat jednotlivě kontrolou **jednotlivých součástí > nástroje Code >** možnost i správce balíčků NuGet v instalačním programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="318d9-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="318d9-160">Také pokud chybí Správce balíčků NuGet v sadě Visual Studio 2015 a starší, zkontrolujte **nástroje > rozšíření a aktualizace...** a vyhledejte rozšíření NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="318d9-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="318d9-161">Pokud se vám nedaří použít instalační program rozšíření v sadě Visual [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)Studio, můžete si rozšíření stáhnout přímo z aplikace .</span><span class="sxs-lookup"><span data-stu-id="318d9-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="318d9-162">Konzola Správce balíčků není v současné době k dispozici v sadě Visual Studio for Mac.</span><span class="sxs-lookup"><span data-stu-id="318d9-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="318d9-163">Ekvivalentní příkazy jsou však k dispozici prostřednictvím [rozhraní příkazového příkazu NuGet](../reference/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="318d9-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="318d9-164">Visual Studio pro Mac má ui pro správu balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="318d9-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="318d9-165">Viz [včetně balíčku NuGet v projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="318d9-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="318d9-166">Konzola Správce balíčků není součástí kódu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="318d9-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="318d9-167">Rozšíření konzoly Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="318d9-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="318d9-168">Některé balíčky instalují nové příkazy pro konzolu.</span><span class="sxs-lookup"><span data-stu-id="318d9-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="318d9-169">Například `MvcScaffolding` vytvoří příkazy, jako `Scaffold` je uvedeno níže, který generuje ASP.NET MVC řadiče a zobrazení:</span><span class="sxs-lookup"><span data-stu-id="318d9-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalace a používání mvcscaffoldu](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="318d9-171">Nastavení profilu prostředí NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="318d9-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="318d9-172">Profil Prostředí PowerShell umožňuje zpřístupnit běžně používané příkazy všude, kde používáte PowerShell.</span><span class="sxs-lookup"><span data-stu-id="318d9-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="318d9-173">NuGet podporuje profil specifický pro NuGet, který se obvykle nachází v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="318d9-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="318d9-174">Chcete-li profil `$profile` najít, zadejte do konzole:</span><span class="sxs-lookup"><span data-stu-id="318d9-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="318d9-175">Další podrobnosti naleznete v části [Profily prostředí Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="318d9-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="318d9-176">Použití cli nuget.exe v konzole</span><span class="sxs-lookup"><span data-stu-id="318d9-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="318d9-177">Chcete-li [ `nuget.exe` rozhraní příkazového řádku](../reference/nuget-exe-cli-reference.md) zpřístupnit v konzole Správce balíčků, nainstalujte balíček [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) z konzoly:</span><span class="sxs-lookup"><span data-stu-id="318d9-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
