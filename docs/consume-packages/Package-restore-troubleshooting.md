---
title: Řešení potíží s obnovením balíčků NuGet v Visual Studio
description: Popis běžných chyb obnovení NuGet v Visual Studio a jejich řešení.
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323619"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="48174-103">Řešení potíží s chybami obnovení balíčků</span><span class="sxs-lookup"><span data-stu-id="48174-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="48174-104">Tento článek se zaměřuje na běžné chyby při obnovování balíčků a postup jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="48174-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="48174-105">Obnovení balíčku se pokusí nainstalovat všechny závislosti balíčku do správného stavu, který odpovídá odkazům na balíček v souboru projektu (*.csproj*) *nebo* packages.configsouboru.</span><span class="sxs-lookup"><span data-stu-id="48174-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="48174-106">(V Visual Studio se odkazy zobrazí v Průzkumník řešení pod **uzlem Závislosti \ NuGet** nebo **Odkazy.)** Pokud chcete obnovit balíčky podle požadovaných kroků, podívejte se na [obnovení balíčků](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="48174-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="48174-107">Pokud balíček odkazuje v souboru projektu (*.csproj)* nebo váš *souborpackages.config* je nesprávný (po obnovení balíčku se neshodují s požadovaným stavem), musíte místo použití obnovení balíčku buď nainstalovat, nebo aktualizovat balíčky.</span><span class="sxs-lookup"><span data-stu-id="48174-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="48174-108">Pokud zde uvedené pokyny pro vás nefungují, zakažte problém na [GitHubu,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abychom mohli váš scénář pečlivěji prozkoumat.</span><span class="sxs-lookup"><span data-stu-id="48174-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="48174-109">Nepoužívejte "Je tato stránka užitečná?"</span><span class="sxs-lookup"><span data-stu-id="48174-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="48174-110">ovládací prvek, který se může zobrazit na této stránce, protože nám nedává možnost vás kontaktovat a získat další informace.</span><span class="sxs-lookup"><span data-stu-id="48174-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="48174-111">Rychlé řešení pro Visual Studio uživatele</span><span class="sxs-lookup"><span data-stu-id="48174-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="48174-112">Pokud používáte následující Visual Studio, nejprve následujícím způsobem povolte obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="48174-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="48174-113">V opačném případě pokračujte k následujícím částem.</span><span class="sxs-lookup"><span data-stu-id="48174-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="48174-114">Vyberte příkaz **> NuGet Správce balíčků > Správce balíčků Nastavení.**</span><span class="sxs-lookup"><span data-stu-id="48174-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="48174-115">Obě možnosti nastavte v **části Obnovení balíčku.**</span><span class="sxs-lookup"><span data-stu-id="48174-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="48174-116">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="48174-116">Select **OK**.</span></span>
1. <span data-ttu-id="48174-117">Znovu sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="48174-117">Build your project again.</span></span>

![Povolení obnovení balíčků NuGet v nástroji nebo možnostech](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="48174-119">Tato nastavení můžete také změnit v `NuGet.Config` souboru. Viz část [o souhlasu.](#consent)</span><span class="sxs-lookup"><span data-stu-id="48174-119">These settings can also be changed in your `NuGet.Config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="48174-120">Pokud je váš projekt starší projekt, který používá obnovení balíčku [](package-restore.md#migrate-to-automatic-package-restore-visual-studio) integrovaného do nástroje MSBuild, možná bude nutné provést migraci na automatické obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="48174-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="48174-121">Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí.</span><span class="sxs-lookup"><span data-stu-id="48174-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="48174-122">Kompletní chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="48174-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="48174-123">K této chybě dochází při pokusu o sestavení projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou v současnosti nainstalovány na počítači nebo v projektu.</span><span class="sxs-lookup"><span data-stu-id="48174-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="48174-124">Při použití formátu [správy PackageReference](package-references-in-project-files.md) může být tato chyba ponechána na migraci z [](/nuget/resources/nuget-faq#working-with-packages) packages.config na PackageReference a je potřeba ji ručně odebrat ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="48174-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](/nuget/resources/nuget-faq#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="48174-125">Při použití [packages.config](../reference/packages-config.md)znamená chyba, že balíček není nainstalovaný ve složce `packages` v kořenovém adresáři řešení.</span><span class="sxs-lookup"><span data-stu-id="48174-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="48174-126">K této situaci obvykle dochází, když zdrojový kód projektu získáte ze správy zdrojového kódu nebo jiného stahování.</span><span class="sxs-lookup"><span data-stu-id="48174-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="48174-127">Balíčky jsou ze správy zdrojového kódu nebo stahování obvykle vynechány, protože je lze obnovit z informačních kanálů balíčků, jako je nuget.org (viz Balíčky a [správy zdrojového kódu).](Packages-and-Source-Control.md)</span><span class="sxs-lookup"><span data-stu-id="48174-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="48174-128">Jejich zahrnutí by jinak nafoukalo úložiště nebo by zbytečně vytvářelo .zip soubory.</span><span class="sxs-lookup"><span data-stu-id="48174-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="48174-129">K této chybě může dojít také v případě, že soubor projektu obsahuje absolutní cesty k umístění balíčků a přesunete projekt.</span><span class="sxs-lookup"><span data-stu-id="48174-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="48174-130">K obnovení balíčků použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="48174-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="48174-131">Pokud jste přesunuli soubor projektu, upravte soubor přímo a aktualizujte odkazy na balíček.</span><span class="sxs-lookup"><span data-stu-id="48174-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="48174-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatické obnovení](package-restore.md#restore-packages-automatically-using-visual-studio) nebo [ruční obnovení)](package-restore.md#restore-packages-manually-using-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="48174-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="48174-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="48174-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="48174-134">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="48174-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="48174-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="48174-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="48174-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="48174-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="48174-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="48174-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="48174-138">Po úspěšném obnovení by měl být balíček ve složce *global-packages.*</span><span class="sxs-lookup"><span data-stu-id="48174-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="48174-139">U projektů, které používají PackageReference, by se měl soubor obnovit znovu. U projektů pomocí by se měl balíček zobrazit `obj/project.assets.json` `packages.config` ve složce `packages` projektu.</span><span class="sxs-lookup"><span data-stu-id="48174-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="48174-140">Projekt by se teď měl úspěšně sestavit.</span><span class="sxs-lookup"><span data-stu-id="48174-140">The project should now build successfully.</span></span> <span data-ttu-id="48174-141">Pokud ne, [zařiďte problém na GitHubu,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abychom vás mohli sledovat.</span><span class="sxs-lookup"><span data-stu-id="48174-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="48174-142">Soubor assetů project.assets.jsse nenašel</span><span class="sxs-lookup"><span data-stu-id="48174-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="48174-143">Kompletní chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="48174-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="48174-144">Soubor udržuje graf závislostí projektu při použití formátu správy PackageReference, který se používá k zajištění, že jsou v počítači nainstalované `project.assets.json` všechny potřebné balíčky.</span><span class="sxs-lookup"><span data-stu-id="48174-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="48174-145">Vzhledem k tomu, že se tento soubor generuje dynamicky prostřednictvím obnovení balíčku, obvykle se nepřidá do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="48174-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="48174-146">V důsledku toho k této chybě dochází při sestavování projektu pomocí nástroje, jako je například , který `msbuild` automaticky obnovuje balíčky.</span><span class="sxs-lookup"><span data-stu-id="48174-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="48174-147">V takovém případě spusťte `msbuild -t:restore` příkaz následovaný příkazem `msbuild` nebo použijte příkaz `dotnet build` (který balíčky automaticky obnoví).</span><span class="sxs-lookup"><span data-stu-id="48174-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="48174-148">Můžete také použít jakoukoli z metod obnovení balíčků v [předchozí části](#missing).</span><span class="sxs-lookup"><span data-stu-id="48174-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="48174-149">Jeden nebo více balíčků NuGet je potřeba obnovit, ale ne, protože nebyl udělen souhlas.</span><span class="sxs-lookup"><span data-stu-id="48174-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="48174-150">Kompletní chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="48174-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="48174-151">Tato chyba znamená, že obnovení balíčku je v konfiguraci NuGet zakázané.</span><span class="sxs-lookup"><span data-stu-id="48174-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="48174-152">Platná nastavení můžete změnit v části Visual Studio, jak je popsáno výše v části Rychlé řešení [pro Visual Studio uživatele](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="48174-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="48174-153">Tato nastavení můžete také upravit přímo v příslušném souboru (obvykle ve Windows a `nuget.config` `%AppData%\NuGet\NuGet.Config` v systému `~/.nuget/NuGet/NuGet.Config` Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="48174-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="48174-154">Ujistěte se, `enabled` že jsou klíče a v části nastavené na Hodnotu `automatic` `packageRestore` True:</span><span class="sxs-lookup"><span data-stu-id="48174-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="48174-155">Pokud upravíte nastavení `packageRestore` přímo v , restartujte Visual Studio, aby se v dialogovém okně možností zobrazují `nuget.config` aktuální hodnoty.</span><span class="sxs-lookup"><span data-stu-id="48174-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="48174-156">Další potenciální podmínky</span><span class="sxs-lookup"><span data-stu-id="48174-156">Other potential conditions</span></span>

- <span data-ttu-id="48174-157">Může dojít k chybám sestavení kvůli chybějícím souborům se zprávou o použití obnovení NuGet ke stažení.</span><span class="sxs-lookup"><span data-stu-id="48174-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="48174-158">Při spuštění obnovení se ale může zobrazit tato informace: "Všechny balíčky jsou už nainstalované a není nic k obnovení".</span><span class="sxs-lookup"><span data-stu-id="48174-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="48174-159">V takovém případě odstraňte složku (při použití ) nebo souboru (při použití `packages` `packages.config` PackageReference) a znovu spusťte `obj/project.assets.json` obnovení.</span><span class="sxs-lookup"><span data-stu-id="48174-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="48174-160">Pokud chyba přetrvává, pomocí příkazu nebo z příkazového řádku vymažte globální balíčky a složky mezipaměti, jak je popsáno v tématu Správa globálních balíčků a složek `nuget locals all -clear` `dotnet nuget locals all --clear` [mezipaměti](managing-the-global-packages-and-cache-folders.md). </span><span class="sxs-lookup"><span data-stu-id="48174-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="48174-161">Při získávání projektu ze správy zdrojového kódu je možné nastavit složky projektu jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="48174-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="48174-162">Změňte oprávnění ke složce a zkuste balíčky obnovit znovu.</span><span class="sxs-lookup"><span data-stu-id="48174-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="48174-163">Možná používáte starou verzi NuGetu.</span><span class="sxs-lookup"><span data-stu-id="48174-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="48174-164">[Zkontrolujte nuget.org/downloads](https://www.nuget.org/downloads) nejnovější doporučené verze.</span><span class="sxs-lookup"><span data-stu-id="48174-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="48174-165">Pro Visual Studio 2015 doporučujeme 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="48174-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="48174-166">Pokud narazíte na jiné problémy, [zakažte problém](https://github.com/NuGet/docs.microsoft.com-nuget/issues) na GitHubu, abychom od vás získali další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="48174-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
