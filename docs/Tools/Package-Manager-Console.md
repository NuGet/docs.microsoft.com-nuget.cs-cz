---
title: "Průvodce konzoly Správce balíčků NuGet | Microsoft Docs"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords: vs.nuget.packagemanager.console
description: "Pokyny k používání konzoly Správce balíčků NuGet v sadě Visual Studio pro práci s balíčky."
keywords: "Konzole Správce balíčků NuGet, NuGet powershell, spravovat balíčky NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b89c51812cee0f64c6f5c39cd9d86bc4a0be068e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/25/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="33af4-104">Konzola správce balíčků</span><span class="sxs-lookup"><span data-stu-id="33af4-104">Package Manager Console</span></span>

<span data-ttu-id="33af4-105">Konzola správce balíčků NuGet je integrovaná v sadě Visual Studio v systému Windows verze 2012 a novější.</span><span class="sxs-lookup"><span data-stu-id="33af4-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="33af4-106">(Není součástí sady Visual Studio pro Mac nebo Visual Studio Code.)</span><span class="sxs-lookup"><span data-stu-id="33af4-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="33af4-107">Konzole vám umožní používat [příkazy prostředí NuGet PowerShell](../tools/powershell-reference.md) najít, instalaci, odinstalaci a aktualizovat balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="33af4-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="33af4-108">Pomocí konzoly je nutné v případech, kde uživatelského rozhraní Správce balíčků neposkytuje způsob, jak provést operaci.</span><span class="sxs-lookup"><span data-stu-id="33af4-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="33af4-109">Použít `nuget.exe` příkazy v konzole, najdete v části [pomocí nuget.exe rozhraní příkazového řádku v konzole](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="33af4-109">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="33af4-110">Například hledání a instalaci balíčku provádí pomocí tří jednoduché kroky:</span><span class="sxs-lookup"><span data-stu-id="33af4-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="33af4-111">Otevřete projekt nebo řešení v sadě Visual Studio a otevřete pomocí konzoly **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkaz.</span><span class="sxs-lookup"><span data-stu-id="33af4-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="33af4-112">Najděte balíčku, který chcete nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="33af4-112">Find the package you want to install.</span></span> <span data-ttu-id="33af4-113">Pokud už víte, to, přeskočte ke kroku 3.</span><span class="sxs-lookup"><span data-stu-id="33af4-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="33af4-114">Spusťte příkaz instalace:</span><span class="sxs-lookup"><span data-stu-id="33af4-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="33af4-115">Všechny operace, které jsou k dispozici v konzole můžete také provést s [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="33af4-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="33af4-116">Příkazy konzoly ale provoz v rámci kontextu Visual Studio a uložené projekt nebo řešení a často dosáhnout více než jejich ekvivalentní příkazy rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="33af4-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="33af4-117">Například instalaci balíčku přes konzolu přidá odkaz na projekt zatímco rozhraní příkazového řádku příkaz neexistuje.</span><span class="sxs-lookup"><span data-stu-id="33af4-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="33af4-118">Z tohoto důvodu vývojáře, kteří pracují v sadě Visual Studio obvykle dáváte přednost, pomocí konzoly nástroje rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="33af4-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="33af4-119">Mnoho konzole operací závisí na s řešením otevřít v sadě Visual Studio s názvem známé cestě.</span><span class="sxs-lookup"><span data-stu-id="33af4-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="33af4-120">Pokud máte neuložené řešení nebo žádné řešení, zobrazí se chyba, "řešení není otevřené nebo není uložené.</span><span class="sxs-lookup"><span data-stu-id="33af4-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="33af4-121">Ujistěte se, že máte řešení otevřené a uložené."</span><span class="sxs-lookup"><span data-stu-id="33af4-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="33af4-122">To znamená, že konzole nemůže určit složku řešení.</span><span class="sxs-lookup"><span data-stu-id="33af4-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="33af4-123">Ukládání neuložené řešení, nebo vytvoření a uložení řešení, pokud nemáte otevřete, by měl opravte chybu.</span><span class="sxs-lookup"><span data-stu-id="33af4-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="33af4-124">Otevření konzoly a ovládací prvky konzoly</span><span class="sxs-lookup"><span data-stu-id="33af4-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="33af4-125">Otevřete konzolu v sadě Visual Studio pomocí **nástroje > Správce balíčků NuGet > Konzola správce balíčků** příkaz.</span><span class="sxs-lookup"><span data-stu-id="33af4-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="33af4-126">Konzole je okno sady Visual Studio, které mohou být uspořádány a umístěný, ale chcete (viz [přizpůsobení rozložení oken v sadě Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="33af4-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="33af4-127">Ve výchozím nastavení fungují příkazy konzoly pro určitý balíček zdrojem a projekt jako sada v ovládacím prvku v horní části okna:</span><span class="sxs-lookup"><span data-stu-id="33af4-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Ovládací prvky konzoly Správce balíčků pro zdroj balíčku a projectu](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="33af4-129">Vyberte jiný balíček zdroje nebo projektu změní tyto výchozí hodnoty pro následné příkazy.</span><span class="sxs-lookup"><span data-stu-id="33af4-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="33af4-130">Způsobem lze potlačit tato nastavení beze změny výchozí hodnoty, většina příkazů podporují `-Source` a `-ProjectName` možnosti.</span><span class="sxs-lookup"><span data-stu-id="33af4-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="33af4-131">Chcete-li spravovat zdroje balíčků, vyberte ikonu zařízení.</span><span class="sxs-lookup"><span data-stu-id="33af4-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="33af4-132">Toto je zástupce **nástroje > Možnosti > Správce balíčků NuGet > zdroje balíčků** dialogové okno jak je popsáno na [uživatelského rozhraní Správce balíčků](Package-Manager-UI.md#package-sources) stránky.</span><span class="sxs-lookup"><span data-stu-id="33af4-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="33af4-133">Ovládací prvek napravo od modulu pro výběr projektu vymaže obsah v konzole:</span><span class="sxs-lookup"><span data-stu-id="33af4-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Nastavení konzoly Správce balíčků a zrušte ovládací prvky](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="33af4-135">Úplně vpravo tlačítko přerušení dlouho běžící příkaz.</span><span class="sxs-lookup"><span data-stu-id="33af4-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="33af4-136">Například běžet `Get-Package -ListAvailable -PageSize 500` obsahuje seznam balíčků horní 500 na výchozí zdroj (například nuget.org), který může trvat několik minut.</span><span class="sxs-lookup"><span data-stu-id="33af4-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Konzola správce balíčků zastavení řízení](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="33af4-138">Instalace balíčku</span><span class="sxs-lookup"><span data-stu-id="33af4-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="33af4-139">V tématu [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="33af4-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="33af4-140">Instalaci balíčku, provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="33af4-140">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="33af4-141">Zobrazí v okně konzoly se smlouvou předpokládané příslušných licenčních podmínek.</span><span class="sxs-lookup"><span data-stu-id="33af4-141">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="33af4-142">Pokud nesouhlasíte s podmínkami, byste měli okamžitě odinstalovat balíček.</span><span class="sxs-lookup"><span data-stu-id="33af4-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="33af4-143">Přidá odkaz na projekt v jakémkoli formát reference je používán.</span><span class="sxs-lookup"><span data-stu-id="33af4-143">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="33af4-144">Odkazy se následně zobrazí v Průzkumníku řešení a formátu souboru použít referenční.</span><span class="sxs-lookup"><span data-stu-id="33af4-144">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="33af4-145">Upozorňujeme však, že s PackageReference, je nutné uložit projektu a podívejte se změny v souboru projektu přímo.</span><span class="sxs-lookup"><span data-stu-id="33af4-145">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="33af4-146">Ukládá do mezipaměti balíčku:</span><span class="sxs-lookup"><span data-stu-id="33af4-146">Caches the package:</span></span>
  - <span data-ttu-id="33af4-147">PackageReference: balíčku je uloží do mezipaměti na `%USERPROFILE%\.nuget\packages` a zámek souboru tj `project.assets.json` se aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="33af4-147">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
  - <span data-ttu-id="33af4-148">`packages.config`: vytvoří `packages` složky v kořenové řešení a zkopíruje soubory balíčku do podsložky v něm.</span><span class="sxs-lookup"><span data-stu-id="33af4-148">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="33af4-149">`package.config` Aktualizaci souboru.</span><span class="sxs-lookup"><span data-stu-id="33af4-149">The `package.config` file is updated.</span></span>
- <span data-ttu-id="33af4-150">Aktualizace `app.config` nebo `web.config` Pokud balíček používá [zdroje a konfiguračním souboru transformace](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="33af4-150">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="33af4-151">Nainstaluje všechny závislosti, pokud ještě není přítomný v projektu.</span><span class="sxs-lookup"><span data-stu-id="33af4-151">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="33af4-152">To může aktualizovat verze balíčku v procesu, jak je popsáno v [řešení závislostí](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="33af4-152">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="33af4-153">Zobrazí soubor readme balíčku, pokud je k dispozici, v okně Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33af4-153">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="33af4-154">Jednou z výhod primární instalace balíčků s `Install-Package` příkaz v konzole je, který přidá odkaz na projekt stejně, jako by se použít uživatelské rozhraní Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="33af4-154">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="33af4-155">Naopak `nuget install` rozhraní příkazového řádku příkaz pouze stáhne balíček a automaticky nepřidá odkaz.</span><span class="sxs-lookup"><span data-stu-id="33af4-155">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="33af4-156">Odinstalace balíčku</span><span class="sxs-lookup"><span data-stu-id="33af4-156">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="33af4-157">V tématu [odinstalovat balíček](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="33af4-157">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="33af4-158">Použití [Get-Package](../tools/ps-ref-get-package.md) zobrazíte všechny balíčky, které jsou aktuálně nainstalované ve výchozím projektu, pokud potřebujete najít identifikátor.</span><span class="sxs-lookup"><span data-stu-id="33af4-158">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="33af4-159">Odinstalace balíčku, provede následující akce:</span><span class="sxs-lookup"><span data-stu-id="33af4-159">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="33af4-160">Odebere odkazy na balíček z projektu (a jakýkoli formát odkaz se používá).</span><span class="sxs-lookup"><span data-stu-id="33af4-160">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="33af4-161">Odkazy se nebude zobrazovat v Průzkumníku řešení.</span><span class="sxs-lookup"><span data-stu-id="33af4-161">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="33af4-162">(Možná budete muset znovu sestavte projekt nevidíte odebrán z **Bin** složky.)</span><span class="sxs-lookup"><span data-stu-id="33af4-162">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="33af4-163">Vrátí zpět změny provedené v `app.config` nebo `web.config` Pokud byl balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="33af4-163">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="33af4-164">Pokud žádné zbývající balíčky pomocí těchto závislostí odebere dříve nainstalovali závislosti.</span><span class="sxs-lookup"><span data-stu-id="33af4-164">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="33af4-165">Jako `Install-Package`, `Uninstall-Package` příkaz má výhodu Správa odkazů v projektu, na rozdíl od `nuget uninstall` rozhraní příkazového řádku příkaz.</span><span class="sxs-lookup"><span data-stu-id="33af4-165">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="33af4-166">Aktualizace balíčku</span><span class="sxs-lookup"><span data-stu-id="33af4-166">Updating a package</span></span>

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

<span data-ttu-id="33af4-167">V tématu [Get-Package](../tools/ps-ref-get-package.md) a [balíčku aktualizace](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="33af4-167">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="33af4-168">Hledání balíčku</span><span class="sxs-lookup"><span data-stu-id="33af4-168">Finding a package</span></span>

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

<span data-ttu-id="33af4-169">V tématu [najít balíček](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="33af4-169">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="33af4-170">V sadě Visual Studio 2013 a starší, použijte [Get-Package](../tools/ps-ref-get-package.md) místo.</span><span class="sxs-lookup"><span data-stu-id="33af4-170">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="33af4-171">Dostupnost konzoly nástroje</span><span class="sxs-lookup"><span data-stu-id="33af4-171">Availability of the console</span></span>

<span data-ttu-id="33af4-172">V aplikaci Visual Studio 2017 NuGet a Správce balíčků NuGet jsou automaticky nainstalovány po výběru některé. Úlohy související s NET; Můžete také nainstalovat ji jednotlivě kontrolou **jednotlivých součástí > Code nástroje > Správce balíčků NuGet** možnosti v instalačním programu Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="33af4-172">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="33af4-173">Zkontrolujte také, pokud jste chybí Správce balíčků NuGet v sadě Visual Studio 2015 a starší, **nástroje > rozšíření a aktualizace...**  a vyhledejte rozšíření Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="33af4-173">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="33af4-174">Pokud nemůžete použít instalační program rozšíření v sadě Visual Studio, si můžete stáhnout rozšíření přímo z [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="33af4-174">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="33af4-175">Konzola správce balíčků není v současné době dostupné pomocí sady Visual Studio for Mac.</span><span class="sxs-lookup"><span data-stu-id="33af4-175">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="33af4-176">Ekvivalentní příkazy, ale jsou k dispozici prostřednictvím [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="33af4-176">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="33af4-177">Visual Studio pro Mac nemá uživatelského rozhraní pro správu balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="33af4-177">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="33af4-178">V tématu [balíček včetně NuGet ve vašem projektu](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="33af4-178">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="33af4-179">Konzola správce balíčků není součástí Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="33af4-179">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="33af4-180">Rozšíření konzole Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="33af4-180">Extending the Package Manager Console</span></span>

<span data-ttu-id="33af4-181">Některé balíčky nainstalujte nové příkazy pro konzolu.</span><span class="sxs-lookup"><span data-stu-id="33af4-181">Some packages install new commands for the console.</span></span> <span data-ttu-id="33af4-182">Například `MvcScaffolding` vytvoří příkazy, jako je `Scaffold` vidíte níže, který generuje kontrolery a zobrazení ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="33af4-182">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Instalace a použití MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="33af4-184">Nastavení profilu NuGet PowerShell</span><span class="sxs-lookup"><span data-stu-id="33af4-184">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="33af4-185">Profil prostředí PowerShell umožňuje zpřístupnit běžně používané příkazy bez ohledu na pomocí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33af4-185">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="33af4-186">NuGet podporuje NuGet konkrétní profil většinou nacházejí v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="33af4-186">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="33af4-187">Chcete-li vyhledat profil, zadejte `$profile` v konzole:</span><span class="sxs-lookup"><span data-stu-id="33af4-187">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="33af4-188">Další podrobnosti najdete v části [profily Windows PowerShell](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="33af4-188">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="33af4-189">Pomocí nuget.exe rozhraní příkazového řádku v konzole</span><span class="sxs-lookup"><span data-stu-id="33af4-189">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="33af4-190">Chcete-li [ `nuget.exe` rozhraní příkazového řádku](nuget-exe-CLI-Reference.md) k dispozici v konzoli správce balíčků nainstalujte [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) balíček z konzoly:</span><span class="sxs-lookup"><span data-stu-id="33af4-190">To make the [`nuget.exe` CLI](nuget-exe-CLI-Reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
