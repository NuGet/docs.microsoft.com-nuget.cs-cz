---
title: Poradce při potížích s obnovením balíčků NuGet v sadě Visual Studio
description: Popis běžných chyb obnovení NuGet v sadě Visual Studio a jejich řešení.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860625"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="aab47-103">Poradce při potížích s chybami obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="aab47-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="aab47-104">Tento článek se zaměřuje na běžné chyby při obnovení balíčků a kroky k jejich vyřešení.</span><span class="sxs-lookup"><span data-stu-id="aab47-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="aab47-105">Nástroj Restore package restore se pokusí nainstalovat všechny závislosti balíčků do správného stavu, který odpovídá odkazům na balíček v souboru projektu (*csproj*) nebo souboru *packages.config.*</span><span class="sxs-lookup"><span data-stu-id="aab47-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="aab47-106">(V sadě Visual Studio se odkazy zobrazí v Průzkumníku řešení pod **závislostmi \ NuGet** nebo **uzel Reference.)** Chcete-li provést požadované kroky k obnovení balíčků, naleznete v [tématu Obnovení balíčků](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="aab47-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="aab47-107">Pokud jsou odkazy na balíček v souboru projektu (*.csproj*) nebo soubor *packages.config* nesprávné (neodpovídají požadovanému stavu po obnovení balíčku), musíte buď nainstalovat nebo aktualizovat balíčky namísto použití nástroje Obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="aab47-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="aab47-108">Pokud pokyny zde nefungují pro vás, [prosím, soubor problém na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) takže můžeme prozkoumat váš scénář pečlivěji.</span><span class="sxs-lookup"><span data-stu-id="aab47-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="aab47-109">Nepoužívejte "Je tato stránka užitečná?"</span><span class="sxs-lookup"><span data-stu-id="aab47-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="aab47-110">které se mohou na této stránce zobrazit, protože nám neumožňuje vás kontaktovat pro další informace.</span><span class="sxs-lookup"><span data-stu-id="aab47-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="aab47-111">Rychlé řešení pro uživatele sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aab47-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="aab47-112">Pokud používáte Visual Studio, nejprve povolte obnovení balíčku následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="aab47-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="aab47-113">V opačném případě pokračujte do následujících oddílů.</span><span class="sxs-lookup"><span data-stu-id="aab47-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="aab47-114">Vyberte příkaz **příkaz U nástroje > Správce balíčků > nastavení Správce balíčků.**</span><span class="sxs-lookup"><span data-stu-id="aab47-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="aab47-115">Nastavte obě možnosti v části **Obnovení balíčku**.</span><span class="sxs-lookup"><span data-stu-id="aab47-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="aab47-116">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="aab47-116">Select **OK**.</span></span>
1. <span data-ttu-id="aab47-117">Sestavte svůj projekt znovu.</span><span class="sxs-lookup"><span data-stu-id="aab47-117">Build your project again.</span></span>

![Povolit obnovení balíčku NuGet v nástroji/možnostech](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="aab47-119">Tato nastavení lze také `NuGet.config` změnit v souboru; naleznete v sekci [souhlas.](#consent)</span><span class="sxs-lookup"><span data-stu-id="aab47-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="aab47-120">Pokud váš projekt je starší projekt, který používá obnovení balíčku integrované MSBuild, budete muset [migrovat](package-restore.md#migrate-to-automatic-package-restore-visual-studio) na automatické obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="aab47-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="aab47-121">Tento projekt odkazuje na balíčky NuGet, které v tomto počítači chybí.</span><span class="sxs-lookup"><span data-stu-id="aab47-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="aab47-122">Úplná chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="aab47-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="aab47-123">K této chybě dochází při pokusu o vytvoření projektu, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky nejsou v současné době nainstalovány v počítači nebo v projektu.</span><span class="sxs-lookup"><span data-stu-id="aab47-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="aab47-124">Při použití formátu správy [PackageReference](package-references-in-project-files.md) chyba znamená, že balíček není nainstalován ve složce *global-packages,* jak je popsáno v [části Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="aab47-124">When using the [PackageReference](package-references-in-project-files.md) management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="aab47-125">Při použití [packages.config](../reference/packages-config.md), chyba znamená, že `packages` balíček není nainstalován ve složce v kořenovém adresáři řešení.</span><span class="sxs-lookup"><span data-stu-id="aab47-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="aab47-126">K této situaci obvykle dochází při získání zdrojového kódu projektu ze správy zdrojového kódu nebo jiného stažení.</span><span class="sxs-lookup"><span data-stu-id="aab47-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="aab47-127">Balíčky jsou obvykle vynechány ze správy zdrojového kódu nebo stahování, protože je lze obnovit z kanálů balíčků, jako je nuget.org (viz [Balíčky a správa zdrojového kódu).](Packages-and-Source-Control.md)</span><span class="sxs-lookup"><span data-stu-id="aab47-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="aab47-128">Jejich zahrnutí by jinak nafouklo úložiště nebo vytvořilo zbytečně velké .zip soubory.</span><span class="sxs-lookup"><span data-stu-id="aab47-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="aab47-129">K chybě může dojít také v případě, že soubor projektu obsahuje absolutní cesty do umístění balíčků a přesunutí projektu.</span><span class="sxs-lookup"><span data-stu-id="aab47-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="aab47-130">K obnovení balíčků použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="aab47-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="aab47-131">Pokud jste přesunuli soubor projektu, upravte soubor přímo a aktualizujte odkazy na balíček.</span><span class="sxs-lookup"><span data-stu-id="aab47-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="aab47-132">[Visual Studio](package-restore.md#restore-using-visual-studio) [(automatické obnovení](package-restore.md#restore-packages-automatically-using-visual-studio) nebo ruční [obnovení)](package-restore.md#restore-packages-manually-using-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="aab47-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="aab47-133">Rozhraní příkazového řádku dotnet</span><span class="sxs-lookup"><span data-stu-id="aab47-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="aab47-134">Rozhraní příkazového řádku nuget.exe</span><span class="sxs-lookup"><span data-stu-id="aab47-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="aab47-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="aab47-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="aab47-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="aab47-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="aab47-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="aab47-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="aab47-138">Po úspěšném obnovení by měl být balíček přítomen ve složce *globální balíčky.*</span><span class="sxs-lookup"><span data-stu-id="aab47-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="aab47-139">U projektů používajících odkaz packagereference `obj/project.assets.json` by obnovení mělo znovu vytvořit soubor. pro projekty pomocí `packages.config`, balíček by `packages` měl být uveden ve složce projektu.</span><span class="sxs-lookup"><span data-stu-id="aab47-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="aab47-140">Projekt by měl nyní úspěšně sestavit.</span><span class="sxs-lookup"><span data-stu-id="aab47-140">The project should now build successfully.</span></span> <span data-ttu-id="aab47-141">Pokud ne, [posuňte na GitHubu problém,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abychom s vámi mohli navázat.</span><span class="sxs-lookup"><span data-stu-id="aab47-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="aab47-142">Soubor datových zdrojů project.assets.json nebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="aab47-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="aab47-143">Úplná chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="aab47-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="aab47-144">Soubor `project.assets.json` udržuje graf závislostí projektu při použití formátu správy PackageReference, který se používá k zajištění, že jsou v počítači nainstalovány všechny potřebné balíčky.</span><span class="sxs-lookup"><span data-stu-id="aab47-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="aab47-145">Vzhledem k tomu, že tento soubor je generován dynamicky prostřednictvím obnovení balíčku, obvykle není přidán do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="aab47-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="aab47-146">V důsledku toho k této chybě dochází při vytváření `msbuild` projektu s nástrojem, jako je například to není automaticky obnovit balíčky.</span><span class="sxs-lookup"><span data-stu-id="aab47-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="aab47-147">V tomto případě `msbuild -t:restore` spustit `msbuild`následuje `dotnet build` , nebo použít (který obnovuje balíčky automaticky).</span><span class="sxs-lookup"><span data-stu-id="aab47-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="aab47-148">Můžete také použít některou z metod obnovení balíčku v [předchozí části](#missing).</span><span class="sxs-lookup"><span data-stu-id="aab47-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="aab47-149">Jeden nebo více balíčků NuGet je třeba obnovit, ale nemůže být, protože nebyl udělen souhlas</span><span class="sxs-lookup"><span data-stu-id="aab47-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="aab47-150">Úplná chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="aab47-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="aab47-151">Tato chyba označuje, že obnovení balíčku je zakázáno v konfiguraci NuGet.</span><span class="sxs-lookup"><span data-stu-id="aab47-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="aab47-152">Příslušná nastavení v sadě Visual Studio můžete změnit, jak je popsáno výše v části [Rychlé řešení pro uživatele sady Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="aab47-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="aab47-153">Tato nastavení můžete také upravit `nuget.config` přímo v `%AppData%\NuGet\NuGet.Config` příslušném `~/.nuget/NuGet/NuGet.Config` souboru (obvykle v systému Windows a na Počítači Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="aab47-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="aab47-154">Ujistěte `enabled` se, že jsou klávesy a `automatic` v části `packageRestore` nastaveny na hodnotu True:</span><span class="sxs-lookup"><span data-stu-id="aab47-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="aab47-155">Pokud upravujete `packageRestore` nastavení `nuget.config`přímo v aplikaci , restartujte visual studio tak, aby dialogové okno možností zobrazovaly aktuální hodnoty.</span><span class="sxs-lookup"><span data-stu-id="aab47-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="aab47-156">Další potenciální podmínky</span><span class="sxs-lookup"><span data-stu-id="aab47-156">Other potential conditions</span></span>

- <span data-ttu-id="aab47-157">Můžete se setkat s chybami sestavení kvůli chybějícím souborům se zprávou, která říká, že chcete použít obnovení NuGet k jejich stažení.</span><span class="sxs-lookup"><span data-stu-id="aab47-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="aab47-158">Spuštění obnovení však může říkat: "Všechny balíčky jsou již nainstalovány a není nic k obnovení."</span><span class="sxs-lookup"><span data-stu-id="aab47-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="aab47-159">V takovém případě `packages` odstraňte složku `packages.config`(při `obj/project.assets.json` použití) nebo soubor (při použití PackageReference) a znovu spusťte obnovení.</span><span class="sxs-lookup"><span data-stu-id="aab47-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="aab47-160">Pokud chyba přetrvává, vymažte globální složky balíčků a mezipamětí, jak je popsáno v části [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md), použijte `nuget locals all -clear` nebo `dotnet locals all --clear` z příkazového řádku vymažte složky *globálních balíčků* a mezipaměti .</span><span class="sxs-lookup"><span data-stu-id="aab47-160">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="aab47-161">Při získávání projektu ze správy zdrojového kódu mohou být složky projektu nastaveny na jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="aab47-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="aab47-162">Změňte oprávnění ke složce a zkuste znovu obnovit balíčky.</span><span class="sxs-lookup"><span data-stu-id="aab47-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="aab47-163">Pravděpodobně používáte starou verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="aab47-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="aab47-164">[Zkontrolujte, nuget.org/downloads](https://www.nuget.org/downloads) najdete nejnovější doporučené verze.</span><span class="sxs-lookup"><span data-stu-id="aab47-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="aab47-165">Pro Visual Studio 2015 doporučujeme 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="aab47-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="aab47-166">Pokud narazíte na jiné problémy, [soubor problém na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) takže můžeme získat další podrobnosti od vás.</span><span class="sxs-lookup"><span data-stu-id="aab47-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
