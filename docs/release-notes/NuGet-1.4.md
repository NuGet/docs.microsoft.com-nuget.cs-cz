---
title: Zpráva k vydání verze NuGet 1,4
description: Poznámky k verzi pro NuGet 1,4, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230704"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="31b7d-103">Zpráva k vydání verze NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="31b7d-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="31b7d-104">[Poznámky k verzi nuget 1,3](../release-notes/nuget-1.3.md) | zpráva k [vydání verze NuGet 1,5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="31b7d-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="31b7d-105">NuGet 1,4 byl vydán 17. června 2011.</span><span class="sxs-lookup"><span data-stu-id="31b7d-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="31b7d-106">Funkce</span><span class="sxs-lookup"><span data-stu-id="31b7d-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="31b7d-107">Aktualizace – vylepšení balíčků</span><span class="sxs-lookup"><span data-stu-id="31b7d-107">Update-Package improvements</span></span>
<span data-ttu-id="31b7d-108">NuGet 1,4 představuje mnoho vylepšení příkazu Update-Package, což usnadňuje udržování balíčků ve stejné verzi napříč více projekty v řešení.</span><span class="sxs-lookup"><span data-stu-id="31b7d-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="31b7d-109">Například při upgradu balíčku na nejnovější verzi je velmi běžné, aby bylo možné všechny projekty s tímto balíčkem nainstalovat na stejný verision.</span><span class="sxs-lookup"><span data-stu-id="31b7d-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="31b7d-110">Příkaz `Update-Package` teď usnadňuje:</span><span class="sxs-lookup"><span data-stu-id="31b7d-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="31b7d-111">Aktualizovat všechny balíčky v jednom projektu</span><span class="sxs-lookup"><span data-stu-id="31b7d-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="31b7d-112">Aktualizace balíčku ve všech projektech</span><span class="sxs-lookup"><span data-stu-id="31b7d-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="31b7d-113">Aktualizovat všechny balíčky ve všech projektech</span><span class="sxs-lookup"><span data-stu-id="31b7d-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="31b7d-114">Proveďte bezpečnou aktualizaci u všech balíčků.</span><span class="sxs-lookup"><span data-stu-id="31b7d-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="31b7d-115">Příznak `-Safe` omezuje upgrady pouze na verze se stejnou částí hlavní a dílčí verze.</span><span class="sxs-lookup"><span data-stu-id="31b7d-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="31b7d-116">Pokud je například 1.0.0 verze balíčku nainstalován a verze 1.0.1, 1.0.2 a 1,1 jsou k dispozici v informačním kanálu, příznak `-Safe` aktualizuje balíček na 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="31b7d-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="31b7d-117">Upgrade bez příznaku `-Safe` by balíček upgradoval na nejnovější verzi 1,1.</span><span class="sxs-lookup"><span data-stu-id="31b7d-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="31b7d-118">Správa balíčků na úrovni řešení</span><span class="sxs-lookup"><span data-stu-id="31b7d-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="31b7d-119">Před balíčkem NuGet 1,4 se instalace balíčku do více projektů nenáročných pomocí dialogového okna.</span><span class="sxs-lookup"><span data-stu-id="31b7d-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="31b7d-120">Je nutné spustit dialog jednou pro každý projekt.</span><span class="sxs-lookup"><span data-stu-id="31b7d-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="31b7d-121">NuGet 1,4 přidává podporu pro instalaci/odinstalaci/aktualizaci balíčků ve více projektech současně.</span><span class="sxs-lookup"><span data-stu-id="31b7d-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="31b7d-122">Stačí spustit kliknutím pravým tlačítkem myši na řešení a výběrem možnosti **Spravovat balíčky NuGet** .</span><span class="sxs-lookup"><span data-stu-id="31b7d-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Dialogové okno Správa balíčků NuGet na úrovni řešení](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="31b7d-124">Všimněte si, že v záhlaví dialogového okna se zobrazí název řešení, nikoli název projektu.</span><span class="sxs-lookup"><span data-stu-id="31b7d-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="31b7d-125">Operace balíčku teď poskytují seznam zaškrtávacích políček se seznamem projektů, na které by se měla operace vztahovat.</span><span class="sxs-lookup"><span data-stu-id="31b7d-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Spravovat výběr projektu balíčků NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="31b7d-127">Další podrobnosti najdete v tématu [Správa balíčků pro řešení](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="31b7d-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="31b7d-128">Omezení upgradu na povolené verze</span><span class="sxs-lookup"><span data-stu-id="31b7d-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="31b7d-129">Ve výchozím nastavení se při spuštění příkazu `Update-Package` na balíčku (nebo aktualizace balíčku pomocí dialogového okna) aktualizuje na nejnovější verzi v informačním kanálu.</span><span class="sxs-lookup"><span data-stu-id="31b7d-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="31b7d-130">Díky nové podpoře aktualizace všech balíčků můžou nastat případy, kdy chcete balíček uzamknout do konkrétního rozsahu verzí.</span><span class="sxs-lookup"><span data-stu-id="31b7d-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="31b7d-131">Můžete například předem určit, že aplikace bude fungovat pouze s verzí 2. \* balíčku, ale ne 3,0 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="31b7d-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="31b7d-132">Aby nedocházelo k nechtěné aktualizaci balíčku na 3, NuGet 1,4 přidá podporu pro omezení rozsahu verzí, na které lze balíčky upgradovat, a to ruční úpravou souboru `packages.config` pomocí nového atributu `allowedVersions`.</span><span class="sxs-lookup"><span data-stu-id="31b7d-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="31b7d-133">Například následující příklad ukazuje, jak uzamknout `SomePackage` balíčku rozsah verze 2,0-3,0 (exkluzivní).</span><span class="sxs-lookup"><span data-stu-id="31b7d-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="31b7d-134">Atribut `allowedVersions` akceptuje hodnoty pomocí [formátu rozsahu verzí](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="31b7d-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="31b7d-135">Všimněte si, že v 1,4 musí být uzamknutí balíčku do konkrétního rozsahu verzí ručně upravováno.</span><span class="sxs-lookup"><span data-stu-id="31b7d-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="31b7d-136">V NuGet 1,5 plánujeme přidat podporu pro vložení tohoto rozsahu pomocí příkazu `Install-Package`.</span><span class="sxs-lookup"><span data-stu-id="31b7d-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="31b7d-137">Vizualizér balíčků</span><span class="sxs-lookup"><span data-stu-id="31b7d-137">Package Visualizer</span></span>
<span data-ttu-id="31b7d-138">Nový Vizualizér balíčků, který se spouští prostřednictvím **nástroje** -> **knihovny správce balíčků** -> možnosti nabídky **Vizualizér balíčků** , umožňuje snadno vizualizovat všechny projekty a jejich závislosti balíčku v rámci řešení.</span><span class="sxs-lookup"><span data-stu-id="31b7d-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="31b7d-139">_**Důležitá Poznámka:** Tato funkce využívá podporu DGML v aplikaci Visual Studio. Vytváření vizualizace se podporuje jenom v Visual Studio Ultimate. Zobrazení diagramu DGML je podporováno pouze v Visual Studio Premium nebo vyšších._</span><span class="sxs-lookup"><span data-stu-id="31b7d-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Vizualizér balíčků](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="31b7d-141">Automatická aktualizace aktualizací pro dialog NuGet</span><span class="sxs-lookup"><span data-stu-id="31b7d-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="31b7d-142">Některé verze NuGet představují nové funkce vyjádřené pomocí `.nuspec` souboru, které nerozumí starší verze dialogového okna NuGet.</span><span class="sxs-lookup"><span data-stu-id="31b7d-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="31b7d-143">Jedním z příkladů je Úvod do NuGet 1,4 pro [určení sestavení rozhraní](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="31b7d-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="31b7d-144">Z tohoto důvodu je důležité použít nejnovější verzi nástroje NuGet, abyste měli jistotu, že budete moci používat balíčky s využitím nejnovějších funkcí.</span><span class="sxs-lookup"><span data-stu-id="31b7d-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="31b7d-145">Aby se aktualizace NuGet zobrazovaly podrobněji, obsahuje dialog NuGet logiku, která zvýrazní, kdy je k dispozici novější verze.</span><span class="sxs-lookup"><span data-stu-id="31b7d-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="31b7d-146">_**Poznámka**: Tato možnost se provádí jenom v případě, že se v aktuální relaci vybrala karta **online** ._</span><span class="sxs-lookup"><span data-stu-id="31b7d-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Dialog spravovat balíčky NuGet s dostupnou novou verzí](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="31b7d-148">Pokud chcete vypnout automatické vyhledávání aktualizací, otevřete dialogové okno nastavení NuGet a zrušte zaškrtnutí políčka **automaticky zjišťovat aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="31b7d-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Nastavení NuGet](./media/nuget-settings.png)

<span data-ttu-id="31b7d-150">Tato funkce se ve skutečnosti přidala do NuGet 1,3, ale nebude viditelná, dokud nebude k dispozici aktualizace 1,3, jako je třeba NuGet 1,4.</span><span class="sxs-lookup"><span data-stu-id="31b7d-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="31b7d-151">Vylepšení dialogu Správce balíčků</span><span class="sxs-lookup"><span data-stu-id="31b7d-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="31b7d-152">**Vylepšené názvy nabídek**: možnosti nabídky pro otevření dialogového okna byly pro přehlednost přejmenovány.</span><span class="sxs-lookup"><span data-stu-id="31b7d-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="31b7d-153">Možnost nabídky teď **spravuje balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="31b7d-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="31b7d-154">**Podokno podrobností zobrazuje poslední datum aktualizace**: v dialogovém okně NuGet se v podokně podrobností balíčku zobrazí datum poslední aktualizace, když je vybraná karta **online** nebo **aktualizovat** .</span><span class="sxs-lookup"><span data-stu-id="31b7d-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="31b7d-155">**Seznam zobrazených značek**: dialogové okno NuGet zobrazí značky.</span><span class="sxs-lookup"><span data-stu-id="31b7d-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="31b7d-156">Vylepšení PowerShellu</span><span class="sxs-lookup"><span data-stu-id="31b7d-156">Powershell Improvements</span></span>
* <span data-ttu-id="31b7d-157">**Podepsané skripty PowerShellu**: NuGet zahrnuje podepsané skripty PowerShellu, které umožňují použití v přísnějších prostředích.</span><span class="sxs-lookup"><span data-stu-id="31b7d-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="31b7d-158">**Dotazování na podporu**: konzola správce balíčků teď podporuje zobrazování výzev prostřednictvím příkazů `$host.ui.Prompt` a `$host.ui.PromptForChoice`.</span><span class="sxs-lookup"><span data-stu-id="31b7d-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="31b7d-159">**Zdrojové názvy balíčků**: zadání názvu zdroje balíčku se podporuje při zadání zdroje balíčku pomocí příznaku `-Source`.</span><span class="sxs-lookup"><span data-stu-id="31b7d-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="31b7d-160">vylepšení příkazového řádku NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="31b7d-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="31b7d-161">**Vlastní příkazy NuGet**: NuGet. exe je rozšiřitelný prostřednictvím vlastních příkazů využívajících MEF.</span><span class="sxs-lookup"><span data-stu-id="31b7d-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="31b7d-162">**Jednodušší pracovní postup pro vytváření balíčků symbolů**: příznak `-Symbols` lze použít pro strukturu složek založenou na běžné konvenci vytvoření balíčku symbolů pouze včetně zdrojových a `.pdb` souborů v rámci složky.</span><span class="sxs-lookup"><span data-stu-id="31b7d-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="31b7d-163">**Určení více zdrojů**: příkaz `NuGet install` podporuje zadání více zdrojů pomocí středníků jako oddělovače nebo zadáním `-Source` několikrát.</span><span class="sxs-lookup"><span data-stu-id="31b7d-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="31b7d-164">**Podpora ověřování proxy**: NuGet 1,4 přidává podporu pro výzvy k zadání přihlašovacích údajů uživatele při použití NuGet za proxy serverem, který vyžaduje ověření.</span><span class="sxs-lookup"><span data-stu-id="31b7d-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="31b7d-165">**NuGet. exe – změna konce aktualizace**: příznak `-Self` se teď vyžaduje, aby se NuGet. exe aktualizoval sám.</span><span class="sxs-lookup"><span data-stu-id="31b7d-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="31b7d-166">`nuget.exe Update` nyní používá cestu k souboru `packages.config` a pokusí se aktualizovat balíčky.</span><span class="sxs-lookup"><span data-stu-id="31b7d-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="31b7d-167">Všimněte si, že tato aktualizace je omezená, protože se nejedná o: \* \* aktualizovat, přidat a odebrat obsah v souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="31b7d-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="31b7d-168">\* \* V rámci balíčku spusťte skripty PowerShellu.</span><span class="sxs-lookup"><span data-stu-id="31b7d-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="31b7d-169">Podpora serveru NuGet pro vkládání balíčků pomocí NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="31b7d-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="31b7d-170">NuGet obsahuje jednoduchý způsob, jak hostovat [zjednodušené úložiště NuGet založené na webu](../hosting-packages/nuget-server.md) prostřednictvím balíčku `NuGet.Server` NuGet.</span><span class="sxs-lookup"><span data-stu-id="31b7d-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="31b7d-171">V případě NuGet 1,4 podporuje odlehčený Server doručování a odstraňování balíčků pomocí NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="31b7d-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="31b7d-172">Nejnovější verze `NuGet.Server` přidá nový `appSetting`s názvem `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="31b7d-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="31b7d-173">Pokud je klíč vynechán nebo je ponechán prázdný, je zablokováno vkládání balíčků do informačního kanálu.</span><span class="sxs-lookup"><span data-stu-id="31b7d-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="31b7d-174">Nastavení apiKey na hodnotu (v ideálním případě silné heslo) umožňuje zatlačte balíčky pomocí NuGet. exe.</span><span class="sxs-lookup"><span data-stu-id="31b7d-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="31b7d-175">Podpora pro edice mango Tools pro Windows Phone</span><span class="sxs-lookup"><span data-stu-id="31b7d-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="31b7d-176">V Release Candidate verze Windows Phone nástrojů pro mango se teď podporuje NuGet.</span><span class="sxs-lookup"><span data-stu-id="31b7d-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="31b7d-177">V současné době Windows Phone nástroje nepodporují Správce rozšíření sady Visual Studio, takže pokud chcete nainstalovat NuGet pro Windows Phone nástroje, budete možná muset stáhnout a spustit VSIX ručně.</span><span class="sxs-lookup"><span data-stu-id="31b7d-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="31b7d-178">Pokud chcete odinstalovat NuGet pro nástroje Windows Phone, spusťte následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="31b7d-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="31b7d-179">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="31b7d-179">Bug Fixes</span></span>
<span data-ttu-id="31b7d-180">Aktualizace NuGet 1,4 obsahovala celkem 88 pracovních položek.</span><span class="sxs-lookup"><span data-stu-id="31b7d-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="31b7d-181">71 z nich bylo označeno jako chyby.</span><span class="sxs-lookup"><span data-stu-id="31b7d-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="31b7d-182">Úplný seznam pracovních položek opravených v NuGet 1,4 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="31b7d-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="31b7d-183">Opravy chyb zaznamenaly:</span><span class="sxs-lookup"><span data-stu-id="31b7d-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="31b7d-184">[Problém 603](http://nuget.codeplex.com/workitem/603): při určení konkrétního zdroje balíčků se správně vyřeší závislosti balíčků v různých úložištích.</span><span class="sxs-lookup"><span data-stu-id="31b7d-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="31b7d-185">[Problém 1036](http://nuget.codeplex.com/workitem/1036): Přidání `NuGet Pack SomeProject.csproj` do události po sestavení už nezpůsobí nekonečnou smyčku.</span><span class="sxs-lookup"><span data-stu-id="31b7d-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="31b7d-186">[Problém 961](http://nuget.codeplex.com/workitem/961): příznak `-Source` podporuje relativní cesty.</span><span class="sxs-lookup"><span data-stu-id="31b7d-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="31b7d-187">Aktualizace NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="31b7d-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="31b7d-188">Krátce po vydání NuGet 1,4 jsme zjistili několik problémů, které byly důležité k opravě.</span><span class="sxs-lookup"><span data-stu-id="31b7d-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="31b7d-189">Konkrétní číslo verze této aktualizace na 1,4 je 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="31b7d-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="31b7d-190">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="31b7d-190">Bug Fixes</span></span>
* <span data-ttu-id="31b7d-191">[Problém 1220](http://nuget.codeplex.com/workitem/1220): aktualizace-Package se nespustí `install.ps1`/`uninstall.ps1` ve všech projektech, pokud existuje víc než jeden projekt.</span><span class="sxs-lookup"><span data-stu-id="31b7d-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="31b7d-192">[Problém 1156](http://nuget.codeplex.com/workitem/1156): zablokování konsolidace správce balíčků v w2k3/XP (když není nainstalované prostředí PowerShell 2)</span><span class="sxs-lookup"><span data-stu-id="31b7d-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
