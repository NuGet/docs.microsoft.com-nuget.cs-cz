---
title: Řešení potíží s obnovení balíčků NuGet v sadě Visual Studio
description: Popis běžné NuGet restore chyby v sadě Visual Studio a postupy jejich řešení.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: dacc95c557af016f535bc1b758473d7062f2ad3f
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981012"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="185f4-103">Řešení potíží s chybami obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="185f4-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="185f4-104">Tento článek se zaměřuje na běžných chyb při obnovování balíčků a kroky k jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="185f4-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="185f4-105">Kompletní informace o obnovování balíčků, najdete v části [obnovení balíčku](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="185f4-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="185f4-106">Pokud zde uvedených pokynů, nebudou fungovat, [založte prosím problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby nám více pečlivě prozkoumat váš scénář.</span><span class="sxs-lookup"><span data-stu-id="185f4-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="185f4-107">Nepoužívejte "je tato stránka užitečná?"</span><span class="sxs-lookup"><span data-stu-id="185f4-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="185f4-108">ovládací prvek, který může zobrazit na této stránce, protože se nám nedává možnost kontaktovat v souvislosti s další informace.</span><span class="sxs-lookup"><span data-stu-id="185f4-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="185f4-109">Rychlé řešení pro uživatele sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="185f4-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="185f4-110">Pokud používáte Visual Studio, nejprve následujícím způsobem povolte obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="185f4-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="185f4-111">V opačném případě pokračujte následující části.</span><span class="sxs-lookup"><span data-stu-id="185f4-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="185f4-112">Vyberte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="185f4-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="185f4-113">Obě možnosti v části Nastavení **obnovení balíčků**.</span><span class="sxs-lookup"><span data-stu-id="185f4-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="185f4-114">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="185f4-114">Select **OK**.</span></span>
1. <span data-ttu-id="185f4-115">Znovu sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="185f4-115">Build your project again.</span></span>

![Povolit obnovení balíčků NuGet v dialogovém okně nástroje/Možnosti](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="185f4-117">Tato nastavení lze také změnit v vaše `NuGet.config` souboru; najdete v článku [souhlas](#consent) oddílu.</span><span class="sxs-lookup"><span data-stu-id="185f4-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="185f4-118">Tento projekt odkazuje na balíčky NuGet, které jsou na tomto počítači chybí</span><span class="sxs-lookup"><span data-stu-id="185f4-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="185f4-119">Kompletní chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="185f4-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="185f4-120">K této chybě dojde při pokusu o vytvoření projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou v současné době nainstalované v počítači nebo v projektu.</span><span class="sxs-lookup"><span data-stu-id="185f4-120">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="185f4-121">Při použití formátu správy PackageReference chyba znamená, že balíček není nainstalována v *global-packages* složky, jak je popsáno na [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="185f4-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="185f4-122">Při použití `packages.config`, chyba znamená, že balíček není nainstalována v `packages` složku v kořenovém adresáři řešení.</span><span class="sxs-lookup"><span data-stu-id="185f4-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="185f4-123">Této situaci dochází běžně, když získal zdrojový kód projektu ze správy zdrojového kódu nebo jiného stahování.</span><span class="sxs-lookup"><span data-stu-id="185f4-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="185f4-124">Balíčky jsou obvykle vynechány ze správy zdrojového kódu nebo soubory ke stažení, protože je možné obnovit z informační kanály balíčků, jako je nuget.org (viz [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="185f4-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="185f4-125">Jejich zahrnování by jinak nafouknutí úložiště nebo vytvořit soubory .zip zbytečně velký.</span><span class="sxs-lookup"><span data-stu-id="185f4-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="185f4-126">Chyba může dojít, pokud váš soubor projektu obsahuje absolutní cesty k umístění balíčku, a přesunout projektu.</span><span class="sxs-lookup"><span data-stu-id="185f4-126">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="185f4-127">Obnovení balíčků, použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="185f4-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="185f4-128">Pokud po přesunutí souboru projektu, upravte soubor přímo aktualizovat odkazy na balíček.</span><span class="sxs-lookup"><span data-stu-id="185f4-128">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="185f4-129">V sadě Visual Studio povolit obnovení balíčků tak, že vyberete **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkazu nabídky nastavení obě možnosti v části **obnovení balíčků**a výběrem  **OK**.</span><span class="sxs-lookup"><span data-stu-id="185f4-129">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="185f4-130">Poté znovu sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="185f4-130">Then build the solution again.</span></span>
- <span data-ttu-id="185f4-131">Pro projekty .NET Core, spusťte `dotnet restore` nebo `dotnet build` (který automaticky spustí obnovení).</span><span class="sxs-lookup"><span data-stu-id="185f4-131">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="185f4-132">Na příkazovém řádku spusťte `nuget restore` (s výjimkou projekty vytvořené pomocí `dotnet`, v takovém případě použijte `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="185f4-132">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="185f4-133">V příkazovém řádku s projekty pomocí formátu PackageReference spustit `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="185f4-133">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="185f4-134">Po úspěšné obnovení by měla být k dispozici v balíčku *global-packages* složky.</span><span class="sxs-lookup"><span data-stu-id="185f4-134">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="185f4-135">Pro projekty pomocí PackageReference obnovení musí znovu vytvořit `obj/project.assets.json` soubor; pro projekty používající `packages.config`, balíček by se měla objevit v projektu `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="185f4-135">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="185f4-136">Projekt by měl nyní úspěšně sestavit.</span><span class="sxs-lookup"><span data-stu-id="185f4-136">The project should now build successfully.</span></span> <span data-ttu-id="185f4-137">V opačném případě [založte problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak jsme poradí s vámi.</span><span class="sxs-lookup"><span data-stu-id="185f4-137">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="185f4-138">Nebyl nalezen project.assets.json souboru prostředků</span><span class="sxs-lookup"><span data-stu-id="185f4-138">Assets file project.assets.json not found</span></span>

<span data-ttu-id="185f4-139">Kompletní chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="185f4-139">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="185f4-140">`project.assets.json` Souboru udržuje graf závislosti projektu při použití formátu správy PackageReference, který se používá k zajištění toho, že jsou v počítači nainstalovány všechny potřebné balíčky.</span><span class="sxs-lookup"><span data-stu-id="185f4-140">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="185f4-141">Protože tento soubor se generuje dynamicky pomocí obnovení balíčků, není obvykle přidat do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="185f4-141">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="185f4-142">V důsledku toho k této chybě dochází při sestavování projektu pomocí nástroje, jako `msbuild` , neobnoví automaticky balíčky.</span><span class="sxs-lookup"><span data-stu-id="185f4-142">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="185f4-143">V takovém případě spusťte `msbuild /t:restore` následovaný `msbuild`, nebo použijte `dotnet build` (což obnoví balíčky automaticky).</span><span class="sxs-lookup"><span data-stu-id="185f4-143">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="185f4-144">Můžete také použít některou z metod obnovení balíčku v [předchozí části](#missing).</span><span class="sxs-lookup"><span data-stu-id="185f4-144">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="185f4-145">Jeden nebo více balíčků NuGet je nutné obnovit, ale nepodařilo, protože nebyl udělen souhlas</span><span class="sxs-lookup"><span data-stu-id="185f4-145">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="185f4-146">Kompletní chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="185f4-146">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="185f4-147">Tato chyba označuje, že obnovení balíčků je zakázáno v konfiguraci Nugetu.</span><span class="sxs-lookup"><span data-stu-id="185f4-147">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="185f4-148">Použít nastavení v sadě Visual Studio můžete změnit, jak je popsáno výše v části [rychlé řešení pro uživatele sady Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="185f4-148">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="185f4-149">Můžete také upravit tato nastavení přímo v příslušné `nuget.config` soubor (obvykle `%AppData%\NuGet\NuGet.Config` na Windows a `~/.nuget/NuGet/NuGet.Config` na Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="185f4-149">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="185f4-150">Ujistěte se, že `enabled` a `automatic` klíče v části `packageRestore` jsou nastaveny na hodnotu True:</span><span class="sxs-lookup"><span data-stu-id="185f4-150">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="185f4-151">Pokud upravíte `packageRestore` přímo v nastavení `nuget.config`, restartujte aplikaci Visual Studio tak, aby se dialogové okno Možnosti zobrazuje aktuální hodnoty.</span><span class="sxs-lookup"><span data-stu-id="185f4-151">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="185f4-152">Další potenciální podmínky</span><span class="sxs-lookup"><span data-stu-id="185f4-152">Other potential conditions</span></span>

- <span data-ttu-id="185f4-153">Chyby sestavení z důvodu chybějících souborů, kterým může dojít u zpráva, že si je stáhnout pomocí obnovení NuGet.</span><span class="sxs-lookup"><span data-stu-id="185f4-153">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="185f4-154">Ale spuštění obnovení může být například "všechny balíčky jsou už nainstalované a neexistuje žádné položky k obnovení."</span><span class="sxs-lookup"><span data-stu-id="185f4-154">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="185f4-155">V takovém případě odstranit `packages` složky (při použití `packages.config`) nebo `obj/project.assets.json` souboru (při použití PackageReference) a spusťte obnovení znovu.</span><span class="sxs-lookup"><span data-stu-id="185f4-155">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="185f4-156">Pokud chyba stále přetrvává, použijte `nuget locals all -clear` nebo `dotnet locals all --clear` z příkazového řádku pro vymazání *global-packages* a jak je popsáno v mezipaměti složky [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="185f4-156">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="185f4-157">Při získávání projekt ze správy zdrojových kódů, složky projektu může být nastavená na jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="185f4-157">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="185f4-158">Změňte oprávnění pro složky a zkuste to znovu obnovují se balíčky.</span><span class="sxs-lookup"><span data-stu-id="185f4-158">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="185f4-159">Může používat stará verze balíčku nuget.</span><span class="sxs-lookup"><span data-stu-id="185f4-159">You may be using an old version of NuGet.</span></span> <span data-ttu-id="185f4-160">Zkontrolujte [nuget.org/downloads](https://www.nuget.org/downloads) nejnovější doporučených verzí.</span><span class="sxs-lookup"><span data-stu-id="185f4-160">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="185f4-161">Pro Visual Studio 2015 doporučujeme 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="185f4-161">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="185f4-162">Pokud narazíte na jiné problémy [založte problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) proto jsme od vás získali více podrobností.</span><span class="sxs-lookup"><span data-stu-id="185f4-162">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
