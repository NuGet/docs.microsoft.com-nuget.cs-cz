---
title: Zpráva k vydání verze NuGet 1,5
description: Poznámky k verzi pro NuGet 1,5, včetně známých problémů, oprav chyb, přidaných funkcí a chcete odeslat obecnou.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383346"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="31cb4-103">Zpráva k vydání verze NuGet 1,5</span><span class="sxs-lookup"><span data-stu-id="31cb4-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="31cb4-104">[Poznámky k verzi nuget 1,4](../release-notes/nuget-1.4.md) | zpráva k [vydání verze NuGet 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="31cb4-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="31cb4-105">NuGet 1,5 byl vydán 30. srpna 2011.</span><span class="sxs-lookup"><span data-stu-id="31cb4-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="31cb4-106">Funkce</span><span class="sxs-lookup"><span data-stu-id="31cb4-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="31cb4-107">Šablony projektů s předinstalovanými balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="31cb4-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="31cb4-108">Při vytváření nové šablony projektu ASP.NET MVC 3 se ve vlastně umístění knihoven skriptů jQuery obsažených v projektu nainstalují balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="31cb4-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="31cb4-109">Šablona projektu ASP.NET MVC 3 obsahuje sadu balíčků NuGet, které se instalují při vyvolání šablony projektu.</span><span class="sxs-lookup"><span data-stu-id="31cb4-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="31cb4-110">Tato možnost zahrnout balíčky NuGet se šablonou projektu je teď funkcí NuGet, kterou může mít _každá_ šablona projektu teď možnost využít.</span><span class="sxs-lookup"><span data-stu-id="31cb4-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="31cb4-111">Další podrobnosti o této funkci najdete [v tomto blogovém příspěvku vývojářem této funkce](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="31cb4-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="31cb4-112">Explicitní odkazy na sestavení</span><span class="sxs-lookup"><span data-stu-id="31cb4-112">Explicit Assembly References</span></span>

<span data-ttu-id="31cb4-113">Přidání nového prvku `<references />`, který slouží k explicitnímu určení, která sestavení v rámci balíčku by měla být odkazována.</span><span class="sxs-lookup"><span data-stu-id="31cb4-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="31cb4-114">Například pokud přidáte následující:</span><span class="sxs-lookup"><span data-stu-id="31cb4-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="31cb4-115">Pak budou odkazy na `xunit.dll` a `xunit.extensions.dll` odkazovány z příslušné [podsložky Framework/profil](../reference/nuspec.md#explicit-assembly-references) složky `lib`, i když jsou ve složce jiná sestavení.</span><span class="sxs-lookup"><span data-stu-id="31cb4-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="31cb4-116">Pokud je tento element vynechán, použije se obvyklé chování, které má odkazovat na každé sestavení ve složce `lib`.</span><span class="sxs-lookup"><span data-stu-id="31cb4-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="31cb4-117">__K čemu se tato funkce používá?__</span><span class="sxs-lookup"><span data-stu-id="31cb4-117">__What is this feature used for?__</span></span>

<span data-ttu-id="31cb4-118">Tato funkce podporuje sestavení pouze pro dobu návrhu.</span><span class="sxs-lookup"><span data-stu-id="31cb4-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="31cb4-119">Například při použití kontraktů kódu musí být sestavení kontraktu vedle sestavení modulu runtime, která se rozšiřují, aby je Visual Studio mohl najít, ale sestavení kontraktu by na ně neměla být odkazováno v projektu a neměla by být kopírována do složky `bin`.</span><span class="sxs-lookup"><span data-stu-id="31cb4-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="31cb4-120">Podobně lze funkci použít pro rozhraní testování částí, jako je například XUnit, které vyžadují, aby jejich nástroje byly umístěny vedle sestavení modulu runtime, ale vyloučeny z odkazů na projekt.</span><span class="sxs-lookup"><span data-stu-id="31cb4-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="31cb4-121">Přidání možnosti pro vyloučení souborů v souboru. nuspec</span><span class="sxs-lookup"><span data-stu-id="31cb4-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="31cb4-122">Element `<file>` v rámci `.nuspec` souboru lze použít k zahrnutí konkrétního souboru nebo sady souborů pomocí zástupného znaku.</span><span class="sxs-lookup"><span data-stu-id="31cb4-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="31cb4-123">Pokud používáte zástupný znak, neexistuje žádný způsob, jak vyloučit určitou podmnožinu zahrnutých souborů.</span><span class="sxs-lookup"><span data-stu-id="31cb4-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="31cb4-124">Předpokládejme například, že chcete všechny textové soubory ve složce s výjimkou konkrétního.</span><span class="sxs-lookup"><span data-stu-id="31cb4-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="31cb4-125">K určení více souborů použijte středníky.</span><span class="sxs-lookup"><span data-stu-id="31cb4-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="31cb4-126">Případně můžete použít zástupnou kartu k vyloučení sady souborů, například všech záložních souborů.</span><span class="sxs-lookup"><span data-stu-id="31cb4-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="31cb4-127">Odebrání balíčků pomocí dialogových oken pro odebrání závislostí</span><span class="sxs-lookup"><span data-stu-id="31cb4-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="31cb4-128">Při odinstalaci balíčku se závislostmi se zobrazí výzva NuGet umožňující odebrání závislostí balíčku spolu s balíčkem.</span><span class="sxs-lookup"><span data-stu-id="31cb4-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Odebírají se závislé balíčky.](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="31cb4-130">vylepšení příkazu `Get-Package`</span><span class="sxs-lookup"><span data-stu-id="31cb4-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="31cb4-131">Příkaz `Get-Package` nyní podporuje parametr `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="31cb4-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="31cb4-132">Příkaz</span><span class="sxs-lookup"><span data-stu-id="31cb4-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="31cb4-133">Zobrazí seznam všech balíčků nainstalovaných v projektu A.</span><span class="sxs-lookup"><span data-stu-id="31cb4-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="31cb4-134">Podpora proxy serverů, které vyžadují ověření</span><span class="sxs-lookup"><span data-stu-id="31cb4-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="31cb4-135">Při používání NuGet za proxy serverem, který vyžaduje ověření, NuGet se teď vyzve k zadání přihlašovacích údajů proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="31cb4-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="31cb4-136">Zadání přihlašovacích údajů umožňuje NuGet připojit se ke vzdálenému úložišti.</span><span class="sxs-lookup"><span data-stu-id="31cb4-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="31cb4-137">Podpora úložišť, která vyžadují ověření</span><span class="sxs-lookup"><span data-stu-id="31cb4-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="31cb4-138">NuGet teď podporuje připojení k [soukromým úložištím](../hosting-packages/local-feeds.md) , která vyžadují základní ověřování nebo ověřování NTLM.</span><span class="sxs-lookup"><span data-stu-id="31cb4-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="31cb4-139">V budoucí verzi se přidá podpora pro ověřování algoritmem Digest.</span><span class="sxs-lookup"><span data-stu-id="31cb4-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="31cb4-140">Vylepšení výkonu úložiště nuget.org</span><span class="sxs-lookup"><span data-stu-id="31cb4-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="31cb4-141">V galerii nuget.org jsme provedli několik vylepšení výkonu, aby se vytvářely výpisy balíčků a hledání rychleji.</span><span class="sxs-lookup"><span data-stu-id="31cb4-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="31cb4-142">Filtrování projektu dialogu řešení</span><span class="sxs-lookup"><span data-stu-id="31cb4-142">Solution dialog project filtering</span></span>
<span data-ttu-id="31cb4-143">V dialogovém okně na úrovni řešení se po zobrazení výzvy k instalaci projektů zobrazí pouze projekty, které jsou kompatibilní s vybraným balíčkem.</span><span class="sxs-lookup"><span data-stu-id="31cb4-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="31cb4-144">Poznámky k verzi balíčku</span><span class="sxs-lookup"><span data-stu-id="31cb4-144">Package Release Notes</span></span>
<span data-ttu-id="31cb4-145">Balíčky NuGet teď zahrnují podporu pro poznámky k verzi.</span><span class="sxs-lookup"><span data-stu-id="31cb4-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="31cb4-146">Poznámky k verzi se zobrazují jenom při prohlížení _aktualizací_ balíčku, takže nedávají smysl přidat ho do vaší první verze.</span><span class="sxs-lookup"><span data-stu-id="31cb4-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Poznámky k verzi na kartě aktualizace](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="31cb4-148">Chcete-li přidat do balíčku poznámky k verzi, použijte nový prvek `<releaseNotes />` metadat v souboru NuSpec.</span><span class="sxs-lookup"><span data-stu-id="31cb4-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="31cb4-149">nuspec & ltfiles/vylepšení&gt;</span><span class="sxs-lookup"><span data-stu-id="31cb4-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="31cb4-150">Soubor `.nuspec` nyní umožňuje prázdný `<files />` prvek, který instruuje NuGet. exe, že neobsahuje žádný soubor v balíčku.</span><span class="sxs-lookup"><span data-stu-id="31cb4-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="31cb4-151">Opravy chyb</span><span class="sxs-lookup"><span data-stu-id="31cb4-151">Bug Fixes</span></span>
<span data-ttu-id="31cb4-152">Aktualizace NuGet 1,5 obsahovala celkem 107 pracovních položek.</span><span class="sxs-lookup"><span data-stu-id="31cb4-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="31cb4-153">103 z nich bylo označeno jako chyby.</span><span class="sxs-lookup"><span data-stu-id="31cb4-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="31cb4-154">Úplný seznam pracovních položek opravených v NuGet 1,5 najdete v [přehledu problémů NuGet pro tuto verzi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="31cb4-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="31cb4-155">Opravy chyb zaznamenaly:</span><span class="sxs-lookup"><span data-stu-id="31cb4-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="31cb4-156">[Problém 1273](http://nuget.codeplex.com/workitem/1273): provedli jsme `packages.config`ější správu verzí pomocí řazení balíčků abecedně a odebráním nadbytečného prázdného znaku.</span><span class="sxs-lookup"><span data-stu-id="31cb4-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="31cb4-157">[Problém 844](http://nuget.codeplex.com/workitem/844): čísla verzí jsou nyní normalizována, aby `Install-Package 1.0` fungovala na balíčku s verzí `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="31cb4-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="31cb4-158">[Problém 1060](http://nuget.codeplex.com/workitem/1060): při vytváření balíčku pomocí NuGet. exe příznak `-Version` Přepisuje `<version />` element.</span><span class="sxs-lookup"><span data-stu-id="31cb4-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
