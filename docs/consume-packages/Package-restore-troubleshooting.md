---
title: Řešení potíží s obnovení balíčku NuGet v sadě Visual Studio
description: Popis běžné NuGet obnovit chyby v sadě Visual Studio a řešení potíží s nimi.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 8e817b8e95c53d27120bf56db52b45b69a5ff973
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816967"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="c5ae9-103">Řešení potíží s chybami obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="c5ae9-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="c5ae9-104">Tento článek se zaměřuje na běžné chyby při obnovování balíčků a kroky k jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="c5ae9-105">Úplné podrobnosti o obnovení balíčků naleznete v tématu [obnovení balíčků](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="c5ae9-106">Pokud pokynů tady nefungují, [prosím soubor problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby jsme více pečlivě zkontrolujte váš scénář.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="c5ae9-107">Nepoužívejte "je tato stránka užitečné?"</span><span class="sxs-lookup"><span data-stu-id="c5ae9-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="c5ae9-108">ovládací prvek, který může vypadat na této stránce, protože se nám nedává možnost kontaktovat v souvislosti s další informace.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="c5ae9-109">Rychlé řešení pro uživatele v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5ae9-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="c5ae9-110">Pokud používáte Visual Studio, nejdřív takto povolte obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="c5ae9-111">V opačném případě pokračujte v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="c5ae9-112">Vyberte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="c5ae9-113">Nastavit obě možnosti v části **obnovení balíčků**.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="c5ae9-114">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-114">Select **OK**.</span></span>
1. <span data-ttu-id="c5ae9-115">Znovu sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-115">Build your project again.</span></span>

![Povolit obnovení balíčků NuGet v Nástroje/možnosti](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="c5ae9-117">Tato nastavení lze změnit také v vaše `NuGet.config` soubor; najdete v článku [souhlas](#consent) části.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="c5ae9-118">Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači</span><span class="sxs-lookup"><span data-stu-id="c5ae9-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="c5ae9-119">Dokončení chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="c5ae9-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="c5ae9-120">K této chybě dojde, pokusíte sestavení projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou nainstalovány v současné době na počítači nebo v projektu.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-120">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="c5ae9-121">Při použití formátu PackageReference správy, chyba znamená, že balíček není nainstalovaný v *globální balíčky* složky, jak je popsáno na, jak je popsáno na [správy globální balíčky a složky mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="c5ae9-122">Při použití `packages.config`, chyba znamená, že balíček není nainstalovaný v `packages` složku v kořenovém adresáři řešení.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="c5ae9-123">K této situaci dochází běžně při získání zdrojového kódu projektu ze správy zdrojového kódu nebo jiného stahování.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="c5ae9-124">Balíčky jsou obvykle ze zdrojového kódu nebo stahování vynechána, protože bylo možné obnovit z balíčku kanály jako nuget.org (viz [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="c5ae9-125">Včetně jejich by jinak nafouknutí úložiště nebo vytvořte .zip zbytečně velké soubory.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="c5ae9-126">Chyba může také dojít, pokud soubor projektu obsahuje absolutní cesty k umístění balíčku a přesunout projektu.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-126">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="c5ae9-127">Aby se obnovily balíčky, použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="c5ae9-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="c5ae9-128">Pokud jste přesunuli souboru projektu, upravte soubor přímo do aktualizovat odkazy v balíčku.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-128">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="c5ae9-129">V sadě Visual Studio, povolit obnovení balíčků výběrem **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkaz nabídky, obě možnosti v části Nastavení **obnovení balíčků**a výběr  **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-129">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="c5ae9-130">Pak znovu sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-130">Then build the solution again.</span></span>
- <span data-ttu-id="c5ae9-131">.NET Core projekty, spusťte `dotnet restore` nebo `dotnet build` (který automaticky spustí obnovení).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-131">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="c5ae9-132">Na příkazovém řádku spusťte `nuget restore` (s výjimkou projektů vytvořených s `dotnet`, v takovém případě použijte `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-132">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="c5ae9-133">Na příkazovém řádku s projekty formátu PackageReference, spusťte `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-133">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="c5ae9-134">Po úspěšné obnovení mají být dostupné v balíčku *globální balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-134">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="c5ae9-135">Pro projekty pomocí PackageReference, by měl znovu obnovení `obj/project.assets.json` souboru; pro projekty pomocí `packages.config`, by se měla objevit balíček v projektu `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-135">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="c5ae9-136">Projekt má nyní sestavit úspěšně.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-136">The project should now build successfully.</span></span> <span data-ttu-id="c5ae9-137">Pokud ne, [souboru problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak nám s vámi následnou akci.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-137">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="c5ae9-138">Prostředky souboru project.assets.json nebyl nalezen</span><span class="sxs-lookup"><span data-stu-id="c5ae9-138">Assets file project.assets.json not found</span></span>

<span data-ttu-id="c5ae9-139">Dokončení chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="c5ae9-139">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="c5ae9-140">`project.assets.json` Souboru udržuje graf závislostí projektu při použití formátu PackageReference správy, který se používá a ujistěte se, že všechny potřebné balíčky jsou nainstalované v počítači.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-140">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="c5ae9-141">Protože tento soubor je generována dynamicky prostřednictvím obnovení balíčku, není obvykle přidán do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-141">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="c5ae9-142">V důsledku toho k této chybě dojde při sestavování projektu nástroj, jako `msbuild` , ale neobnoví automaticky balíčky.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-142">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="c5ae9-143">V takovém případě spusťte `msbuild /t:restore` následuje `msbuild`, nebo použijte `dotnet build` (což obnoví balíčky automaticky).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-143">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="c5ae9-144">Můžete také použít některou z metod obnovení balíčku v [předchozí části](#missing).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-144">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="c5ae9-145">Jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas</span><span class="sxs-lookup"><span data-stu-id="c5ae9-145">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="c5ae9-146">Dokončení chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="c5ae9-146">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="c5ae9-147">Tato chyba znamená, že obnovení balíčku je zakázáno v konfiguraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-147">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="c5ae9-148">Použít nastavení v sadě Visual Studio můžete změnit, jak je popsáno výše v části [rychlé řešení pro Visual Studio uživatele](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-148">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="c5ae9-149">Můžete také upravit tato nastavení přímo v příslušné `nuget.config` souboru (obvykle `%AppData%\NuGet\NuGet.Config` v systému Windows a `~/.nuget/NuGet/NuGet.Config` na Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-149">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="c5ae9-150">Zajistěte, aby `enabled` a `automatic` klíče v části `packageRestore` jsou nastaveny na hodnotu True:</span><span class="sxs-lookup"><span data-stu-id="c5ae9-150">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="c5ae9-151">Pokud chcete upravit `packageRestore` nastavení přímo v `nuget.config`, restartujte Visual Studio, aby se dialogové okno Možnosti zobrazuje aktuální hodnoty.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-151">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="c5ae9-152">Další potenciální podmínky</span><span class="sxs-lookup"><span data-stu-id="c5ae9-152">Other potential conditions</span></span>

- <span data-ttu-id="c5ae9-153">Chyby sestavení z důvodu chybějících souborů, může dojít u zpráva, že je stáhnout pomocí obnovení NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-153">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="c5ae9-154">Však spuštění obnovení říci, "všechny balíčky jsou už nainstalované a neexistuje žádné položky k obnovení."</span><span class="sxs-lookup"><span data-stu-id="c5ae9-154">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="c5ae9-155">V takovém případě odstraňte `packages` složky (při použití `packages.config`) nebo `obj/project.assets.json` souboru (při použití PackageReference) a spusťte obnovení znovu.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-155">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="c5ae9-156">Pokud chyba stále přetrvává, použijte `nuget locals all -clear` nebo `dotnet locals all --clear` z příkazového řádku zrušte *globální balíčky* a složky mezipaměti, jak je popsáno na [správy globální balíčky a složky mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="c5ae9-156">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="c5ae9-157">Při získávání projektu od správy zdrojového kódu, může být vaše složky projektu nastaven jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-157">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="c5ae9-158">Změňte oprávnění složky a znovu Probíhá obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-158">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="c5ae9-159">Možná používáte starší verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-159">You may be using an old version of NuGet.</span></span> <span data-ttu-id="c5ae9-160">Zkontrolujte [nuget.org/downloads](https://www.nuget.org/downloads) nejnovější doporučená verze.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-160">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="c5ae9-161">Pro Visual Studio 2015 doporučujeme 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-161">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="c5ae9-162">Pokud narazíte na jiné problémy [souboru problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak jsme od vás získali další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="c5ae9-162">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>