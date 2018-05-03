---
title: Průvodce konzoly Správce balíčků NuGet
description: Pokyny k používání konzoly Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 64912f0dc32a492d9c23a02f45b4303c69faf340
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/26/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="bb51f-103">Konzola správce balíčků</span><span class="sxs-lookup"><span data-stu-id="bb51f-103">Package Manager Console</span></span>

<span data-ttu-id="bb51f-104">Konzola správce balíčků NuGet je integrovaná v sadě Visual Studio v systému Windows verze 2012 a novější.</span><span class="sxs-lookup"><span data-stu-id="bb51f-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="bb51f-105">(Není součástí sady Visual Studio pro Mac nebo Visual Studio Code.)</span><span class="sxs-lookup"><span data-stu-id="bb51f-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="bb51f-106">Konzole vám umožní používat [příkazy prostředí NuGet PowerShell](../tools/powershell-reference.md) najít, instalaci, odinstalaci a aktualizovat balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb51f-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="bb51f-107">Pomocí konzoly je nutné v případech, kde uživatelského rozhraní Správce balíčků neposkytuje způsob, jak provést operaci.</span><span class="sxs-lookup"><span data-stu-id="bb51f-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="bb51f-108">Použít `nuget.exe` příkazy v konzole, najdete v části [pomocí nuget.exe rozhraní příkazového řádku v konzole](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="bb51f-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="bb51f-109">Například hledání a instalaci balíčku provádí pomocí tří jednoduché kroky:</span><span class="sxs-lookup"><span data-stu-id="bb51f-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="bb51f-110">Otevřete projekt nebo řešení v sadě Visual Studio a otevřete pomocí konzoly **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkaz.</span><span class="sxs-lookup"><span data-stu-id="bb51f-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="bb51f-111">Najděte balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="bb51f-111">Find the package you want to install.</span></span> <span data-ttu-id="bb51f-112">Pokud už víte, to, přeskočte ke kroku 3.</span><span class="sxs-lookup"><span data-stu-id="bb51f-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="bb51f-113">Spusťte příkaz instalace:</span><span class="sxs-lookup"><span data-stu-id="bb51f-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="bb51f-114">Všechny operace, které jsou k dispozici v konzole můžete také provést s [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="bb51f-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="bb51f-115">Příkazy konzoly ale provoz v rámci kontextu Visual Studio a uložené projekt nebo řešení a často dosáhnout více než jejich ekvivalentní příkazy rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="bb51f-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="bb51f-116">Například instalaci balíčku přes konzolu přidá odkaz na projekt zatímco rozhraní příkazového řádku příkaz neexistuje.</span><span class="sxs-lookup"><span data-stu-id="bb51f-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="bb51f-117">Z tohoto důvodu vývojáře, kteří pracují v sadě Visual Studio obvykle dáváte přednost, pomocí konzoly nástroje rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="bb51f-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="bb51f-118">Mnoho konzole operací závisí na s řešením otevřít v sadě Visual Studio s názvem známé cestě.</span><span class="sxs-lookup"><span data-stu-id="bb51f-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="bb51f-119">Pokud máte neuložené řešení nebo žádné řešení, zobrazí se chyba, "řešení není otevřené nebo není uložené.</span><span class="sxs-lookup"><span data-stu-id="bb51f-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="bb51f-120">Ujistěte se, že máte řešení otevřené a uložené."</span><span class="sxs-lookup"><span data-stu-id="bb51f-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="bb51f-121">To znamená, že konzole nemůže určit složku řešení.</span><span class="sxs-lookup"><span data-stu-id="bb51f-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="bb51f-122">Ukládání neuložené řešení, nebo vytvoření a uložení řešení, pokud nemáte otevřete, by měl opravte chybu.</span><span class="sxs-lookup"><span data-stu-id="bb51f-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="bb51f-123">Otevření konzoly a ovládací prvky konzoly</span><span class="sxs-lookup"><span data-stu-id="bb51f-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="bb51f-124">Otevřete konzolu v sadě Visual Studio pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkaz.</span><span class="sxs-lookup"><span data-stu-id="bb51f-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="bb51f-125">Konzole je okno sady Visual Studio, které mohou být uspořádány a umístěný, ale chcete (viz [přizpůsobení rozložení oken v sadě Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="bb51f-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="bb51f-126">Ve výchozím nastavení fungují příkazy konzoly pro určitý balíček zdrojem a projekt jako sada v ovládacím prvku v horní části okna:</span><span class="sxs-lookup"><span data-stu-id="bb51f-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projectu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="bb51f-128">Vyberte jiný balíček zdroje nebo projektu změní tyto výchozí hodnoty pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="bb51f-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="bb51f-129">Způsobem lze potlačit tato nastavení beze změny výchozí hodnoty, většina příkazů podporují `-Source` a `-ProjectName` možnosti.</span><span class="sxs-lookup"><span data-stu-id="bb51f-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="bb51f-130">Chcete-li spravovat zdroje balíčků, vyberte ikonu zařízení.</span><span class="sxs-lookup"><span data-stu-id="bb51f-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="bb51f-131">Toto je zástupce **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků** dialogové okno jak je popsáno na [uživatelského rozhraní Správce balíčků](package-manager-ui.md#package-sources) stránky.</span><span class="sxs-lookup"><span data-stu-id="bb51f-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="bb51f-132">Ovládací prvek napravo od modulu pro výběr projektu vymaže obsah v konzole:</span><span class="sxs-lookup"><span data-stu-id="bb51f-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Nastavení konzoly Správce balíčků a zrušte ovládací prvky](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="bb51f-134">Úplně vpravo tlačítko přerušení dlouho běžící příkaz.</span><span class="sxs-lookup"><span data-stu-id="bb51f-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="bb51f-135">Například běžet `Get-Package -ListAvailable -PageSize 500` obsahuje seznam balíčků horní 500 na výchozí zdroj (například nuget.org), který může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="bb51f-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Konzola správce balíčků zastavení řízení](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="bb51f-137">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="bb51f-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="bb51f-138">V tématu [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="bb51f-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="bb51f-139">Instalace balíčku v konzole provádí stejný postup, jak je popsáno na [co se stane, když je nainstalován balíček](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), s těmito přídavky:</span><span class="sxs-lookup"><span data-stu-id="bb51f-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="bb51f-140">Konzole zobrazí příslušných licenčních podmínek v jeho okno s předpokládané smlouvy.</span><span class="sxs-lookup"><span data-stu-id="bb51f-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="bb51f-141">Pokud nesouhlasíte s podmínkami, byste měli okamžitě odinstalovat balíček.</span><span class="sxs-lookup"><span data-stu-id="bb51f-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="bb51f-142">Také odkaz na balíček, přidá se do souboru projektu a zobrazí se v **Průzkumníku řešení** pod **odkazy** uzlu, je nutné uložit projektu a podívejte se změny v souboru projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="bb51f-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="bb51f-143">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="bb51f-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="bb51f-144">V tématu [odinstalovat balíček](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="bb51f-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="bb51f-145">Použití [Get-Package](../tools/ps-ref-get-package.md) zobrazíte všechny balíčky, které jsou aktuálně nainstalované ve výchozím projektu, pokud potřebujete najít identifikátor.</span><span class="sxs-lookup"><span data-stu-id="bb51f-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="bb51f-146">Odinstalace balíčku, provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="bb51f-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="bb51f-147">Odebere odkazy na balíček z projektu (a ať formátu správy se používá).</span><span class="sxs-lookup"><span data-stu-id="bb51f-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="bb51f-148">Odkazy na nebude zobrazovat v **Průzkumníku řešení**.</span><span class="sxs-lookup"><span data-stu-id="bb51f-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="bb51f-149">(Možná budete muset znovu sestavte projekt nevidíte odebrán z **Bin** složky.)</span><span class="sxs-lookup"><span data-stu-id="bb51f-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="bb51f-150">Vrátí zpět změny provedené v `app.config` nebo `web.config` Pokud byl balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="bb51f-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="bb51f-151">Pokud žádné zbývající balíčky pomocí těchto závislostí odebere dříve nainstalovali závislosti.</span><span class="sxs-lookup"><span data-stu-id="bb51f-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="bb51f-152">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="bb51f-152">Updating a package</span></span>

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

<span data-ttu-id="bb51f-153">V tématu [Get-Package](../tools/ps-ref-get-package.md) a [balíčku aktualizace](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="bb51f-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="bb51f-154">Hledání balíčku</span><span class="sxs-lookup"><span data-stu-id="bb51f-154">Finding a package</span></span>

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

<span data-ttu-id="bb51f-155">V tématu [najít balíček](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="bb51f-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="bb51f-156">V sadě Visual Studio 2013 a starší, použijte [Get-Package](../tools/ps-ref-get-package.md) místo.</span><span class="sxs-lookup"><span data-stu-id="bb51f-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="bb51f-157">Dostupnost konzoly nástroje</span><span class="sxs-lookup"><span data-stu-id="bb51f-157">Availability of the console</span></span>

<span data-ttu-id="bb51f-158">V aplikaci Visual Studio 2017 NuGet a Správce balíčků NuGet jsou automaticky nainstalovány po výběru některé. Úlohy související s NET; Můžete také nainstalovat ji jednotlivě kontrolou **jednotlivých součástí > Code nástroje > Správce balíčků NuGet** možnosti v instalačním programu Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bb51f-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="bb51f-159">Zkontrolujte také, pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015 a starší, **nástroje > rozšíření a aktualizace...**  a vyhledejte rozšíření Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb51f-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="bb51f-160">Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, si můžete stáhnout rozšíření přímo z [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="bb51f-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="bb51f-161">Konzola správce balíčků není v současné době dostupné pomocí sady Visual Studio for Mac.</span><span class="sxs-lookup"><span data-stu-id="bb51f-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="bb51f-162">Ekvivalentní příkazy, ale jsou k dispozici prostřednictvím [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="bb51f-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="bb51f-163">Visual Studio pro Mac nemá uživatelského rozhraní pro správu balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb51f-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="bb51f-164">V tématu [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="bb51f-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="bb51f-165">Konzola správce balíčků není součástí Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bb51f-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="bb51f-166">Rozšíření konzole Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="bb51f-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="bb51f-167">Některé balíčky nainstalujte nové příkazy pro konzolu.</span><span class="sxs-lookup"><span data-stu-id="bb51f-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="bb51f-168">Například `MvcScaffolding` vytvoří příkazy, jako je `Scaffold` vidíte níže, který generuje kontrolery a zobrazení ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="bb51f-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalace a použití MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="bb51f-170">Nastavení profilu NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb51f-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="bb51f-171">Profil prostředí PowerShell umožňuje zpřístupnit běžně používané příkazy bez ohledu na pomocí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb51f-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="bb51f-172">NuGet podporuje NuGet konkrétní profil většinou nacházejí v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="bb51f-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="bb51f-173">Chcete-li vyhledat profil, zadejte `$profile` v konzole:</span><span class="sxs-lookup"><span data-stu-id="bb51f-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="bb51f-174">Další podrobnosti najdete v části [profily Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb51f-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="bb51f-175">Pomocí nuget.exe rozhraní příkazového řádku v konzole</span><span class="sxs-lookup"><span data-stu-id="bb51f-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="bb51f-176">Chcete-li [ `nuget.exe` rozhraní příkazového řádku](nuget-exe-cli-reference.md) k dispozici v konzoli správce balíčků nainstalujte [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) balíček z konzoly:</span><span class="sxs-lookup"><span data-stu-id="bb51f-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
