---
title: "Poznámky k verzi NuGet 1.4 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Poznámky k verzi pro včetně známé problémy, opravy chyb, přidaných funkcí a chcete 1.4 NuGet."
keywords: "NuGet 1.4 poznámky k verzi, opravy chyb známé problémy, přidat funkce, chcete"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bc0800361551b996d958e03b9cfa3d745b78e43d
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="d4109-104">Poznámky k verzi 1,4 NuGet</span><span class="sxs-lookup"><span data-stu-id="d4109-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="d4109-105">[Poznámky k verzi NuGet 1.3](../release-notes/nuget-1.3.md) | [poznámky k verzi NuGet 1.5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="d4109-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="d4109-106">NuGet 1.4 byla vydána 17 června 2011.</span><span class="sxs-lookup"><span data-stu-id="d4109-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="d4109-107">Funkce</span><span class="sxs-lookup"><span data-stu-id="d4109-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="d4109-108">Vylepšení balíčku aktualizace</span><span class="sxs-lookup"><span data-stu-id="d4109-108">Update-Package improvements</span></span>
<span data-ttu-id="d4109-109">NuGet 1.4 představuje mnoho vylepšení příkaz balíčku aktualizace bylo snazší zachovat balíčky na stejnou verzi napříč více projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="d4109-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="d4109-110">Například při upgradu na nejnovější verzi balíčku, je velmi běžné na má všechny projekty, ve kterém je tento balíček nainstalován aktualizovat, aby stejné verision.</span><span class="sxs-lookup"><span data-stu-id="d4109-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="d4109-111">`Update-Package` Příkaz teď usnadňuje:</span><span class="sxs-lookup"><span data-stu-id="d4109-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="d4109-112">Aktualizovat všechny balíčky v jednom projektu</span><span class="sxs-lookup"><span data-stu-id="d4109-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="d4109-113">Aktualizovat balíček ve všech projektech</span><span class="sxs-lookup"><span data-stu-id="d4109-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="d4109-114">Aktualizovat všechny balíčky ve všech projektech</span><span class="sxs-lookup"><span data-stu-id="d4109-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="d4109-115">"Bezpečnou" aktualizaci provést u všech balíčků</span><span class="sxs-lookup"><span data-stu-id="d4109-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="d4109-116">`-Safe` Příznak omezí upgrade na pouze verze se stejnou hlavní a vedlejší verze součástí.</span><span class="sxs-lookup"><span data-stu-id="d4109-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="d4109-117">Například, pokud je nainstalována verze 1.0.0 balíčku a ve informačního kanálu, jsou dostupné verze 1.0.1, 1.0.2 a 1.1 `-Safe` příznak se balíček aktualizuje na verzi 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="d4109-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="d4109-118">Upgrade bez `-Safe` příznak by upgrade balíčku na nejnovější verzi 1.1.</span><span class="sxs-lookup"><span data-stu-id="d4109-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="d4109-119">Spravovat balíčky na úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="d4109-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="d4109-120">Před NuGet 1.4 instalaci balíčku do více projektů byla náročná, v dialogovém okně.</span><span class="sxs-lookup"><span data-stu-id="d4109-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="d4109-121">Je vyžadován, spouštění dialogu jednou za projektu.</span><span class="sxs-lookup"><span data-stu-id="d4109-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="d4109-122">NuGet 1.4 přidává podporu pro instalaci/odinstalaci nebo aktualizaci balíčků ve více projektech ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="d4109-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="d4109-123">Jednoduše spustit kliknutím pravým tlačítkem na řešení a výběrem **spravovat balíčky NuGet** možnost nabídky.</span><span class="sxs-lookup"><span data-stu-id="d4109-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Dialogové okno Spravovat balíčky NuGet úroveň řešení](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="d4109-125">Všimněte si, že v záhlaví okna řešení je zobrazen název, ne název projektu.</span><span class="sxs-lookup"><span data-stu-id="d4109-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="d4109-126">Balíček operations teď poskytovat seznam všech políček se seznamem projekty, které by měl použít operaci.</span><span class="sxs-lookup"><span data-stu-id="d4109-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Spravovat výběr projektu balíčky NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="d4109-128">Další podrobnosti naleznete v tématu na [Správa balíčků pro řešení](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="d4109-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="d4109-129">Chovaly upgraduje povolené verze</span><span class="sxs-lookup"><span data-stu-id="d4109-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="d4109-130">Ve výchozím nastavení při spuštění `Update-Package` na balíček (nebo aktualizaci balíčku v dialogu), ji budou aktualizovány na nejnovější verzi v informačním kanálu.</span><span class="sxs-lookup"><span data-stu-id="d4109-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="d4109-131">Nové podpory pro aktualizaci všech balíčků můžou nastat případy, ve kterých chcete zamknout balíček na konkrétní verzi rozsah.</span><span class="sxs-lookup"><span data-stu-id="d4109-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="d4109-132">Například může vědět předem, že vaše aplikace bude fungovat pouze s 2.\* verze balíčku, ale není 3.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="d4109-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="d4109-133">Prevence omylem aktualizace balíčku na 3 NuGet 1.4 přidává podporu pro omezíte rozsah verze, které balíčky lze přidat k ruční úpravě `packages.config` souboru pomocí možnosti nového `allowedVersions` atribut.</span><span class="sxs-lookup"><span data-stu-id="d4109-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="d4109-134">Například následující příklad ukazuje, jak k uzamčení `SomePackage` balíček verze rozsahu 2.0-3.0 (kromě).</span><span class="sxs-lookup"><span data-stu-id="d4109-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="d4109-135">`allowedVersions` Atribut přijímá hodnoty pomocí [verze rozsah formátu](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="d4109-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="d4109-136">Všimněte si, že v 1.4, uzamčení balíčku na konkrétní verzi rozsah musí být ručně upravovat.</span><span class="sxs-lookup"><span data-stu-id="d4109-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="d4109-137">V NuGet 1.5 plánujeme přidat podporu pro tento rozsah prostřednictvím umístění `Install-Package` příkaz.</span><span class="sxs-lookup"><span data-stu-id="d4109-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="d4109-138">Vizualizér balíčku</span><span class="sxs-lookup"><span data-stu-id="d4109-138">Package Visualizer</span></span>
<span data-ttu-id="d4109-139">Nový balíček vizualizér, spustí prostřednictvím **nástroje** -> **Správce balíčků knihoven** -> **balíček vizualizér** nabídky možnost vám umožňuje snadno zobrazit všechny projekty a závislosti jejich balíčků v rámci řešení.</span><span class="sxs-lookup"><span data-stu-id="d4109-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="d4109-140">_**Důležité upozornění:** tato funkce využívá DGML podpory v sadě Visual Studio. Vytváření vizualizace je podporována pouze v sadě nástrojů Visual Studio Ultimate. Zobrazení diagramu DGML je podporována pouze v aplikaci Visual Studio Premium nebo vyššího._</span><span class="sxs-lookup"><span data-stu-id="d4109-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Vizualizér balíčku](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="d4109-142">Kontrola automatické aktualizace pro dialogové okno NuGet</span><span class="sxs-lookup"><span data-stu-id="d4109-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="d4109-143">Některé verze NuGet zavádět nové funkce prostřednictvím vyjádřené `.nuspec` souborů, které nejsou rozumí starší verze NuGet dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="d4109-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="d4109-144">Jedním z příkladů je zavedení v 1.4 NuGet pro [zadání sestavení architektury](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="d4109-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="d4109-145">Z toho důvodu je důležité, abyste používali nejnovější verzi balíčku nuget k zajištění, že používáte balíčky s využitím nejnovějších funkcí.</span><span class="sxs-lookup"><span data-stu-id="d4109-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="d4109-146">Provádění aktualizací NuGet více viditelných, dialogové okno NuGet obsahuje logiku ke zvýraznění je k dispozici novější verze.</span><span class="sxs-lookup"><span data-stu-id="d4109-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="d4109-147">_**Poznámka:**: Kontrola se provádí pouze v případě **Online** karta byla vybrána v aktuální relaci._</span><span class="sxs-lookup"><span data-stu-id="d4109-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Spravovat balíčky NuGet dialogové okno s dostupná nová verze](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="d4109-149">Chcete-li vypnout automatickou kontrolu aktualizací, přejděte do dialogového okna nastavení NuGet a zrušte zaškrtnutí políčka **automaticky vyhledávat aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="d4109-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Nastavení NuGet](./media/nuget-settings.png)

<span data-ttu-id="d4109-151">Tato funkce je ve skutečnosti přidaná do NuGet 1.3, ale nebude viditelná, samozřejmě, dokud nebude aktualizace 1.3, jako je například NuGet 1.4, byla k dispozici.</span><span class="sxs-lookup"><span data-stu-id="d4109-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="d4109-152">Vylepšení dialogové okno Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="d4109-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="d4109-153">**Názvy nabídek vylepšené**: možnosti nabídky spustit dialogové okno pro přehlednost přejmenovaný.</span><span class="sxs-lookup"><span data-stu-id="d4109-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="d4109-154">Možnost nabídky je nyní **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d4109-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="d4109-155">**V podokně podrobností se zobrazí datum poslední aktualizace**: NuGet dialogovém okně zobrazí datum poslední aktualizace v podokně podrobností pro balíček při **Online** nebo **aktualizace** vybraná karta.</span><span class="sxs-lookup"><span data-stu-id="d4109-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="d4109-156">**Seznam značek zobrazí**: Nuget dialogovém okně zobrazí značky.</span><span class="sxs-lookup"><span data-stu-id="d4109-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="d4109-157">Vylepšení prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4109-157">Powershell Improvements</span></span>
* <span data-ttu-id="d4109-158">**Podepsané skriptů prostředí PowerShell**: NuGet zahrnuje podepsaných skriptů prostředí Powershell povolení využití v prostředí s více omezením.</span><span class="sxs-lookup"><span data-stu-id="d4109-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="d4109-159">**Výzvy podporu**: konzole Správce balíčků teď podporuje výzvy prostřednictvím `$host.ui.Prompt` a `$host.ui.PromptForChoice` příkazy.</span><span class="sxs-lookup"><span data-stu-id="d4109-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="d4109-160">**Balíček názvy zdrojů**: poskytnutí název zdroje balíčku je podporován při zadávání zdrojový balíček pomocí `-Source` příznak.</span><span class="sxs-lookup"><span data-stu-id="d4109-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="d4109-161">vylepšení nuget.exe příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="d4109-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="d4109-162">**Vlastní příkazy pro balíčky NuGet**: nuget.exe je rozšiřitelný prostřednictvím vlastní příkazy pomocí MEF.</span><span class="sxs-lookup"><span data-stu-id="d4109-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="d4109-163">**Jednodušší pracovního postupu pro vytváření balíčků symbol**: `-Symbols` příznak lze použít pro strukturu složek normální založené na konvenci vytváření balíčku symboly pouze zahrnutím zdroji a `.pdb` soubory ve složce.</span><span class="sxs-lookup"><span data-stu-id="d4109-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="d4109-164">**Zadání více zdrojů**: `NuGet install` příkaz podporuje zadání více zdrojů pomocí středníky jako oddělovač nebo zadáním `-Source` vícekrát.</span><span class="sxs-lookup"><span data-stu-id="d4109-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="d4109-165">**Podpora ověřování proxy**: NuGet 1.4 přidává podporu pro výzvu pro přihlašovací údaje uživatele při použití NuGet za proxy server, který vyžaduje ověření.</span><span class="sxs-lookup"><span data-stu-id="d4109-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="d4109-166">**nuget.exe aktualizovat nejnovější změny**: `-Self` příznak je nyní požadované pro nuget.exe aktualizovalo samo.</span><span class="sxs-lookup"><span data-stu-id="d4109-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="d4109-167">`nuget.exe Update` Teď má v cestě k `packages.config` soubor a pokusí se aktualizace balíčků.</span><span class="sxs-lookup"><span data-stu-id="d4109-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="d4109-168">Všimněte si, že tato aktualizace je omezená, v tom, že není nebude: ** aktualizovat, přidat, odebrat obsah v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="d4109-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="d4109-169">** Spouštět skripty prostředí Powershell v rámci balíčku.</span><span class="sxs-lookup"><span data-stu-id="d4109-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="d4109-170">Podpora serveru NuGet pro vkládání balíčky pomocí nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d4109-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="d4109-171">NuGet obsahuje jednoduchý způsob, jak hostitele [jednoduché webové na základě úložiště NuGet](../hosting-packages/nuget-server.md) prostřednictvím `NuGet.Server` balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="d4109-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="d4109-172">S NuGet 1.4 lightweight server podporuje vkládání a odstraňování balíčky pomocí nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="d4109-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="d4109-173">Nejnovější verzi `NuGet.Server` přidá nový `appSetting`s názvem `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="d4109-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="d4109-174">Pokud tento parametr vynechán nebo je prázdné, když zavedete balíčků informačního kanálu je zakázána.</span><span class="sxs-lookup"><span data-stu-id="d4109-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="d4109-175">Nastavení na hodnotu (v ideálním případě silné heslo) apiKey umožňuje vkládání balíčky pomocí nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="d4109-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="d4109-176">Podpora pro Windows Phone nástroje Mango Edition</span><span class="sxs-lookup"><span data-stu-id="d4109-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="d4109-177">NuGet se teď podporuje v verze release candidate nástrojů pro Windows Phone pro Mango.</span><span class="sxs-lookup"><span data-stu-id="d4109-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="d4109-178">V současné době nástroje Windows Phone nemá podporu pro správce rozšíření sady Visual Studio proto k instalaci nástroje NuGet pro Windows Phone, budete muset stáhnout a spustit VSIX ručně.</span><span class="sxs-lookup"><span data-stu-id="d4109-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="d4109-179">Odinstalace nástrojů NuGet pro Windows Phone, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="d4109-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="d4109-180">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="d4109-180">Bug Fixes</span></span>
<span data-ttu-id="d4109-181">NuGet 1.4 měl celkem 88 pracovní položky, které jsou pevné.</span><span class="sxs-lookup"><span data-stu-id="d4109-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="d4109-182">71 těchto byly označeny jako chyby.</span><span class="sxs-lookup"><span data-stu-id="d4109-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="d4109-183">Úplný seznam pracovní položky pevné v NuGet 1.4 prosím zobrazení [sledovací modul problém NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d4109-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="d4109-184">Opravy chyb vhodné poznamenat:</span><span class="sxs-lookup"><span data-stu-id="d4109-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="d4109-185">[Problém 603](http://nuget.codeplex.com/workitem/603): závislosti balíčků v různých úložišť přeloží správně při zadávání zdrojové konkrétní balíček.</span><span class="sxs-lookup"><span data-stu-id="d4109-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="d4109-186">[Problém 1036](http://nuget.codeplex.com/workitem/1036): přidání `NuGet Pack SomeProject.csproj` po už vytvořit událost způsobí, že nekonečné smyčce.</span><span class="sxs-lookup"><span data-stu-id="d4109-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="d4109-187">[Problém 961](http://nuget.codeplex.com/workitem/961): `-Source` příznak podporuje relativní cesty.</span><span class="sxs-lookup"><span data-stu-id="d4109-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="d4109-188">Aktualizace NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="d4109-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="d4109-189">Krátce po vydání NuGet 1.4 zjistili jsme několik problémů, které by bylo potřeba opravit.</span><span class="sxs-lookup"><span data-stu-id="d4109-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="d4109-190">Číslo konkrétní verze této aktualizace 1.4 je 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="d4109-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="d4109-191">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="d4109-191">Bug Fixes</span></span>
* <span data-ttu-id="d4109-192">[Problém 1220](http://nuget.codeplex.com/workitem/1220): balíček aktualizace neprovede `install.ps1` / `uninstall.ps1` ve všech projektech po více než jeden projektu</span><span class="sxs-lookup"><span data-stu-id="d4109-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="d4109-193">[Problém 1156](http://nuget.codeplex.com/workitem/1156): konzole Správce balíčků zablokované na W2K3/Windows XP (Pokud není nainstalované prostředí Powershell 2)</span><span class="sxs-lookup"><span data-stu-id="d4109-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
