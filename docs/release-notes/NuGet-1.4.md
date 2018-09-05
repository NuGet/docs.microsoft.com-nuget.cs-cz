---
title: Zpráva k vydání verze 1.4 NuGet
description: Zpráva k vydání verze pro NuGet 1.4, včetně známých problémů, opravy chyb, nové funkce a chcete.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550628"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="2926d-103">Zpráva k vydání verze 1.4 NuGet</span><span class="sxs-lookup"><span data-stu-id="2926d-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="2926d-104">[Zpráva k vydání verze NuGet 1.3](../release-notes/nuget-1.3.md) | [zpráva k vydání verze NuGet 1.5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="2926d-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="2926d-105">NuGet 1.4 byla vydána 17 dne 2011.</span><span class="sxs-lookup"><span data-stu-id="2926d-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="2926d-106">Funkce</span><span class="sxs-lookup"><span data-stu-id="2926d-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="2926d-107">Vylepšení aktualizace balíčků</span><span class="sxs-lookup"><span data-stu-id="2926d-107">Update-Package improvements</span></span>
<span data-ttu-id="2926d-108">NuGet 1.4 přináší spoustu vylepšení příkazu Update-Package to usnadňuje zachovat balíčky na stejnou verzi více projektů v řešení.</span><span class="sxs-lookup"><span data-stu-id="2926d-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="2926d-109">Například při upgradu na nejnovější verzi balíčku, je velmi běžné vyžadovat všechny projekty se tento balíček aktualizovat tak, aby stejné verision.</span><span class="sxs-lookup"><span data-stu-id="2926d-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="2926d-110">`Update-Package` Příkaz nyní usnadňuje:</span><span class="sxs-lookup"><span data-stu-id="2926d-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="2926d-111">Aktualizovat všechny balíčky v jednom projektu</span><span class="sxs-lookup"><span data-stu-id="2926d-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="2926d-112">Aktualizovat balíček ve všech projektech</span><span class="sxs-lookup"><span data-stu-id="2926d-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="2926d-113">Aktualizovat všechny balíčky ve všech projektech</span><span class="sxs-lookup"><span data-stu-id="2926d-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="2926d-114">Provádění "bezpečné" aktualizace na všechny balíčky</span><span class="sxs-lookup"><span data-stu-id="2926d-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="2926d-115">`-Safe` Příznak omezí upgrade na pouze verze pomocí stejné verze komponenty hlavní a podverze.</span><span class="sxs-lookup"><span data-stu-id="2926d-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="2926d-116">Pokud je nainstalována verze 1.0.0 balíčku a verze 1.0.1, 1.0.2 a 1.1, jsou k dispozici v informačním kanálu, například `-Safe` příznak je balíček aktualizován na 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="2926d-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="2926d-117">Bez upgradu `-Safe` příznak by balíček upgradu na nejnovější verze 1.1.</span><span class="sxs-lookup"><span data-stu-id="2926d-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="2926d-118">Správa balíčků na úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="2926d-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="2926d-119">Před NuGet 1.4 instalaci balíčku do více projektů byla náročná, pomocí dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="2926d-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="2926d-120">To nutné, spouští se dialogové okno jednou za projektu.</span><span class="sxs-lookup"><span data-stu-id="2926d-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="2926d-121">NuGet 1.4 přidává podporu pro instalace/odinstalace/aktualizuje balíčky v několika projektech současně.</span><span class="sxs-lookup"><span data-stu-id="2926d-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="2926d-122">Jednoduše spustit tak, že kliknete pravým tlačítkem řešení a vyberete **spravovat balíčky NuGet** nabídky.</span><span class="sxs-lookup"><span data-stu-id="2926d-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Dialogové okno řešení úroveň spravovat balíčky NuGet](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="2926d-124">Všimněte si, že v záhlaví dialogového okna, název řešení se zobrazí, nikoli název projektu.</span><span class="sxs-lookup"><span data-stu-id="2926d-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="2926d-125">Operace balíčků teď poskytují seznam zaškrtávacích políček seznam projektů, které se má použít operaci.</span><span class="sxs-lookup"><span data-stu-id="2926d-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Správa výběr projektu balíčky NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="2926d-127">Další podrobnosti naleznete v tématu o [Správa balíčků pro řešení](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="2926d-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="2926d-128">Omezení upgraduje povolené verze</span><span class="sxs-lookup"><span data-stu-id="2926d-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="2926d-129">Ve výchozím nastavení při spuštění `Update-Package` příkaz balíčku (nebo aktualizaci balíčku pomocí dialogového okna), se aktualizují na nejnovější verzi v informačním kanálu.</span><span class="sxs-lookup"><span data-stu-id="2926d-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="2926d-130">S novou podporu pro všechny balíčky aktualizací můžou nastat případy, ve kterých chcete zamknout balíček na rozsah konkrétní verze.</span><span class="sxs-lookup"><span data-stu-id="2926d-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="2926d-131">Například můžete vědět předem, že vaše aplikace bude fungovat jenom s 2.\* verze balíčku, ale ne 3.0 a novějších.</span><span class="sxs-lookup"><span data-stu-id="2926d-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="2926d-132">Aby nedošlo k neúmyslné balíček aktualizace na 3, NuGet 1.4 přidává podporu pro omezení rozsahu verzí, které balíčky je možné upgradovat na tak, že ručně upravíte `packages.config` souborů pomocí nové `allowedVersions` atribut.</span><span class="sxs-lookup"><span data-stu-id="2926d-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="2926d-133">Například následující příklad ukazuje, jak uzamknout `SomePackage` 2.0-3.0 (výhradní) v rozsahu balíčku verze.</span><span class="sxs-lookup"><span data-stu-id="2926d-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="2926d-134">`allowedVersions` Atribut je možné zadat hodnoty pomocí [formát rozsahu verze](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="2926d-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="2926d-135">Mějte na paměti, že 1.4, uzamčení balíček na rozsah konkrétní verze musí být ručně upravit.</span><span class="sxs-lookup"><span data-stu-id="2926d-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="2926d-136">1.5 NuGet plánujeme přidat podporu pro uvedení tento rozsah prostřednictvím `Install-Package` příkazu.</span><span class="sxs-lookup"><span data-stu-id="2926d-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="2926d-137">Balíček Vizualizéru</span><span class="sxs-lookup"><span data-stu-id="2926d-137">Package Visualizer</span></span>
<span data-ttu-id="2926d-138">Nový balíček vizualizéru, spustí prostřednictvím **nástroje** -> **Správce balíčků knihoven** -> **balíčku Vizualizéru** klikněte na možnost vám umožní snadno Vizualizujte všechny projekty a závislosti jejich balíčků v rámci řešení.</span><span class="sxs-lookup"><span data-stu-id="2926d-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="2926d-139">_**Důležitá poznámka:** tato funkce využívá výhod podpory DGML v sadě Visual Studio. Vytvoření vizualizace je podporována pouze v sadě Visual Studio Ultimate. Zobrazení diagramu DGML je podporována pouze v aplikaci Visual Studio Premium nebo vyšší._</span><span class="sxs-lookup"><span data-stu-id="2926d-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Balíček Vizualizéru](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="2926d-141">Kontrola automatické aktualizace v dialogovém okně NuGet</span><span class="sxs-lookup"><span data-stu-id="2926d-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="2926d-142">Některé verze NuGet zavádět nové funkce vyjádřena `.nuspec` souborů, které nebudou srozumitelné pro starší verze NuGet dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="2926d-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="2926d-143">Jedním z příkladů je zavedení 1.4 NuGet pro [zadání sestavení rozhraní](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="2926d-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="2926d-144">Z toho důvodu je důležité, abyste používali nejnovější verzi balíčku nuget k zajištění, že může používat balíčky, které využívají nejnovější funkce.</span><span class="sxs-lookup"><span data-stu-id="2926d-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="2926d-145">Provádění aktualizací NuGet viditelnější, dialogové okno NuGet obsahuje logiku a zvýraznit, když je dostupná novější verze.</span><span class="sxs-lookup"><span data-stu-id="2926d-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="2926d-146">_**Poznámka:**: Kontrola se provádí pouze v případě **Online** kartu byla vybrána v aktuální relaci._</span><span class="sxs-lookup"><span data-stu-id="2926d-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Spravovat balíčky NuGet dialogové okno s dostupná nová verze](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="2926d-148">Chcete-li vypnout automatickou kontrolu aktualizací, přejděte do dialogového okna nastavení NuGet a zrušte zaškrtnutí políčka **automaticky vyhledávat aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="2926d-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Nastavení NuGet](./media/nuget-settings.png)

<span data-ttu-id="2926d-150">Tuto funkci ve skutečnosti byl přidán NuGet 1.3, ale nebude viditelné, samozřejmě, až do aktualizace 1.3, jako je NuGet 1.4, byl k dispozici.</span><span class="sxs-lookup"><span data-stu-id="2926d-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="2926d-151">Vylepšení dialogového okna Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="2926d-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="2926d-152">**Názvy nabídek vylepšené**: spuštění dialogového okna Možnosti nabídky byly přejmenovány nejasnostem.</span><span class="sxs-lookup"><span data-stu-id="2926d-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="2926d-153">Možnost nabídky je nyní **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2926d-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="2926d-154">**V podokně podrobností se zobrazí nejnovější data aktualizací**: Zobrazí se dialogové okno NuGet datum poslední aktualizace v podokně podrobností pro balíček při **Online** nebo **aktualizuje** vybraná karta.</span><span class="sxs-lookup"><span data-stu-id="2926d-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="2926d-155">**Seznam značek zobrazí**: Nuget dialogové okno zobrazí značky.</span><span class="sxs-lookup"><span data-stu-id="2926d-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="2926d-156">Vylepšení prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="2926d-156">Powershell Improvements</span></span>
* <span data-ttu-id="2926d-157">**Podepsané skripty prostředí PowerShell**: NuGet zahrnuje podepsaných skriptů prostředí Powershell umožňuje využití v prostředích s více omezující.</span><span class="sxs-lookup"><span data-stu-id="2926d-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="2926d-158">**Dotazování podporu**: konzoly Správce balíčků teď podporuje dotazování přes `$host.ui.Prompt` a `$host.ui.PromptForChoice` příkazy.</span><span class="sxs-lookup"><span data-stu-id="2926d-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="2926d-159">**Balíček názvy zdrojů**: poskytnutí název zdroje balíčku je podporováno, pokud zadáte zdroj balíčku pomocí `-Source` příznak.</span><span class="sxs-lookup"><span data-stu-id="2926d-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="2926d-160">vylepšení příkazového řádku nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2926d-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="2926d-161">**Vlastní příkazy pro balíčky NuGet**: nuget.exe je rozšiřitelný prostřednictvím vlastní příkazy pomocí MEF.</span><span class="sxs-lookup"><span data-stu-id="2926d-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="2926d-162">**Jednodušší pracovního postupu pro vytváření balíčků symbolů**: `-Symbols` příznak lze použít k vytvoření balíčku symbolů pouze zahrnutím zdroj struktury složek normální založené na konvenci a `.pdb` soubory ve složce.</span><span class="sxs-lookup"><span data-stu-id="2926d-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="2926d-163">**Zadání více zdrojů**: `NuGet install` příkaz podporuje zadání více zdrojů pomocí středníkem jako oddělovač nebo zadáním `-Source` více než jednou.</span><span class="sxs-lookup"><span data-stu-id="2926d-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="2926d-164">**Podpora proxy serveru ověřování**: NuGet 1.4 přidává podporu pro vás vyzve k zadání přihlašovacích údajů uživatele při použití NuGet za proxy serverem, který vyžaduje ověření.</span><span class="sxs-lookup"><span data-stu-id="2926d-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="2926d-165">**nuget.exe aktualizovat zásadní změna**: `-Self` příznak je nyní nutné zahrnout nuget.exe aktualizovalo samo.</span><span class="sxs-lookup"><span data-stu-id="2926d-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="2926d-166">`nuget.exe Update` nyní přijímá cesty k `packages.config` soubor a pokusí se aktualizace balíčků.</span><span class="sxs-lookup"><span data-stu-id="2926d-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="2926d-167">Všimněte si, že tato aktualizace je omezený v tom, že se tak nestane: ** aktualizaci, přidání, odebrání obsahu v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="2926d-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="2926d-168">** Spouštění Powershellových skriptů v rámci balíčku.</span><span class="sxs-lookup"><span data-stu-id="2926d-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="2926d-169">Podpora serveru NuGet pro vkládání balíčků pomocí nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2926d-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="2926d-170">NuGet obsahuje jednoduchý způsob, jak hostitele [jednoduché webové na základě úložiště NuGet](../hosting-packages/nuget-server.md) prostřednictvím `NuGet.Server` balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="2926d-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="2926d-171">S NuGet 1.4 jednoduchý server podporuje vkládání a odstraňování balíčků s využitím nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="2926d-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="2926d-172">Nejnovější verzi `NuGet.Server` přidá nový `appSetting`s názvem `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="2926d-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="2926d-173">Když tento parametr vynechán nebo je prázdné, nahráním balíčky do informačního kanálu se vypne.</span><span class="sxs-lookup"><span data-stu-id="2926d-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="2926d-174">Nastavení apiKey na hodnotu (v ideálním případě silné heslo) umožňuje vložit balíčky pomocí nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="2926d-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="2926d-175">Podpora pro Windows Phone Tools Mango Edition</span><span class="sxs-lookup"><span data-stu-id="2926d-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="2926d-176">NuGet se teď podporuje ve verzi Release candidate nástroje Windows Phone pro Mango.</span><span class="sxs-lookup"><span data-stu-id="2926d-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="2926d-177">V současné době nástroje Windows Phone nemá podporu pro správce rozšíření sady Visual Studio, proto k instalaci nástroje NuGet pro Windows Phone, budete muset stáhnout a spustit ručně VSIX.</span><span class="sxs-lookup"><span data-stu-id="2926d-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="2926d-178">Odinstalace nástroje NuGet pro Windows Phone, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="2926d-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="2926d-179">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="2926d-179">Bug Fixes</span></span>
<span data-ttu-id="2926d-180">NuGet 1.4 bylo celkem 88 pracovní položky opraveno.</span><span class="sxs-lookup"><span data-stu-id="2926d-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="2926d-181">71 z nich byly označeny jako chyby.</span><span class="sxs-lookup"><span data-stu-id="2926d-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="2926d-182">Úplný seznam pracovních položek opravených NuGet 1.4 prosím zobrazení [NuGet sledování problémů pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="2926d-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="2926d-183">Opravy chyb za zmínku:</span><span class="sxs-lookup"><span data-stu-id="2926d-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="2926d-184">[Problém 603](http://nuget.codeplex.com/workitem/603): závislosti balíčků v různých úložištích řeší správně při zadávání zdroj konkrétního balíčku.</span><span class="sxs-lookup"><span data-stu-id="2926d-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="2926d-185">[Problém 1036](http://nuget.codeplex.com/workitem/1036): přidání `NuGet Pack SomeProject.csproj` na událost po sestavení už způsobuje nekonečnou smyčku.</span><span class="sxs-lookup"><span data-stu-id="2926d-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="2926d-186">[Problém 961](http://nuget.codeplex.com/workitem/961): `-Source` příznak podporuje relativní cesty.</span><span class="sxs-lookup"><span data-stu-id="2926d-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="2926d-187">Aktualizace NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="2926d-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="2926d-188">Krátce po vydání NuGet 1.4 našli jsme několik problémů, které byly potřeba opravit.</span><span class="sxs-lookup"><span data-stu-id="2926d-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="2926d-189">Počet konkrétní verzi této aktualizace 1.4 je 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="2926d-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="2926d-190">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="2926d-190">Bug Fixes</span></span>
* <span data-ttu-id="2926d-191">[Problém 1220](http://nuget.codeplex.com/workitem/1220): Update-Package neprovede `install.ps1` / `uninstall.ps1` ve všech projektech po více než jeden projekt</span><span class="sxs-lookup"><span data-stu-id="2926d-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="2926d-192">[Problém 1156](http://nuget.codeplex.com/workitem/1156): konzole Správce balíčků zablokované W2K3/XP (Pokud není nainstalovaný Powershell 2)</span><span class="sxs-lookup"><span data-stu-id="2926d-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
