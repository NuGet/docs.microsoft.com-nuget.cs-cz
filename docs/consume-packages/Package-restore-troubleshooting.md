---
title: Řešení potíží s obnovením balíčku NuGet v aplikaci Visual Studio
description: Popis běžných chyb obnovení NuGet v aplikaci Visual Studio a jejich řešení.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 9f680a714717d1bde0472f2e1266cacfd8bd4d5f
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699714"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="9f354-103">Řešení potíží s chybami při obnovení balíčku</span><span class="sxs-lookup"><span data-stu-id="9f354-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="9f354-104">Tento článek se zaměřuje na běžné chyby při obnovení balíčků a postupu jejich řešení.</span><span class="sxs-lookup"><span data-stu-id="9f354-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="9f354-105">Obnovení balíčku se pokusí nainstalovat všechny závislosti balíčků do správného stavu odpovídajícího odkazům na balíček v souboru projektu (*. csproj*) nebo souboru *packages.config* .</span><span class="sxs-lookup"><span data-stu-id="9f354-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="9f354-106">(V aplikaci Visual Studio se odkazy zobrazí v Průzkumník řešení pod uzlem **závislosti \ NuGet** nebo **odkazy** .) Postup obnovení balíčků pomocí požadovaných kroků najdete v tématu [obnovení balíčků](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="9f354-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="9f354-107">Pokud balíček odkazuje v souboru projektu (*. csproj*) nebo je soubor *packages.config* nesprávný (neshoduje se s požadovaným stavem po obnovení balíčku), je třeba nainstalovat nebo aktualizovat balíčky namísto použití obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="9f354-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="9f354-108">Pokud vám pokyny pro vás nefungují, [Zajistěte prosím problém na GitHubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , abychom mohli podrobněji prošetřit svůj scénář.</span><span class="sxs-lookup"><span data-stu-id="9f354-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="9f354-109">Nepoužívejte tuto stránku jako užitečnou?</span><span class="sxs-lookup"><span data-stu-id="9f354-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="9f354-110">ovládací prvek, který se může zobrazit na této stránce, protože nám nedává možnost kontaktovat vám další informace</span><span class="sxs-lookup"><span data-stu-id="9f354-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="9f354-111">Rychlé řešení pro uživatele sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9f354-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="9f354-112">Pokud používáte sadu Visual Studio, nejprve povolte obnovení balíčku následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="9f354-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="9f354-113">V opačném případě pokračujte v následujících oddílech.</span><span class="sxs-lookup"><span data-stu-id="9f354-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="9f354-114">Vyberte **nástroje > správce balíčků NuGet > nabídce Nastavení správce balíčků** .</span><span class="sxs-lookup"><span data-stu-id="9f354-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="9f354-115">V části **obnovení balíčku** nastavte obě možnosti.</span><span class="sxs-lookup"><span data-stu-id="9f354-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="9f354-116">Vyberte **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f354-116">Select **OK**.</span></span>
1. <span data-ttu-id="9f354-117">Sestavte projekt znovu.</span><span class="sxs-lookup"><span data-stu-id="9f354-117">Build your project again.</span></span>

![Povolit obnovení balíčků NuGet v nástrojích/možnostech](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="9f354-119">Tato nastavení lze také změnit v souboru. `NuGet.config` informace najdete v části věnované [souhlasu](#consent) .</span><span class="sxs-lookup"><span data-stu-id="9f354-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="9f354-120">Pokud je váš projekt starší projekt, který používá obnovení balíčku integrovaného MSBuild, může být nutné [migrovat](package-restore.md#migrate-to-automatic-package-restore-visual-studio) na automatické obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="9f354-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="9f354-121">Tento projekt odkazuje na balíčky NuGet, které na tomto počítači chybí.</span><span class="sxs-lookup"><span data-stu-id="9f354-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="9f354-122">Úplná chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="9f354-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="9f354-123">K této chybě dochází, když se pokusíte sestavit projekt, který obsahuje odkazy na jeden nebo více balíčků NuGet, ale tyto balíčky se v počítači nebo v projektu aktuálně neinstalují.</span><span class="sxs-lookup"><span data-stu-id="9f354-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="9f354-124">Při použití formátu správy [PackageReference](package-references-in-project-files.md) může být tato chyba zbylé z packages.config do migrace PackageReference a musí být [ručně odebrána](../resources/NuGet-FAQ.md#working-with-packages) ze souboru projektu.</span><span class="sxs-lookup"><span data-stu-id="9f354-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](../resources/NuGet-FAQ.md#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="9f354-125">Při použití [packages.config](../reference/packages-config.md)chyba znamená, že balíček není nainstalován ve `packages` složce v kořenu řešení.</span><span class="sxs-lookup"><span data-stu-id="9f354-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="9f354-126">K této situaci obvykle dochází, když získáte zdrojový kód projektu ze správy zdrojového kódu nebo z jiného stahování.</span><span class="sxs-lookup"><span data-stu-id="9f354-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="9f354-127">Balíčky jsou obvykle vynechány ze správy zdrojového kódu nebo ze souborů ke stažení, protože je lze obnovit z kanálů balíčků jako nuget.org (viz [balíčky a Správa zdrojového kódu](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="9f354-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="9f354-128">Zahrnutí by jinak dispozici determinističtější úložiště nebo vytvářet zbytečně velké soubory. zip.</span><span class="sxs-lookup"><span data-stu-id="9f354-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="9f354-129">K této chybě může dojít také v případě, že soubor projektu obsahuje absolutní cesty k umístěním balíčků a přesouváte projekt.</span><span class="sxs-lookup"><span data-stu-id="9f354-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="9f354-130">K obnovení balíčků použijte jednu z následujících metod:</span><span class="sxs-lookup"><span data-stu-id="9f354-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="9f354-131">Pokud jste přesunuli soubor projektu, upravte soubor přímo a aktualizujte odkazy na balíčky.</span><span class="sxs-lookup"><span data-stu-id="9f354-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="9f354-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([Automatické obnovení](package-restore.md#restore-packages-automatically-using-visual-studio) nebo [Ruční obnovení](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="9f354-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="9f354-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="9f354-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="9f354-134">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="9f354-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="9f354-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="9f354-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="9f354-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="9f354-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="9f354-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="9f354-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="9f354-138">Po úspěšném obnovení by měl být balíček přítomen ve složce *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="9f354-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="9f354-139">Pro projekty, které používají PackageReference, by měl obnovení soubor znovu vytvořit `obj/project.assets.json` ; pro projekty `packages.config` , které používají, by se měl balíček zobrazit ve `packages` složce projektu.</span><span class="sxs-lookup"><span data-stu-id="9f354-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="9f354-140">Projekt by se teď měl úspěšně sestavit.</span><span class="sxs-lookup"><span data-stu-id="9f354-140">The project should now build successfully.</span></span> <span data-ttu-id="9f354-141">Pokud ne, zapište [problém na GitHubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , abychom mohli pokračovat s vámi.</span><span class="sxs-lookup"><span data-stu-id="9f354-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="9f354-142">Soubor assetů project.assets.jsnebyl nalezen.</span><span class="sxs-lookup"><span data-stu-id="9f354-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="9f354-143">Úplná chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="9f354-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="9f354-144">`project.assets.json`Soubor udržuje graf závislosti projektu při použití formátu správy PackageReference, který se používá k tomu, aby se zajistilo, že jsou v počítači nainstalovány všechny potřebné balíčky.</span><span class="sxs-lookup"><span data-stu-id="9f354-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="9f354-145">Vzhledem k tomu, že tento soubor je generován dynamicky prostřednictvím obnovení balíčku, obvykle není přidán do správy zdrojového kódu.</span><span class="sxs-lookup"><span data-stu-id="9f354-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="9f354-146">V důsledku toho k této chybě dochází při sestavování projektu s nástrojem `msbuild` , který neobnoví automaticky balíčky.</span><span class="sxs-lookup"><span data-stu-id="9f354-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="9f354-147">V takovém případě spusťte `msbuild -t:restore` `msbuild` nebo použijte `dotnet build` (který automaticky obnoví balíčky).</span><span class="sxs-lookup"><span data-stu-id="9f354-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="9f354-148">Můžete také použít kteroukoli z metod obnovení balíčků v [předchozí části](#missing).</span><span class="sxs-lookup"><span data-stu-id="9f354-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="9f354-149">Nejméně jeden balíček NuGet je potřeba obnovit, ale nedala se k němu udělit souhlas.</span><span class="sxs-lookup"><span data-stu-id="9f354-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="9f354-150">Úplná chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="9f354-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="9f354-151">Tato chyba znamená, že obnovení balíčku je v konfiguraci NuGet zakázané.</span><span class="sxs-lookup"><span data-stu-id="9f354-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="9f354-152">V aplikaci Visual Studio můžete změnit příslušná nastavení, jak je popsáno výše v části [rychlé řešení pro uživatele sady Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="9f354-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="9f354-153">Tato nastavení můžete také upravit přímo v příslušném `nuget.config` souboru (obvykle ve `%AppData%\NuGet\NuGet.Config` Windows a v systému `~/.nuget/NuGet/NuGet.Config` Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9f354-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="9f354-154">Ujistěte se, `enabled` že `automatic` klíče a v části `packageRestore` jsou nastaveny na hodnotu true:</span><span class="sxs-lookup"><span data-stu-id="9f354-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="9f354-155">Pokud upravíte `packageRestore` nastavení přímo v `nuget.config` , restartujte Visual Studio tak, aby se v dialogovém okně Možnosti zobrazily aktuální hodnoty.</span><span class="sxs-lookup"><span data-stu-id="9f354-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="9f354-156">Další možné podmínky</span><span class="sxs-lookup"><span data-stu-id="9f354-156">Other potential conditions</span></span>

- <span data-ttu-id="9f354-157">Může dojít k chybám sestavení z důvodu chybějících souborů. zpráva říká použití obnovení NuGet ke stažení.</span><span class="sxs-lookup"><span data-stu-id="9f354-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="9f354-158">Při spuštění obnovení ale může znamenat, že všechny balíčky jsou už nainstalované a neexistuje žádná obnova. "</span><span class="sxs-lookup"><span data-stu-id="9f354-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="9f354-159">V takovém případě odstraňte `packages` složku (při použití `packages.config` ) nebo `obj/project.assets.json` soubor (při použití PackageReference) a znovu spusťte obnovení.</span><span class="sxs-lookup"><span data-stu-id="9f354-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="9f354-160">Pokud chyba stále přetrvává, pomocí `nuget locals all -clear` příkazu nebo `dotnet nuget locals all --clear` z příkazového řádku zrušte zaškrtnutí popsaných složek *Global-Packages* a cache, jak je popsáno v tématu [Správa globálních balíčků a složek mezipaměti](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="9f354-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="9f354-161">Při získávání projektu ze správy zdrojového kódu mohou být složky projektu nastaveny jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="9f354-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="9f354-162">Změňte oprávnění složky a zkuste znovu obnovit balíčky.</span><span class="sxs-lookup"><span data-stu-id="9f354-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="9f354-163">Je možné, že používáte starou verzi NuGet.</span><span class="sxs-lookup"><span data-stu-id="9f354-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="9f354-164">Vyhledejte nejnovější Doporučené verze v [NuGet.org/downloads](https://www.nuget.org/downloads) .</span><span class="sxs-lookup"><span data-stu-id="9f354-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="9f354-165">Pro Visual Studio 2015 doporučujeme 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="9f354-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="9f354-166">Pokud narazíte na jiné problémy, zapište [problém na GitHubu](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , abychom vám mohli získat další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="9f354-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
