---
title: Průvodce konzoly Správce balíčků NuGet
description: Pokyny k používání konzoly Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546875"
---
# <a name="package-manager-console"></a><span data-ttu-id="05160-103">Konzola správce balíčků</span><span class="sxs-lookup"><span data-stu-id="05160-103">Package Manager Console</span></span>

<span data-ttu-id="05160-104">Konzola správce balíčků NuGet je součástí sady Visual Studio ve Windows 2012 a novější verze.</span><span class="sxs-lookup"><span data-stu-id="05160-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="05160-105">(Není součástí sady Visual Studio pro Mac nebo Visual Studio Code.)</span><span class="sxs-lookup"><span data-stu-id="05160-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="05160-106">Konzole vám umožní používat [příkazy prostředí NuGet PowerShell](../tools/powershell-reference.md) najít, nainstalovat, odinstalujte a aktualizovat balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="05160-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="05160-107">Pomocí konzoly je nutné v případech, kdy uživatelské rozhraní Správce balíčků neposkytuje způsob, jak provádět operace.</span><span class="sxs-lookup"><span data-stu-id="05160-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="05160-108">Použití `nuget.exe` příkazy v konzole, najdete v článku [pomocí nuget.exe rozhraní příkazového řádku v konzole](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="05160-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="05160-109">Vyhledání a instalace balíčku se provádí pomocí tří snadných kroků:</span><span class="sxs-lookup"><span data-stu-id="05160-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="05160-110">Otevřete projekt nebo řešení v sadě Visual Studio a otevřete konzoly pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu.</span><span class="sxs-lookup"><span data-stu-id="05160-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="05160-111">Vyhledání balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="05160-111">Find the package you want to install.</span></span> <span data-ttu-id="05160-112">Pokud již tohle už znáte, pokračujte krokem 3.</span><span class="sxs-lookup"><span data-stu-id="05160-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="05160-113">Spuštění instalačního příkazu:</span><span class="sxs-lookup"><span data-stu-id="05160-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="05160-114">Všechny operace, které jsou k dispozici v konzole je možné provést pomocí [rozhraní příkazového řádku NuGet](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="05160-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="05160-115">Příkazy konzoly však pracovat v rámci sady Visual Studio a uložené projekt nebo řešení a často dosáhnout více než jejich ekvivalentní příkazy rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="05160-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="05160-116">Například při instalaci balíčku prostřednictvím konzoly přidá odkaz na projekt služba nepodporuje příkaz rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="05160-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="05160-117">Z tohoto důvodu vývojáři pracující v sadě Visual Studio obvykle raději pomocí konzoly nástroje rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="05160-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="05160-118">Mnoho operací konzole závisí na řešení otevřít v sadě Visual Studio s názvem známé cesty.</span><span class="sxs-lookup"><span data-stu-id="05160-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="05160-119">Pokud už máte neuložené řešení nebo žádné řešení, se zobrazí chyba, "řešení není otevřené nebo nebyl uložen.</span><span class="sxs-lookup"><span data-stu-id="05160-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="05160-120">Ujistěte se, že máte řešení otevřené a uložené."</span><span class="sxs-lookup"><span data-stu-id="05160-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="05160-121">To znamená, že konzoly nelze určit složku řešení.</span><span class="sxs-lookup"><span data-stu-id="05160-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="05160-122">Ukládání neuložené řešení, nebo vytvářet a ukládat řešení, pokud ho nemáte otevřete, vyřešte chybu.</span><span class="sxs-lookup"><span data-stu-id="05160-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="05160-123">Otevřete konzoly a ovládací prvky konzoly</span><span class="sxs-lookup"><span data-stu-id="05160-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="05160-124">Otevřete konzolu v sadě Visual Studio pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkazu.</span><span class="sxs-lookup"><span data-stu-id="05160-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="05160-125">Visual Studio okno, které můžete uspořádat a umístěn libovolně je konzola (viz [přizpůsobení rozložení oken v sadě Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="05160-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="05160-126">Ve výchozím nastavení příkazy konzoly fungovat proti konkrétní balíček zdroje a projekt jako sada v ovládacím prvku v horní části okna:</span><span class="sxs-lookup"><span data-stu-id="05160-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projektu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="05160-128">Vyberte jiný balíček zdrojové a/nebo projekt se změní tyto výchozí hodnoty pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="05160-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="05160-129">Způsobem lze potlačit tato nastavení, aniž byste měnili výchozí hodnoty, většina příkazů podporují `-Source` a `-ProjectName` možnosti.</span><span class="sxs-lookup"><span data-stu-id="05160-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="05160-130">Pokud chcete spravovat zdroje balíčků, vyberte ikonu ozubeného kola.</span><span class="sxs-lookup"><span data-stu-id="05160-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="05160-131">Toto je zástupce **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků** dialogovému oknu, jak je popsáno na [uživatelské rozhraní Správce balíčků](package-manager-ui.md#package-sources) stránky.</span><span class="sxs-lookup"><span data-stu-id="05160-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="05160-132">Ovládací prvek vpravo od selektor projektu vymaže obsah v konzole:</span><span class="sxs-lookup"><span data-stu-id="05160-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Nastavení konzoly Správce balíčků a vymazat ovládacích prvků](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="05160-134">Úplně vpravo tlačítko přeruší dlouhotrvající příkazu.</span><span class="sxs-lookup"><span data-stu-id="05160-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="05160-135">Například systém `Get-Package -ListAvailable -PageSize 500` uvádí balíčky horní 500 na výchozí zdroj (jako je nuget.org), což může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="05160-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Ovládací prvek stop Konzola správce balíčků](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="05160-137">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="05160-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="05160-138">Zobrazit [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="05160-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="05160-139">Instalace balíčku v konzole provádí stejným způsobem, jak je popsáno v [co se stane, když je nainstalován balíček](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), s těmito přídavky:</span><span class="sxs-lookup"><span data-stu-id="05160-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="05160-140">Této konzole se zobrazují v okně s implicitní dohodu příslušných licenčních podmínkách.</span><span class="sxs-lookup"><span data-stu-id="05160-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="05160-141">Pokud nesouhlasíte s podmínkami, byste měli odinstalovat balíček okamžitě.</span><span class="sxs-lookup"><span data-stu-id="05160-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="05160-142">Také odkaz na balíček se přidá do souboru projektu a zobrazí se v **Průzkumníka řešení** pod **odkazy** uzel, je nutné uložit projekt tak, aby se změny v souboru projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="05160-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="05160-143">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="05160-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="05160-144">Zobrazit [odinstalovat balíček](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="05160-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="05160-145">Použití [Get-Package](../tools/ps-ref-get-package.md) zobrazíte všechny balíčky, které jsou aktuálně nainstalované ve výchozím projektu, pokud je potřeba najít identifikátor.</span><span class="sxs-lookup"><span data-stu-id="05160-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="05160-146">Odinstalace balíčku provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="05160-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="05160-147">Odebere odkazy na balíček z projektu (a jakékoli formátu správy se používá).</span><span class="sxs-lookup"><span data-stu-id="05160-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="05160-148">Odkazy se už nezobrazují v **Průzkumníka řešení**.</span><span class="sxs-lookup"><span data-stu-id="05160-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="05160-149">(Možná budete muset znovu sestavte projekt a prohlédněte si ho odebrat z **Bin** složky.)</span><span class="sxs-lookup"><span data-stu-id="05160-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="05160-150">Obrátí všechny změny provedené `app.config` nebo `web.config` kdy byl nainstalován balíček.</span><span class="sxs-lookup"><span data-stu-id="05160-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="05160-151">Odstraní dříve nainstalovali závislosti, pokud žádné zbývající balíčky pomocí těchto závislostí.</span><span class="sxs-lookup"><span data-stu-id="05160-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="05160-152">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="05160-152">Updating a package</span></span>

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

<span data-ttu-id="05160-153">Zobrazit [Get-Package](../tools/ps-ref-get-package.md) a [Update-Package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="05160-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="05160-154">Vyhledání balíčku</span><span class="sxs-lookup"><span data-stu-id="05160-154">Finding a package</span></span>

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

<span data-ttu-id="05160-155">Zobrazit [najít balíček](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="05160-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="05160-156">V sadě Visual Studio 2013 a dříve, použít [Get-Package](../tools/ps-ref-get-package.md) místo.</span><span class="sxs-lookup"><span data-stu-id="05160-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="05160-157">Dostupnost konzoly nástroje</span><span class="sxs-lookup"><span data-stu-id="05160-157">Availability of the console</span></span>

<span data-ttu-id="05160-158">V sadě Visual Studio 2017 Správce balíčků NuGet a NuGet jsou automaticky nainstalovány se některé vyberte. Úlohy související s NET; můžete ho také nainstalovat jednotlivě kontrolou **jednotlivé komponenty > kód nástroje > Správce balíčků NuGet** možnost v instalačním programu sady Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="05160-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="05160-159">Zkontrolujte taky, pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015 a starší, **nástroje > rozšíření a aktualizace...**  a hledání rozšíření Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="05160-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="05160-160">Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, můžete stáhnout přímo z rozšíření [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="05160-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="05160-161">Konzola správce balíčků není v současné době k dispozici se sadou Visual Studio pro Mac.</span><span class="sxs-lookup"><span data-stu-id="05160-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="05160-162">Ekvivalentní příkazy, ale jsou k dispozici prostřednictvím [rozhraní příkazového řádku NuGet](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="05160-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="05160-163">Visual Studio pro Mac má uživatelské rozhraní pro správu balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="05160-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="05160-164">Zobrazit [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="05160-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="05160-165">Konzola správce balíčků není součástí systému Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="05160-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="05160-166">Rozšíření konzole Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="05160-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="05160-167">Některé balíčky nainstalovat nové příkazy konzoly.</span><span class="sxs-lookup"><span data-stu-id="05160-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="05160-168">Například `MvcScaffolding` vytvoří příkazů, jako jsou `Scaffold` vidíte níže, která generuje zobrazení a kontrolery ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="05160-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalace a použití MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="05160-170">Nastavení profilu NuGet Powershellu</span><span class="sxs-lookup"><span data-stu-id="05160-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="05160-171">Profil PowerShell umožňuje zpřístupnit často používané příkazy bez ohledu na to pomocí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="05160-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="05160-172">NuGet podporuje NuGet konkrétní profil většinou nacházejí v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="05160-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="05160-173">Chcete-li najít profil, zadejte `$profile` v konzole:</span><span class="sxs-lookup"><span data-stu-id="05160-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="05160-174">Další podrobnosti najdete v [profily Windows Powershellu](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="05160-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="05160-175">Pomocí nuget.exe rozhraní příkazového řádku v konzole</span><span class="sxs-lookup"><span data-stu-id="05160-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="05160-176">Aby [ `nuget.exe` rozhraní příkazového řádku](nuget-exe-cli-reference.md) dostupná v konzole Správce balíčků, instalaci [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) balíček z konzoly:</span><span class="sxs-lookup"><span data-stu-id="05160-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
