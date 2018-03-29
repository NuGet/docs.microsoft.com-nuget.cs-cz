---
title: Řešení potíží s balíček NuGet obnovit v sadě Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Popis běžné NuGet obnovit chyby v sadě Visual Studio a řešení potíží s nimi.
keywords: Řešení potíží s obnovení balíčku NuGet, obnovení balíčků, řešení potíží
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 27a43ceaefdf3a7842183a64ea57d05416d6cb02
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="39d8a-104">Řešení potíží s chybami obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="39d8a-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="39d8a-105">Tento článek se zaměřuje na běžné chyby při obnovování balíčků a kroky k jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="39d8a-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="39d8a-106">Úplné podrobnosti o obnovení balíčků naleznete v tématu [obnovení balíčků](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="39d8a-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="39d8a-107">Pokud pokynů tady nefungují, [prosím soubor problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby jsme více pečlivě zkontrolujte váš scénář.</span><span class="sxs-lookup"><span data-stu-id="39d8a-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="39d8a-108">Nepoužívejte "je tato stránka užitečné?"</span><span class="sxs-lookup"><span data-stu-id="39d8a-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="39d8a-109">ovládací prvek, který může vypadat na této stránce, protože se nám nedává možnost kontaktovat v souvislosti s další informace.</span><span class="sxs-lookup"><span data-stu-id="39d8a-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="39d8a-110">Rychlé řešení pro uživatele v sadě Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39d8a-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="39d8a-111">Pokud používáte Visual Studio, nejdřív takto povolte obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="39d8a-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="39d8a-112">V opačném případě pokračujte v následujících částech.</span><span class="sxs-lookup"><span data-stu-id="39d8a-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="39d8a-113">Vyberte **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="39d8a-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="39d8a-114">Nastavit obě možnosti v části **obnovení balíčků**.</span><span class="sxs-lookup"><span data-stu-id="39d8a-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="39d8a-115">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="39d8a-115">Select **OK**.</span></span>
1. <span data-ttu-id="39d8a-116">Znovu sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="39d8a-116">Build your project again.</span></span>

![Povolit obnovení balíčků NuGet v Nástroje/možnosti](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="39d8a-118">Tato nastavení lze změnit také v vaše `NuGet.config` soubor; najdete v článku [souhlas](#consent) části.</span><span class="sxs-lookup"><span data-stu-id="39d8a-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="39d8a-119">Tento projekt odkazuje na balíčky NuGet, které nejsou v tomto počítači</span><span class="sxs-lookup"><span data-stu-id="39d8a-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="39d8a-120">Dokončení chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="39d8a-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="39d8a-121">K této chybě dojde, pokusíte sestavení projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou nainstalovány v současné době na počítači nebo v projektu.</span><span class="sxs-lookup"><span data-stu-id="39d8a-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="39d8a-122">Při použití formátu PackageReference správy, chyba znamená, že balíček není nainstalovaný v *globální balíčky* složky, jak je popsáno na, jak je popsáno na [správy globální balíčky a složky mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="39d8a-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="39d8a-123">Při použití `packages.config`, chyba znamená, že balíček není nainstalovaný v `packages` složku v kořenovém adresáři řešení.</span><span class="sxs-lookup"><span data-stu-id="39d8a-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="39d8a-124">K této situaci dochází běžně při získání zdrojového kódu projektu ze správy zdrojového kódu nebo jiného stahování.</span><span class="sxs-lookup"><span data-stu-id="39d8a-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="39d8a-125">Balíčky jsou obvykle ze zdrojového kódu nebo stahování vynechána, protože bylo možné obnovit z balíčku kanály jako nuget.org (viz [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="39d8a-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="39d8a-126">Včetně jejich by jinak nafouknutí úložiště nebo vytvořte .zip zbytečně velké soubory.</span><span class="sxs-lookup"><span data-stu-id="39d8a-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="39d8a-127">Aby se obnovily balíčky, použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="39d8a-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="39d8a-128">V sadě Visual Studio, povolit obnovení balíčků výběrem **nástroje > Správce balíčků NuGet > Nastavení správce balíčků** příkaz nabídky, obě možnosti v části Nastavení **obnovení balíčků**a výběr  **OK**.</span><span class="sxs-lookup"><span data-stu-id="39d8a-128">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="39d8a-129">Pak znovu sestavte řešení.</span><span class="sxs-lookup"><span data-stu-id="39d8a-129">Then build the solution again.</span></span>
- <span data-ttu-id="39d8a-130">.NET Core projekty, spusťte `dotnet restore` nebo `dotnet build` (který automaticky spustí obnovení).</span><span class="sxs-lookup"><span data-stu-id="39d8a-130">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="39d8a-131">Na příkazovém řádku spusťte `nuget restore` (s výjimkou projektů vytvořených s `dotnet`, v takovém případě použijte `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="39d8a-131">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="39d8a-132">Na příkazovém řádku s projekty formátu PackageReference, spusťte `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="39d8a-132">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="39d8a-133">Po úspěšné obnovení mají být dostupné v balíčku *globální balíčky* složky.</span><span class="sxs-lookup"><span data-stu-id="39d8a-133">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="39d8a-134">Pro projekty pomocí PackageReference, by měl znovu obnovení `obj/project.assets.json` souboru; pro projekty pomocí `packages.config`, by se měla objevit balíček v projektu `packages` složky.</span><span class="sxs-lookup"><span data-stu-id="39d8a-134">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="39d8a-135">Projekt má nyní sestavit úspěšně.</span><span class="sxs-lookup"><span data-stu-id="39d8a-135">The project should now build successfully.</span></span> <span data-ttu-id="39d8a-136">Pokud ne, [souboru problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak nám s vámi následnou akci.</span><span class="sxs-lookup"><span data-stu-id="39d8a-136">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="39d8a-137">Prostředky souboru project.assets.json nebyl nalezen</span><span class="sxs-lookup"><span data-stu-id="39d8a-137">Assets file project.assets.json not found</span></span>

<span data-ttu-id="39d8a-138">Dokončení chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="39d8a-138">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="39d8a-139">`project.assets.json` Souboru udržuje graf závislostí projektu při použití formátu PackageReference správy, který se používá a ujistěte se, že všechny potřebné balíčky jsou nainstalované v počítači.</span><span class="sxs-lookup"><span data-stu-id="39d8a-139">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="39d8a-140">Protože tento soubor je generována dynamicky prostřednictvím obnovení balíčku, není obvykle přidán do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="39d8a-140">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="39d8a-141">V důsledku toho k této chybě dojde při sestavování projektu nástroj, jako `msbuild` , ale neobnoví automaticky balíčky.</span><span class="sxs-lookup"><span data-stu-id="39d8a-141">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="39d8a-142">V takovém případě spusťte `msbuild /t:restore` následuje `msbuild`, nebo použijte `dotnet build` (což obnoví balíčky automaticky).</span><span class="sxs-lookup"><span data-stu-id="39d8a-142">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="39d8a-143">Můžete také použít některou z metod obnovení balíčku v [předchozí části](#missing).</span><span class="sxs-lookup"><span data-stu-id="39d8a-143">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="39d8a-144">Jeden nebo více balíčků NuGet je potřeba, ale nebylo možné, protože nebyl udělen souhlas</span><span class="sxs-lookup"><span data-stu-id="39d8a-144">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="39d8a-145">Dokončení chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="39d8a-145">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="39d8a-146">Tato chyba znamená, že obnovení balíčku je zakázáno v konfiguraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="39d8a-146">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="39d8a-147">Použít nastavení v sadě Visual Studio můžete změnit, jak je popsáno výše v části [rychlé řešení pro Visual Studio uživatele](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="39d8a-147">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="39d8a-148">Můžete také upravit tato nastavení přímo v příslušné `nuget.config` souboru (obvykle `%AppData%\NuGet\NuGet.Config` v systému Windows a `~/.nuget/NuGet/NuGet.Config` na Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="39d8a-148">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="39d8a-149">Zajistěte, aby `enabled` a `automatic` klíče v části `packageRestore` jsou nastaveny na hodnotu True:</span><span class="sxs-lookup"><span data-stu-id="39d8a-149">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="39d8a-150">Pokud chcete upravit `packageRestore` nastavení přímo v `nuget.config`, restartujte Visual Studio, aby se dialogové okno Možnosti zobrazuje aktuální hodnoty.</span><span class="sxs-lookup"><span data-stu-id="39d8a-150">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="39d8a-151">Další potenciální podmínky</span><span class="sxs-lookup"><span data-stu-id="39d8a-151">Other potential conditions</span></span>

- <span data-ttu-id="39d8a-152">Chyby sestavení z důvodu chybějících souborů, může dojít u zpráva, že je stáhnout pomocí obnovení NuGet.</span><span class="sxs-lookup"><span data-stu-id="39d8a-152">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="39d8a-153">Však spuštění obnovení říci, "všechny balíčky jsou už nainstalované a neexistuje žádné položky k obnovení."</span><span class="sxs-lookup"><span data-stu-id="39d8a-153">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="39d8a-154">V takovém případě odstraňte `packages` složky (při použití `packages.config`) nebo `obj/project.assets.json` souboru (při použití PackageReference) a spusťte obnovení znovu.</span><span class="sxs-lookup"><span data-stu-id="39d8a-154">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="39d8a-155">Pokud chyba stále přetrvává, použijte `nuget locals all -clear` nebo `dotnet locals all --clear` z příkazového řádku zrušte *globální balíčky* a složky mezipaměti, jak je popsáno na [správy globální balíčky a složky mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="39d8a-155">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="39d8a-156">Při získávání projektu od správy zdrojového kódu, může být vaše složky projektu nastaven jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="39d8a-156">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="39d8a-157">Změňte oprávnění složky a znovu Probíhá obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="39d8a-157">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="39d8a-158">Možná používáte starší verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="39d8a-158">You may be using an old version of NuGet.</span></span> <span data-ttu-id="39d8a-159">Zkontrolujte [nuget.org/downloads](https://www.nuget.org/downloads) nejnovější doporučená verze.</span><span class="sxs-lookup"><span data-stu-id="39d8a-159">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="39d8a-160">Pro Visual Studio 2015 doporučujeme 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="39d8a-160">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="39d8a-161">Pokud narazíte na jiné problémy [souboru problém na Githubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak jsme od vás získali další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="39d8a-161">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>